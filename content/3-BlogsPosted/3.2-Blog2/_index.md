---
title: "Blog 2"
date: 2025-06-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# HOW AWS WAF HELPS SCALE TO WIN DEFEND AGAINST DDoS ATTACKS

**Original AWS publication date:** July 14, 2025

**Topics:** DDoS, Amazon CloudFront, AWS WAF, rate limiting, and CAPTCHA

During the 2024 United States presidential election season, Scale to Win became the target of DDoS events exceeding two million requests per second from nearly ten thousand IP addresses. After a brief period of downtime early in the events, the team worked with AWS to build a layered defense using Amazon CloudFront, AWS WAF, and AWS Shield Advanced.

The case demonstrates that DDoS defense is not simply a matter of adding application servers. If malicious requests still reach the Application Load Balancer and application, connection and compute capacity can be exhausted before Auto Scaling responds. An effective design filters traffic as close to the edge as possible, prevents direct access to the origin, and applies different policies to different client types.

## 1. The original architecture and its limitation

Scale to Win initially pointed DNS directly to an Application Load Balancer. The ALB served as the single entry point and distributed requests to an EC2 application fleet. The design was simple, but legitimate and malicious traffic both consumed Regional ALB capacity before application-level processing could occur.

When an event grows to millions of requests per second, adding EC2 instances does not solve the network-layer problem or the load-balancer bottleneck. It also forces the backend to spend resources on TLS, connections, and requests that provide no business value.

## 2. Moving protection to the AWS edge

The updated path places CloudFront and AWS WAF in front of the ALB:

`Users → CloudFront + AWS WAF → Application Load Balancer → EC2`

CloudFront provides a global edge network with more capacity for large network events than an individual ALB. AWS WAF attached to CloudFront inspects requests at the edge, while AWS Shield Advanced provides additional DDoS protection and response support.

This topology provides three major benefits:

* Abnormal TCP and HTTP traffic can be absorbed before it reaches the VPC.
* WAF capacity scales with CloudFront to accommodate sudden traffic growth.
* CloudFront geographic restrictions can exclude regions that the service does not support. In this case, more than half of the malicious traffic came from countries Scale to Win blocked, reducing both request volume and WAF cost.

## 3. Preventing attackers from bypassing CloudFront

Placing CloudFront before an ALB is insufficient if the ALB endpoint remains directly accessible. An attacker who discovers the origin hostname can bypass every edge rule and send requests straight to the load balancer.

Scale to Win protects the origin with two controls:

1. The ALB security group accepts traffic only from the CloudFront managed prefix list.
2. CloudFront inserts a custom shared secret header into origin requests. The ALB listener forwards requests only when the header matches; all others receive HTTP 403.

The second control matters because an attacker could create a separate CloudFront distribution and configure the victim ALB as its origin. That traffic would come from a valid CloudFront address, but it would not contain the expected secret. Secrets Manager and Lambda can be used to rotate the value and update both the CloudFront and ALB configurations.

## 4. Combining heuristics with hard limits

Scale to Win uses two complementary detection approaches instead of relying on one rule.

### Traffic-pattern heuristics

The team examines sampled requests and AWS WAF logs to identify characteristics common in attack traffic but rare in legitimate requests, such as headers, query parameters, URIs, or request-body patterns. A new rule should first use the **Count** action to measure false positives and false negatives. Amazon Athena queries can correlate matches with IPs producing large volumes. The action changes to **Block** only after validation.

Attackers can modify parameters or replay requests that resemble legitimate sessions, so heuristics are valuable for rapid response but require continuous monitoring and adjustment.

### JA3 and JA4 fingerprints

JA3 and JA4 derive fingerprints from TLS ClientHello attributes. A botnet often uses a limited number of client implementations and therefore produces a few common fingerprints. A fingerprint is not an identity, however: legitimate software might share it, and advanced attackers can randomize TLS properties. JA3/JA4 should therefore complement volume, IP, path, and behavioral signals rather than act as the only blocking rule.

### Hard rate limits by source IP

AWS WAF rate-based rules cap requests from an IP address during a time window. Source IP is a stronger signal because a forged source generally cannot complete a TCP or TLS handshake. A single low threshold is still unsafe: a campaign office, dormitory, or university can place hundreds of legitimate users behind one NAT address.

## 5. Separating machine and browser traffic

Scale to Win classifies requests by URI path to distinguish machine-facing webhook and API routes from browser-facing application routes. Each group can then receive suitable authentication and thresholds.

### Machine-to-machine traffic

Twilio webhooks and legitimate API clients can send tens of thousands of requests from a small number of addresses, and they cannot solve a CAPTCHA. Controls for this traffic include:

* IP sets based on provider-published addresses or static proxy endpoints.
* Early allow rules for verified paths and sources before browser rules are evaluated.
* API keys, request signatures, or certificate authentication where supported.
* Per-client rate limits that return HTTP 429, paired with controlled client retries.

### Browser traffic

Browser requests use a two-tier strategy:

* A lower threshold represents the expected traffic of roughly two or three users. Requests above it receive a CAPTCHA challenge instead of an immediate block.
* A higher threshold represents the largest legitimate case with hundreds of users sharing one IP. Requests above it are blocked.

Rule priority must preserve the intended evaluation order and allow validated CAPTCHA requests within the permitted range. This design keeps the normal experience unchanged, challenges uncertain traffic, and blocks only volumes beyond the largest valid scenario.

## 6. Integrating CAPTCHA correctly

Instead of relying only on an interstitial WAF response, a frontend can use the AWS WAF CAPTCHA JavaScript API. The user completes a challenge within the application experience, receives a token, and sends that token with subsequent requests. This gives the application better control and avoids unexpectedly failing a critical action.

A solved token can still be copied and distributed across a botnet. CAPTCHA cannot therefore be treated as sufficient proof without examining how the token is used.

## 7. Preventing CAPTCHA token reuse

Scale to Win monitors the relationship between tokens and source IP addresses. If the same token appears from many IPs within a short period, it is likely being shared. AWS WAF labels, logs, and custom rules can identify and block this pattern.

This control asks not only whether a client holds a valid token, but whether its token behavior is plausible. It illustrates how context and event correlation strengthen a basic verification mechanism.

## 8. Observing and tuning rules

WAF policies should not be deployed once and forgotten. Each new rule needs a Count phase, dashboards for allowed, blocked, and challenged requests, complete logs, and Athena queries to evaluate its effect. Useful signals include false-positive rate, top source addresses, targeted paths, fingerprints, countries, and WAF capacity consumption.

As attack tactics change, heuristics and thresholds must change as well. Observability enables the team to respond quickly without turning the protection layer into a source of downtime for legitimate users.

## 9. Results and value

The final design contains several independent barriers: Shield and CloudFront absorb traffic, geographic restrictions remove unsupported regions, WAF classifies requests, the security group and shared secret protect the origin, and rate limits, CAPTCHA, and token-reuse detection govern application-layer behavior.

The architecture helped Scale to Win remain available during large DDoS events, reduced load on the ALB and EC2 fleet, and still supported offices with many users behind one IP as well as high-volume webhooks. It demonstrates defense in depth: if an attacker evades one signal, other controls continue to enforce policy.

## 10. Personal takeaway

My main lesson is that rate limiting works only when traffic types are understood. One global threshold can block a webhook or a group of users behind NAT, while a threshold that is too high cannot stop a botnet. Requests must be classified by path, source, and authentication capability before combining heuristics, hard limits, and CAPTCHA.

The second lesson is to protect the origin. If an ALB remains directly reachable, investment in CloudFront WAF rules can be bypassed. Finally, every security rule requires logs, a Count-mode validation stage, and a tuning process. Observability is part of the defense system, not an optional add-on.

## Article links

* [Facebook post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2180420536056240/)
* [Source article on the AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/how-scale-to-win-uses-aws-waf-to-block-ddos-events/)
