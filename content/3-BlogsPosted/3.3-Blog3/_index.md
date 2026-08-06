---
title: "Blog 3"
date: 2026-03-26
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# ARCHITECTING SYSTEMS FOR AGENTIC AI DEVELOPMENT ON AWS

**Original AWS publication date:** March 26, 2026

**Topics:** Agentic AI, feedback loops, codebase architecture, testing, and CI/CD

An AI coding assistant can suggest code, while an AI agent can accept a broader goal, edit multiple files, run tests, deploy, and refine its work from the results. Faster code generation, however, does not automatically produce a faster development cycle. If every validation attempt waits for cloud provisioning, a long pipeline, or manual human inspection, an agent merely creates a larger queue of changes instead of delivering reliable software more quickly.

This article examines two areas that must evolve together: **system architecture** must provide short feedback loops and disposable environments, while **codebase architecture** must expose boundaries, rules, and test evidence clearly enough for an agent to understand human intent.

## 1. Why traditional architecture slows agents

Many cloud systems were designed for human-driven workflows with long-lived environments, infrequent releases, post-deployment integration testing, and operational knowledge held by a small number of engineers. This creates several bottlenecks for agents:

* Business logic is tightly coupled to cloud SDKs and services and cannot be tested locally.
* Every change requires a full stack, adding delay and cost to experiments that may be incorrect.
* Inconsistent repository structure makes it difficult to identify the correct file and impact area.
* APIs and architectural rules exist only as tribal knowledge, so changes can break service contracts.
* Slow or missing tests give the agent no objective signal for self-correction.

The solution is therefore not only a more detailed prompt. Architecture must make rapid and safe validation a foundational requirement.

## 2. Layered feedback loops

An Agentic AI workflow should not use production cloud resources as the first test environment. Changes move through loops of increasing cost and fidelity:

1. Formatting, linting, type checks, and unit tests run immediately on the development machine.
2. Local service emulation or containers validate important integration paths.
3. A minimal cloud stack confirms behavior that cannot be accurately emulated.
4. A preview environment runs smoke and end-to-end tests.
5. CI/CD enforces security checks, review, approval, and deployment policy.

The agent receives cheap feedback first and uses cloud resources only after basic validation succeeds. This lowers the time, cost, and risk of each iteration.

## 3. Local emulation as the default validation path

### Serverless applications

For AWS Lambda and Amazon API Gateway, AWS Serverless Application Model (AWS SAM) can run a local API with `sam local start-api`. An agent can invoke endpoints, inspect responses and logs, modify code, and retry within seconds. Unit tests cover small logic units, while SAM adds validation of wiring, event shapes, and handler behavior closer to Lambda.

### Container applications

Applications intended for Amazon ECS or AWS Fargate should build and run locally from the same Dockerfile. The agent can validate startup, health endpoints, environment variables, dependencies, and request behavior before pushing an image. Reusing the deployment artifact reduces differences between local and deployed execution.

### Data persistence

DynamoDB Local offers a compatible API for create, read, update, and delete operations. An agent can create sample tables, seed data, test repositories, and reset state quickly. Data access should remain behind an interface so domain tests do not require a database, while integration tests can switch between local and AWS adapters.

Emulation is not perfectly identical to the cloud, but it provides the fastest first feedback layer. Hybrid and preview tests cover the remaining differences.

## 4. Offline development for data and analytics

Data pipelines are often difficult to test because they depend on large datasets and distributed runtimes. AWS Glue provides Docker images with ETL libraries that can run jobs locally. An agent can use a reduced dataset containing edge cases, inspect schemas and intermediate transformations, and validate output before starting a cloud job.

The broader principle is to separate pure transformation logic from service input and output. Local tests validate data rules, while a later cloud run focuses on scale, permissions, partitioning, and performance. Simple logic errors no longer consume a complete Glue execution.

## 5. Hybrid testing with lightweight cloud resources

Some Amazon SNS, Amazon SQS, IAM, and network-policy behaviors cannot be fully emulated. In those cases, Infrastructure as Code using AWS CloudFormation or AWS CDK can create a small stack isolated by branch or task.

The agent deploys only the required queue, topic, role, and supporting components; invokes them through the AWS SDK; validates events, retries, dead-letter behavior, and permissions; and then tears the stack down. Unique names, ownership tags, automatic expiration, and restricted permissions prevent orphaned resources or accidental access to real data.

The cloud becomes a controlled test dependency rather than the only manually managed environment shared by every change.

## 6. Preview environments and contract-first design

When several services interact, a preview environment provides a short-lived stack for a branch or pull request. The pipeline creates the environment through IaC, deploys artifacts, runs smoke and end-to-end tests, and removes resources when validation completes. Each change is isolated and cannot destabilize a shared integration environment.

Contract-first design defines APIs up front through OpenAPI, event schemas, or versioned interfaces. Client and server teams can generate mocks, run contract tests, and implement in parallel. An agent receives explicit input, output, error-code, and versioning requirements instead of guessing how services communicate.

Combining preview environments with contract tests proves both that individual services honor the interface and that the actual end-to-end cloud path works before production.

## 7. AI-friendly codebase architecture

Fast infrastructure is insufficient when the repository is difficult to understand. An agent-friendly codebase uses predictable directories, small modules, directed dependencies, and standard build and test commands.

### Domain, application, and infrastructure boundaries

A structure inspired by Domain-Driven Design and hexagonal architecture may include:

* `/domain` for entities, value objects, and business rules without AWS dependencies.
* `/application` for use cases and orchestration through interfaces or ports.
* `/infrastructure` for DynamoDB, SNS, SQS, HTTP, and AWS SDK adapters.
* `/interfaces` or `/api` for handlers, controllers, and external schemas.

Dependencies point toward the domain, while external services connect through adapters. The agent can modify a business rule and run unit tests without AWS credentials. When it changes an adapter, the impact area and required integration tests are easier to identify.

## 8. Encoding intent with project rules

Directory names communicate structure but cannot explain every decision. A repository should store concise, specific guidance such as:

* Only infrastructure code may import an AWS SDK.
* Database access must pass through a repository interface.
* A public API change must update OpenAPI and contract tests.
* Cloud resources must be declared through IaC with ownership tags and cleanup behavior.
* Production IAM and destructive data operations require approval.

Files such as `AGENTS.md`, `CONTRIBUTING.md`, `RUNBOOK.md`, or Kiro steering files allow an agent to read these rules in the repository. Guidance should point to executable commands and short examples instead of relying on long, unverifiable prose.

## 9. Tests as executable specifications

In an agentic workflow, tests both prevent regressions and define expected behavior.

* **Unit tests** validate domain logic in isolation and run after every small change.
* **Contract tests** confirm that producers and consumers honor OpenAPI or event schemas and detect breaking changes early.
* **Integration tests** exercise adapters, databases, and messaging flows locally or in a hybrid stack.
* **Smoke tests** run in preview environments to reveal deployment-only failures such as missing IAM permissions, environment variables, or routes.

When failures contain clear diagnostics, an agent can compare expected and actual behavior and refine its work. Flaky or ambiguous tests create incorrect loops, so stability and diagnosability matter as much as coverage.

## 10. Monorepositories and machine-readable documentation

A monorepo can expose services, shared libraries, IaC, and contracts in one context, allowing an agent to assess system-wide impact. Organizations using multiple repositories need an equivalent mechanism to supply contracts and version mappings.

Documentation should favor structures that tools can parse: YAML or JSON schemas, OpenAPI, package manifests, task runners, and consistent commands. Diagrams and prose remain useful to humans, but machine-verifiable state allows the agent to validate facts rather than infer them.

## 11. Integrating agents safely into CI/CD

An agent may create a branch, edit code, and open a pull request, but the pipeline remains the policy-enforcement boundary. Appropriate guardrails include:

* Required formatting, linting, type checks, and unit, contract, and integration tests.
* Static analysis, dependency scanning, secret scanning, and IaC checks.
* Branch protection and review for production-impacting code.
* Short-lived credentials, least privilege, and separation between development and production accounts.
* Manual approval for IAM, networking, data migrations, and destructive operations.
* Complete logs of changes, commands, artifacts, and deployment results.

Autonomy can expand as the team collects evidence that the workflow is reliable. Agents can handle low-risk changes automatically while humans retain control of decisions with a large blast radius.

## 12. Results and value

With these patterns, initial validation can fall from tens of minutes to seconds in the local loop, while the cloud is reserved for higher-fidelity checks. Agents receive objective signals for self-correction, experiment cost falls, and integration errors are detected before production.

Human developers benefit even without AI: modules are clearer, onboarding is faster, tests are more reliable, and preview environments reduce contention between teams. Architecture designed for agents is fundamentally architecture that explains and verifies itself more effectively.

## 13. Personal takeaway

Agentic AI effectiveness depends on more than model capability. A powerful model constrained by slow pipelines, missing tests, and unclear boundaries still produces slow and risky results. Feedback loops, code boundaries, executable specifications, and guardrails determine how independently an agent can work.

The goal is also not to remove humans from delivery. Automation should handle small, repetitive, verifiable loops, while people remain responsible for goals, tradeoffs, sensitive data, and high-impact decisions. This is how an agent becomes a productivity multiplier without sacrificing control.

## Article links

* [Facebook post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2201707250594235/?rdid=Le865pC3R2JaAgDY#)
* [Source article on the AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/architecting-for-agentic-ai-development-on-aws/)
