+++
title = "Introduction"
date = 2026-07-16
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

# SPLITLY WORKSHOP OVERVIEW

## Problem statement

During trips, shared living, and group activities, different members often pay on behalf of the group. Manual records easily miss expenses, make receipts difficult to reconcile, and require repeated calculations to determine who owes whom. Splitly keeps members, expenses, split rules, balances, and evidence in one place.

## Architecture implemented in this workshop

![Splitly deployment architecture](/images/5-Workshop/Splitly/5.1-Overview/diagram1.png)

The main request flow is:

1. Users access the EC2 public address over HTTP port 80.
2. **Nginx** serves the React/Vite production build and forwards `/api/` requests to `127.0.0.1:5000`.
3. The **Node.js/Express** API handles authentication, groups, members, expenses, and settlement logic. **PM2** keeps the process running.
4. The backend stores application data in **MongoDB Atlas** and uploads receipt images to **Amazon S3** through the EC2 IAM role.
5. **Amazon CloudWatch** provides logs and metrics. Administrators use **AWS Systems Manager Session Manager**, avoiding a publicly exposed SSH port.

For this lab, frontend and backend share one EC2 instance so the complete flow is easy to deploy and inspect. A future production evolution could host the frontend on S3 and CloudFront and add Route 53, ACM, and AWS WAF. Those services are an extension, not a requirement of the current workshop.

## Expected result

At completion, the EC2 instance serves the Splitly UI, Nginx routes API calls correctly, `splitly-api` is `online`, MongoDB Atlas is reachable, and configured receipt operations can use S3. The validation section tests each layer independently so infrastructure, backend, frontend, and proxy failures can be distinguished.
