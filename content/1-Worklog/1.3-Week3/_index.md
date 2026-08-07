---
title: "Week 3 Worklog"
date: 2026-06-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Learn Amazon EC2 instance selection, images, storage, and access methods.
* Understand scaling, load balancing, startup automation, and monitoring.
* Practice deploying and diagnosing a simple web workload.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Compared EC2 families and pricing options.<br>Read about AMIs and the Nitro System, still fuzzy on some details.<br>Decided t3/t4g would be enough for this project, no need for anything bigger. | 01/06/2026 | 01/06/2026 | <https://000004.awsstudygroup.com/> |
| Tuesday | Studied EBS volumes, snapshots, instance store, key pairs.<br>Tried gp3 vs io volumes, gp3 seems fine for this scale.<br>Took a snapshot just to see the process, deleted it after. | 02/06/2026 | 02/06/2026 | <https://000004.awsstudygroup.com/> <br> <https://000058.awsstudygroup.com/> |
| Wednesday | Launched an EC2, attached an extra volume.<br>Wrote a small User Data script to install packages on boot.<br>Checked instance metadata, made sure it was using IMDSv2 not v1. | 03/06/2026 | 03/06/2026 | <https://000004.awsstudygroup.com/> |
| Thursday | Read about Auto Scaling and ALB, health checks.<br>Set up a target group, watched how an unhealthy instance gets swapped out.<br>Still need to read more on scaling policies later. | 04/06/2026 | 04/06/2026 | <https://000006.awsstudygroup.com/> |
| Friday | Checked CloudWatch metrics/logs for the test instance.<br>Stopped the web service on purpose to see the alarm trigger.<br>Terminated everything after, don't want lab resources running overnight. | 05/06/2026 | 05/06/2026 | <https://000008.awsstudygroup.com/> |

### Week 3 Achievements:

* Learned to choose EC2 and storage configurations according to workload needs.
* Understood persistent EBS storage versus temporary instance storage.
* Used startup automation and safer administration methods.
* Understood the roles of health checks, load balancing, and scaling.
* Practiced using metrics and logs as evidence during troubleshooting.
