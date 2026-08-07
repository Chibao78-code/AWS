---
title: "Week 12 Worklog"
date: 2026-08-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Validate Splitly layer by layer and resolve deployment issues systematically.
* Complete monitoring, security, cost, cleanup, and operations guidance.
* Finalize the bilingual workshop and internship report.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Cross-checked stack outputs against the running EC2.<br>Confirmed Security Group only had the ports it should.<br>Session Manager still worked fine, no public SSH key needed. | 03/08/2026 | 03/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://000037.awsstudygroup.com/> |
| Tuesday | Hit a small health endpoint, API responded fine.<br>Scanned PM2 logs for anything weird at startup, looked clean.<br>Refreshed a deep SPA route in the browser to make sure Nginx fallback works. | 04/08/2026 | 04/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Wednesday | Ran the full user journey with a test account: login, group, expense.<br>Balance and settlement numbers matched what I expected on paper.<br>Uploaded/retrieved a receipt, triggered a notification and a complaint to check both. | 05/08/2026 | 05/08/2026 | [../../5-workshop/5.4-test/](../../5-workshop/5.4-test/) <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Checked CloudWatch metrics against rough CPU/network baselines.<br>Sent a test SNS alert, got it in email so that part works.<br>Wrote a short table of common symptoms -> likely cause for the report. | 06/08/2026 | 06/08/2026 | <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| Friday | Took final screenshots of the working site in both languages.<br>Backed up the CloudFormation template and my config notes.<br>Deleted the stack + leftover EIP/S3 test objects, then proofread the whole report. | 07/08/2026 | 07/08/2026 | [../../5-workshop/5.5-cleanup/](../../5-workshop/5.5-cleanup/) <br> <https://cloudjourney.awsstudygroup.com/> |

### Week 12 Achievements:

* Validated infrastructure, backend, frontend, proxy, database, and receipt-storage layers independently.
* Confirmed the main Splitly business flows against prepared test data.
* Documented a troubleshooting matrix based on observable symptoms and logs.
* Reviewed security and cost controls and removed workshop-specific billable resources safely.
* Completed the Splitly proposal, deployment workshop, and twelve-week worklog for final review before August 9, 2026.
