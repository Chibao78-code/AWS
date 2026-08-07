---
title: "Week 5 Worklog"
date: 2026-06-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Start the Splitly project and define its first development scope.
* Analyze users, group-expense workflows, splitting rules, and data relationships.
* Establish the frontend, backend, database, and Git foundations.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Wrote down the shared-expense problem in my own words.<br>Roughed out member vs admin roles, kept feature list small on purpose.<br>Didn't want to over-scope this in week 1 of the project. | 15/06/2026 | 15/06/2026 | [../../2-proposal/](../../2-proposal/) |
| Tuesday | Drafted use cases: register, group, member, expense, balance, settlement, receipt, notification.<br>Drew a rough sequence diagram for register -> settlement flow.<br>Some edge cases (empty group, one member) I left as TODO for now. | 16/06/2026 | 16/06/2026 | [../../2-proposal/](../../2-proposal/) |
| Wednesday | Set up the folders for frontend (React/Vite/TS) and backend (Node/Express/TS).<br>Turned on strict mode in tsconfig, fixed the errors it complained about.<br>Tested the Vite dev proxy against one dummy Express route, worked fine. | 17/06/2026 | 17/06/2026 | <https://react.dev/learn> <br> <https://vite.dev/guide/> <br> <https://expressjs.com/en/guide/routing.html> <br> <https://www.mongodb.com/docs/atlas/> |
| Thursday | Sketched the first MongoDB schemas: user, group, expense, settlement.<br>Went back and forth on embed vs reference for group members, picked reference.<br>Added an index on group membership since that'll be queried a lot. | 18/06/2026 | 18/06/2026 | <https://www.mongodb.com/docs/manual/data-modeling/> <br> [../../2-proposal/](../../2-proposal/) |
| Friday | Set a branch naming convention, nothing fancy.<br>Made `.env.example` with fake values, added `.gitignore` entries.<br>Broke the 12-week plan into rough weekly code goals. | 19/06/2026 | 19/06/2026 | <https://git-scm.com/docs> <br> [../../2-proposal/](../../2-proposal/) |

### Week 5 Achievements:

* Started Splitly development on June 15, 2026 with a clearly defined problem and scope.
* Identified the main users, business flows, and acceptance expectations.
* Selected a practical React, Express, TypeScript, and MongoDB Atlas stack.
* Prepared the initial data model and project structure.
* Established rules for branches, reviews, environment variables, and secret protection.
