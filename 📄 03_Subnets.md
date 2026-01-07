# Subnet Design

## Create Subnets

### Public-A
- CIDR: 192.168.1.0/24
- AZ: ap-south-1a
- Auto assign public IP: ENABLED

### App-A
- CIDR: 192.168.2.0/24
- AZ: ap-south-1a
- Auto assign: DISABLED

### DB-B
- CIDR: 192.168.3.0/24
- AZ: ap-south-1b
- Auto assign: DISABLED

## Purpose
Subnets divide VPC network into tiers.
