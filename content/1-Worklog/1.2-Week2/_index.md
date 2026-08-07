---
title: "Week 2 Worklog"
date: 2026-05-25
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Understand Amazon VPC and the relationship between subnets, routes, and gateways.
* Compare Security Groups and Network ACLs.
* Build and verify a small public/private network environment.

### Tasks to be carried out this week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | Read about CIDR planning and Availability Zones.<br>Sketched a subnet layout on paper, public block and private block.<br>Kept the math simple, didn't overthink the sizing. | 25/05/2026 | 25/05/2026 | <https://000003.awsstudygroup.com/> |
| Tuesday | Created the VPC, subnets, route table, and IGW.<br>Attached IGW to the VPC, set the default route on the public subnet.<br>Traced a packet path on paper to double check the route made sense. | 26/05/2026 | 26/05/2026 | <https://000003.awsstudygroup.com/> |
| Wednesday | Compared Security Group vs NACL, tested a few rules.<br>SG felt easier since it's stateful, return traffic just works.<br>NACL needed explicit rules both ways, took a couple of tries to get right. | 27/05/2026 | 27/05/2026 | <https://000003.awsstudygroup.com/> |
| Thursday | Read about NAT Gateway, Elastic IP, Flow Logs.<br>Deployed a NAT Gateway in the public subnet, attached an EIP.<br>Updated the private route table, turned on Flow Logs to watch traffic. | 28/05/2026 | 28/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000074.awsstudygroup.com/> |
| Friday | Launched a test EC2 in the private subnet.<br>Confirmed it could reach the internet through NAT but not be reached directly.<br>Terminated it and deleted the NAT Gateway + EIP right after, don't want idle charges. | 29/05/2026 | 29/05/2026 | <https://000003.awsstudygroup.com/> <br> <https://000004.awsstudygroup.com/> |

### Week 2 Achievements:

* Understood how VPC, subnets, route tables, Internet Gateway, and NAT Gateway work together.
* Distinguished network controls at instance and subnet level.
* Practiced tracing a request path instead of changing rules without evidence.
* Verified basic EC2 connectivity inside a VPC.
* Improved awareness of network isolation and least-access design.
