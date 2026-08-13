---
title: "Event 1 - FCAJ Community Day"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


## Event Overview

The **FCAJ Community Day (June 2026)** was organized by the **AWS Study Group / FCAJ Community**. This event was dedicated to exploring the latest shifts in the tech industry, focusing heavily on career trends in Cloud and AI Engineering, AI-driven FinOps and Cloud Security, and the architecture of enterprise AI solutions like Amazon Q Business and Model Context Protocol (MCP) Server.

---

## Event Objectives

My primary objectives for attending this community day were:
- To understand how the rapid adoption of AI agents and coding assistants impacts the future of software engineering roles.
- To discover practical applications of AI in specialized fields like FinOps and Cloud Security.
- To learn the infrastructure architectural requirements and cost considerations for deploying enterprise-grade private AI solutions.
- To network with industry professionals and align my internship learning path with current market demands.

---

## Main Content

The presentations and discussions centered around three major themes:

### 1. Career Trends in the Agentic AI Era
The tech industry is seeing rapid AI adoption, with AI agents and coding assistants significantly improving development productivity. Consequently, companies are raising recruitment standards, placing greater emphasis on candidates who can effectively leverage AI tools. As cloud systems grow, managing infrastructure becomes increasingly complex, and AI alone cannot fully understand the complete context of source code, cloud infrastructure, and business logic within large enterprise systems.

### 2. AI Applications in FinOps and Cloud Security
- **FinOps:** Finance teams often lack technical cloud knowledge, while cloud engineers may overlook financial cost management. AI bridges this gap by analyzing AWS billing data, detecting abnormal spending patterns, and recommending cost optimization strategies.
- **Cloud Security:** Security issues are sometimes overlooked or discovered too late. AI Agents can automate security assessments, review Infrastructure as Code (IaC) configurations, support penetration testing, and continuously analyze system logs to identify potential threats.

### 3. Cost Considerations for Private AI Infrastructure
When deploying enterprise AI solutions (such as Amazon Q Business or an MCP Server) inside a private AWS Virtual Private Cloud (VPC), organizations must consider the infrastructure costs to maintain a secure environment. Example monthly costs include:
- **Route 53 Resolver:** ~$180 (DNS resolution for private endpoints)
- **Application Load Balancer (ALB):** ~$32 (Routing requests to internal services)
- **EC2 instances:** Depends on instance type (Hosting MCP Server)
- **AWS Secrets Manager & Data Transfer:** Usage-based
Overall, the estimated fixed infrastructure cost is approximately USD 250–350 per month, excluding actual AI model usage and data processing costs.

---

## Knowledge Gained

By actively participating in the sessions, I took away several critical insights:
- **AI as a Collaborator, Not a Replacement:** Roles such as Cloud Engineer, DevOps, and Solution Architect remain essential because they require practical experience, architectural decision-making, and business understanding. Rather than viewing AI as a replacement, we should learn how to use it to automate repetitive tasks.
- **Hidden Infrastructure Costs:** Many AI projects focus only on LLM API pricing while overlooking the cost of supporting infrastructure (VPC networking, Load Balancers, Secrets Manager). 
- **Capacity Planning is Crucial:** Infrastructure costs must be estimated based on the expected number of users and projected monthly data transfer before deploying any AI solution into production.

---

## Application to Startups Blogs

The insights from the FCAJ Community Day directly influence how I approach the infrastructure of the **Startups Blogs** project:
- **Proactive Cost Management (FinOps mindset):** I will pay closer attention to the AWS billing dashboard and optimize resource usage for the Startups Blogs environment, ensuring our architecture is not just functional but also cost-effective.
- **Security First:** Applying AI concepts to our security practices, such as rigorously reviewing our IaC configurations and IAM roles to prevent vulnerabilities from reaching our production deployment.
- **Future-proofing Architecture:** Understanding the underlying infrastructure needed for private AI (VPCs, ALB, Route 53) prepares me for future scenarios where we might need to integrate AI agents securely into the Startups Blogs platform.

---

## Photos

![FCAJ Community Day](/images/events/event3.jpeg)
<p align="center"><em>Figure 1. Group photo at the FCAJ Community Day - June 2026 event.</em></p>

---

## Conclusion

Attending the **FCAJ Community Day** was a highly rewarding experience that broadened my perspective on the intersection of Cloud Computing and AI. It reinforced the reality that while AI tools are transforming how we write code, the core engineering skills—system design, security, and operational reliability—are more important than ever. The lessons on FinOps and infrastructure cost planning provided a practical reality check that will undoubtedly benefit my decision-making process in the Startups Blogs project and my future career as a Cloud Engineer.
