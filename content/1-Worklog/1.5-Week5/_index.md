---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Week 5 Objectives:

* Grasp the concept of containerization, know how to package and deploy applications using Docker.
* Grasp the Infrastructure as Code (IaC) mindset to automate infrastructure management and provisioning.
* Use AWS CloudFormation to simultaneously deploy AWS resources through templates.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Deploy applications with Docker <br>&emsp; + Learn concepts of Containerization, Docker Engine, Image, Dockerfile <br> - **Practice:** <br>&emsp; + Install Docker engine <br>&emsp; + Pull and test-run basic base images                            | 29/06/2025 | 29/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Deploy applications with Docker <br>&emsp; + Container build and run process <br> - **Practice:** <br>&emsp; + Write Dockerfile to package applications <br>&emsp; + Build image and deploy container on EC2                                          | 30/06/2025 | 30/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Initialize Infrastructure as Code with AWS CloudFormation <br>&emsp; + Learn the IaC mindset <br>&emsp; + Structure of CloudFormation Templates (JSON/YAML) <br> - **Practice:** <br>&emsp; + Write a basic template defining Parameters and Resources| 01/07/2025 | 01/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Initialize IaC with AWS CloudFormation <br>&emsp; + Declare network resources <br> - **Practice:** <br>&emsp; + Write a template to automatically deploy Custom VPC, Subnet, Internet Gateway, and Security Group                                     | 02/07/2025 | 02/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Initialize IaC with AWS CloudFormation <br>&emsp; + Deploy the entire system <br> - **Practice:** <br>&emsp; + Launch a Stack to automatically deploy an EC2 instance and an RDS database via script                                                    | 03/07/2025 | 03/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 5 Achievements:

* Successfully packaged applications using Docker:
  * Understood the benefits of containerization in isolating the code execution environment, ensuring consistency between dev and production environments.
  * Independently wrote Dockerfiles to package real-world applications into standalone Docker Images.

* Automated cloud infrastructure with AWS CloudFormation (IaC):
  * Shifted mindset from manual operations on the AWS Console to managing infrastructure through code.
  * Launched a CloudFormation Stack capable of rebuilding the entire network architecture (VPC) and servers (EC2, RDS) consistently using automated scripts.