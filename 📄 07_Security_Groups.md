# Security Groups

## Bastion-SG
- Inbound: 22 from My IP

## App-SG
- Inbound: 22 from Bastion-SG
- Outbound: ALL

## MongoDB-SG
- Inbound: 27017 from App-SG ONLY
- Outbound: deny public

## Purpose
Instance level stateful firewall.
