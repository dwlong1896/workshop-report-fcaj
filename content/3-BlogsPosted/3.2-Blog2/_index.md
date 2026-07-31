---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon Aurora DSQL: An active-active distributed SQL database, completely abandoning traditional locking mechanisms

If you've ever had to choose a database for a system that needs to run in multiple regions simultaneously, you're probably familiar with the classic dilemma: if you want speed and serverless scaling, choose DynamoDB, but you have to relearn design thinking (single-table design) and lose SQL entirely; if you want to keep familiar SQL, choose RDS/Aurora, but deploying active-active multi-region with strong consistency (ensuring all regions read/write the latest data without synchronization delay) is extremely difficult to do right.

Amazon Aurora DSQL is AWS's answer to this gap — a serverless, distributed SQL database supporting active-active multi-region with strong consistency, but it comes with some architectural trade-offs that I think anyone planning to use it should clearly understand before starting to code.
{{< figure
  src="/images/3.2.1.jpg"
  alt="Architecture Overview"
  class="image-70"
  caption="Figure 1. Architecture overview of Amazon Aurora DSQL with an active-active multi-region model and serverless architecture."
>}} 

### 1. What is Aurora DSQL?

In short: this is a PostgreSQL-compatible database, but it completely separates compute and storage into a "shared-nothing" distributed architecture.

Some notable figures:
* SLA of 99.99% for a single-region cluster, 99.999% for a multi-region cluster.
* No need to provision instances, no need to patch, scales to 0 when idle — truly serverless.
* Billed by DPU (Distributed Processing Unit) — a unit measuring distributed processing capacity, similar to the "capacity unit" concept you're familiar with in Aurora Serverless v2, but measured for a distributed infrastructure with more components — plus a storage fee of $0.33/GB-month. Every month includes 100,000 DPUs + 1GB of storage permanently free (not limited to 12 months like the standard free tier), sufficient for a dev environment or a low-traffic personal app.
{{< figure
  src="/images/3.2.2.jpg"
  alt="Shared-nothing architecture"
  class="image-70"
  caption="Figure 2. Shared-nothing architecture of Aurora DSQL, where compute and storage are separated to support scalability and high availability."
>}} 

### 2. Core difference: OCC instead of traditional locking

This is the most important part because it directly affects how you write code.

Standard PostgreSQL uses MVCC (Multi-Version Concurrency Control) combined with row-level locking — when two transactions modify the same row of data, the later transaction must wait (block) until the previous transaction commits or rollbacks.

Aurora DSQL uses OCC (Optimistic Concurrency Control): transactions run freely without needing to acquire locks beforehand; conflicts are only checked at commit time. If two transactions modify the same data, the transaction that commits first wins, and the other receives a serialization error (standard PostgreSQL error code SQLSTATE 40001, or DSQL-specific codes like `OC000`/`OC001`) instead of hanging and waiting.

Benefits: there are never deadlocks, and a transaction is not blocked by another slow-running transaction. But the price to pay: your application must write its own retry logic for transactions that encounter serialization errors — this is not a bug, but an intentionally designed behavior. If you have an endpoint that continuously updates the same row of data (e.g., counting the inventory of a hot product, or the balance of a high-frequency trading account), the retry rate will spike, and actual throughput will drop — this is a characteristic bottleneck of all OCC systems, not just DSQL.

Furthermore, due to the lock-free mechanism, Aurora DSQL currently only supports snapshot isolation (equivalent to PostgreSQL's REPEATABLE READ level) — it does not fully support other isolation levels like SERIALIZABLE that some legacy PostgreSQL applications might rely on.

### 3. DDL must also run asynchronously

Another interesting consequence of the OCC architecture: DDL (Data Definition Language — structure-altering commands like creating tables, creating indexes) cannot be a locking operation in a fully optimistic distributed system. Therefore, instead of CREATE INDEX like standard PostgreSQL (which can only run immediately when the table has no data), Aurora DSQL requires CREATE INDEX ASYNC — it runs as a background task, not blocking reads/writes to the table while the index is being built.

### 4. So what is Aurora DSQL missing compared to "real" PostgreSQL?

According to official documentation and some engineers who have tested it in practice, there are some notable limitations:
* Does not fully support explicit locking (`SELECT ... FOR UPDATE` and similar) in the traditional PostgreSQL style, because it conflicts with the OCC philosophy.
* Some features like sequences, triggers, and complex PL/pgSQL functions are still limited or not fully compatible.
* Only has snapshot isolation as mentioned above.

For these reasons, many engineers who have tested DSQL have given a fairly consistent recommendation: do not use it to "lift-and-shift" a legacy production PostgreSQL application without modifying the code, because the risk of transaction failures due to serialization errors or missing features is quite high. Conversely, for a new application designed from scratch for serverless, DSQL is a highly considerable option.

### 5. When to use it, when not to?

Suitable for:
* New applications, serverless architectures, wanting to keep SQL instead of relearning NoSQL single-table design.
* Needing active-active multi-region with strong consistency without wanting to build the synchronization mechanism yourself.
* Data writing patterns that are relatively evenly distributed (not continuously concentrating updates on a few rows/keys).

Consider other options (Aurora PostgreSQL, RDS, or DynamoDB) when:
* Migrating a legacy PostgreSQL application that has many complex transactions, uses explicit locks, triggers, or requires isolation levels other than snapshot.
* Workloads have "hot keys" that are updated continuously at high frequency (counters, fast transaction account balances) — OCC will cause the retry rate to spike in this case.
{{< figure
  src="/images/3.2.3.jpg"
  alt="Shared-nothing architecture"
  class="image-70"
  caption="Figure 3. Comparison of Aurora DSQL with Aurora PostgreSQL and DynamoDB by architecture, scalability, and use cases."
>}} 
### 6. Conclusion

Aurora DSQL doesn't try to "pretend" to be 100% PostgreSQL compatible — AWS trades off some familiar features and behaviors in exchange for true serverless architecture and active-active multi-region capability that previously was almost only achievable by products like Google Spanner or CockroachDB. For those doing graduation theses or personal projects needing to test distributed architecture without wanting to spend money provisioning a dedicated cluster, the permanent free tier of DSQL (100,000 DPUs + 1GB storage/month) is a pretty good playground to practice.

Note on reliability: the information on architecture, feature limits, and pricing in the article was synthesized from official AWS documentation and some technical articles by engineers who directly tested DSQL. Because this is a relatively new service (more than 1 year since GA) and AWS is still regularly adding features/expanding regions, some limits (e.g., the list of unsupported PostgreSQL features) may have changed — so always check the official "PostgreSQL compatibility" page before deciding to use it for a real project.

Thank you everyone for reading! If anyone has tried writing retry logic for OCC in Aurora DSQL, I would love to hear more practical experience, especially how to handle it so the code doesn't get messy from having to retry at multiple layers.

### References

* https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-aurora-dsql-generally-available
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with-concurrency-control.html
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with.html
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with-postgresql-compatibility-unsupported-features.html
* https://aws.amazon.com/rds/aurora/dsql/pricing/