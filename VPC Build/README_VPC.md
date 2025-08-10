# AWS Virtual Private Cloud (VPC) Build

This repository documents my hands-on project creating a custom Amazon VPC from scratch, 
including defining CIDR ranges, creating subnets, attaching an Internet Gateway, 
and ensuring public internet access for selected resources.

## What’s inside

- **Step-by-step AWS VPC build guide** in [`docs/VPC_GUIDE.md`](docs/VPC_GUIDE.md)
- Explanation of **VPC basics** and components (CIDR, subnets, gateways)
- Notes on **testing internet access** for public subnets
- Practical example using **Canada Central** AWS region

## Prerequisites

- An AWS account with permissions to create networking components
- Basic understanding of:
  - IP addressing & CIDR notation (e.g., `10.0.0.0/16`)
  - Public vs private subnets
  - Internet Gateways

## Quick start

1. **Log in to AWS Console → VPC service**.
2. Create a new VPC:
   - IPv4 CIDR: e.g., `10.0.0.0/16`
   - Tenancy: Default
3. **Create a subnet**:
   - Name: `Public 1`
   - CIDR: e.g., `10.0.1.0/24`
   - AZ: Choose one in your preferred region
   - Enable auto-assign public IPv4
4. **Create an Internet Gateway (IGW)**:
   - Name: e.g., `MyVPC-IGW`
   - Attach it to your VPC
5. **Update route table** for the public subnet:
   - Destination: `0.0.0.0/0`
   - Target: Your IGW
6. **Test connectivity** by launching an EC2 instance in the public subnet.

## Repository structure (example)

```
.
├── docs/
│   └── VPC_GUIDE.md
├── README.md
└── diagrams/
    └── vpc_architecture.png
```

## Notes & tips

- Creating a public subnet requires both a route to an IGW **and** auto-assigned public IPs.
- Always use the least privilege security group settings for your EC2 instances.
- CIDR `/16` gives 65,536 IP addresses; adjust to your needs.

## License

MIT (or choose another license for your repo).