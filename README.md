# AWS Scalable Web Application
## Architecture Overview
![AWS Architecture](<./AWS High available and scalable web app.png>)
A highly available and scalable web application hosted on AWS using EC2, Application Load Balancer, Auto Scaling, and Amazon RDS.

The architecture is deployed inside a VPC across two Availability Zones to ensure high availability, fault tolerance, and scalability.

## AWS Services

| Service                       | Purpose                                                                  |
| ----------------------------- | ------------------------------------------------------------------------ |
| **Amazon Route 53**           | Manages DNS and routes users to the application.                         |
| **Amazon CloudFront**         | Caches static assets and reduces response latency.                       |
| **AWS WAF**                   | Protects the application against common web attacks.                     |
| **Amazon VPC**                | Provides an isolated network environment.                                |
| **Public Subnets**            | Host the internet-facing Application Load Balancer.                      |
| **Private Subnets**           | Host EC2 instances and RDS databases securely.                           |
| **Internet Gateway**          | Enables internet connectivity for public resources.                      |
| **NAT Gateway**               | Provides outbound internet access for private resources.                 |
| **Application Load Balancer** | Distributes incoming traffic across healthy EC2 instances.               |
| **EC2 + Auto Scaling**        | Runs the application and automatically adjusts capacity based on demand. |
| **Amazon RDS Multi-AZ**       | Provides a highly available database with automatic failover.            |
| **Systems Manager**           | Provides secure access to EC2 instances through Session Manager.         |
| **Amazon CloudWatch**         | Monitors infrastructure metrics and application health.                  |
| **Amazon SNS**                | Sends notifications when CloudWatch alarms are triggered.                |

## Architecture Components

### 1. Networking

- One VPC spanning two Availability Zones.
- Public subnets for the load balancer.
- Private application subnets for EC2 instances.
- Separate private database subnets for RDS.
- Internet Gateway and NAT Gateways for network connectivity.
- Security Groups and Network ACLs for traffic control.

### 2. Application Layer

- Application Load Balancer distributes incoming requests.
- EC2 instances run inside private subnets.
- Auto Scaling Group manages EC2 instances across both Availability Zones.
- Scaling policies automatically adjust the number of instances based on demand.

### 3. Database Layer

- Amazon RDS deployed using a Multi-AZ configuration.
- Primary database handles application requests.
- Standby database maintains synchronous replication.
- Automatic failover provides database availability.

### 4. Security and Monitoring

- AWS WAF protects against common web vulnerabilities.
- Security Groups and NACLs control network traffic.
- Systems Manager Session Manager provides secure instance access without requiring public SSH.
- CloudWatch monitors infrastructure performance.
- SNS sends alerts and notifications.

## Request Flow

1. Users access the application through its domain name.
2. Route 53 resolves the domain to CloudFront.
3. CloudFront serves cached content or forwards requests to the ALB.
4. AWS WAF filters incoming requests.
5. The ALB distributes traffic across healthy EC2 instances.
6. EC2 instances process requests and communicate with RDS when needed.
7. The response returns to the user through the ALB and CloudFront.

## High Availability & Scalability

- **Multi-AZ Deployment:** Resources are distributed across two Availability Zones.
- **Auto Scaling:** Automatically adds or removes EC2 instances based on application demand.
- **Load Balancing:** Distributes traffic across healthy application instances.
- **Database Failover:** RDS automatically switches to the standby database if the primary fails.
- **CloudFront Caching:** Reduces origin load and improves response times.
- **Monitoring:** CloudWatch and SNS provide infrastructure monitoring and notifications.
