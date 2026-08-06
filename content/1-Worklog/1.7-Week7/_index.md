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
| Monday | Refined equal, custom, and percentage split rules, including rounding and total validation. | 29/06/2026 | 29/06/2026 | [../../2-proposal/](../../2-proposal/) <br> <https://www.mongodb.com/docs/manual/data-modeling/> |
| Tuesday | Implemented balance aggregation, debtor/creditor relationships, and settlement suggestions. | 30/06/2026 | 30/06/2026 | <https://www.mongodb.com/docs/manual/aggregation/> <br> [../../2-proposal/](../../2-proposal/) |
| Wednesday | Added settlement creation, status transitions, and permission checks for confirmation actions. | 01/07/2026 | 01/07/2026 | <https://expressjs.com/en/guide/using-middleware.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Designed receipt metadata and the file-upload abstraction in preparation for Amazon S3 integration. | 02/07/2026 | 02/07/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Friday | Integrated group, expense, balance, and settlement screens; performed end-to-end test cases. | 03/07/2026 | 03/07/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Week 7 Achievements:

* Implemented multiple splitting methods with input and rounding validation.
* Produced balances and settlement suggestions from expense data.
* Added controlled settlement-status changes.
* Separated receipt metadata from binary-file storage concerns.
* Completed the first end-to-end version of Splitly's main expense workflow.
