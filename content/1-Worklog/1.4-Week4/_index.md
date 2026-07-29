---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Master the Database Migration process from on-premise systems to AWS RDS.
* Use AWS DMS and SCT to convert schema and replicate data with minimal downtime.
* Practice migrating a virtual machine from an on-premise environment to Amazon EC2 following the Lift-and-Shift model.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                             | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Database Migration with AWS DMS & SCT <br>&emsp; + Learn about the architecture of AWS Database Migration Service <br> - **Practice:** <br>&emsp; + Launch a Replication Instance <br>&emsp; + Configure Source and Target Endpoints           | 22/06/2025 | 22/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Database Migration with AWS DMS & SCT <br>&emsp; + Learn about the Schema Conversion Tool <br> - **Practice:** <br>&emsp; + Install AWS SCT <br>&emsp; + Evaluate and convert schema from the source database to the target RDS                | 23/06/2025 | 23/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Database Migration with AWS DMS & SCT <br>&emsp; + Migration Task execution flow <br> - **Practice:** <br>&emsp; + Run a Migration Task to replicate data <br>&emsp; + Check data integrity after synchronizing to RDS                         | 24/06/2025 | 24/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Migrate virtual servers with AWS VM Import/Export <br>&emsp; + Learn the process of importing/exporting virtual machines (VMware, VirtualBox...) <br> - **Practice:** <br>&emsp; + Prepare a VM image in a supported format (OVA, VMDK) <br>&emsp; + Configure IAM Role for the Import feature | 25/06/2025 | 25/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Migrate virtual servers with AWS VM Import/Export <br>&emsp; + Lift-and-Shift deployment model <br> - **Practice:** <br>&emsp; + Execute the command to import a VM into an Amazon Machine Image (AMI) <br>&emsp; + Launch an EC2 Instance from the newly created AMI | 26/06/2025 | 26/06/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 4 Achievements:

* Successfully migrated database with AWS DMS and SCT:
  * Knew how to use SCT to evaluate compatibility and automatically convert schema to the target database.
  * Successfully established a continuous data replication flow using DMS, allowing large-scale data migration to the Cloud while the on-premise system remains operational.

* Migrated server infrastructure to the Cloud with AWS VM Import/Export:
  * Grasped the Lift-and-Shift method.
  * Successfully packaged and imported an internal virtual machine into an AMI, then operated it stably in the Amazon EC2 environment.