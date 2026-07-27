---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:

* Apply modular design principles (modularity) to transition applications from Monolith to Microservices.
* Deploy and operate Containers following the Serverless model via AWS Fargate.
* Get acquainted with a large-scale Container Orchestration platform (Kubernetes) via Amazon EKS.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                            | Start Date | Completion Date | Reference Material                        |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Monolith to Microservices with Docker and AWS Fargate <br>&emsp; + Learn about Amazon ECS and Fargate architecture <br> - **Practice:** <br>&emsp; + Create an ECS Cluster <br>&emsp; + Write a Task Definition to define resources (CPU, RAM) for the Docker container | 27/07/2025 | 27/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Monolith to Microservices with Docker and AWS Fargate <br>&emsp; + Load Balancing for Containers <br> - **Practice:** <br>&emsp; + Deploy an ECS Service running on Fargate <br>&emsp; + Integrate an Application Load Balancer to distribute traffic                       | 28/07/2025 | 28/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Get acquainted with Amazon EKS <br>&emsp; + Learn about Kubernetes (K8s) architecture <br>&emsp; + Concepts of Control Plane, Worker Node, Pod <br> - **Practice:** <br>&emsp; + Install and configure CLI tools                                                            | 29/07/2025 | 29/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Get acquainted with Amazon EKS <br>&emsp; + Initialize Kubernetes infrastructure on AWS <br> - **Practice:** <br>&emsp; + Use `eksctl` to provision an EKS Cluster <br>&emsp; + Initialize a Managed Node Group to allocate compute capacity                                | 30/07/2025 | 30/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Get acquainted with Amazon EKS <br>&emsp; + Deploy applications to Kubernetes <br> - **Practice:** <br>&emsp; + Write YAML manifests (Deployment, Service) <br>&emsp; + Apply manifests to run application Pods and expose them to the public internet                      | 31/07/2025 | 31/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 9 Achievements:

* Transitioned to Microservices architecture:
  * Applied modularity to separate application layers.
  * Packaged and ran backend and frontend services in independent containers.
* Operated Serverless Containers with AWS Fargate:
  * Ran Docker containers in production without the need to provision underlying servers.
  * Integrated a Load Balancer to automatically route traffic to containers.
* Mastered Kubernetes platform on AWS (EKS):
  * Understood how an enterprise-standard orchestration platform operates.
  * Successfully initialized a cluster, managed Nodes, and used declarative code (YAML files) to deploy and manage the lifecycle of application Pods.