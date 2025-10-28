---
title: 'Moving to Multi-Cluster EKS'
description: 'On building an active/active EKS architecture with Application Load Balancers'
pubDate: 2025-10-28
heroImage: '../../assets/aws-k8s.png'
---

Back in 2021, I worked on migrating Onfido's infrastructure from single production EKS clusters per region to a multi-cluster architecture. We wrote about it on the [AWS Containers Blog](https://aws.amazon.com/blogs/containers/onfidos-journey-to-a-multi-cluster-amazon-eks-architecture/).

## Why Multi-Cluster?

During a Kubernetes upgrade, we experienced a brief service degradation. Testing upgrades in preproduction was thorough, but production has a way of surfacing edge cases you didn't anticipate. The incident made it clear: we needed a way to take a cluster offline for maintenance without affecting traffic.

The requirements were straightforward:
- Deploy services across multiple clusters easily
- Serve production traffic from multiple clusters simultaneously
- Shift traffic between clusters instantly, for planned or unplanned scenarios

## The Architecture Decision

We evaluated federation technologies like KubeFed and service mesh solutions. Both could work, but their maturity at the time ([kubefed is now deprecated](https://github.com/kubernetes-retired/kubefed)), and operational overhead were not confidence inspiring. Instead, we chose independent clusters in the same region with a single Application Load Balancer routing between them.

The key: ALB weighted listener rules. Each cluster got its own target group, and we could adjust traffic distribution through rule weights. This gave us gradual traffic migration during upgrades and clear visibility into which cluster was handling requests.

## The Result

The architecture eliminated the nervousness around cluster upgrades. We could shift traffic to one cluster, upgrade the other, validate everything worked, then shift back and scale down the second cluster.

The [AWS blog post](https://aws.amazon.com/blogs/containers/onfidos-journey-to-a-multi-cluster-amazon-eks-architecture/) has the full technical details and architecture diagrams.

## First post

This is the first post in this blog. The architecture described here is from 2021, and a lot has changed since then. I'll write more about recent learnings and current best practices in future posts.