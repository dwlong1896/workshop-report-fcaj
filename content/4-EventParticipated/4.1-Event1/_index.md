---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: “Final Competition of Cloud Architect and Meeting”

### Purpose of the Event

- Final Competition of Cloud Architect
- Securing Web Apps with AWS Security Agent
- Introduction to Service Level Agreement (SLA) and Monitoring
- An effective roadmap to conquering the AWS Cloud Practitioner exam

### List of Speakers

- **Thinh Nguyen** - DevOps/DevSecOps/Cloud Engineer, Styl Solutions First Cloud AI Journey
- **Ngo Le Tan Huy** - Admin First Cloud AI Journey
- **Nguyen Huynh Son** - Admin First Cloud AI Journey

### Key Highlights
#### Final Competition of Cloud Architect
- The competition between the two teams KAKAT and Ngu Dai Hiep was extremely thrilling.
- Challenging questions revolving around system architecture, security, and AWS services.


#### Securing Web Apps with AWS Security Agent
##### Introduction to Frontier Agent

- Automated reasoning, utilizing Amazon Bedrock to plan and execute tasks without human intervention.
- Full lifecycle encompassing design review, source code security, and penetration testing.
- Performing actual exploits to verify vulnerabilities instead of just predicting them.

##### Key Features of Frontier Agent

- Design Review: Analyzes architectural documents before coding, supporting standards such as PCI DSS, NIST CSF, and AWS Well-Architected.
- Code Review: Integrates directly into PRs on GitHub/GitLab, automatically proposing patches.
- Automated Pentesting: Simulates multi-step exploit chains, authenticates as a real user, and provides detailed attack graphs.

##### Technical Limitations
- Authentication Blocking: The agent cannot bypass complex security layers such as MFA, biometrics, or mTLS.
- Logic Flaws: Difficulty in detecting fraud based on complex business logic.
- Cost Control: Complex applications can consume execution hours very quickly, requiring close monitoring.

#### Introduction to Service Level Agreement (SLA) and Monitoring

##### Foundation of SLA and Risk Management
- SLA is a commitment to the service quality level between a provider and a customer.
- SLA does not guarantee the entire user experience; it is only a part of risk management.
- Risk management includes identification, monitoring, response, and continuous improvement.

##### The Monitoring Pyramid Mindset
- The monitoring pyramid tracks everything from infrastructure to user experience.
- Monitoring infrastructure alone is insufficient to detect all issues.
- Upper-layer monitoring helps detect impacts on users and the business early.

##### Practical Illustration via Demo
- Infrastructure might report as normal even though dependent services are failing.
- Health checks might succeed, but users still cannot log in.
- Infrastructure metrics do not fully reflect the actual user experience.

##### Alerting and Response Process
- Effective monitoring must detect incidents before customers report them.
- CloudWatch converts metrics into alerts sent via Email or Slack.


#### Introduction to the Roadmap for Conquering the AWS Cloud Practitioner Certificate

##### Overview and Structure of the AWS Cloud Practitioner Exam (CLF-C02)
- 65 questions in 90 minutes 
- Passing score: 700/1000
- Validity: 3 years
- Cloud Concepts (24%), Security and Compliance (30%), Cloud Technology and Services (34%), Billing, Pricing, and Support (12%)

##### Core AWS Services for Technology and Infrastructure 
- Includes Compute (EC2, Lambda), Storage (S3, EBS), and Networking (VPC, Route 53).

##### Revision Strategies and Effective Exam Tips
- Using the elimination method.
- Associating keywords with specific use cases.

### What Was Learned

#### Knowledge and Mindset for Automated Security
- Understanding the superiority of applying AI (like Amazon Bedrock via Frontier Agent) into the security process (DevSecOps).
- Grasping the capability to automate design assessment, code review, and pentesting without much human intervention.

#### Risk Management and System Monitoring Mindset
- Realizing that SLA is just part of the service commitment, and system monitoring needs to focus on actual user experience instead of merely looking at infrastructure metrics (CPU, RAM).
- Understanding how the monitoring pyramid works and the necessity of configuring early alerts via CloudWatch to proactively respond before customers complain.

#### AWS Learning Roadmap and Strategy
- Mastering the exam structure and the weight of each section in the AWS Cloud Practitioner (CLF-C02) exam.
- Gaining effective exam strategies such as the elimination method and associating keywords with specific use cases of core AWS services (EC2, S3, VPC...).

### Event Experience

Attending the **“Final Competition of Cloud Architect and Meeting”** event was a very rewarding experience, providing me with a comprehensive view of security, system monitoring, and especially AWS certification orientation. Some notable experiences:

#### The vibrant and dramatic atmosphere of the final round
- The competition between the two teams KAKAT and Ngu Dai Hiep not only brought excitement but was also a great opportunity for me to listen to how seniors solved tough problems regarding system architecture and security on AWS.

#### Expanding perspective on application security with AI
- For the first time, I heard in detail about using Agents (Frontier Agent) to automate the entire security lifecycle. Although there are still technical limitations such as MFA blocking or complex logic flaws, the potential of AI in information security is immense.

#### Changing mindset about monitoring
- The demo on SLA and Monitoring truly touched upon practical issues: a system can report as "safe", but users still cannot use it. This helped me realize the importance of monitoring from the user's perspective.

#### Gaining additional motivation to learn
- Listening to the sharing about the AWS Cloud Practitioner exam roadmap helped me outline a clearer study plan, reducing ambiguity and giving me more motivation to conquer this certificate soon.

#### Lessons Learned
- A "Security by Design" mindset is necessary, and one must always put user experience at the center when building and monitoring any system.
- Taking certification exams is not just to get a degree, but more importantly, to learn how to think and master the practical use cases of cloud systems.

#### Some pictures from the event
![Cloud Architect Final Competition](/images/event1a.jpg)
![Meeting First Cloud AI Journey](/images/event1b.jpg)
> Overall, the event not only provided deep technical knowledge but also strongly inspired me, helping me more clearly shape my architectural design thinking as well as my professional development path on the AWS cloud platform.
