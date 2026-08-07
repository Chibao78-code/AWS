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
| Monday | Double checked IAM permissions before deploying anything.<br>Confirmed the S3 bucket name I picked was actually available.<br>Made sure no secret was going in as a plain CloudFormation parameter. | 27/07/2026 | 27/07/2026 | [../../5-workshop/5.2-prerequiste/](../../5-workshop/5.2-prerequiste/) <br> <https://000037.awsstudygroup.com/> |
| Tuesday | Ran `create-stack`, watched the events tab for failures.<br>One rollback happened because of a typo in a subnet CIDR, fixed and reran.<br>Checked outputs had the EC2 public IP and bucket name. | 28/07/2026 | 28/07/2026 | <https://000037.awsstudygroup.com/> |
| Wednesday | Opened a Session Manager session, cloned the repo onto the instance.<br>Filled in the real `.env` values (MongoDB URI, JWT secret).<br>Built the API, ran it with PM2, checked `pm2 logs` for errors. | 29/07/2026 | 29/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://000058.awsstudygroup.com/> |
| Thursday | Built the frontend, copied dist files to Nginx's web root.<br>Added the SPA fallback so refreshing a route doesn't 404.<br>Set up the `/api/` proxy block pointing to `127.0.0.1:5000`. | 30/07/2026 | 30/07/2026 | [../../5-workshop/5.3-deploycode-webserver/](../../5-workshop/5.3-deploycode-webserver/) <br> <https://nginx.org/en/docs/> <br> <https://pm2.keymetrics.io/docs/usage/quick-start/> |
| Friday | Checked backend logs for a successful MongoDB Atlas connection.<br>Uploaded a test receipt to confirm the IAM Role actually works against S3.<br>`pm2 status` looked healthy, and CloudWatch started showing data. | 31/07/2026 | 31/07/2026 | <https://www.mongodb.com/docs/atlas/> <br> <https://000048.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |

### Week 11 Achievements:

* Provisioned the required network, compute, storage, identity, and monitoring resources.
* Administered EC2 through Session Manager without requiring public SSH.
* Ran the backend under PM2 and kept port 5000 behind Nginx.
* Served the React/Vite production build through Nginx.
* Established the application flow among EC2, MongoDB Atlas, and the S3 receipt bucket.
