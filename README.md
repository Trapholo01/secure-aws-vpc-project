# Secure AWS VPC Infrastructure Deployment

## Project Overview

This project demonstrates the design and implementation of a **secure, tiered AWS VPC architecture** using the AWS Management Console. The infrastructure ensures that resources in a **private subnet** remain isolated while still allowing controlled outbound Internet access via a NAT Gateway.

This project was completed as a **beginner-friendly learning exercise**, focusing on correct networking logic, security principles, and professional cloud documentation.

---

## Objectives

* Create a custom VPC with a defined CIDR range
* Design public and private subnets within the same Availability Zone
* Enable secure internet access for private resources using a NAT Gateway
* Apply routing rules and network-level security
* Validate connectivity and security behavior

---

## Architecture Overview

### VPC Design

* **VPC CIDR:** `10.0.0.0/16`
* **Availability Zone:** Single AZ (e.g. us-east-1a)

### Subnets

| Subnet Type    | Name           | CIDR Block   |
| -------------- | -------------- | ------------ |
| Public Subnet  | Public-Subnet  | 10.0.25.0/24 |
| Private Subnet | Private-Subnet | 10.0.50.0/24 |

### Gateways

* **Internet Gateway:** Enables public internet access
* **NAT Gateway:** Enables outbound internet access for private subnet resources

---

## Architecture

![Architecture Diagram](architecture-diagram/SecureAWSVPCArchitecture.drawio.png)

The architecture follows a standard **two-tier VPC model**:

* The **Public Subnet** contains:
  * Internet Gateway (attached to the VPC)
  * NAT Gateway with an Elastic IP

* The **Private Subnet**:
  * Has no direct internet route
  * Routes outbound traffic through the NAT Gateway

---

## Routing Configuration

### Public Route Table (`Public-RT`)

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

Associated with: **Public-Subnet**

### Private Route Table (`Private-RT`)

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

Associated with: **Private-Subnet**

---

## Network Security

### Network Access Control List (NACL)

* Applied to both public and private subnets
* Default allow rules used for this project
* Adds an additional layer of network-level security

---

## Connectivity Testing

To verify secure connectivity:

1. An EC2 instance is launched in the **Private Subnet** without a public IP address
2. The instance successfully accesses the internet (e.g. OS updates or ping tests)
3. Direct inbound access from the internet is **not possible**, confirming security

This proves that:

* Outbound traffic flows through the NAT Gateway
* The private subnet remains protected from direct external access

---

## Repository Structure

```
secure-aws-vpc-project/
│
├── screenshots/
│   ├── vpc-cidr.png
│   ├── public-route-table.png
│   ├── private-route-table.png
│   ├── nat-gateway.png
│   ├── internet-gateway.png
│
├── architecture-diagram/
│   └── architecture-diagram.png
└── README.md
```

---

## Evaluation Checklist

*  Correct CIDR allocation
*  NAT Gateway placed in Public Subnet
*  Secure routing for Private Subnet
*  Clear naming conventions
*  Professional documentation

---

## Conclusion

This project demonstrates a foundational understanding of AWS VPC networking and security principles. It showcases how to securely isolate private resources while still allowing controlled internet access for updates and outbound communication.
