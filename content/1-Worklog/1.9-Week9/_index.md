---
title: "Week 9 Worklog"
date: 2026-07-13
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Design an AWS architecture appropriate for the current Splitly scale and budget.
* Define network, compute, receipt storage, database connectivity, monitoring, and cost controls.
* Document current limitations and a practical expansion path.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Mapped the browser, React/Vite, Nginx, Node.js/Express, MongoDB Atlas, and receipt-data flows. | 13/07/2026 | 13/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000112.awsstudygroup.com/> |
| Tuesday | Designed a VPC, public subnet, Internet Gateway, Security Group, EC2, and stable public-address model. | 14/07/2026 | 14/07/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |
| Wednesday | Designed an S3 Receipts Bucket and least-privilege EC2 IAM Role; separated file storage from metadata. | 15/07/2026 | 15/07/2026 | <https://000069.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| Thursday | Added Session Manager, CloudWatch, SNS, AWS Budgets, secret-management guidance, and resource tagging. | 16/07/2026 | 16/07/2026 | <https://000058.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Friday | Completed the current architecture diagram and proposed a future CloudFront, Route 53, ACM, WAF, ALB, and CI/CD expansion. | 17/07/2026 | 17/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000094.awsstudygroup.com/> <br> <https://000026.awsstudygroup.com/> <br> <https://000017.awsstudygroup.com/> |

### Week 9 Achievements:

* Selected a single-EC2 architecture suitable for the current student-project scope.
* Defined the complete request path and trust boundaries.
* Prevented direct public access to backend port 5000 and planned Session Manager administration.
* Added observability, alerts, budgets, and secret-handling requirements.
* Documented the single-instance limitation and a measured path for later expansion.
