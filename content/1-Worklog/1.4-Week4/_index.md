---
title: "Week 4 Worklog"
date: 2026-06-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Complete pre-project research on AWS storage, databases, identity, and monitoring.
* Compare service choices for a web application that stores business data and uploaded files.
* Prepare an architecture checklist before Splitly development begins.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Read about S3 objects, storage classes, versioning, lifecycle rules.<br>Turned on versioning on a test bucket, uploaded/overwrote a file to see it work.<br>Set a lifecycle rule to move old objects to a cheaper class, just for practice. | 08/06/2026 | 08/06/2026 | <https://000057.awsstudygroup.com/> <br> <https://000069.awsstudygroup.com/> |
| Tuesday | Compared RDS, DynamoDB, MongoDB Atlas.<br>Leaning towards MongoDB Atlas since the data model feels more flexible.<br>Not 100% sure yet, might revisit this decision later. | 09/06/2026 | 09/06/2026 | <https://000005.awsstudygroup.com/> <br> <https://000060.awsstudygroup.com/> |
| Wednesday | Read about IAM policy evaluation, least privilege.<br>Traced through an example: explicit deny always wins, that part is clear now.<br>Looked at KMS briefly, and how secrets could be stored instead of plain env files. | 10/06/2026 | 10/06/2026 | <https://000044.awsstudygroup.com/> <br> <https://000033.awsstudygroup.com/> <br> <https://000096.awsstudygroup.com/> |
| Thursday | Studied CloudWatch, SNS, Budgets, tagging.<br>Set up a basic alarm -> SNS test notification, got the email.<br>Wrote down a simple tag naming idea (project name + env). | 11/06/2026 | 11/06/2026 | <https://000008.awsstudygroup.com/> <br> <https://000077.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> <br> <https://000013.awsstudygroup.com/> |
| Friday | Put together everything from this week into one checklist.<br>Frontend, backend, database, storage, security, monitoring, cost - one line each.<br>Still a few open questions, will figure them out once coding starts. | 12/06/2026 | 12/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 4 Achievements:

* Understood why uploaded files and business records should use storage designed for their different access patterns.
* Learned to combine IAM roles, bucket policies, and Block Public Access instead of embedding credentials.
* Compared database choices and their operational trade-offs.
* Connected monitoring, alerting, backup, and budget control to application operations.
* Completed the research phase and prepared to begin Splitly development on June 15, 2026.
