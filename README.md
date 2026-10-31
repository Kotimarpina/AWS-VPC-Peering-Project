
# AWS VPC Peering – Private Connectivity Between Two VPCs

## Project Overview

This project demonstrates how to establish private network connectivity between two Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**.

The infrastructure is configured in the AWS Mumbai Region (`ap-south-1`) within the same AWS account. It uses EC2 instances, public and private subnets, route tables, security groups, an Internet Gateway, and a Bastion Host to demonstrate secure communication between resources across two VPCs.

## Project Objectives

- Create and configure two independent AWS VPCs.
- Configure public and private subnets.
- Deploy EC2 instances in the respective subnets.
- Establish a VPC Peering connection.
- Configure route tables to enable communication between VPCs.
- Implement security groups to control network traffic.
- Use a Bastion Host as an administrative access point.
- Verify private connectivity using ICMP and SSH tests.

## AWS Architecture

### VPC A – `10.10.0.0/16`

| Component | Configuration |
|---|---|
| Public Subnet | `10.10.1.0/24` |
| Private Subnet | `10.10.2.0/24` |
| Bastion Host | `10.10.1.10` |
| App-A | `10.10.2.10` |
| Internet Gateway | `ewb-igw-a` |

### VPC B – `10.20.0.0/16`

| Component | Configuration |
|---|---|
| Private Subnet | `10.20.1.0/24` |
| App-B | `10.20.1.10` |

## AWS Services Used

- Amazon VPC
- Amazon EC2
- VPC Peering
- Internet Gateway (IGW)
- Route Tables
- Security Groups
- EC2 Instance Connect

## Network Configuration

### VPC Peering

A peering connection named `ewb-a-b-peer` was created between VPC A and VPC B.

The connection uses the following peering ID:

`pcx-0681831548570ed5c`

The peering connection was accepted and reached the **Active** state.

### Route Table Configuration

The following routes were configured to enable communication between the two VPCs:

| Route Table | Destination CIDR | Target |
|---|---|---|
| `ewb-rt-a-private` | `10.20.0.0/16` | VPC Peering |
| `ewb-rt-b-private` | `10.10.0.0/16` | VPC Peering |
| `ewb-rt-a-public` | `10.20.0.0/16` | VPC Peering |

The public route table also maintains its default Internet Gateway route.

### Security Configuration

Security groups were created separately for the Bastion Host, App-A, and App-B.

- Bastion Host: SSH access restricted to the administrator's public IP and EC2 Instance Connect access.
- App-A: SSH access from the Bastion Host and ICMP Echo Request from App-B.
- App-B: SSH access from the Bastion Host and ICMP Echo Request from App-A.

## Project Implementation

1. Created VPC A and VPC B with non-overlapping CIDR blocks.
2. Created the required public and private subnets.
3. Configured the Internet Gateway for VPC A.
4. Created and associated the route tables.
5. Configured security groups for the EC2 instances.
6. Created an EC2 key pair.
7. Launched the Bastion Host, App-A, and App-B.
8. Created and accepted the VPC Peering connection.
9. Added the required peering routes to all three route tables.

## Connectivity Verification

The following tests are planned as part of the validation phase:

- App-A to App-B ICMP connectivity.
- App-B to App-A ICMP connectivity.
- SSH access to private instances through the Bastion Host.
- Controlled security group rule removal and restoration to demonstrate traffic filtering.

**Note:** Update this section with actual test results and screenshots after completing the validation.

## Key Learnings

- Understanding AWS VPC networking and CIDR addressing.
- Configuring public and private subnets.
- Understanding VPC Peering and route propagation requirements.
- Implementing security group-based traffic filtering.
- Understanding Bastion Host architecture.
- Learning the importance of network routing and access control in cloud environments.

## Project Information

- **Project:** AWS VPC Peering – Connect Two VPCs
- **Training:** EWB Courses
- **Cloud Provider:** Amazon Web Services (AWS)
- **Region:** Asia Pacific (Mumbai)
- **Status:** Infrastructure configured; connectivity validation pending.

## Author

**Your Name**

## Disclaimer

This project was developed for educational and internship purposes. AWS resources should be reviewed and cleaned up after testing to avoid unnecessary charges.
