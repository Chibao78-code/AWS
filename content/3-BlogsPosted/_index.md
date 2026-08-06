---
title: "Blogs Posted"
date: 2026-07-07
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

During my AWS learning journey, I studied the original material, compared two reference internship reports, and rewrote three practical architecture topics: operating Kubernetes at enterprise scale, protecting applications from DDoS attacks, and designing software delivery environments for Agentic AI. These pages go beyond service summaries by describing the problem, the interaction between architectural components, the results, and my own lessons learned.

All three posts were shared with the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) community. Each page uses the publication date of its original AWS Architecture Blog article because Facebook requires authentication before showing the post date; these dates were therefore verified independently rather than copied from either reference project.

### [Blog 1 - Optimizing Kubernetes Operations with Amazon EKS Auto Mode](3.1-Blog1/)

Blog 1 examines how Generali Malaysia modernized insurance applications as microservices on Amazon EKS. It focuses on how EKS Auto Mode reduces node provisioning, Bottlerocket patching, add-on, load balancer, storage, and scaling work, while still requiring maintenance windows, Pod Disruption Budgets, and Node Disruption Budgets so that managed infrastructure updates do not interrupt critical services.

The post also describes the surrounding security and observability architecture: GuardDuty correlates attack signals, Inspector prioritizes vulnerabilities in images that are actually running, Network Firewall controls egress, Secrets Manager centralizes secrets, and CloudWatch with Managed Grafana provides namespace-level dashboards. Cost allocation tags, split cost allocation, Savings Plans, and Graviton connect Kubernetes consumption to business projects and optimization decisions.

**Original AWS publication date:** March 23, 2026

**Facebook post:** [View the post](https://www.facebook.com/photo?fbid=1647830246522148)

### [Blog 2 - How AWS WAF Helps Scale to Win Defend Against DDoS Attacks](3.2-Blog2/)

Blog 2 presents the layered defense that Scale to Win built after DDoS events exceeded two million requests per second. Traffic is routed through Amazon CloudFront and AWS WAF so malicious requests can be absorbed, classified, and blocked at the edge before consuming Application Load Balancer and application-server capacity.

The design goes beyond simple rate limiting. It protects the origin with a managed prefix list and shared secret header, combines heuristic detection with JA3/JA4 fingerprints, separates machine-to-machine traffic from browser traffic, defines two browser rate thresholds, challenges suspicious users with CAPTCHA, and detects CAPTCHA tokens reused from multiple IP addresses. The case demonstrates how to improve attack resistance without unnecessarily blocking legitimate high-volume users.

**Original AWS publication date:** July 14, 2025

**Facebook post:** [View the post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2180420536056240/)

### [Blog 3 - Architecting for Agentic AI Development on AWS](3.3-Blog3/)

Blog 3 explains why faster AI code generation does not automatically shorten software delivery. When a system depends on long-lived cloud environments, slow pipelines, tightly coupled code, and manual testing, an agent still waits minutes or hours to validate a change. The proposed solution treats rapid feedback, explicit boundaries, and automated validation as first-class architecture requirements.

The post covers local emulation with AWS SAM, containers, and DynamoDB Local; offline development for AWS Glue; hybrid tests using small cloud stacks; on-demand preview environments; OpenAPI and contract-first design; domain/application/infrastructure code boundaries; project rules; unit, contract, and smoke tests; machine-readable documentation; and CI/CD guardrails with human approval for high-risk operations.

**Original AWS publication date:** March 26, 2026

**Facebook post:** [View the post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2201707250594235/?rdid=Le865pC3R2JaAgDY#)
