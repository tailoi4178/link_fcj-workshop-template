---
title: "Eclipse Dataspace Components on AWS: Cost Optimization Strategies"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---



While exploring articles on the **AWS Architecture Blog**, I came across the article **"Eclipse Dataspace Components on AWS: Cost Optimization Strategies."** At first, I expected it to focus mainly on reducing AWS costs. However, after reading it, I realized that the main objective is not simply to spend less, but to design an architecture that matches different workload requirements and optimizes costs from the beginning.

One aspect I found particularly interesting is that the article explains not only the estimated monthly costs but also why certain AWS services contribute more to the overall infrastructure cost. This provides practical guidance for selecting the right architecture instead of using the same deployment model for every environment.

---

## Article Overview

This article is the third and final part of the **Eclipse Dataspace Components (EDC)** series on AWS. While the previous articles focused on deployment architecture, security, and reliability, this one emphasizes the remaining pillars of the **AWS Well-Architected Framework**:

- Performance Efficiency
- Cost Optimization
- Sustainability

Instead of listing AWS service prices, the article identifies the primary cost drivers within an EDC deployment and compares deployment strategies for **Business-Critical Workloads** and **Non-Critical Workloads**.

---

## EDC Deployment Architecture on AWS

The article presents a reference architecture for deploying **Eclipse Dataspace Components (EDC)** on AWS.

The architecture includes:

- Amazon API Gateway for receiving external requests.
- Network Load Balancer for distributing incoming traffic.
- Amazon ECS hosting both the **EDC Control Plane** and **EDC Data Plane**.
- Amazon Aurora PostgreSQL as the primary database.
- AWS Secrets Manager for storing sensitive credentials.
- Amazon Cognito for OAuth 2.0 authentication.
- Amazon S3 for object storage and integration with external data sources.

This architecture separates each component into dedicated services, making the system easier to scale, maintain, and optimize for both performance and cost.

**Figure 1. Eclipse Dataspace Components Reference Architecture on AWS**

![Eclipse Dataspace Components Architecture on AWS](/images/edc-architecture.png)

*Figure 1. Reference architecture for deploying Eclipse Dataspace Components (EDC) on AWS.*

From the architecture diagram, I observed that Amazon API Gateway receives external requests before forwarding them to the Network Load Balancer. The EDC services run on Amazon ECS, while Amazon Aurora PostgreSQL stores application data. Amazon Cognito handles authentication, AWS Secrets Manager secures sensitive information, and Amazon S3 provides object storage and data exchange capabilities.

---

## Workload Categories

One of the most useful concepts presented in the article is the classification of workloads into two categories.

### Business-Critical Workloads

These workloads require:

- High availability
- High reliability
- Strong performance
- Continuous operation

Since they support important business functions, they are deployed using more robust infrastructure to ensure stability and availability.

### Non-Critical Workloads

These workloads include:

- Development environments
- Testing environments
- Proof of Concept (PoC)
- Other systems that can tolerate temporary interruptions

This comparison highlights that development and testing environments do not necessarily require the same infrastructure as production systems, helping organizations reduce unnecessary costs.

---

## Major Cost Drivers

Before reading the article, I assumed that Amazon API Gateway or Amazon S3 would contribute the highest operational costs.

However, AWS identifies the primary cost drivers as:

- Amazon Aurora PostgreSQL
- Amazon ECS running on AWS Fargate
- Network Load Balancer

Meanwhile, services such as Amazon API Gateway, Amazon S3, and Amazon ECR account for only a small portion of the total monthly cost.

This demonstrates that database, compute, and networking resources are the main contributors to infrastructure expenses. Identifying these cost drivers is essential for effective cost optimization.

---

## Cost Comparison

The article compares two deployment scenarios.

### Business-Critical

Recommended infrastructure:

- Amazon Aurora PostgreSQL db.r6g.large
- Amazon ECS with AWS Fargate
- Network Load Balancer

Estimated monthly cost: **approximately USD 387**.

### Non-Critical

Recommended infrastructure:

- Amazon Aurora db.t4g.medium
- AWS Fargate Spot

Estimated monthly cost: **approximately USD 164**, representing about **58% cost savings** compared to the Business-Critical deployment.

This comparison shows that cost optimization is not about removing services but about selecting infrastructure that matches the actual workload requirements.

---

## Cost Optimization Recommendations

The article also provides several practical recommendations for reducing AWS operating costs:

- Use **AWS Fargate Spot** for interruptible workloads.
- Configure **Amazon S3 Lifecycle Policies** to move data into lower-cost storage classes automatically.
- Monitor spending using **AWS Cost Explorer** and **AWS Budgets**.
- Consider **Savings Plans** for long-running and predictable workloads.

These recommendations can be applied not only to EDC deployments but also to many other AWS-based applications.

---

## Key Takeaways

After reading the article, I learned several important lessons:

- Not every environment requires production-level infrastructure.
- Database, compute, and load balancing services usually account for the largest portion of AWS costs.
- Infrastructure should be selected according to workload importance.
- Continuous cost monitoring helps identify unnecessary spending.
- Designing an appropriate architecture from the beginning leads to long-term cost savings.

---

## Conclusion

This article helped me understand that AWS cost optimization is more than simply reducing resources. It involves designing an architecture that fits different workload requirements while maintaining performance and reliability.

In my opinion, this is a valuable article for anyone interested in **AWS Architecture**, the **AWS Well-Architected Framework**, or **FinOps**, as it provides practical insights into building cost-efficient and scalable cloud architectures.

---

## References

- AWS Architecture Blog: *Eclipse Dataspace Components on AWS: Cost Optimization Strategies*
- https://aws.amazon.com/blogs/architecture/eclipse-dataspace-components-on-aws-cost-optimization-strategies/