---
title: "Week 8 Worklog"
date: 2026-07-06
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Expand Splitly with notifications, complaints, and optional integrations.
* Improve validation, authorization, and module organization.
* Test the application before designing its AWS deployment.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Designed notification preferences and inbox.<br>Made a per-user setting for which events trigger a notification.<br>Kept read/unread state instead of just firing one-off alerts. | 06/07/2026 | 06/07/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Tuesday | Added notification status (unread/read/archived).<br>Debated whether settlement reminders should be scheduled or manual.<br>Went with manual trigger for now, easier to test. | 07/07/2026 | 07/07/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Wednesday | Built complaint submission form + endpoint.<br>Required-field validation, nothing fancy.<br>Only group admin can resolve complaints, logged each status change. | 08/07/2026 | 08/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Reviewed Gmail App Password and VNPay Sandbox key handling.<br>Confirmed nothing with `VITE_` prefix leaks a secret into the browser bundle.<br>Double checked `.gitignore` covers the env file properly. | 09/07/2026 | 09/07/2026 | <https://support.google.com/accounts/answer/185833> <br> <https://sandbox.vnpayment.vn/apis/docs/> <br> <https://000096.awsstudygroup.com/> |
| Friday | Manual regression test across all modules with one test account.<br>Listed the env vars and ports the app actually needs.<br>Wrote these down as prerequisites for the AWS deployment workshop next. | 10/07/2026 | 10/07/2026 | [../../5-workshop/](../../5-workshop/) <br> [../../2-proposal/](../../2-proposal/) |

### Week 8 Achievements:

* Added a structured notification and preference model.
* Completed the basic user-to-administrator complaint workflow.
* Improved module separation, validation, and authorization checks.
* Documented safe boundaries for external-service credentials.
* Produced a stable application baseline for AWS architecture planning.
