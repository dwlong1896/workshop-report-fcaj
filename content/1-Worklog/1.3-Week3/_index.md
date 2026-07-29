---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Week 3 Objectives:

* Grasp Amazon S3 storage service, manage basic Objects, and host static websites.
* Deploy, secure, and connect to a relational database with Amazon RDS.
* Set up resource monitoring and automated alerting systems via Amazon CloudWatch.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Host static websites with Amazon S3 <br>&emsp; + Learn about S3 Buckets, Objects, and access control mechanisms <br> - **Practice:** <br>&emsp; + Create a Bucket, configure Block Public Access <br>&emsp; + Upload and manage basic static files                                                    | 15/06/2025 | 15/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Host static websites with Amazon S3 <br>&emsp; + Mechanism of serving static web directly from an S3 Bucket <br> - **Practice:** <br>&emsp; + Enable Static Website Hosting feature <br>&emsp; + Configure Bucket Policy <br>&emsp; + Deploy a static web interface                                 | 16/06/2025 | 16/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create a database on Amazon RDS <br>&emsp; + Learn about DB Engines (MySQL, PostgreSQL...) <br> - **Practice:** <br>&emsp; + Launch an RDS instance in a Private Subnet <br>&emsp; + Configure a Security Group to only allow connections from the application server                               | 17/06/2025 | 17/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Create a database on Amazon RDS <br>&emsp; + Learn about Endpoints and automated Backup mechanisms of RDS <br> - **Practice:** <br>&emsp; + Establish a secure connection from the backend application running on EC2 to RDS <br>&emsp; + Perform test data queries                                 | 18/06/2025 | 18/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Create a monitoring system with Amazon CloudWatch <br>&emsp; + Concepts of Metrics, Logs, and Alarms on AWS <br> - **Practice:** <br>&emsp; + Read and monitor CPU and RAM charts of EC2 and RDS <br>&emsp; + Create an Alarm to automatically send an email alert when the server's CPU exceeds 80%| 19/06/2025 | 19/06/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 3 Achievements:

* Understand the basics of Amazon S3 object storage service:
  * Know how to configure and securely grant access permissions for static resource files.
  * Distribute Frontend applications directly from S3 to the Internet at a low cost with smooth operation.

* Safely administer and operate cloud databases with Amazon RDS:
  * Launch a relational database and protect it by placing it deep within the internal network (Private Subnet).
  * Clearly understand the Endpoint concept; successfully connect the data flow from Backend to Database, completing a basic multi-tier web application architecture.

* Automate the system monitoring process using Amazon CloudWatch:
  * Know how to look up logs and read Metrics to visually assess the health of the entire infrastructure.
  * Successfully set up an automated alerting system, ensuring timely notifications are always received if server resources become overloaded.