# AWS-Cloud-Architectural-Design-for-Ecommerce-in-Africa-v1
A proposed architectural design for a cost-effective and reliable AWS Cloud architecture for an e-commerce platform targeting Africa region with a strong emphasis on high availability, security, monitoring, and low latency.

<b>Proposed Solution:</b>

*** For Infrastructure Setup:
AWS Region Selection & Availability Zones (AZs): Since we focus on African customers, we will choose Cape Town, South Africa as the region. Now, to ensure redundancy and high availability, then we will deploy across multiple AZs within the Cape Town region so that if one AZ fails, others will continue operations.


*** For Compute Layer:
Option 1
 AWS Lambda: This could be useful for now to save costs, as it ensures that the app won't continuously be running. Which means, we pay based on calls or usage of the application itself.  

Option 2
Amazon Elastic Load Balancer (ELB): Use Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances to provide scalability and fault tolerance.
Amazon EC2 with Auto Scaling: Reserved Instances are recommended to deploy application servers on EC2 instances since we are not sure of the workloads and need to enable Auto Scaling to reduce the cost by scaling-in and scaling-out to adjust instances based on-demand.


*** For Data Layer:
Amazon RDS (Relational Database Service): Based on the high performance and availability required in the project, it’s recommended to use  RDS with Amazon Aurora to store our user information because of is fault-tolerant and automated backups. For the best practices to release much load from the primary DB, we need to enable Read Replicas. 

Amazon S3: Use Amazon S3 Intelligent-tiering (and also enable versioning and lifecycle policy) to store product images and enable Access Point for Amazon CloudFront to reduce latency.


*** For Content Delivery and Caching:
Amazon CloudFront: Use CloudFront as a Content Delivery Network (CDN) to reduce latency for our users and cache all static assets (e.g. images).
Amazon ElastiCache (Redis or Memcached): To reduce our database workload and improve response times for our users. We will set up the caching for frequently accessed data (e.g., homepage, list of items).


*** For Security:

Encryption at Rest and in Transit:
AWS-managed keys (KMS) need to be enabled for all data on RDS and S3.
SSL/TLS certificates will be used for security and encrypted communication between customers and the application.

IAM and Access Management: Use IAM roles and policies to give least-privilege access to ensure that only authorized services and users can access specific data.
VPC and Security Groups: Deploy resources in a Virtual Private Cloud (VPC) with private and public subnets.

AWS WAF (Web Application Firewall): Apply a WAF in front of the ALB to protect the application against common threats, such as SQL injection and cross-site scripting.
AWS Shield: Use AWS Shield (standard, no additional cost) to protect against DDoS attacks.


*** For Monitoring and Logging:
Amazon CloudWatch: Use CloudWatch for monitoring and other metrics and also set up Alarms for notification of unusual activities.
AWS CloudTrail: Enable CloudTrail to log API calls for auditing and compliance.
AWS Config: Use AWS Config for tracking and managing changes to configurations, ensuring that resources remain compliant.



