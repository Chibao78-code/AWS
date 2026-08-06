---
title: "Blog 1"
date: 2026-06-04
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# OPTIMIZING KUBERNETES OPERATIONS WITH AMAZON EKS AUTO MODE

**Original AWS publication date:** March 23, 2026

**Topics:** Kubernetes, operations, security, observability, and cost optimization

The insurance industry is moving more digital services to the cloud to meet customer expectations for fast, reliable, and consistent access. Generali Malaysia began its AWS migration in 2019 and selected Amazon Elastic Kubernetes Service (Amazon EKS) for its modernized applications. As the number of microservices and platform tenants increased, the challenge moved beyond simply running containers to operating many workloads securely, reliably, and at a controlled cost.

This article examines how Generali combines Amazon EKS Auto Mode with AWS security, observability, and cost-management services. The main lesson is that infrastructure automation cannot stand alone: sustainable operations require upgrades, security, monitoring, and cost allocation to be designed as one system.

## 1. The challenge of scaling Kubernetes operations

In a conventional cluster, the platform team provisions and replaces nodes, patches operating systems, manages EKS add-ons, configures storage and load balancers, upgrades Kubernetes, monitors resources, and troubleshoots incidents. When multiple projects share the platform, manual processes create three common problems:

* Configurations diverge between clusters and tenants, increasing security and compliance risk.
* Teams overprovision resources to handle uncertain demand, increasing cost while reducing utilization efficiency.
* Engineers spend more time maintaining infrastructure and less time supporting application teams and product improvements.

Generali needed to expand application adoption while maintaining a lean operations team. It therefore aligned the platform with the Operational Excellence, Security, Reliability, Performance Efficiency, and Cost Optimization pillars of the AWS Well-Architected Framework.

## 2. The role of Amazon EKS Auto Mode

EKS Auto Mode expands the infrastructure responsibilities managed by AWS. It automatically handles several important capabilities:

* Selecting, provisioning, and replacing EC2 nodes according to workload demand and node-pool configuration.
* Scaling resources up and down to reduce unnecessary idle capacity.
* Providing managed integration for load balancing and block storage.
* Patching Bottlerocket, updating default EKS add-ons, and supporting cluster upgrades.
* Standardizing infrastructure operations so application teams do not build separate node-management processes.

This allows the DevOps team to focus on workload quality, upgrade compatibility, and application support instead of repetitive maintenance. Automation, however, does not remove the need for operational design.

## 3. Controlling disruption during node updates

EKS Auto Mode regularly releases new Amazon Machine Images and replaces older nodes with updated ones. If a workload is not prepared for this lifecycle, node replacement can stop multiple replicas of a service simultaneously and cause an outage.

Generali reduces this risk through the following measures:

* Scheduling maintenance windows during off-peak hours.
* Defining **Pod Disruption Budgets** so a minimum number of service replicas remain available.
* Defining **Node Disruption Budgets** to limit how many nodes can be replaced at once.
* Using the **Horizontal Pod Autoscaler** so replica counts follow traffic rather than remaining permanently overprovisioned.
* Running stateless microservices, treating pods as immutable, and using Helm charts as a standardized deployment mechanism.

These principles separate durable data from the pod lifecycle. When a pod or node is replaced, the platform can create a new replica without losing critical state.

## 4. Layered security architecture

EKS Auto Mode reduces infrastructure administration but does not replace security controls. Generali adds several services that detect, prioritize, and prevent threats at different stages.

### Amazon GuardDuty Extended Threat Detection

GuardDuty correlates signals from EKS audit logs, runtime behavior, malware activity, and AWS API activity. Instead of presenting isolated alerts, Extended Threat Detection can construct the sequence of a multi-stage attack, such as container exploitation followed by privilege escalation and movement inside a cluster.

The security team receives the affected resources, event timeline, and priority in a consolidated investigation. This reduces analysis time and directs remediation toward components with the greatest potential blast radius.

### Amazon Inspector

A vulnerable image in a repository might not be in use, while an image running in many pods requires urgent attention. Inspector maps Amazon ECR images to running EKS containers and adds context such as cluster ARN, pod count, and last in-use date.

This runtime context helps the team prioritize remediation by actual exposure instead of working from an undifferentiated list of repository CVEs.

### AWS Network Firewall

A compromised workload may attempt to download additional payloads or exfiltrate data. Generali places EKS workloads in private subnets and routes outbound traffic through Network Firewall. Policies can allow HTTPS only to approved hostnames using Server Name Indication, while CloudWatch logs record accessed hostnames for review.

This egress control limits connections to unapproved external services and produces evidence for auditing and anomaly investigation.

### AWS Secrets Manager and External Secrets Operator

Secrets should not be embedded in source code, Helm charts, or deployment manifests. Generali stores credentials centrally in Secrets Manager and uses External Secrets Operator to synchronize required values into Kubernetes Secrets on a recurring schedule.

This design separates credential lifecycle from application code, supports rotation and auditing, and prevents every application team from implementing a separate secret-retrieval mechanism.

## 5. Observability by cluster, namespace, and application

A multi-tenant platform must give each team visibility into the components it owns. Generali uses Amazon CloudWatch as a data source for cluster health, nodes, pods, resource utilization, logs, traces, and application signals. Amazon Managed Grafana presents this information through dashboards scoped to EKS namespaces or projects.

Clear dashboards and alerts help the operations team determine whether an incident originates in a node, Kubernetes configuration, or the application itself. Using the managed service also avoids maintaining a separate Grafana infrastructure stack.

## 6. Cost allocation and optimization

Automatic scaling solves only part of the cost problem. Because several business units share the platform, Generali must identify which project is responsible for each part of consumption. AWS Billing split cost allocation data for Amazon EKS uses attributes such as cluster, namespace, deployment, and node tags to analyze Kubernetes costs alongside other AWS spending.

With this information, the team can:

* Find namespaces or deployments that require right-sizing.
* Apply EC2 Savings Plans to predictable baseline capacity across approved node-pool instance types.
* Use lower-cost Graviton instances when container images support ARM64.
* Discuss cost by application and business unit instead of looking only at one cluster-wide bill.

## 7. Results

Combining EKS Auto Mode with integrated AWS services moved Generali from a Kubernetes environment with extensive manual work toward a more automated and standardized platform. The main outcomes include less node and upgrade administration, stronger threat detection and vulnerability prioritization, faster incident diagnosis, improved resource efficiency, and shorter application delivery cycles.

More importantly, the DevOps team can devote additional time to supporting application teams and preparing the platform for new workloads, including AI models and agentic applications, instead of repeatedly maintaining infrastructure components.

## 8. Personal takeaway

This case taught me that a production Kubernetes platform should not be judged only by whether the cluster is running. It should answer five questions together: Can infrastructure update automatically? Can upgrades occur without disrupting workloads? Are threats and vulnerabilities prioritized correctly? Can each team observe what it owns? Can cost be traced to the responsible application?

EKS Auto Mode addresses much of the compute and cluster lifecycle, but the full operational value comes from combining disruption budgets, stateless workloads, threat detection, vulnerability management, egress control, secret management, observability, and cost allocation into one coherent architecture.

## Article links

* [Facebook post](https://www.facebook.com/photo?fbid=1647830246522148)
* [Source article on the AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/how-generali-malaysia-optimizes-operations-with-amazon-eks/)
