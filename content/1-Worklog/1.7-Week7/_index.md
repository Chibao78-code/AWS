---
title: "Week 7 Worklog"
date: 2026-06-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Complete the expense-splitting and balance-calculation flows.
* Add settlement tracking and receipt support.
* Integrate the main business screens with backend APIs.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Finished equal/custom/percentage split logic.<br>Handled the rounding remainder for equal split (someone has to get the extra cent).<br>Percentage split must sum to exactly 100, added a check for that. | 29/06/2026 | 29/06/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://www.mongodb.com/docs/manual/data-modeling/> |
| Tuesday | Balance calculation using MongoDB aggregation.<br>Summed paid vs owed per member, then worked out who owes who.<br>Simplified the settlement suggestions so it's not one transaction per expense. | 30/06/2026 | 30/06/2026 | <https://www.mongodb.com/docs/manual/aggregation/> <br> [../../2-proposal/](../../2-proposal/) |
| Wednesday | Settlement creation and status (pending/confirmed/rejected).<br>Only the debtor can mark as paid, only the creditor confirms it.<br>Logged each status change, useful for debugging later. | 01/07/2026 | 01/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Designed receipt metadata schema (key, content type, uploader).<br>Not storing the file itself in MongoDB, just the reference.<br>Sketched an upload service interface, will plug in S3 later. | 02/07/2026 | 02/07/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Friday | Connected group/expense/balance/settlement screens.<br>Ran through the full flow manually a few times.<br>Found a mismatch between calculated balance and what showed on screen, fixed it. | 03/07/2026 | 03/07/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Week 7 Achievements:

* Implemented multiple splitting methods with input and rounding validation.
* Produced balances and settlement suggestions from expense data.
* Added controlled settlement-status changes.
* Separated receipt metadata from binary-file storage concerns.
* Completed the first end-to-end version of Splitly's main expense workflow.
