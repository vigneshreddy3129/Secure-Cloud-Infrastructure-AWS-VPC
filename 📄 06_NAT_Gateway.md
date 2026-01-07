# NAT Gateway

1. Create NAT Gateway in Public-A
2. Allocate Elastic IP
3. Update private-rt

- Destination: 0.0.0.0/0
- Target: NAT Gateway

## Purpose
Private instances access internet only outbound.
