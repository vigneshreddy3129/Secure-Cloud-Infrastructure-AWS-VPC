# Secure Cloud Infrastructure Deployment Using AWS VPC

## 📌 Project Overview
This project demonstrates the design and deployment of a secure 3-tier cloud infrastructure using **AWS Virtual Private Cloud (VPC)**.  
The environment hosts public access layer, application servers, and MongoDB database in isolated private subnets with controlled internet access via NAT Gateway.

## 🎯 Objectives
- Create a custom AWS VPC with private IP range
- Deploy infrastructure across multiple Availability Zones
- Configure Internet Gateway for public traffic
- Enable outbound internet for private servers using NAT Gateway
- Implement security using Security Groups and Network ACLs
- Launch EC2 instances for App and MongoDB with bastion host
- Validate secure communication on port **27017** internally

---

## 🏗 Architecture Design

### CIDR Planning
- **VPC CIDR:** `192.168.0.0/16`
- Public Subnet: `192.168.1.0/24` – AZ ap-south-1a  
- Private App Subnet: `192.168.2.0/24` – AZ ap-south-1a  
- Private DB Subnet: `192.168.3.0/24` – AZ ap-south-1b

### Components
- VPC (Mumbai region – ap-south-1)
- Subnets (Public + Private)
- Internet Gateway (IGW)
- NAT Gateway with Elastic IP
- Public and Private Route Tables
- Security Groups
- Network ACLs
- EC2 Instances with EBS
- MongoDB Database

### Traffic Flow
User → Internet Gateway → Public Subnet (Bastion/Web) →  
Private Subnet (App) → Private Subnet (MongoDB on 27017)

---

## 🛠 Prerequisites

### Tools Required
- AWS Account
- GitHub Account
- SSH Client (Putty/OpenSSH)
- AWS Console access
- Basic Networking Knowledge

### AWS Services Used
- Amazon VPC  
- EC2 + EBS  
- IGW  
- NAT Gateway  
- Security Groups  
- NACL  
- Route Tables

---

## 🚀 Implementation Steps

### 1. Create VPC
- Login AWS Console  
- Select **ap-south-1 (Mumbai)**  
- Create VPC with:
  - Name: `secure-prod-vpc`
  - CIDR: `192.168.0.0/16`
  - Tenancy: default

---

### 2. Create Subnets
- Public subnet with auto-assign public IP enabled  
- App and DB subnets with auto-assign disabled  
- Spread across 2 Availability Zones

---

### 3. Internet Gateway
- Create IGW named `secure-igw`
- Attach to `secure-prod-vpc`

---

### 4. Route Tables

#### Public Route Table
- Name: `public-rt`
- Add route:  
  - Destination `0.0.0.0/0`
  - Target → Internet Gateway
- Associate → Public Subnet

#### Private Route Table
- Name: `private-rt`
- Add route later → NAT Gateway
- Associate → App + DB subnets

---

### 5. NAT Gateway
- Create NAT Gateway in Public Subnet  
- Allocate Elastic IP  
- Update Private RT:
  - `0.0.0.0/0 → NAT Gateway`

---

### 6. Security Groups

#### Bastion SG
- Allow SSH 22 from My IP

#### App SG
- Allow SSH from Bastion SG  
- Allow outbound all

#### MongoDB SG
- Allow **27017 only from App SG / App Subnet**  
- Deny all public access

---

### 7. Network ACL

#### Public NACL
- Inbound: 22, 80  
- Outbound: all

#### Private NACL
- Inbound: 27017 internal only  
- Block `0.0.0.0/0` inbound

---

### 8. Launch EC2

- Bastion host → public subnet  
- Application server → private app subnet  
- MongoDB server → private DB subnet  
- Working directories:
  - `/opt/app`
  - MongoDB data `/var/lib/mongo`

---

## ✅ Testing & Validation

### Test Cases
1. SSH to Bastion → ✔ Success  
2. Bastion → App SSH → ✔  
3. App → MongoDB 27017 → ✔  
4. Direct Internet → MongoDB → ❌ Blocked  
5. Private instance internet via NAT → ✔

---

## 📈 Outcomes
- Successfully designed AWS VPC using **192.168.0.0/16** private range  
- MongoDB exposed only internally on port 27017  
- Bastion host used for secure administration  
- Controlled routing between public and private tiers  
- Console-documented infrastructure suitable for interviews

---

## 🔮 Future Enhancements
- Terraform IaC implementation  
- Jenkins pipeline to launch EC2 inside this VPC  
- MongoDB replication in private subnet  
- Monitoring using CloudWatch / ELK

---

## 📁 Repository Contents
- Step by step guides  
- Architecture diagram  
- Screenshots from AWS console  
- Security configuration documents

---

### Author
**Vignesh**  
