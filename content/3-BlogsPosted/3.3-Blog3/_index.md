---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# AWS Cost Anomaly Detection: The gatekeeper that prevents unexpected AWS bills

Anyone learning AWS has surely heard the story: turning on a GPU instance to train a model overnight, then forgetting to turn it off; or an auto scaling group inflating during a load test and no one remembering to scale it back down; opening AWS Billing at the end of the month, the cost increases abnormally. This is exactly a cost anomaly — an unusual, unexpected expense.

Today I introduce AWS Cost Anomaly Detection (CAD) — a completely free tool in AWS Billing and Cost Management, which uses machine learning to learn your normal "spending rhythm" and alerts you immediately when something is abnormal, instead of letting you discover it yourself through the end-of-month bill.

### 1. How is CAD different from setting your own alert thresholds (AWS Budgets)?

Many new AWS users often confuse CAD with AWS Budgets — but these two tools solve two different problems:
{{< figure
  src="/images/3.3.2.jpg"
  alt="AWS Budgets"
  class="image-70"
  caption="Figure 1. AWS Budgets uses fixed thresholds, while Cost Anomaly Detection uses machine learning to detect anomalous spending patterns."
>}}
* AWS Budgets: you set a fixed threshold yourself. Simple, but a fixed threshold cannot reflect that your spending naturally fluctuates over time (for example: training models more on weekends than weekdays).
* Cost Anomaly Detection: does not use fixed thresholds, but builds a baseline of normal spending from historical data using machine learning, then compares actual spending with the predicted level for each time frame. Thanks to this, CAD understands that your EC2 costs naturally increase every Monday morning due to a scheduled batch job — and will not trigger an alert for it. But if suddenly there is a strange data-transfer pattern on S3 causing the bill to triple at 2 AM on a Saturday, CAD will detect it immediately.

In other words: Budgets is suitable as a hard "safety net" when you first get an account, while CAD works best when you have at least a few weeks of spending data for the model to learn your normal rhythm — both should be used in parallel, not replacing each other.

### 2. How it works

The CAD pipeline consists of these steps:

1. Data collection: CAD collects detailed billing and usage data across all monitored accounts/services.
2. Historical analysis: the machine learning model learns from a few weeks to a few months of past spending data to build a behavioral baseline.
3. Anomaly detection: the model continuously predicts the expected spending level for the next time frame (usually daily) and compares it with actual spending.
4. Alerting & root cause analysis: if the deviation exceeds your set threshold, CAD sends an alert with a suggestion of which service/resource is causing the anomaly.

A notable improvement AWS announced at the end of 2025: the algorithm switched to comparing based on a rolling 24-hour window instead of a fixed calendar day — helping to detect faster (no need to wait until the end of the day to compare) and more accurately (comparing the exact corresponding timeframe, avoiding confusion between morning and evening patterns).

### 3. Four types of Monitors — choose the right cost "perspective"
{{< figure
  src="/images/3.3.1.jpg"
  alt="Cost Monitor"
  class="image-70"
  caption="Figure 2. Creating a cost monitoring tool in AWS Billing and Cost Management."
>}} 
When creating a Cost Monitor, you choose 1 of 4 dimensions to monitor:

* AWS Services: monitors anomalies for each individual service (EC2, S3, RDS...) — most suitable for personal/learning accounts because it is simple and doesn't require a complex organizational structure.
* Linked Account: monitors spending across multiple child accounts in an AWS Organization — useful when a company has multiple teams, each with their own account.
* Cost Allocation Tag: monitors based on tags you assign yourself (e.g., Environment=Production, Project=X) — helps to know exactly which project/team is generating the anomaly instead of just a generic "EC2 increased".
* Cost Category: groups costs according to a custom-defined business structure (combining accounts, tags, services...).

A great point: since AWS expanded AWS managed monitors to all 4 types above (previously managed monitors were only available for AWS Services), you can create a monitor that "automatically covers" all newly arising accounts/tags later on without having to recreate it manually — very suitable when your organization is constantly adding new accounts or projects.

Note on limits: each account can have a maximum of 1 AWS Service Monitor + 500 custom monitors (total max 501 monitors), and they can all be attached to the same alert subscription.

### 4. Setting up alerts
{{< figure
  src="/images/3.3.3.jpg"
  alt="Configuration"
  class="image-70"
  caption="Figure 3. Configuring Alert Subscription to receive abnormal cost alerts."
>}} 
After creating a monitor, you configure the Alert Subscription including:
* Alert channel: email or SNS (from SNS it can be further forwarded via AWS Chatbot to Slack).
* Trigger threshold: by absolute amount, by percentage difference from prediction, or combining both (e.g., "only alert when the increase exceeds 40% AND exceeds $100" — this combination helps reduce false alarms for small fluctuations but still catches truly significant spikes).
* Frequency: real-time (immediate), daily summary, or weekly.

Specifically for new Cost Explorer accounts, AWS automatically enables a default AWS Services Monitor with a daily email alert, so often you already have CAD running in the background without noticing.

### 5. Limitations you need to know — CAD is not a perfect "shield"

To set the right expectations, there are a few things CAD cannot do:
* Does not proactively prevent spending — CAD only detects and alerts after the cost has been incurred; it does not automatically stop or limit resources like a real "circuit breaker".
* Has latency — billing data takes time to process, so there is usually a delay of a few hours to about 1 day; an abnormal spending spike on Saturday night might only be reported on Monday morning.
* New monitors need time to "warm up" — a newly created monitor can take up to 24 hours to start working, and for a completely new service in an account, CAD needs about 10 days of historical data before it can detect anomalies for that service.
* Does not calculate unit economics — CAD does not automatically convert costs into "cost per customer/feature", so if you need analysis at that level, you still need specialized FinOps tools or to build your own dashboard.

### 6. A few practical recommendations for personal/learning accounts

* Start with the AWS Services Monitor (default, simple, doesn't require a complex tag structure).
* Set alert thresholds combining both absolute amounts and percentages, and don't set the monetary threshold too low (a few USD) for a learning account — because the spending baseline is already very small, a low threshold easily triggers continuous false alarms.
* While the account is newly created (not enough historical data for CAD to learn), use AWS Budgets with a hard threshold as a temporary safety net — for example, capping at $5-$10 — in parallel with CAD.
* If learning/working in an AWS Organization with multiple accounts (like a school or company lab environment), you should create an additional Cost Allocation Tag Monitor using a `Project` or `Team` tag so that when there's an alert, you know immediately which project is causing the anomaly instead of having to search the whole account.

### 7. Conclusion

CAD cannot replace the consciousness of turning off resources after use, but it is an automatic, free defense layer worth turning on from the very first day of creating an AWS account — especially useful for students doing internships or graduation projects who have to turn on expensive GPU/big data instances for short periods. The biggest cost during the AWS learning process usually doesn't come from a lack of knowledge, but from forgetting to turn something off — and this is exactly the tool born to catch that forgetting error as early as possible.

**Note on reliability:** the algorithm mechanism, monitor types, and limits mentioned above were synthesized from official AWS documentation (docs.aws.amazon.com, What's New page) and some technical analysis articles from third-party FinOps platforms. Because AWS updates the CAD algorithm quite frequently (there have been at least 2 improvements in accuracy/latency just in 2025), some operational details may have changed — so always check the official User Guide before relying entirely on this tool for a production account.

Thank you everyone for reading! If anyone has ever been "hit" by an unexpected bill because they forgot to turn off a resource, please share your experience; surely anyone learning AWS has at least one such story.

### References

* https://docs.aws.amazon.com/cost-management/latest/userguide/getting-started-ad.html
* https://aws.amazon.com/aws-cost-management/aws-cost-anomaly-detection/faqs
* https://aws.amazon.com/about-aws/whats-new/2025/11/aws-cost-anomaly-detection-accelerates-anomaly
* https://aws.amazon.com/about-aws/whats-new/2025/07/aws-cost-anomaly-detection-improves-accuracy-model-enhancements
* https://aws.amazon.com/blogs/aws-cloud-financial-management/extending-aws-managed-monitors-in-cost-anomaly-detection/

Link to the article: https://www.facebook.com/groups/awsstudygroupfcj/permalink/2228079044623722/?rdid=UfKIY40XQuTCrdo9