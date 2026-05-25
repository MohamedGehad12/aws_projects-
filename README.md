# 🌐 AWS Scalable Web Application — ALB, Auto Scaling & Multi-AZ RDS

> Production-grade web application on AWS using EC2, VPC, ALB, Auto Scaling, 
> CloudFront, and Multi-AZ RDS — built for high availability and scalability.

---

## 📌 Project Overview

This project demonstrates a fully production-ready web application deployed 
on AWS using EC2 instances inside a properly architected VPC. The architecture 
spans two Availability Zones for high availability, uses an Application Load 
Balancer for traffic distribution, Auto Scaling for elasticity, and a Multi-AZ 
RDS instance for a resilient database backend — with all compute resources 
secured inside private subnets.


---

## ☁️ AWS Services Used

| Service | Role |
|---|---|
| **Amazon VPC** | Public & private subnets, NAT Gateway, route tables, NACLs |
| **Amazon EC2 + ASG** | Launch Template, target tracking scaling policies |
| **Application Load Balancer** | Layer 7 routing, listener rules, target group health checks |
| **AWS WAF** | OWASP Top 10 protection, rate limiting rules |
| **Amazon CloudFront** | Cache static assets, reduce latency globally |
| **Amazon RDS Multi-AZ** | MySQL/PostgreSQL with automated failover |
| **Amazon Route 53** | Alias record pointing to ALB, health checks |
| **AWS Systems Manager** | Session Manager for bastion-free secure instance access |
| **Amazon CloudWatch** | Dashboards, alarms, metrics |
| **Amazon SNS** | Notifications and alerts |

---

## 🏛️ Architecture Overview

### VPC Design

Region
└── VPC (10.0.0.0/16)
├── Availability Zone A
│   ├── Public Subnet 1   → NAT Gateway, Internet Gateway
│   └── Private Subnet 1  → EC2 (Auto Scaling Group)
│   └── Private Subnet 3  → RDS Primary
│
└── Availability Zone B
├── Public Subnet 2   → (reserved for HA)
└── Private Subnet 2  → EC2 (Auto Scaling Group)
└── Private Subnet 4  → RDS Standby

### Traffic Flow
Users
→ DNS Resolution (Route 53)
→ AWS WAF (OWASP protection)
→ Amazon CloudFront (static asset caching)
→ Application Load Balancer (Layer 7 routing)
→ Auto Scaling Group / EC2 (private subnets)
→ RDS Multi-AZ (primary → synchronous replication → standby)

---

## 🔄 High Availability Design

- **Two Availability Zones** — all critical components are duplicated across AZ-A and AZ-B
- **Auto Scaling Group** — automatically adds/removes EC2 instances based on demand
- **ALB Health Checks** — unhealthy instances are automatically removed from rotation
- **RDS Multi-AZ** — synchronous replication to standby; automatic failover in case of primary failure
- **NAT Gateway** — allows private subnet instances to reach the internet for updates without being publicly exposed

---

## 🛡️ Security Layers

| Layer | Protection |
|---|---|
| AWS WAF | OWASP Top 10, rate-based rules |
| Security Groups | Stateful inbound/outbound rules per resource |
| NACLs | Stateless subnet-level traffic filtering |
| Private Subnets | EC2 and RDS never directly exposed to internet |
| NAT Gateway | Outbound-only internet access for private instances |
| Session Manager | No SSH keys, no bastion host needed |
| IAM Roles | Least-privilege roles for EC2 and other services |

---

## 📡 Observability

- **CloudWatch Dashboards** — CPU, memory, request count, DB connections
- **CloudWatch Alarms** — trigger Auto Scaling and alert on anomalies
- **SNS Notifications** — email/SMS alerts on alarm state changes
- **ALB Access Logs** — full request logging to S3
- **RDS Enhanced Monitoring** — OS-level metrics for database instances

---

## 📚 Key Learning Outcomes

- ✅ Design VPCs with correct subnet, route table, and NAT Gateway configurations
- ✅ Build highly available architectures across multiple Availability Zones
- ✅ Configure ALB listener rules and target group health checks
- ✅ Implement Auto Scaling with target tracking and step scaling policies
- ✅ Secure applications with WAF, Security Groups, NACLs, and private subnets
- ✅ Use Systems Manager Session Manager as a bastion-free access alternative
- ✅ Set up Multi-AZ RDS with automated failover for database resilience
- ✅ Integrate CloudFront to cache static assets and reduce origin load

---

## 🗂️ Repository Structure
aws_projects/
│
├── project-1
│   
│
├── README.md
└── LICENSE

---

## 👤 Author

**Mohamed Gehad**
- GitHub: [@MohamedGehad12](https://github.com/MohamedGehad12)

---
