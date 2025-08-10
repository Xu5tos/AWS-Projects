# End-to-End Guide — AWS Virtual Private Cloud (VPC) Build

This guide walks through creating a custom VPC in AWS, defining network ranges, 
setting up subnets, and attaching internet connectivity.

---

## 1) Understanding Amazon VPC

- **VPC** = Isolated, customizable network inside AWS.
- Lets you control:
  - IP address range (CIDR block)
  - Subnets
  - Routing tables
  - Gateways
  - Security

Why: VPCs give you full control over how AWS resources connect to each other and the internet.

---

## 2) Create the VPC

1. Go to **AWS Console → VPC → Create VPC**.
2. Name: `MyVPC`
3. IPv4 CIDR: `10.0.0.0/16` (adjust based on needs)
4. Tenancy: Default
5. Click **Create VPC**

**CIDR Notation refresher**:
- `10.0.0.0/16` → 65,536 IP addresses
- `/24` → 256 IP addresses

---

## 3) Create a Public Subnet

1. In **Subnets**, click **Create Subnet**.
2. Select `MyVPC`
3. Name: `Public 1`
4. AZ: Select one from your chosen region (e.g., `ca-central-1a`)
5. IPv4 CIDR: `10.0.1.0/24`
6. Enable **Auto-assign public IPv4 address**.

Why: Auto-assigned public IPs let instances in this subnet talk to the internet.

---

## 4) Create an Internet Gateway (IGW)

1. Go to **Internet Gateways → Create internet gateway**.
2. Name: `MyVPC-IGW`
3. Click **Attach to VPC** and choose `MyVPC`.

Why: An IGW is the bridge between your VPC and the internet.

---

## 5) Update Route Table

1. Go to **Route Tables**.
2. Find the route table for your public subnet (or create a new one).
3. Add route:
   - Destination: `0.0.0.0/0`
   - Target: `MyVPC-IGW`

Why: This tells AWS that internet-bound traffic should go via the IGW.

---

## 6) Test Connectivity

1. Launch an EC2 instance in `Public 1` subnet.
2. Assign a security group allowing SSH from your IP.
3. SSH into the instance using its public IP.
4. Run:

```bash
ping google.com
```

If replies come back, your VPC + public subnet + IGW are correctly configured.

---

## 7) Security Best Practices

- Restrict inbound traffic with security groups & NACLs.
- Avoid exposing sensitive resources to the internet.
- Use private subnets for databases or internal apps.

---

## Appendix — Quick Commands

```bash
# CIDR calculator example
# AWS Console → VPC wizard does this for you

# Test EC2 connectivity
ssh -i mykey.pem ec2-user@<public-ip>
```