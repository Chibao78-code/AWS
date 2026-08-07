---
title: "Week 10 Worklog"
date: 2026-07-20
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Refine Splitly business rules and backend module boundaries.
* Prepare repeatable infrastructure and deployment configuration.
* Define security and acceptance checks before deploying to AWS.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Re-checked settlement confirm permission.<br>Made sure a random member can't confirm someone else's settlement.<br>Added a test case for exactly that, it was passing but wanted proof. | 20/07/2026 | 20/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Tuesday | Pulled notification preference logic into its own service.<br>It was too tangled with expense/settlement code before.<br>Traced which events currently write a notification, some were missing. | 21/07/2026 | 21/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Wednesday | Added 5-member cap for Free Plan groups.<br>Tested adding a 6th member, got the expected error.<br>Cleaned up error response format, was inconsistent across endpoints before. | 22/07/2026 | 22/07/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Wrote the CloudFormation template: VPC, subnet, route, SG, EC2, IAM Role, S3.<br>Added CloudWatch alarm resources into the same template.<br>Ran into a circular dependency issue once, reordered resources to fix it. | 23/07/2026 | 23/07/2026 | <https://000037.awsstudygroup.com/> |
| Friday | Drafted `.env.example` with all backend vars the EC2 will need.<br>Planned Nginx config and PM2 process name on paper first.<br>Wrote a short acceptance checklist for what "deployed" actually means. | 24/07/2026 | 24/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000096.awsstudygroup.com/> |

### Week 10 Achievements:

* Strengthened authorization around settlement actions.
* Improved notification-module maintainability and group-plan validation.
* Converted infrastructure requirements into a repeatable CloudFormation design.
* Defined safe server-side configuration without committing credentials.
* Prepared testable criteria for infrastructure, backend, frontend, proxy, database, and receipt storage.
