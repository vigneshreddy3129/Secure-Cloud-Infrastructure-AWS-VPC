# Network ACL

## Public NACL
- Inbound: 22, 80
- Outbound: ALL

## Private NACL
- Inbound: 27017 internal only
- Block 0.0.0.0/0 inbound

## Difference
- SG = stateful
- NACL = stateless
