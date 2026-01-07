# Architecture Overview

## Goal
Design secure network for hosting application and MongoDB database.

## CIDR
VPC range: 192.168.0.0/16

## Layers

### 1. Public Layer
- Bastion host
- Internet Gateway attached

### 2. Application Layer
- Private EC2
- Access only via bastion

### 3. Database Layer
- MongoDB EC2
- Access on 27017 from app only

## Traffic Flow
User → IGW → Public subnet → Bastion →  
App subnet → MongoDB subnet.
