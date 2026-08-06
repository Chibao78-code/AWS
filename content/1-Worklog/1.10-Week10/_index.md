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
| Monday | Reviewed settlement confirmation permissions and ensured that only the appropriate party can confirm a payment. | 20/07/2026 | 20/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Tuesday | Refactored notification preferences and reviewed dependencies between notification and business modules. | 21/07/2026 | 21/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Wednesday | Added and tested subscription-related group-member limits and consistent API error responses. | 22/07/2026 | 22/07/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Designed CloudFormation resources for VPC, subnet, routes, Security Group, EC2, IAM Role, S3, and monitoring. | 23/07/2026 | 23/07/2026 | <https://000037.awsstudygroup.com/> |
| Friday | Prepared environment-variable templates, Nginx/PM2 plans, MongoDB Atlas access, and deployment acceptance criteria. | 24/07/2026 | 24/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000096.awsstudygroup.com/> |

### Week 10 Achievements:

* Strengthened authorization around settlement actions.
* Improved notification-module maintainability and group-plan validation.
* Converted infrastructure requirements into a repeatable CloudFormation design.
* Defined safe server-side configuration without committing credentials.
* Prepared testable criteria for infrastructure, backend, frontend, proxy, database, and receipt storage.
