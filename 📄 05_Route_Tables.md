# Route Tables

## Public Route Table

- Name: public-rt
- Route:
  - Destination: 0.0.0.0/0
  - Target: Internet Gateway

- Associate → Public-A subnet

---

## Private Route Table

- Name: private-rt
- Associate → App-A + DB-B

## Purpose
Route table controls traffic direction.
