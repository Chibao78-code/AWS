---
title: "Week 11 Worklog"
date: 2026-07-27
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Provision the Splitly lab infrastructure on AWS.
* Deploy the Node.js backend and React/Vite frontend on Amazon EC2.
* Connect MongoDB Atlas, Amazon S3, and CloudWatch safely.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Reviewed deployment permissions, parameters, Region, resource names, bucket uniqueness, and secret-handling requirements. | 27/07/2026 | 27/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000037.awsstudygroup.com/> |
| Tuesday | Created and monitored the CloudFormation stack; verified VPC, subnet, routes, Security Group, EC2, IAM Role, and outputs. | 28/07/2026 | 28/07/2026 | <https://000037.awsstudygroup.com/> |
| Wednesday | Connected through Session Manager, cloned the repository, configured backend variables, built the API, and started it with PM2. | 29/07/2026 | 29/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://000058.awsstudygroup.com/> |
| Thursday | Built the React/Vite frontend and configured Nginx to serve the SPA and proxy `/api/` to `127.0.0.1:5000`. | 30/07/2026 | 30/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Friday | Verified MongoDB Atlas connectivity, EC2 IAM access to the S3 receipt bucket, PM2 status, Nginx, and initial CloudWatch data. | 31/07/2026 | 31/07/2026 | <https://www.mongodb.com/docs/atlas/> <br> <https://000048.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |

### Week 11 Achievements:

* Provisioned the required network, compute, storage, identity, and monitoring resources.
* Administered EC2 through Session Manager without requiring public SSH.
* Ran the backend under PM2 and kept port 5000 behind Nginx.
* Served the React/Vite production build through Nginx.
* Established the application flow among EC2, MongoDB Atlas, and the S3 receipt bucket.
