# Secure Cloud Infrastructure Deployment Using AWS VPC

## 📌 Project Overview
This project demonstrates the design and deployment of a secure 3-tier cloud infrastructure using **AWS Virtual Private Cloud (VPC)**. The infrastructure is built across multiple Availability Zones to host application servers, database layer (MongoDB), and a public access layer with controlled and hardened security.

## 🎯 Objective
- Create an isolated private network in AWS using VPC  
- Separate resources into Public, Application, and Database subnets  
- Provide internet access using Internet Gateway and NAT Gateway  
- Implement security using Security Groups and Network ACL  
- Deploy and test EC2 instances and MongoDB communication securely.

---

## 🏗 Architecture Design

### CIDR Planning
- **VPC CIDR:** `10.0.0.0/16`  
- **Public Subnet (Web/Bastion):** `10.0.1.0/24` → ap-south-1a  
- **Private App Subnet:** `10.0.2.0/24` → ap-south-1a  
- **Private DB Subnet (MongoDB):** `10.0.3.0/24` → ap-south-1b  

### Components Used
- VPC  
- Subnets in different AZs  
- Internet Gateway (IGW)  
- NAT Gateway with Elastic IP  
- Route Tables  
- Security Groups  
- Network ACL (NACL)  
- EC2 Instances  
- EBS Storage  
- MongoDB on port **27017**

---

## ⚙ Implementation Steps

1. Selected AWS Region → **ap-south-1 (Mumbai)**  
2. Created VPC with CIDR `10.0.0.0/16`  
3. Designed public and private subnets across AZs  
4. Attached **Internet Gateway** for public traffic  
5. Configured **Route Tables**  
   - Public RT → `0.0.0.0/0 → IGW`  
   - Private RT → `0.0.0.0/0 → NAT`
6. Created **NAT Gateway** in public subnet for outbound internet of private servers  
7. Implemented Security Groups  
   - Bastion SG → SSH 22 from my IP  
   - App SG → SSH from Bastion SG  
   - DB SG → MongoDB 27017 from App SG only  
8. Configured **Network ACL** at subnet level  
9. Launched EC2 instances in respective subnets  
10. Tested end-to-end connectivity.

---

## 🔐 Security Implementation

### Security Groups
- Restricted SSH access to Bastion host only  
- MongoDB layer is not accessible from internet  
- Internal communication allowed only from Application subnet on **27017**

### Network ACL
- Public subnet → allow 22, 80 outbound all  
- Private DB subnet → block all internet inbound, allow only internal MongoDB traffic.

---

## 🧪 Testing & Validation

| Test Case | Result |
|------|--------|
| SSH to Bastion from Internet | ✔ Allowed |
| Bastion → App SSH | ✔ Allowed |
| App → MongoDB 27017 | ✔ Allowed |
| Direct Internet → DB | ✖ Blocked |
| Private subnet outbound via NAT | ✔ Allowed |

The tests confirm that the database layer is fully protected and reachable only through the application tier.

---

## 📁 Working Directories

- Application path: `/opt/app`  
- EC2 storage: default **EBS volumes**  
- Deployment tier segregation using Route Table associations.

---

## 🚀 Outcome

- Built a secure and isolated AWS network  
- Reduced public exposure of database  
- Implemented enterprise-style subnet and firewall design  
- Enabled reliable hosting for future CI/CD and IaC automation.

---

## 🔮 Future Enhancements

- Terraform IaC scripts for VPC automation  
- Jenkins pipeline to deploy EC2 inside this VPC  
- MongoDB replication in private subnet  
- Monitoring using ELK stack.

---

## 🤝 Author
**Vignesh**
