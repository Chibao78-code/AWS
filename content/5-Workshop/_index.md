+++
title = "Workshop"
date = 2026-07-16
weight = 5
chapter = false
pre = "<b>5. </b>"
+++

# DEPLOYING SPLITLY ON AWS

This workshop covers the complete deployment of **Splitly**, a group expense management and bill-splitting application. AWS CloudFormation provisions the foundation; the React/Vite frontend and Node.js/Express backend run on Amazon EC2; Amazon S3 stores receipt images; and Amazon CloudWatch supports operational monitoring.

After completing the workshop, you will be able to:

- Explain the request flow from the browser to the frontend, API, and data services.
- Provision repeatable networking, security, and compute resources with CloudFormation.
- Configure environment variables without committing secrets to source control.
- Build React/Vite, manage Node.js/Express with PM2, and configure Nginx as a reverse proxy.
- Validate each system layer, diagnose common failures, and remove lab resources safely.

Workshop sections:

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Deploy code and web server](5.3-DeployCode-WebServer/)
4. [System testing](5.4-Test/)
5. [Resource cleanup](5.5-Cleanup/)

<!-- {{% notice warning %}}
Resource names, repository URLs, IP addresses, connection strings, and credentials shown here are placeholders. Replace them with the Splitly team's values and never commit secrets to Git.
{{% /notice %}} -->
