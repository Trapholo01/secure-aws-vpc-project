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
* **Availability Zone:** Single AZ (us-east-1a)
![VPC CIDR Proof](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/vpc-cidr.png)


### Subnets

| Subnet Type    | Name           | CIDR Block   |
| -------------- | -------------- | ------------ |
| Public Subnet  | Public-Subnet  | 10.0.25.0/24 |
| Private Subnet | Private-Subnet | 10.0.50.0/24 |

### Gateways

* **Internet Gateway:** Enables public internet access
![Internet Gateway Status](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/internet-gateway.png)
* **NAT Gateway:** Enables outbound internet access for private subnet resources
![NAT Gateway Status](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/nat-gateway.png)
  
---

## Architecture

![Architecture Diagram](https://github.com/Trapholo01/secure-aws-vpc-project/blob/82cc55c2edba0d500d75c2c968bed6311e5fd2ed/architecture-diagram/Secure%20AWS%20VPC%20Architecture.drawio.png)

The architecture follows a standard **three-tier VPC model**:

* The **Public Subnet** contains:
  * Internet Gateway (attached to the VPC)
  * NAT Gateway with an Elastic IP
  ![Public Subnet Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/public-subnet.png)

* The **Private Subnet**:
  * Has no direct internet route
  * Routes outbound traffic through the NAT Gateway
  ![Private Subnet Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/private-subnet.png)

---

## Routing Configuration

### Public Route Table (`Public-RT`)

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

Associated with: **Public-Subnet**
![Public Route Table Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/public-route-table.png)

### Private Route Table (`Private-RT`)

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

Associated with: **Private-Subnet**
![Private Route Table Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/private-route-table.png)

---

## Network Security

### Network Access Control List (NACL)

* Applied to both public and private subnets
* Default allow rules used for this project
* Adds an additional layer of network-level security

![Connectivity Test Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/9afe7e035df9c8b333b3a94708a84f0aef9c22f4/screenshots/secure%20nacl.png)

---

## Connectivity Testing

To verify secure connectivity:

1. An EC2 instance is launched in the **Private Subnet** without a public IP address
2. The instance successfully accesses the internet (e.g. OS updates or ping tests)
3. Direct inbound access from the internet is **not possible**, confirming security

This proves that:

* Outbound traffic flows through the NAT Gateway
* The private subnet remains protected from direct external access

![Connectivity Test Screenshot](https://github.com/Trapholo01/secure-aws-vpc-project/blob/2e1c7ada63d3c0c9276e25a50bb3d3f881c79f5e/screenshots/connectivity-test.png)

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
│   ├── public-subnet.png
│   ├── private-subnet.png
│   ├── connectivity-test.png
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
