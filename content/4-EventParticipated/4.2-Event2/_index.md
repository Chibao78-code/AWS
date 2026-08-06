---
title: "Event 2"
date: 2026-08-06
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# AWS, DEVOPS, AI, AND SECURITY MEETUP REPORT

## 1. Event overview

Event 2 connected five areas that are highly relevant to the technology industry: real-time systems on AWS, Docker containerization, GraphRAG, Machine Learning for intrusion detection, and a career journey from IT Helpdesk to Cloud/DevOps.

Although each session used a different technology stack, the common message was that tools should not be selected simply because they are popular. Architecture must begin with latency, scalability, reliability, security, and the team's ability to operate the resulting system.

## 2. Event objectives

- Share examples of AWS services used in real projects.
- Clarify Docker's role in software development and deployment.
- Introduce the combination of Generative AI and graph databases.
- Explain how Machine Learning can complement rule-based network defenses.
- Provide practical career guidance for System Administration, Cloud, and DevOps.
- Give students an opportunity to learn from speakers and the technology community.

## 3. Speakers

- **Nguyen Quoc Bao**
- **Huynh Quoc Bao**
- **Viet Phat**
- **Le Hoang Gia Dai**
- **Tran Trung Vinh**

## 4. Main sessions

### 4.1 Multiplayer in the Cloud – connecting Godot clients with AWS WebSockets

Nguyen Quoc Bao presented the communication problem in multiplayer games. UDP, WebSocket, and HTTP Polling were compared according to connection behavior, latency, and implementation complexity.

WebSocket is suitable when clients and servers require continuous two-way communication without creating a new HTTP request for every update. In the presented model, Godot clients connect to AWS infrastructure, Lambda processes event-driven logic, and DynamoDB stores state required for matchmaking or game sessions. AWS GameLift was introduced as a more specialized option for large-scale real-time games.

The key lesson was that real-time behavior depends on more than a protocol. A system must also manage connection lifecycles, player identity, disconnections, retry behavior, and state consistency across clients.

### 4.2 Docker and the containerization model

Huynh Quoc Bao explained the difference between virtual machines and containers. A virtual machine provides isolation by running a guest operating system, while a container shares the host kernel and packages the application with its required dependencies. Containers therefore tend to start faster and consume fewer resources.

Docker creates a repeatable environment from development to deployment. An image describes the package, while a container is a running instance of that image. Its practical value is reducing “works on my machine” differences, standardizing builds, and providing a foundation for CI/CD and microservices.

Containerization does not automatically solve every operational concern. Teams still need to manage secrets, storage, logs, networking, image vulnerabilities, and update procedures.

### 4.3 Building GraphRAG with Amazon Bedrock and Amazon Neptune

Viet Phat introduced Retrieval-Augmented Generation and the limitations of retrieving isolated text chunks. When a question requires multi-hop reasoning, similarity search alone may miss the relationships required to form a complete answer.

GraphRAG adds a Knowledge Graph to represent entities and relationships. Amazon Neptune manages graph data, while Amazon Bedrock provides foundation models for response generation. This approach can improve multi-step retrieval and make the relationship chain behind an answer more explicit.

The session also highlighted the trade-off between managed services and open-source solutions. Managed services reduce operational effort, but teams must evaluate cost, customization, data control, and vendor dependency.

### 4.4 Machine Learning-based NIDS on AWS

Le Hoang Gia Dai presented an architecture combining AWS WAF with a Machine Learning-based Network Intrusion Detection System. WAF is effective for known rules, but a purely rule-based approach may struggle with new behavior or complex signal patterns.

The project used the CSE-CIC-IDS2018 dataset to train a traffic-classification model and displayed results through a real-time dashboard. Machine Learning served as an additional detection layer for suspicious patterns, while WAF continued to filter requests according to configured rules.

An ML model does not replace conventional security controls. Its usefulness depends on data quality, feature selection, false-positive rates, model updates, and a human process for verifying alerts.

### 4.5 From IT Helpdesk to Senior System Administrator

Tran Trung Vinh shared a career progression from IT Helpdesk to System Administration and toward Cloud/DevOps. Helpdesk experience builds a foundation in user communication, information gathering, incident classification, and structured troubleshooting.

Linux, networking, access control, system services, and automation become core skills for a Sysadmin. These fundamentals remain relevant in Cloud/DevOps: cloud services change how resources are provisioned but do not remove the need to understand operating systems and networks.

The career and interview discussion emphasized building skills step by step, practicing through projects, and explaining technical decisions rather than memorizing tool names.

## 5. Knowledge gained

### 5.1 Technical knowledge

- Learned which factors influence the choice between UDP, WebSocket, and HTTP Polling.
- Understood how containers differ from virtual machines and how Docker improves deployment consistency.
- Learned why a Knowledge Graph can improve RAG tasks that require multi-hop reasoning.
- Recognized the complementary roles of AWS WAF, NIDS, and Machine Learning in defense in depth.
- Understood that Linux, networking, and troubleshooting are shared foundations for Sysadmin, Cloud, and DevOps roles.

### 5.2 Architecture and career mindset

- Select services according to requirements rather than popularity.
- Evaluate operational cost and complexity before adopting a managed service.
- Include observability, security, and deployment in the design from the beginning.
- Learn through real projects and document the reasoning used to solve problems.
- Build a career roadmap from fundamentals toward specialized tools.

## 6. Application to Splitly

The event ideas can be applied selectively to Splitly:

1. **Real-time notifications:** WebSocket may support future group notifications or settlement-status updates. REST APIs remain simpler for the current scale; WebSocket should be introduced only for a clear real-time requirement.
2. **Containerization:** packaging the Node.js backend with Docker would improve build consistency and prepare for CI/CD. It is a later step after the current EC2 + PM2 process is stable.
3. **Purposeful AI:** GraphRAG is unnecessary for core bill splitting. If Splitly later provides an assistant for complex expense-history or transaction-relationship questions, Bedrock and Neptune should be evaluated against measurable value and cost.
4. **Defense in depth:** the future architecture includes AWS WAF, but it still requires least-privilege Security Groups, CloudWatch logs, dependency updates, and an incident process. ML-based NIDS becomes reasonable only when sufficient traffic and evaluation data exist.
5. **Operations fundamentals:** Linux, networking, and troubleshooting directly support Nginx, PM2, ports, DNS, IAM, and MongoDB/S3 connectivity diagnosis.
6. **Repeatable delivery:** Docker and DevOps practices encourage the team to document and automate builds, tests, and infrastructure instead of relying on undocumented manual steps.

## 7. Experience and reflection

I appreciated that each technology was presented through a concrete problem: multiplayer requires persistent communication, Docker addresses environment differences, GraphRAG models connected knowledge, NIDS detects suspicious behavior, and a Sysadmin keeps systems operating. AWS services therefore became tools within architecture decisions rather than a disconnected list of product names.

![Photo from the event](/images/4-Event/Splitly/event-2-meetup-2026.jpg)

> The event showed me that Cloud/DevOps development requires both breadth and depth: enough awareness to choose among different technologies, together with strong Linux, networking, security, and operations fundamentals to turn a design into a dependable system.
