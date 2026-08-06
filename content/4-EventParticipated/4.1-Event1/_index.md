---
title: "Event 1"
date: 2026-08-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# SATURDAY MEETUP REPORT

## 1. Event overview

Saturday Meetup combined technical learning, product-development experience, and personal-growth skills. The sessions covered safe and cost-conscious ways to begin learning AWS, a Hackathon product journey, the challenges of maintaining a real application, and the role of confidence in continuous learning.

The most valuable aspect was that the speakers used real experience rather than isolated theory. The event connected technology learning, prototyping, teamwork, and production operations—the same stages that the Splitly project is currently going through.

## 2. Event objectives

- Help beginners learn and practice AWS while controlling cost.
- Introduce guided learning environments and local AWS service emulation.
- Explain how a Hackathon team turns an idea into a product under time constraints.
- Share lessons from deploying, operating, and maintaining a real project.
- Encourage learners to accept challenges and build confidence through practice.

## 3. Speakers

- **Huynh Thai Linh**
- **Huynh An Khuong**
- **Mai Quoc Anh**
- **Nguyen Tran Minh Quan**
- **Nguyen Thi Quynh Nhu**
- **Nghia Tran**

## 4. Main sessions

### 4.1 Learning AWS effectively without unexpected cost

Huynh Thai Linh began with concerns shared by many AWS beginners: exceeding a budget, forgetting to delete lab resources, or avoiding experimentation because the resulting charges are unclear. The answer is not to stop practicing, but to choose an appropriate learning environment and develop disciplined resource-management habits.

Two approaches were introduced:

- **AWS Cloud Quest:** a task-based learning environment that combines guided labs with gamification. It provides a structured path before learners build independent infrastructure.
- **Floci:** a local emulator for selected AWS services that can be used to test application logic and integrations before deploying to a real AWS account.

Compared with LocalStack, Floci was discussed in terms of speed, resource consumption, and a favorable usage model for some scenarios. Nevertheless, emulators cover only part of the AWS service catalog, may return mock data, and cannot fully reproduce IAM, networking, quotas, or production behavior. They are useful during early development but do not replace final testing on AWS.

The practical lesson is to combine several controls: use emulation where appropriate, configure budgets and alerts, tag resources, and follow a cleanup checklist after every lab.

### 4.2 Hackathon journey and the SynthHunter project

Huynh An Khuong, Mai Quoc Anh, and Nguyen Tran Minh Quan shared their Hackathon journey and the development of **SynthHunter**. Their story covered the compressed product lifecycle: selecting a problem, shaping an idea, agreeing on scope, assigning work, designing the architecture, and completing a demonstrable product within a limited period.

The architecture and collaboration discussion showed that a good idea must still be translated into prioritized tasks. A Hackathon team cannot implement every possible feature; success depends on identifying the core value, producing one complete end-to-end flow, and addressing critical risks early.

The session also emphasized communication and time management. Responsibilities should be clear, but the team must integrate frequently because independently completed components do not guarantee that the final product works as a whole.

### 4.3 Building confidence in learning

Nguyen Thi Quynh Nhu discussed how self-doubt can cause learners to miss opportunities, avoid new challenges, and stop when difficulty appears. Common causes include fear of failure, fear of judgment, and excessive focus on the final outcome instead of progress.

The 5P Rule was introduced as a practical framework for gradually overcoming fear. Other suggestions included starting with small goals, recognizing daily achievements, maintaining a learning mindset, and choosing progress over perfection.

The central message was that confidence does not mean always knowing the answer. It develops when a learner takes action, observes the result, receives feedback, and continues to improve.

### 4.4 Real-world development experience from TuviDaiviet

Nghia Tran shared lessons from building and maintaining **TuviDaiviet**. Unlike a short-lived demonstration, a real product must handle technical defects, operational requirements, user feedback, and continuous improvement.

The challenges and opportunities described in this session demonstrated that development does not end when a feature is coded. A team must also deploy, monitor, troubleshoot, maintain, and feed real user feedback back into the product plan.

## 5. Knowledge and skills gained

### Technical knowledge

- Learned how AWS Cloud Quest, local emulation, and a real AWS account can serve different learning stages.
- Understood emulator limitations and why IAM, networking, and data flows must be verified on AWS.
- Recognized that cost management begins with budgets, alerts, tags, and resource-cleanup procedures.
- Gained insight into selecting a minimum architecture for a time-limited Hackathon product.
- Understood that deployment, monitoring, and maintenance belong to the product lifecycle rather than being separate post-development tasks.

### Skills and mindset

- Define product scope around core value instead of attempting every idea.
- Break work into clear responsibilities and integrate results frequently.
- Manage time while working under a deadline.
- Treat failures and feedback as information for improving the product.
- Build confidence through small achievements and continuous practice.

## 6. Application to the Splitly project

The meetup lessons can be applied directly to Splitly:

1. **AWS cost control:** configure AWS Budgets, monitor EC2/public IPv4 usage, and follow a CloudFormation cleanup checklist after labs.
2. **Pre-deployment testing:** selected S3 behavior may be emulated locally, but IAM Roles, bucket policies, and presigned URLs must be validated on AWS.
3. **MVP prioritization:** stabilize sign-in, groups, expenses, balances, settlements, and receipts before adding secondary features.
4. **Clear ownership:** divide frontend, backend, data, AWS, and documentation tasks while defining frequent integration points.
5. **Product operations:** use PM2 and CloudWatch for failure visibility, document deployment/recovery, and treat user feedback as input to the next version.
6. **Experimental mindset:** release small changes, validate them with evidence, and adjust instead of waiting for a perfect version.

## 7. Reflection

The event showed that effective technology learning requires three elements at the same time: an appropriate practice environment, collaboration that turns knowledge into a product, and the resilience to learn from mistakes. The AWS session offered safer practice options; SynthHunter demonstrated the importance of scope and teamwork; the confidence session emphasized action and progress; and TuviDaiviet provided a realistic view of responsibility after release.

![Photo from Event 1](/images/4-Event/Splitly/event-1-pic.jpg)

> My main takeaway is that a strong product is not measured only by its feature count. It also depends on cost control, team coordination, reliable operations, and continuous improvement from real feedback.
