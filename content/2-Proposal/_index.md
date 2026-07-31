---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Cloud E-Wallet  
## An E-wallet System Utilizing AWS Cloud Computing Architecture


### 1. Overview

Our team proposes the **Cloud E-Wallet** project, a simulated e-wallet web application that allows users to manage their accounts, top-up, withdraw, transfer money, and pay for online services. In addition to building the core transaction features, the project also focuses on deploying and operating the entire system on the AWS cloud infrastructure. The objective of the project is to provide a comprehensive practical environment, helping the team grasp the actual software operation process. Since this is purely an educational project, all transactions are simulated and completely independent of actual banking systems.

### 2. Problem Statement
#### *Current Issues*
In daily life, traditional financial transactions using cash often bring many inconveniences such as waiting time, risk of loss, confusion when giving small change, and especially the difficulty in systematically tracking expenses. Furthermore, paying for utilities such as electricity, water, or telecommunications via traditional methods requires users to go to collection points, consuming time and effort.
Additionally, deploying an e-wallet application requires high security, consistent transaction data, and a scalable system. If the team only develops and tests on a personal computer (localhost), it will be difficult to evaluate actual performance, lacking an environment to configure domains, isolate network traffic, or set up HTTPS security. This creates a need for a comprehensive cloud deployment solution to thoroughly resolve the above issues.

#### *Solution*

To address the shortcomings of traditional payments, the **Cloud E-Wallet** platform uses AWS services to deploy the system: **Amazon EC2** and **Application Load Balancer (ALB)** serve to process transactions smoothly; **Amazon RDS** (MySQL) is used to store data securely, applying database transactions to ensure balance integrity; **Amazon S3** and **CloudFront** provide a high-speed user interface. Finally, the system integrates **Amazon SES** for automated email verification, delivering a seamless and secure experience just like real financial applications.

### 3. Solution Architecture

#### *Diagram*

![Cloud E-Wallet deployment architecture on AWS](/images/5-Workshop/5.1-Prerequisites/architecture.png)
<p align="center"><i>Deployment Diagram</i></p>

Flow description:
1. **Access:** Users access via a domain managed by **Cloudflare DNS**, then are routed to **Amazon CloudFront**.
2. **Routing:** CloudFront directs static UI load requests to **Amazon S3**, and routes API call requests to the **ALB** load balancer.
3. **Logic Processing:** ALB evenly distributes API requests to **Amazon EC2** servers to process e-wallet transactions.
4. **Data & Communication:** EC2 stores data in the **Amazon RDS** database and uses **Amazon SES** to send automated emails.
5. **Monitoring:** System activities are tracked via **Amazon CloudWatch**.

#### *Services Used*

| Component | Role |
| --- | --- |
| Cloudflare DNS | Manages `cloud-ewallet.com` and sender domain verification records |
| CloudFront | Receives HTTPS from browsers; routes frontend and `/api/*` |
| S3 | Stores static React build files |
| ALB | Forwards APIs, performs backend health checks |
| EC2 | Runs Spring Boot in Docker |
| RDS MySQL | Stores data in a private subnet |
| Amazon SES SMTP | Sends verification and password reset emails; uses SMTP `587`, authentication, and STARTTLS |
| CloudWatch | Monitors AWS service metrics |

### 3.3. Component Design

- **Domain Resolution:** Cloudflare DNS is responsible for managing the `cloud-ewallet.com` domain and storing records for email verification.
- **Web Interface:** Amazon S3 stores the static files of the React application, combined with the Amazon CloudFront content delivery network to speed up access and provide secure connections via HTTPS.
- **Routing & Load Balancing:** Application Load Balancer (ALB) receives API requests, performs health checks, and safely distributes the load to backend servers.
- **Business Logic Processing:** Amazon EC2 acts as the compute server, running Spring Boot (Docker) containers to handle all e-wallet transaction logic.
- **Data Storage:** Amazon RDS (MySQL) is deployed independently in a private subnet to absolutely protect user information, balances, and transaction history.
- **User Communication:** Amazon SES SMTP handles sending automated verification and password recovery emails through a STARTTLS connection.
- **System Monitoring:** Amazon CloudWatch is used to monitor performance metrics and record the actual operational status of AWS services.

## 4. Functional Scope

### 4.1. User

- Register, verify/resend verification email, log in, and log out.
- Forgot and reset password.
- View/update profile and balance.
- Simulated top-up, lookup recipient, transfer money, and pay for services.
- View transaction history.

### 4.2. Administrator

- Overview dashboard.
- View and lock/unlock users.
- View transactions.
- Add, edit, activate, or deactivate services.


## 5. Technical Implementation

### Implementation Phases

Our team implemented the project through five phases:

1. **Research and Design:** Analyze requirements, define the scope of the simulated e-wallet, design the database and frontend – backend – AWS architecture.
2. **Local Development:** Build the React frontend, Spring Boot REST API, and MySQL; complete authentication, authorization, wallet business logic, and admin page.
3. **Packaging and Cloud Preparation:** Test backend/frontend, Dockerize Spring Boot, create VPC, subnets, Security Groups, and prepare RDS.
4. **Deployment and Integration:** Deploy frontend to S3/CloudFront, run backend containers on EC2 behind ALB, connect to RDS, configure Cloudflare DNS, and Amazon SES SMTP.
5. **Testing and Refinement:** Perform health checks, smoke tests for business features, verify emails, review network security, monitor costs, and finalize documentation.

### Technical Requirements

- **Frontend:** React 19, TypeScript, and Vite; built into static files on S3, distributed via CloudFront, and supports responsive design.
- **Backend:** Java 17, Spring Boot, Spring Security, JDBC, and Actuator; packaged with Docker, runs on EC2 port `8080`, and only accepts application traffic from ALB.
- **Database:** Amazon RDS for MySQL in a private subnet; Security Group only allows backend EC2 to connect on port `3306`; Vietnamese data uses `utf8mb4`.
- **Email:** Amazon SES SMTP in `ap-southeast-1`, port `587`, authentication, and STARTTLS; domain identity/DKIM verified via Cloudflare.
- **Security:** BCrypt, time-limited JWT, `user`/`admin` roles, secrets stored outside Git, HTTPS from users to CloudFront, and inbound traffic restricted by Security Groups.
- **Operations:** ALB uses `/actuator/health` for health checks; CloudWatch provides AWS metrics; frontend and backend are currently deployed manually.

## 6. Execution Plan

| Phase | Detailed Tasks |
| --- | --- |
| Week 1 | Survey requirements, design overall AWS architecture, database schema, and prepare source code repository. |
| Week 2 | Initialize project, configure local development environment, set up basic APIs, and frontend directory structure. |
| Week 3 | Program core modules: Registration, login (JWT), user authentication, and authorization (Admin/User). |
| Week 4 | Program e-wallet business logic (1): Integrate top-up feature, track balances, and manage account information. |
| Week 5 | Program e-wallet business logic (2): Transfer features, service payments, and recording transaction history. |
| Week 6 | Build the Admin Dashboard interface, test (Unit test/Integration test) the entire system locally. |
| Week 7 | Package application (Dockerize Spring Boot) and configure basic AWS network infrastructure (VPC, Security Groups, EC2, RDS). |
| Week 8 | Deploy auxiliary AWS services: Set up S3, CloudFront for frontend, and configure Application Load Balancer (ALB). |
| Week 9 | Configure domain with Cloudflare DNS, integrate email verification feature using Amazon SES, and perform production testing. |
| Week 10 | Final evaluation, performance optimization, handle outstanding bugs, finalize project report and user guide documentation. |

## 7. Budget Estimation

The costs below are **estimates**, not actual invoices. Our team assumes resources are placed in the Singapore Region (`ap-southeast-1`), using On-Demand pricing, running 730 hours/month, excluding taxes or Free Tier. The maximum level is only an upper bound within the scope of the report's assumptions; AWS does not automatically limit costs if traffic or resources continue to increase.

### Initial Costs

| Expense Item | Cost |
| --- | ---: |
| Purchase `cloud-ewallet.com` domain via Cloudflare | **$10.98** |
| AWS services setup fee | **$0.00** |
| **Total initial costs, paid once** | **$10.98** |

The domain is recorded as an initial purchase based on the amount the team paid and **is not allocated to the monthly maintenance cost** in the table below.

### Usage Assumptions

| Category | Minimum | Average | Assumed Maximum |
| --- | --- | --- | --- |
| EC2 and EBS | 1 `t3.micro`, 730 hours, 8 GB gp3 | Same as minimum | Same as minimum |
| RDS MySQL | 1 `db.t3.micro` Single-AZ, 20 GB | Same as minimum | Same as minimum |
| ALB | 730 hours, avg 0.1 LCU | 730 hours, avg 0.3 LCU | 730 hours, avg 1 LCU |
| S3 | 1 GB, few requests | 5 GB, approx 30,000 GET & 3,000 PUT | 20 GB, approx 100,000 GET & 10,000 PUT |
| CloudFront | 5 GB and approx 50,000 requests | 30 GB and approx 250,000 requests | 100 GB and approx 1,000,000 requests |
| Amazon SES | 1,000 text emails/month | 3,000 text emails/month | 10,000 text emails/month |
| CloudWatch | Basic metrics only | 1 GB log ingested | 5 GB log ingested |

### Monthly Maintenance Costs

| Service | Minimum (USD) | Average (USD) | Assumed Maximum (USD) |
| --- | ---: | ---: | ---: |
| EC2 `t3.micro` | 9.64 | 9.64 | 9.64 |
| EBS gp3 8 GB | 0.80 | 0.80 | 0.80 |
| RDS MySQL `db.t3.micro` + 20 GB | 21.74 | 21.74 | 21.74 |
| Application Load Balancer + LCU | 18.98 | 20.15 | 24.24 |
| S3 storage and requests | 0.03 | 0.15 | 0.70 |
| CloudFront data transfer and requests | 0.61 | 3.65 | 12.10 |
| Amazon SES | 0.16 | 0.48 | 1.60 |
| CloudWatch | 0.00 | 0.50 | 2.50 |
| **Estimated total maintenance/month** | **51.96** | **57.11** | **73.32** |
| **First-month total if adding domain cost** | **62.94** | **68.09** | **84.30** |

### Conditions for Each Cost Level

- **Minimum – $51.96/month:** The demo system runs continuously with one `t3.micro` EC2, one `db.t3.micro` Single-AZ RDS, and one ALB; max ~1 GB on S3, 5 GB via CloudFront, 1,000 SES emails, and uses only basic CloudWatch metrics. Does not include Free Tier, taxes, snapshots, or additional resources outside the table.
- **Average – $57.11/month:** Maintains the same compute/database configuration but with more frequent usage: ~5 GB S3, 30 GB CloudFront, 3,000 SES emails, 1 GB CloudWatch Logs, and an average of 0.3 LCU. This is a suitable scenario for teams doing trials and periodic demonstrations.
- **Assumed Maximum – $73.32/month:** Still keeps one small-sized EC2 and RDS but assumes traffic increases to 20 GB S3, 100 GB CloudFront, 10,000 SES emails, 5 GB logs, and an average of 1 LCU. If there's a need to upgrade the EC2/RDS type, add targets, Multi-AZ, NAT Gateway, WAF, or exceed these thresholds, the actual cost may be higher than this level.

AWS prices change over time, by Region, account type, and actual usage. References: [AWS EC2 Pricing](https://aws.amazon.com/ec2/pricing/on-demand/), [Amazon RDS for MySQL Pricing](https://aws.amazon.com/rds/mysql/pricing/), [Elastic Load Balancing Pricing](https://aws.amazon.com/elasticloadbalancing/pricing/), [Amazon CloudFront Pricing](https://aws.amazon.com/cloudfront/pricing/), [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/), and [Amazon SES Pricing](https://aws.amazon.com/ses/pricing/).

## 8. Risk Assessment and Mitigation Strategy

| Risk | Impact Level | Likelihood | Mitigation Strategy |
| --- | --- | --- | --- |
| **Exposure of sensitive data (Credentials)** | Very High | Low | - Remove all sensitive information (DB passwords, JWT secrets, AWS keys) from the source code.<br>- Use a local `.env` file and the platform's environment variable management feature when deploying to the cloud. |
| **Transaction & balance data discrepancy** | Very High | Medium | - Apply **Database Transactions** (ACID) for all top-up/transfer operations.<br>- Use Row-level locking mechanisms in MySQL to prevent overwrite errors when there are many concurrent transactions (Race condition). |
| **Backend service disruption (Downtime)** | High | Medium | - Establish continuous **Health check** mechanisms via ALB to remove faulty nodes.<br>- Configure Docker to automatically restart containers upon application crashes. |
| **Uncontrollable AWS costs** | Medium | Medium | - Regularly monitor the **AWS Billing & Cost Explorer** dashboard.<br>- Proactively cleanup unused resources after the project ends. |
| **Email sending feature disruption (SES)** | Medium | High | - Complete configuring DNS records (DKIM, SPF) on Cloudflare to prevent emails from being marked as spam.<br>- Monitor bounces, complaints, and sending limits in Amazon SES. |

## 9. Achieved Results

The Cloud E-Wallet project delivers specific functional values:

- **For End Users:** Provides a convenient, secure online e-wallet platform. Users can easily top up (simulated), perform internal transfer transactions quickly, and pay for utility bills (electricity, water, internet, etc.) with just a few clicks. All spending histories are transparently stored and summarized to help manage personal finances more effectively.
- **For Administrators:** Provides an intuitive central Admin Dashboard, allowing strict management of user accounts, panoramic tracking of the simulated cash flow within the system, as well as flexible monitoring and configuration of the service payment categories.
- **System Perspective:** A platform deployed on AWS with HTTPS, network separation, and access control using Security Groups. User experience is optimized with fast page load speeds, secure authentication with encryption, and smooth automated operational processes.