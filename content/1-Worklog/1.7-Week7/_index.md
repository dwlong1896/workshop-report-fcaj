---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
### Week 7 Objectives:

* Grasp Microservices architecture, know how to design and decouple a Monolith system into independent services.
* Get acquainted with Serverless architecture, build automated processing flows with AWS Lambda, Amazon S3, and DynamoDB.
* Apply AWS Step Functions to orchestrate complex business workflows.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                                                                              | Start Date | Completion Date | Reference Material                        |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Create Microservices <br>&emsp; + Learn the differences between Monolithic and Microservices architecture <br> - **Practice:** <br>&emsp; + Design a plan to decouple a monolithic SpringBoot backend application into independent bounded contexts                                                             | 13/07/2025 | 13/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Serverless – Lambda & DynamoDB <br>&emsp; + Learn about Serverless compute (AWS Lambda) and NoSQL database (DynamoDB) <br> - **Practice:** <br>&emsp; + Create a basic table on DynamoDB <br>&emsp; + Write a first Lambda function                                                                             | 14/07/2025 | 14/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Serverless – Lambda interacting with S3 <br>&emsp; + Learn about Event-driven architecture mechanisms <br> - **Practice:** <br>&emsp; + Configure Event Trigger: Automatically trigger a Lambda function whenever a static file is uploaded to the S3 bucket                                                    | 15/07/2025 | 15/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Integrate a complete Serverless flow <br>&emsp; + How serverless services communicate securely with each other <br> - **Practice:** <br>&emsp; + Program a Lambda function to read file metadata from an S3 event and execute a command to write a record to DynamoDB                                         | 16/07/2025 | 16/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Get acquainted with AWS Step Functions <br>&emsp; + Learn about State Machines and orchestration steps (Task, Choice, Parallel) <br> - **Practice:** <br>&emsp; + Create a workflow sequentially orchestrating multiple Lambda functions to process business logic without timing out                           | 17/07/2025 | 17/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Know how to design Microservices systems:
  * Know the pros and cons and how to break down a large system (monolith) into smaller services, making it easy to scale and maintain independently.

* Shift to Serverless architecture:
  * Successfully operate a logic-executing backend (Lambda) without managing any EC2 servers.
  * Integrate a non-relational database (DynamoDB).

* Successfully build Event-Driven workflows:
  * Automate data processing flow: The system is capable of detecting when a new file appears on S3 to trigger code, then automatically updates data to DynamoDB.

* Orchestrate workflows with Step Functions:
  * Know how to connect and visualize discrete services into a seamless business process.