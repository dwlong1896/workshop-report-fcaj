---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives:

* Manage user identity, authentication, and authorization with Amazon Cognito.
* Grasp asynchronous communication models to decouple microservices.
* Build a highly scalable order processing architecture using Amazon SQS and SNS.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                                                                                 | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Serverless – Authentication with Amazon Cognito <br>&emsp; + Learn concepts of User Pool and Identity Pool <br> - **Practice:** <br>&emsp; + Create a User Pool to manage the user list <br>&emsp; + Configure policies for password and MFA                                                                     | 20/07/2025 | 20/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Serverless – Authentication with Amazon Cognito <br>&emsp; + Integrate Cognito into a real-world application <br> - **Practice:** <br>&emsp; + Simulate frontend calling sign-up and sign-in APIs <br>&emsp; + Process and validate the JWT token returned from Cognito                                            | 21/07/2025 | 21/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Serverless – Message Queuing with Amazon SQS <br>&emsp; + Learn about Message Queue and the benefits of decoupling <br> - **Practice:** <br>&emsp; + Create a Standard Queue and a FIFO Queue <br>&emsp; + Write scripts to send, receive, and delete messages in the Queue                                      | 22/07/2025 | 22/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Serverless – Pub/Sub Messaging with Amazon SNS <br>&emsp; + Publish/Subscribe architecture <br> - **Practice:** <br>&emsp; + Create an SNS Topic <br>&emsp; + Configure Subscribe to automatically send Email notifications when a new event is published to the Topic                                             | 23/07/2025 | 23/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Serverless – Processing orders with SQS and SNS <br>&emsp; + Fanout architecture model <br> - **Practice:** <br>&emsp; + Combine SNS and SQS: Configure an SNS Topic to push messages simultaneously to multiple SQS Queues <br>&emsp; + Simulate a backend flow of creating orders, processing payments, and sending notifications | 24/07/2025 | 24/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 8 Achievements:

* Managed Authentication with Amazon Cognito:
  * Successfully built a complete sign-up/sign-in flow.
  * Knew how to use JWT tokens to authorize requests sent to the backend API.

* Solved bottleneck issues using Amazon SQS:
  * Understood and applied the Message Queue mechanism to buffer requests.
  * Ensured the system does not crash or drop data during sudden traffic spikes, increasing fault tolerance.

* Deployed Fanout Event-driven architecture with Amazon SNS & SQS:
  * Mastered the Pub/Sub model to broadcast information to multiple different services simultaneously.