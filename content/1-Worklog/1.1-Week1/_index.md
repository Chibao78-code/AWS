---
title: "Week 1 Worklog"
date: 2026-05-18
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Become familiar with the First Cloud AI Journey program and its learning process.
* Understand cloud-computing fundamentals and the AWS global infrastructure.
* Learn account security, IAM basics, AWS CLI, and cost-control practices.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Joined the program and read through the internship requirements.<br>Watched the orientation video, took notes on grading criteria.<br>Sketched a rough 12-week plan on paper first, then typed it up. | 18/05/2026 | 18/05/2026 | <https://youtu.be/AQlsd0nWdZk?si=QmmvhYeTisGPtctd> |
| Tuesday | Read about cloud concepts, Regions, AZs, edge locations.<br>Got confused at first between Region and AZ, re-read the doc twice.<br>Wrote down which service categories seem relevant to the project later. | 19/05/2026 | 19/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wednesday | Went through account creation steps and turned on MFA on my phone.<br>Created an IAM user instead of using root, attached a basic policy.<br>Tried inline policy vs group policy just to see the difference. | 20/05/2026 | 20/05/2026 | <https://000001.awsstudygroup.com/> <br> <https://000002.awsstudygroup.com/> |
| Thursday | Installed AWS CLI, picked a default Region (ap-southeast-1).<br>Set up a named profile so I don't hardcode keys anywhere.<br>Ran `aws sts get-caller-identity` to check it's working, then listed some buckets. | 21/05/2026 | 21/05/2026 | <https://000011.awsstudygroup.com/> |
| Friday | Read about Budgets, Cost Explorer, Free Tier limits.<br>Set a budget alert at a small threshold just to test it works.<br>Checked Free Tier usage so far, nothing close to the limit yet. | 22/05/2026 | 22/05/2026 | <https://000007.awsstudygroup.com/> <br> <https://000009.awsstudygroup.com/> |

### Week 1 Achievements:

* Understood the AWS global infrastructure and the roles of common compute, storage, networking, database, and security services.
* Became familiar with secure account access using MFA and non-root IAM identities.
* Configured AWS CLI and practiced basic resource discovery commands.
* Learned to create budget alerts and check costs before and after a lab.
* Established a habit of documenting work and removing unused resources.
