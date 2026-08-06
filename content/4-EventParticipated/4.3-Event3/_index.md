---
title: "Event 3"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# AGENT FORGE – DEEPDIVE DAY 1 REPORT

## 1. Event information

- **Topic:** Agent Forge – Deepdive Day 1.
- **Program:** 3-Day AgentForge Workshop.
- **Time:** 09:00–12:00, Saturday, August 1, 2026 (GMT+7).
- **Location:** [Bitexco Financial Tower, Ho Chi Minh City](https://www.google.com/maps/search/?api=1&query=Bitexco%20Financial%20Tower&query_place_id=ChIJ6-qHzzovdTERKuM7X5ehack).
- **Field:** Artificial Intelligence and AWS.
- **Role:** Workshop attendee.

Day 1 focused on **Foundations & Agent Setup**, taking participants from Amazon Bedrock AgentCore concepts to a basic deployed agent with tools, a knowledge source, a web interface, and user authentication.

## 2. Workshop objectives

- Understand Amazon Bedrock AgentCore's role in the lifecycle of an AI agent.
- Distinguish the responsibilities of Runtime, Gateway, and Identity.
- Deploy a basic agent to a managed environment.
- Connect the agent to external tools and a Knowledge Base.
- Build a web interface through which users can interact with the agent.
- Integrate Amazon Cognito authentication before permitting application access.
- Develop a security mindset for agents that can call tools and act on data.

## 3. Foundations: Amazon Bedrock AgentCore

The first part introduced AgentCore and the three components named in the agenda.

### 3.1 AgentCore Runtime

Runtime hosts agent or tool code. Rather than building the entire server, scaling layer, and session-management mechanism, a development team packages its agent logic and deploys it to Runtime. Each runtime has its own identity and version, supporting controlled updates.

One important distinction is that a model and an agent runtime are not the same thing. A model generates responses; a runtime receives requests, maintains session context, executes application logic, and coordinates tool calls.

### 3.2 AgentCore Gateway

Gateway provides a unified access point through which agents discover and call tools, APIs, or other services. Instead of connecting an agent directly to systems that each use a different authentication method, Gateway standardizes how targets are exposed and how traffic is controlled.

Tools still need clear descriptions, validated inputs, and narrowly scoped permissions. Gateway organizes access to tools, while the development team remains responsible for deciding which tools the agent may invoke and which actions require user confirmation.

### 3.3 AgentCore Identity

Identity addresses authentication in two directions. Inbound access determines which user or application may invoke an agent. Outbound access gives the agent appropriate credentials for tools, AWS resources, or third-party services without embedding secrets in source code.

A workload identity gives the agent a distinct identity for policy enforcement and auditing. This is especially important when an agent acts for a user because the system must distinguish the agent's permissions, the user's permissions, and the destination service's permissions.

## 4. Hands-on lab

### 4.1 Deploying a basic agent

The lab began by preparing agent logic and deploying it to AgentCore Runtime. This step demonstrated the path from source code to an endpoint that can be invoked by a web interface or another application.

Relevant deployment checks include the execution role, Region, dependencies, runtime configuration, and logs. A running agent is not automatically production-ready; failures, timeouts, least-privilege access, and unavailable tools still require testing.

### 4.2 Connecting external tools and a Knowledge Base

An agent becomes more useful when it can retrieve managed information or invoke an external function. A tool provides a structured action, while a Knowledge Base supplies information that helps ground an answer.

The session clarified two purposes:

- A **Knowledge Base** is suitable for questions that require documents, instructions, or reference material.
- A **tool** is suitable for calling an API, retrieving dynamic data, or executing a defined business operation.

Agents should not receive broad database or API access. A small tool with a clear input/output contract and one responsibility is easier to test, authorize, and audit.

### 4.3 Building a Web UI with Amazon Cognito

The Web UI lets users submit requests and view agent responses. Amazon Cognito authenticates users first, after which the resulting token participates in the agent invocation flow.

Authentication also demonstrates that a chat interface is only the outer layer. The backend must still validate tokens, determine identity, restrict data by user, and treat frontend input as untrusted.

## 5. Architecture flow understood from the workshop

A request can be understood as the following sequence:

1. The user signs in to the Web UI through Amazon Cognito.
2. The Web UI sends a request and token to the agent.
3. AgentCore Runtime validates the request and runs the agent logic in its session.
4. When an action is required, the agent invokes a tool through AgentCore Gateway.
5. AgentCore Identity supplies or controls the credentials required by the agent/tool.
6. The tool reaches an API, AWS resource, or Knowledge Base within its permitted scope.
7. The result returns to Runtime, where the agent produces a response for the Web UI.

Security therefore does not reside in one component. Cognito authenticates the user, Runtime protects the execution endpoint, Gateway manages paths to tools, and Identity manages workload identities and credentials.

## 6. Knowledge and skills gained

### Technical knowledge

- Distinguished models, agents, runtimes, gateways, identities, tools, and Knowledge Bases.
- Understood that a production agent requires execution, authentication, and integration layers—not only a prompt.
- Learned to divide agent capabilities into tools with explicit contracts.
- Recognized the difference between inbound and outbound authentication.
- Understood Cognito's role in protecting the Web UI and backend invocation flow.
- Considered least privilege, logs, timeouts, tool failures, and agent-action auditing.

### Design mindset

- Begin with one measurable use case instead of a broadly privileged agent.
- Separate reference retrieval from state-changing actions.
- Require confirmation before sensitive or difficult-to-reverse operations.
- Evaluate accuracy, task-completion rate, latency, cost, and safety.
- Do not treat a functional chat interface as proof of complete security.

## 7. Potential application to Splitly

AgentCore is unnecessary for the current Splitly version, but the workshop suggests a reasonable future extension: a **group-expense assistant**.

An initial experiment could:

- Answer questions such as “Which category has the group spent the most on?” or “Which expenses are unsettled?”.
- Retrieve Splitly usage guidance from a Knowledge Base.
- Invoke read-only tools such as `getGroupSummary`, `listUnsettledExpenses`, or `findReceiptMetadata`.
- Explain calculated balances without independently modifying transactions.

If the feature is developed, the team should apply these controls:

1. Cognito or the existing authentication system must identify the correct user.
2. A request may access only groups in which that user is a member.
3. The agent calls controlled business APIs instead of receiving broad MongoDB access.
4. Tools that change an expense or settlement require explicit confirmation.
5. Receipt and financial data must not appear in logs or prompts beyond what is necessary.
6. Agent functionality is added only after the core expense-splitting system is stable.

## 8. Experience and reflection

The event was short but well structured: it began with three foundation components, then moved into deployment, tool integration, and an authenticated user interface. This sequence helped me understand AgentCore as a system of distinct responsibilities rather than a single AI service.

![Photo from Agent Forge – Deepdive Day 1](/images/4-Event/Splitly/event-3-pic.jpg)

> My most important takeaway is that identity and authorization must be designed as core functionality when an AI agent can invoke tools. A useful agent must not only answer well; it must act within scope, remain auditable, and protect user data.

## 9. Reference documentation

- [Amazon Bedrock AgentCore Runtime – How it works](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-how-it-works.html)
- [Amazon Bedrock AgentCore Gateway](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html)
- [Amazon Bedrock AgentCore Identity](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/identity.html)
