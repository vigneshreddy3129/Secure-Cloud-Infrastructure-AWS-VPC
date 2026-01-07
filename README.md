# Secure Cloud Infrastructure Using AWS VPC

## 📌 Overview
This project shows step-by-step creation of AWS networking infrastructure with CIDR **192.168.0.0/16**.  
It follows 3-tier model:

- Public subnet → Bastion / Web
- Private App subnet → Application
- Private DB subnet → MongoDB (port 27017)

Internet access to private resources allowed only outbound via NAT Gateway.

---

## 🎯 Goals
- Create AWS VPC
- Design subnets in multiple AZs
- Configure IGW
- Configure NAT Gateway
- Setup Route Tables
- Apply Security Groups
- Apply Network ACLs
- Launch EC2
- Test secure communication

---

## 🧩 Services Used
- Amazon VPC
- Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- NACL
- EC2 + EBS
- Elastic IP

---

## 🏗 CIDR Plan

| Component | CIDR |
|---|---|
| VPC | 192.168.0.0/16 |
| Public-A | 192.168.1.0/24 |
| App-A | 192.168.2.0/24 |
| DB-B | 192.168.3.0/24 |

---

## 🔐 Security
- SSH 22 allowed only to bastion
- App reachable only from bastion
- MongoDB 27017 allowed only from app layer
- Direct internet to DB blocked.

---

## 🧪 Testing
All validations documented in 10_Testing.md with screenshots.

---

## 👤 Author
Vignesh – AWS & DevOps Fresher Project
