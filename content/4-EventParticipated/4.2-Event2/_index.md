---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “FCAJ x Agentic AI Build Week”

### Purpose of the Event

- Sharing information and experience from the Hackathon competition
- Introducing the products of the teams participating in the Hackathon


### List of Speakers

- **Mr. Nguyen Gia Hung** - Head of Solutions Architect in Vietnam
- **Mr. Joseph Marazota** - Head of Technology of Asia
- **Hackathon participating teams**

### Key Highlights

#### OneTeam - KFC Order Chatbot via Conversation
- Multi-channel ordering chatbot via Zalo and WhatsApp, customers order directly within the chat window.
- Uses Bedrock **AgentCore**, **Tiny Fish** to scrape menu data from the KFC website and save it to DynamoDB; includes an order confirmation step before finalizing to prevent repetitive errors like McDonald's.
- Relatively cheap cost, end-to-end latency is only 3-4 seconds.
#### Signal C – Competitor Strategy Analysis 
- Multi-agent architecture collecting discrete signals (financial reports, news...) to synthesize competitor strategy information and estimate ROI.
- Supervisor-agent architecture coordinating sub-agents, with a self-grading & retry mechanism before requiring human review.
- Issue: Costs increase sharply due to dependence on third-party services.
#### BL Team – Generating AWS Architecture from Natural Language
- Solves the tight deadline pressure for Solution Architects: input requirements, AI draws the architecture, edits, exports pricing, and deploys automatically.
- Has a mechanism to block unauthorized services right from the output; the challenge is ensuring consistent output.
#### 3K – Crowd Monitoring with AI Cameras 
- Uses YOLO + ByteTrack to detect, count people by area, alert when overloaded, and suggest coordination.
- Lessons on cost optimization when choosing AI models.
#### Six Pillar – Assisting Anti-Money Laundering Investigations for Banks
- Solves the problem of 90-95% of alerts being false positives, reducing case processing time from ~3 hours to a few minutes.
- 3-tier architecture: Fast Detection, Deep Investigation, Case Management 
### What Was Learned
 
#### Clearly Define Scope 
- Avoid trying to include too many features.
- Aim for a "just enough" MVP to prove the idea within a limited time.
#### Prioritize Execution Over Theory
- The product must run, so deploy it for real.
#### Teamwork 
- Debate the issue, no personal attacks.
- Clear role division based on each person's strengths.
#### Find the Right Practical Pain Point
- Fancy technology is meaningless if it does not solve the actual business problem of the customer and the market.
#### Cost Control and Hallucination Mitigation
- Optimize costs right from the beginning.
- Use double-checks and guardrails to reduce AI hallucinations.
- Always keep humans in the decision loop.
### Application to Work
- Design systems following the supervisor-agent model coordinating specialized sub-agents instead of one agent doing everything.
- Use pre-filtering and deep-processing architecture to optimize AI costs at scale.
- Always design stopping points for human intervention on high-risk decisions.
### Event Experience
 
#### Hackathon Atmosphere
- The seniors brought an overnight working atmosphere, many funny moments while still maintaining an optimistic spirit. 
- A never-give-up spirit despite many difficulties, members coming from various backgrounds, having to present to the judging panel in a short time.
#### Lessons Learned
- Through this, I learned that strong psychological preparation is as important as technical skills; boldly participate even without experience; networking is also a great value of hackathons.


#### Some pictures from the event
![FCAJ x Agentic AI Build Week](/images/event2a.jpg)
![FCAJ x Agentic AI Build Week](/images/event2b.jpg)
> Overall, the event not only provided technical knowledge but also helped me change my mindset about application design, system modernization, and coordinating more effectively among teams.
