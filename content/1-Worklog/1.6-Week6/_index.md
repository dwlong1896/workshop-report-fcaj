---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
### Week 6 Objectives:

* Manage and securely access EC2 servers without managing SSH Keys or opening public ports.
* Ensure data safety by setting up an automated backup strategy for the entire system.
* Master pricing models to optimize operating costs on AWS.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                                 | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Work with AWS Systems Manager – Session Manager <br>&emsp; + Learn about Systems Manager architecture and SSM Agent <br> - **Practice:** <br>&emsp; + Configure IAM Role to allow EC2 to communicate with Systems Manager <br>&emsp; + Check the SSM Agent on the EC2 instance | 06/07/2025 | 06/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Work with AWS Systems Manager – Session Manager <br>&emsp; + Security best practices when accessing servers <br> - **Practice:** <br>&emsp; + Access the EC2 shell directly on the web console via Session Manager                                                 | 07/07/2025 | 07/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Deploy a system backup plan with AWS Backup <br>&emsp; + Learn about centralized backup management mechanisms on AWS <br> - **Practice:** <br>&emsp; + Create a Backup Vault to safely store backups <br>&emsp; + Configure a Backup Plan defining automated schedules       | 08/07/2025 | 08/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Deploy a system backup plan with AWS Backup <br>&emsp; + Manage the lifecycle of recovery points <br> - **Practice:** <br>&emsp; + Assign resources (EC2, RDS) to the Backup Plan <br>&emsp; + Practice the data Restore process from a backup                           | 09/07/2025 | 09/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Optimize costs with Savings Plans and Reserved Instances <br>&emsp; + Learn about pricing models (On-Demand, Reserved, Savings Plans) <br> - **Practice:** <br>&emsp; + Analyze usage and compare costs between models <br>&emsp; + Plan right-sizing for EC2 and RDS        | 10/07/2025 | 10/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 6 Achievements:

* Securely managed servers with AWS Systems Manager:
  * Eliminated the risk of exposing SSH Keys and potential security vulnerabilities from opening port 22 to the internet.
  * Successfully accessed the command line of an EC2 instance directly from the web browser via Session Manager.
* Ensured data protection with AWS Backup:
  * Set up a centralized automated backup mechanism for multiple resource types based on defined policies.
  * Mastered the restore process, ensuring fast disaster recovery capabilities and maintaining data integrity during system incidents.
* Optimized costs with Savings Plans and Reserved Instances:
  * Mastered cost optimization strategies through usage commitments with Savings Plans and Reserved Instances.
  * Knew how to choose suitable commitment plans to minimize costs for long-term and stable workloads, compared to default On-Demand pricing.