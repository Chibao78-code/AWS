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
| Monday | Drew the request flow: browser -> Nginx -> Express -> MongoDB Atlas.<br>Marked where receipt files would flow separately from the business data.<br>Nothing built yet, just diagramming this week. | 13/07/2026 | 13/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000112.awsstudygroup.com/> |
| Tuesday | Sketched VPC + public subnet + IGW + Security Group + EC2.<br>Picked one EC2 for now, budget doesn't allow more.<br>Elastic IP so the address doesn't change if the instance restarts. | 14/07/2026 | 14/07/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |
| Wednesday | Planned S3 Receipts Bucket with Block Public Access on.<br>IAM Role for EC2 scoped to just that bucket, nothing broader.<br>DB stores only the object key/URL, not the actual file. | 15/07/2026 | 15/07/2026 | <https://000069.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| Thursday | Added Session Manager instead of opening SSH publicly.<br>Listed the CloudWatch metrics/alarms I'll need for the backend.<br>Rough tagging idea so cost tracking is at least possible later. | 16/07/2026 | 16/07/2026 | <https://000058.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Friday | Finalized the diagram for this phase (single EC2).<br>Wrote down a "later" list: CloudFront, Route 53, ACM, WAF, ALB, CI/CD.<br>Not doing any of that now, just noting it for the proposal doc. | 17/07/2026 | 17/07/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://000094.awsstudygroup.com/> <br> <https://000026.awsstudygroup.com/> <br> <https://000017.awsstudygroup.com/> |

### Week 9 Achievements:

* Selected a single-EC2 architecture suitable for the current student-project scope.
* Defined the complete request path and trust boundaries.
* Prevented direct public access to backend port 5000 and planned Session Manager administration.
* Added observability, alerts, budgets, and secret-handling requirements.
* Documented the single-instance limitation and a measured path for later expansion.
