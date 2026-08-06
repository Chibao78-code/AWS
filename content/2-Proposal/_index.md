---
title: "Proposal"
date: 2026-08-06
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# SPLITLY – GROUP EXPENSE MANAGEMENT PLATFORM

## An AWS deployment proposal for recording, splitting, and reconciling shared expenses

## 1. Proposal summary

Splitly addresses a common situation: several people join a trip, event, or shared household, while different members pay for different items. When expenses are scattered across chat messages, spreadsheets, and receipt photos, it becomes difficult to determine who paid, who owes money, and how the group should settle accurately.

This proposal deploys Splitly on AWS as a centralized web application. The frontend uses React, TypeScript, and Vite; the backend uses Node.js, Express, and TypeScript; and MongoDB Atlas stores business data. In the current phase, frontend and backend share one Amazon EC2 instance to match the scale and budget of a student project. Amazon S3 stores receipt images, Amazon CloudWatch supports observability, Amazon SNS delivers alerts, and AWS Budgets monitors spending.

The objective is not merely to publish a website. The project establishes a repeatable deployment process, controlled access, diagnostic logging, cost visibility, and a practical path for future growth.

## 2. Problem, users, and scope

### 2.1 Problem to solve

Manual group-expense methods have recurring limitations:

- A group may contain many expenses and payers, making the overall balance difficult to follow.
- Split rules may be unequal, and balances can be calculated incorrectly when an expense changes or is removed.
- Settlement status is unclear, forcing members to reconcile the same payment repeatedly.
- Receipt images are scattered and hard to retrieve when a transaction is disputed.
- After deployment, the team lacks metrics, logs, and alerts to investigate application failures.

### 2.2 Users

- **Member:** joins groups and views relevant expenses and balances.
- **Payer/expense creator:** records the amount, participants, split method, and receipt.
- **Group administrator:** manages members, performs authorized corrections, and follows settlement progress.
- **System administrator:** deploys releases, monitors resources, handles incidents, and controls AWS costs.

### 2.3 In-scope capabilities

- User registration, sign-in, and profile management.
- Group creation, member invitation/addition, and basic role management.
- Expense recording with payer, participants, and split rules.
- Balance calculation, settlement suggestions, and settlement-status tracking.
- Electronic receipt storage in Amazon S3 with transaction metadata.
- Notifications, disputes, or corrections related to an expense.
- Gmail and VNPay Sandbox integration when configuration is provided.
- Application logging, infrastructure metrics, operational alerts, and budget alerts.

### 2.4 Out of scope for the current phase

Multi-Region deployment, Auto Scaling, load balancing, native mobile applications, and production payment processing are not included in the current implementation. CloudFront, Route 53, AWS WAF, ACM, and moving the frontend away from EC2 are treated as the next infrastructure phase.

## 3. Current solution architecture

![Current Splitly architecture](/images/2-Proposal/Splitly/Architecture_Final.png)

The current solution is organized into four component groups.

### 3.1 Access and network layer

- Resources are placed in `ap-southeast-1` to reduce latency for users in Vietnam.
- EC2 runs in a public subnet inside an Amazon VPC and reaches the Internet through an Internet Gateway.
- The Security Group permits only required traffic. HTTP port 80 serves the workshop deployment; backend port 5000 listens internally and is not exposed directly to the Internet.
- Administrators use AWS Systems Manager Session Manager where possible instead of relying on a public SSH port.
- An Elastic IP keeps the public address stable across instance restarts, but public IPv4 usage must be monitored because charges may apply.

### 3.2 Presentation and application layer

- React/Vite is built into HTML, CSS, and JavaScript files in the EC2 `dist` directory.
- Nginx serves the frontend on port 80 and provides fallback routing for the Single Page Application.
- Nginx forwards `/api/` requests to Node.js/Express at `127.0.0.1:5000`.
- PM2 manages the `splitly-api` process, provides restart behavior, and exposes application logs for diagnosis.
- The backend handles authentication, groups, expenses, balances, settlements, receipts, disputes, and notifications.

### 3.3 Data and integration layer

- MongoDB Atlas stores users, groups, expenses, settlements, notifications, and receipt metadata.
- The Amazon S3 Receipts Bucket stores uploaded receipt files. The database retains the object key, URL, and related metadata instead of binary file contents.
- The backend communicates with Gmail SMTP and VNPay Sandbox over the Internet when those integrations are enabled.
- The bucket name, Region, and presigned-URL lifetime are supplied through backend environment variables.

### 3.4 Security, monitoring, and cost control

- EC2 assumes an IAM Role for access to the intended S3 bucket and monitoring services; AWS Access Keys are not embedded in source code.
- MongoDB URIs, JWT secrets, Gmail App Passwords, and VNPay keys are never committed to Git. The lab uses a server-side `.env` file; production should move them to AWS Secrets Manager or Systems Manager Parameter Store.
- CloudWatch collects required metrics and logs. Alarms can publish events to SNS for administrator email delivery.
- AWS Budgets tracks actual and forecasted spending so the team can respond before usage materially exceeds the plan.

### 3.5 AWS service responsibilities

| Service | Responsibility in Splitly |
|---|---|
| Amazon EC2 | Runs Nginx, the built frontend, and the Node.js backend |
| Amazon VPC | Provides network isolation, subnetting, routes, and Internet connectivity |
| Security Group | Controls inbound and outbound EC2 traffic |
| Amazon S3 | Stores user-uploaded receipts |
| AWS IAM | Grants least-privilege EC2 access to S3 and CloudWatch |
| AWS Systems Manager | Provides Session Manager administration for EC2 |
| Amazon CloudWatch | Collects metrics/logs and creates alarms |
| Amazon SNS | Delivers operational notifications |
| AWS Budgets | Monitors and alerts on cost |

MongoDB Atlas, Gmail, and VNPay are external services that participate directly in the application flow.

## 4. Proposed expansion architecture

![Proposed Splitly expansion](/images/2-Proposal/Splitly/Architecture_Update.png)

When traffic and security requirements grow, the frontend should be separated from EC2:

1. React/Vite is built and uploaded to a dedicated S3 Frontend Bucket.
2. CloudFront distributes static content through edge locations and caches eligible assets.
3. Route 53 manages the domain, while AWS Certificate Manager supplies the TLS certificate for HTTPS.
4. AWS WAF filters requests that pass through CloudFront according to configured rules.
5. EC2 continues to provide REST APIs and connect to MongoDB Atlas and the S3 Receipts Bucket during the transition.

Separating the frontend enables independent releases, lowers the EC2 serving workload, and improves page delivery. For comprehensive production API protection, the API flow should also pass through a managed entry point such as a CloudFront behavior, an Application Load Balancer, or API Gateway. Placing WAF only in front of the frontend distribution does not automatically protect every direct request to EC2.

Later phases may add Auto Scaling, an Application Load Balancer, a private backend subnet, database backups, CI/CD, and centralized secret management. These components should be introduced after measured traffic and availability requirements justify them.

## 5. Technical implementation plan

### Phase 1 – Requirements and design

- Normalize use cases, user roles, and expense-splitting rules.
- Review the frontend/backend structure and MongoDB schema.
- Document the current architecture, trust boundaries, and sensitive-data flow.
- Define resource naming, Region, and tagging conventions.

### Phase 2 – Infrastructure preparation

- Use CloudFormation to provision the VPC, subnet, routes, Security Group, EC2, and IAM role.
- Create an S3 Receipts Bucket with Block Public Access and an appropriate policy.
- Prepare MongoDB Atlas Network Access and a limited database identity.
- Configure CloudWatch, SNS, and AWS Budgets for the lab scope.

### Phase 3 – Application deployment

- Connect to EC2 through Session Manager and clone the team's repository.
- Configure backend environment variables, install dependencies, build, and run the API with PM2.
- Configure the production frontend, build React/Vite, and verify `dist/index.html`.
- Configure Nginx to serve the frontend and reverse-proxy `/api/` to the backend.

### Phase 4 – Validation and handover

- Validate infrastructure, PM2, the backend listener, Nginx, and browser access.
- Test sign-in, group creation, expense entry, balance calculation, and receipt upload.
- Review CloudWatch logs, application failures, and cost alerts.
- Complete operations, recovery, and resource-cleanup guidance.

## 6. Requirements and acceptance criteria

### 6.1 Technical requirements

- Frontend: React, TypeScript, and Vite; no secrets in `VITE_` variables.
- Backend: Node.js, Express, TypeScript, and REST APIs; PM2 maintains the process.
- Web server: Nginx serves the SPA and proxies API traffic.
- Data: MongoDB Atlas stores business records; S3 stores receipts.
- Security: least-privilege IAM Role and Security Group; secrets absent from the repository.
- Observability: backend logs, EC2 metrics, and an administrator alert channel.

### 6.2 Acceptance criteria

- The CloudFormation stack completes successfully and provisioned resources are healthy.
- The Splitly UI is reachable through the public address, and refreshing an SPA route does not return 404.
- `splitly-api` is `online`, and the API responds through Nginx without exposing port 5000 publicly.
- A user can create a group, record expenses, and obtain balances that match the test dataset.
- A receipt is stored in the intended S3 bucket and its metadata is associated with the correct transaction.
- No real credential appears in Git, report screenshots, or shared logs.
- The team can diagnose a simulated failure through PM2/CloudWatch and receive a configured alert.

## 7. Proposed schedule

| Period | Main objective | Deliverable |
|---|---|---|
| Weeks 1–2 | Requirements analysis and design | Use cases, data schema, architecture diagram |
| Weeks 3–5 | Core feature completion | Authentication, groups, expenses, settlements, receipts |
| Weeks 6–8 | Infrastructure and deployment | CloudFormation stack, EC2, S3, running application |
| Weeks 9–10 | Testing and security review | Test evidence, reviewed IAM/SG, logs and alarms |
| Weeks 11–12 | Optimization, documentation, handover | Report, operations guide, expansion plan |

The schedule may change with software progress, but a phase is complete only after its corresponding deliverable has been validated.

## 8. Cost estimation and control

The project should not copy a fixed total from a sample report because AWS costs depend on the date, Region, account eligibility, EC2 runtime, S3 usage, log volume, and Internet traffic. Before deployment, the team should create a new AWS Pricing Calculator estimate using measured or explicitly documented assumptions.

Primary cost drivers include:

- EC2 instance type and running hours.
- Public IPv4/Elastic IP usage.
- S3 storage, requests, and data transfer.
- CloudWatch log ingestion/retention, custom metrics, and alarms.
- Internet data transfer; MongoDB Atlas charges are outside the AWS bill.

Controls include resource tagging, AWS Budgets, limited log retention, cleanup of lab resources, S3 lifecycle review, and stopping or deleting EC2 when no longer needed. The final cost report must state the estimate date and workload assumptions.

## 9. Risks and responses

| Risk | Impact | Mitigation and contingency |
|---|---|---|
| EC2 or backend process outage | High | PM2 restart and CloudWatch alarm; redeploy from the repository and CloudFormation |
| MongoDB Atlas connectivity loss | High | Limited DB identity, allowlist checks, log monitoring; use Atlas backup when required |
| Receipt upload/read failure | Medium | Least-privilege IAM, Region/bucket validation, bounded retry; preserve metadata for reconciliation |
| Secret exposure in Git or logs | High | `.gitignore`, pre-commit review, credential rotation, and migration to a secret store |
| Overly broad Security Group | High | Do not expose port 5000; prefer Session Manager; review rules periodically |
| Incorrect split calculation | High | Unit tests for splitting/rounding, reference datasets, and an adjustment audit trail |
| Unexpected AWS cost | Medium | AWS Budgets, tags, early alerts, and removal of unused resources |
| Single EC2 as a failure point | High | Accept for the lab; back up configuration and maintain an ALB/Auto Scaling roadmap |

## 10. Expected outcomes

- Splitly operates on AWS with an end-to-end frontend, API, database, and receipt flow.
- Members manage shared spending more transparently with less manual calculation and reconciliation.
- The team applies IAM Roles, file/metadata separation, centralized monitoring, and budget alerts.
- Infrastructure can be reproduced with CloudFormation and is supported by deployment, testing, troubleshooting, and cleanup documentation.
- The current design provides a clear foundation for frontend separation, HTTPS, domain management, WAF, load balancing, and CI/CD in a later phase.
