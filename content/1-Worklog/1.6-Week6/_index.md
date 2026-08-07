---
title: "Week 6 Worklog"
date: 2026-06-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Implement the first Splitly business modules.
* Connect the frontend, REST API, and MongoDB Atlas.
* Validate authentication, group membership, and expense input.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Set up the Express app skeleton, DB connection.<br>Added one error-handling middleware instead of try/catch everywhere.<br>App now fails fast on startup if an env var is missing, saved me from a silly bug. | 22/06/2026 | 22/06/2026 | <https://expressjs.com/en/guide/error-handling.html> <br> <https://www.mongodb.com/docs/atlas/> |
| Tuesday | Built register/login, JWT auth.<br>Hashed passwords, added expiry to the token.<br>Wrote middleware to reject requests with no/bad token, tested with Postman. | 23/06/2026 | 23/06/2026 | <https://datatracker.ietf.org/doc/html/rfc7519> <br> <https://expressjs.com/en/guide/using-middleware.html> |
| Wednesday | Group creation and adding members.<br>Creator becomes admin automatically.<br>Added a check so only admin can edit group settings, forgot this at first then fixed it. | 24/06/2026 | 24/06/2026 | <https://expressjs.com/en/guide/routing.html> <br> [../../2-proposal/](../../2-proposal/) |
| Thursday | Expense record: payer, participants, amount, category, split.<br>Validated amount > 0 and participants must be in the group.<br>Added category field mainly for future filtering, not used yet. | 25/06/2026 | 25/06/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Friday | Wired login and group screens to the API.<br>Tested wrong password, duplicate group name cases.<br>Double-checked API response matched what's actually in MongoDB Atlas. | 26/06/2026 | 26/06/2026 | <https://react.dev/learn> <br> <https://expressjs.com/en/guide/routing.html> |

### Week 6 Achievements:

* Established a working request flow from React to Express and MongoDB Atlas.
* Completed the initial authentication and authorization structure.
* Implemented core group, member, and expense operations.
* Added validation to reduce invalid or unauthorized changes.
* Practiced debugging across frontend, backend, and database layers.
