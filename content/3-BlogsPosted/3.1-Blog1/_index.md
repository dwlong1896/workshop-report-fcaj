---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Amazon S3 Vectors: When S3 learns to store and search vectors

If you have ever built a RAG (Retrieval-Augmented Generation) application or a semantic search system, you surely had to choose a place to store vector embeddings
{{< figure
  src="/images/3.1.2.jpg"
  alt="Vector Space SE"
  class="image-70"
  caption="Figure 1. Illustration of the Sentence Embeddings vector space."
>}} 
The problem is that most specialized vector databases are designed to serve high-speed queries, so they keep the entire index in memory or on a constantly running compute cluster — this is very expensive when you have hundreds of millions to billions of vectors but most of that data is not queried frequently (e.g., embeddings of all internal company documents, or medical images stored for many years).

Amazon S3 Vectors was born to solve this exact problem: transforming S3 into a native vector storage location without needing to set up a separate cluster.

### 1. What is S3 Vectors?

S3 Vectors adds a completely new bucket type to S3 — the vector bucket — alongside the familiar general-purpose, directory, and table buckets. Three core concepts:

* Vector bucket: a specialized bucket type for storing and querying vectors.
* Vector index: inside the vector bucket, you organize data into indexes — each similarity search will run on a specific index.
* Vector: the embedding itself, accompanied by metadata (key-value, e.g., publication year, author, category) to filter results later.

A notable technical point: writing data to S3 Vectors is strongly consistent, and S3 automatically optimizes how vectors are stored over time to keep costs low even as the dataset grows.

In terms of scale, a single index supports up to 2 billion vectors, and a bucket can contain up to 10,000 indexes. Query latency ranges from under 1 second to about 100ms.
{{< figure
  src="/images/3.1.4.jpg"
  alt="Data storage and querying"
  class="image-70"
  caption="Figure 2. Data storage and querying workflow in Amazon S3 Vectors."
>}} 
### 2. Pricing mechanism

S3 Vectors charges under 3 separate categories, quite different from standard S3:

a) Storage
The size of a vector = vector data + metadata + key. For example, a 1024-dimensional vector (dimension — the number of numeric values representing that embedding, popular embedding models like Titan or Cohere usually output 1024 or 1536 dimensions): each dimension takes 4 bytes → 1024 × 4 bytes = 4KB of raw vector data, plus metadata and the key to get the total chargeable size.

b) PUT (data writing)
Charged per GB of logical data written. You can send multiple vectors in a single PUT request to optimize costs — similar to the familiar "batch" principle when working with DynamoDB or SQS.

c) Query (data querying)
This part consists of 3 cost layers added together: a fixed fee per query, a fee based on the volume of data processed (calculated in $/TB, and this calculation is proportional to the size of the entire index, so the larger the index, the more data each query "scans" — but in return, the unit price per TB decreases as the index crosses the 100,000 and 10 million vector milestones), and a fee based on the data returned (the first 512KB of each query is free).

A specific example according to the official pricing documentation: a RAG system with 10 million vectors (each vector ~6.17KB including vector data + metadata + key), divided into 40 indexes for 40 customers, data updated every 6 months, running 1 million queries/month (returning 100 results/query) — the estimated total cost falls around $11/month for storage, writing, and querying in the US East (N. Virginia) region. This figure helps to visualize: the main cost comes from query volume, not storage — so if your application queries infrequently but stores a lot, S3 Vectors will be very cheap; conversely, if you query continuously at high frequency, the cost will increase rapidly, and a dedicated vector database (paying a fixed compute fee) might be more economical.

### 3. Built-in integration with the AWS ecosystem

Instead of writing your own synchronization pipeline, S3 Vectors comes with built-in integrations for:

* Amazon Bedrock Knowledge Bases: directly select an S3 Vectors vector index as the vector store when creating a Knowledge Base for RAG, without needing to provision additional infrastructure.
* Amazon OpenSearch Service: use S3 Vectors as a low-cost storage tier, then export snapshots to OpenSearch Serverless when high QPS (queries per second) and low latency are needed for "hot" data.
* Security is managed via IAM like other S3 resources but resides in a separate `s3vectors` namespace, so you can write separate policies for the vector bucket without affecting existing standard S3 policies. Additionally, Block Public Access is always enabled by default and cannot be turned off.

{{< figure
  src="/images/3.1.3.jpg"
  alt="Operational Architecture"
  class="image-70"
  caption="Figure 3. Operational architecture of Amazon S3 Vectors."
>}}
{{< figure
  src="/images/3.1.1.jpg"
  alt="RAG System Architecture"
  class="image-70"
  caption="Figure 4. RAG system architecture using Amazon Bedrock Knowledge Bases."
>}}

### 4. Practical use cases

According to AWS documentation, typical use cases for similarity search using S3 Vectors include:

* Finding similar medical images across millions of images to assist in diagnosis.
* Detecting copyright-infringing content in large media repositories.
* Removing duplicate or near-duplicate images in massive image datasets.
* Finding specific scenes in long videos (video understanding).
* Semantic search in corporate internal documents — searching by meaning instead of exact keywords.
* Recommending similar products/content (personalization).

### 5. So when should you use S3 Vectors, and when should you not?

You should use it when:
* You have a large dataset (tens of millions to billions of vectors) but most of it is queried infrequently — e.g., long-term storage data, archive documents, historical logs.
* You want to avoid operating a dedicated vector database cluster (patching, scaling, high availability) just to serve a few queries per minute.
* You are using Bedrock Knowledge Bases and want to reduce vector store costs for RAG.

Consider using a dedicated vector database (OpenSearch, Milvus, Pinecone...) when:
* Your application needs very high QPS, with stable latencies of tens of milliseconds (e.g., real-time product recommendations on a high-traffic e-commerce site).
* You need advanced search features like hybrid search (combining full-text + vector), aggregations, or complex faceted search — this is where AWS also recommends using OpenSearch.

A practical architecture many teams are adopting: store all vectors in S3 Vectors as the low-cost "source of truth", and only export the "hot" data (frequently queried) to OpenSearch Serverless to serve at high speed — combining both instead of choosing just one.

### 6. Conclusion

S3 Vectors doesn't aim to completely replace dedicated vector databases, but fills a gap: storing vectors at a massive scale at a cost close to standard object storage, instead of the cost of an always-on compute cluster. For those doing projects related to RAG/semantic search with a limited budget, this is an option worth trying before jumping straight into a compute-billed vector database.

**Note on reliability:** The technical figures (limits on vectors/indexes, latency, pricing formulas) were taken directly from the official AWS documentation and pricing pages at the time of writing. Since this is a fairly new service, some limits/prices may be adjusted by AWS over time — so always check the official documentation/pricing pages before factoring it into real budget calculations.

Thank you everyone for reading! If anyone has tried S3 Vectors for a personal project, I'd love to hear more about your practical experience, especially regarding query latency as the index grows larger.

### References

* https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-vectors.html
* https://aws.amazon.com/s3/pricing/
* https://aws.amazon.com/about-aws/whats-new/2025/12/amazon-s3-vectors-generally-available/
* https://aws.amazon.com/s3/features/vectors

Link to the article: https://www.facebook.com/groups/awsstudygroupfcj/permalink/2225204894911137/?rdid=cg8lX8UFeXdY4OIr#