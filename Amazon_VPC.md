# 🌐 Amazon VPC (Virtual Private Cloud)

![AWS](https://img.shields.io/badge/AWS-VPC-orange?logo=amazon-aws&logoColor=white)
![Networking](https://img.shields.io/badge/Category-Networking-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What Is Amazon VPC?

**Amazon Virtual Private Cloud (VPC)** is a logically isolated virtual network in AWS where you can launch resources such as EC2 instances, databases, and application servers.

You control important networking settings, including:

- IP address ranges
- Subnets
- Route tables
- Internet connectivity
- Network security

**In simple words:**

> VPC is your private network in AWS where you organize and manage your cloud resources.

## 🎯 Why Do We Need VPC?

VPC helps you:

- 🔐 Isolate cloud resources within a network.
- 🌐 Control internet connectivity.
- 🧩 Divide networks into subnets.
- 🛡️ Apply network security rules.
- 🔄 Connect multiple AWS resources.
- 🏗️ Design secure application architectures.

## 🏗️ VPC Architecture

A typical VPC can contain public and private subnets across multiple Availability Zones.

```text
                       Internet
                           |
                           v
                    Internet Gateway
                           |
                           v
                 ┌─────────────────────┐
                 │        VPC          │
                 │                     │
                 │  ┌───────────────┐  │
                 │  │ Public Subnet │  │
                 │  │               │  │
                 │  │ Load Balancer │  │
                 │  └───────┬───────┘  │
                 │          │          │
                 │          v          │
                 │  ┌───────────────┐  │
                 │  │ Private Subnet│  │
                 │  │               │  │
                 │  │ Spring Boot   │  │
                 │  │ EC2           │  │
                 │  └───────┬───────┘  │
                 │          │          │
                 │          v          │
                 │  ┌───────────────┐  │
                 │  │ Private Subnet│  │
                 │  │               │  │
                 │  │ Database      │  │
                 │  └───────────────┘  │
                 │                     │
                 └─────────────────────┘
```

## 🧩 Major VPC Components

### 1. VPC

A VPC is an isolated virtual network in an AWS Region.
When creating a VPC, you specify an IPv4 CIDR block.

Example:

```text
10.0.0.0/16
```

This defines the private IPv4 address range available to the VPC.

### 2. CIDR Block
**CIDR (Classless Inter-Domain Routing)** represents an IP address range.

Example:

```text
10.0.0.0/16
```

A `/16` IPv4 network contains 65,536 total addresses.

AWS reserves five IPv4 addresses in each subnet, so not all addresses are assignable to resources.

Other examples:

| CIDR | Total IPv4 Addresses |
|---|---:|
| `10.0.0.0/16` | 65,536 |
| `10.0.1.0/24` | 256 |
| `10.0.2.0/24` | 256 |
| `10.0.1.0/28` | 16 |

### 3. Subnet

A **subnet** is a smaller IP address range inside a VPC.
Subnets help organize resources and control network routing.

There are two common subnet designs:

**Public Subnet**

A subnet whose route table has a route to an Internet Gateway.

Typical resources:
- Internet-facing load balancers
- Bastion hosts, when required
- Public-facing application resources

**Private Subnet**

A subnet that does not have a direct route to an Internet Gateway.

Typical resources:
- Application servers
- Databases
- Internal services

Example:

```text
VPC: 10.0.0.0/16
       |
       ├── Public Subnet:  10.0.1.0/24
       |
       ├── Private Subnet: 10.0.2.0/24
       |
       └── Private Subnet: 10.0.3.0/24
```

**Important:** A subnet is not public merely because it has a public IP address. Its route table and internet gateway connectivity determine whether it is public.

### 4. Availability Zone

An **Availability Zone (AZ)** is an isolated location within an AWS Region.

You can create subnets in different AZs to improve application availability.

Example:

```text
              AWS Region
                   |
          ┌────────┴────────┐
          |                 |
          v                 v
       AZ - A             AZ - B
          |                 |
     Public Subnet     Public Subnet
          |                 |
     Private Subnet    Private Subnet
```

### 5. Route Table

A **Route Table** contains rules that determine where network traffic is directed.

Example:

| Destination | Target |
|---|---|
| `10.0.0.0/16` | Local |
| `0.0.0.0/0` | Internet Gateway |

Explanation:

- `10.0.0.0/16 → local`: Allows routing within the VPC.
- `0.0.0.0/0 → Internet Gateway`: Routes other IPv4 destinations toward the internet gateway.

Each subnet must be associated with a route table. If no explicit association exists, the VPC's main route table is used.

### 6. Internet Gateway (IGW)

An **Internet Gateway** enables communication between a VPC and the internet.

It must be attached to the VPC.

For an EC2 instance to communicate directly with the public internet using an Internet Gateway, it also needs an appropriate public IPv4 address, route, and security configuration.

```text
EC2 Instance
     |
     v
Public Subnet
     |
     v
Route Table
     |
     v
Internet Gateway
     |
     v
Internet
```

### 7. NAT Gateway

A **NAT Gateway** allows resources in a private subnet to initiate connections to external destinations, such as the internet, without allowing unsolicited internet connections to reach those resources through the NAT Gateway.

Example:

```text
Private EC2
     |
     v
Private Route Table
     |
     v
NAT Gateway
     |
     v
Internet Gateway
     |
     v
Internet
```

A NAT Gateway is commonly placed in a public subnet and uses an Elastic IP for internet access.

**Remember:**
- Internet Gateway: Enables internet connectivity for appropriately configured resources.
- NAT Gateway: Enables outbound internet access for private subnet resources.

## 🔐 Network Security Components

### Security Group

A Security Group is a stateful virtual firewall associated with network interfaces.

It controls allowed inbound and outbound traffic.

### Network ACL (NACL)

A Network ACL is a stateless firewall applied at the subnet level.

It supports both allow and deny rules.

| Feature | Security Group | Network ACL |
|---|---|---|
| Applied to | Network interface | Subnet |
| Stateful | Yes | No |
| Rules | Allow only | Allow and deny |
| Evaluation | All applicable rules | Rule number order |

## ☕ Spring Boot Application Example

Suppose you deploy a production-style Spring Boot application.

```text
                     Internet
                         |
                         v
                 Internet Gateway
                         |
                         v
                 Public Subnet
                         |
                         v
                 Application Load
                     Balancer
                         |
                         v
                 Private Subnet
                         |
                         v
                  Spring Boot EC2
                         |
                         v
                 Private Database
                         |
                         v
                    Amazon RDS
```

Security design:

1. Users access the application through HTTPS.
2. The load balancer accepts public traffic.
3. The Spring Boot EC2 instance accepts traffic only from the load balancer.
4. The database accepts connections only from the application tier.
5. Private resources use a NAT Gateway if they need outbound internet access.

## 📊 Important AWS Networking Comparisons

| Component | Main Purpose |
|---|---|
| VPC | Isolated virtual network |
| Subnet | Divides a VPC IP range |
| CIDR | Defines an IP address range |
| Route Table | Directs network traffic |
| Internet Gateway | Connects a VPC to the internet |
| NAT Gateway | Enables outbound internet access from private subnets |
| Security Group | Stateful resource-level firewall |
| Network ACL | Stateless subnet-level firewall |
| Availability Zone | Isolated location within a Region |

## 🎤 Interview Questions

### 1. What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage cloud resources.

### 2. What is a subnet?

A subnet is a range of IP addresses within a VPC used to organize resources.

### 3. What is the difference between public and private subnets?

A public subnet has a route to an Internet Gateway, while a private subnet does not have a direct route to an Internet Gateway.

### 4. What is a CIDR block?

CIDR specifies an IP address range, such as `10.0.0.0/16`.

### 5. What is an Internet Gateway?

An Internet Gateway enables internet communication for appropriately configured resources in a VPC.

### 6. What is a NAT Gateway?

A NAT Gateway allows resources in private subnets to initiate outbound connections to external networks without accepting unsolicited inbound connections through the NAT Gateway.

### 7. What is a Route Table?

A Route Table contains routing rules that determine where network traffic is sent.

### 8. Can a VPC have multiple subnets?

Yes. A VPC can contain multiple subnets across different Availability Zones.

### 9. Can a private EC2 instance access the internet?

Yes. It can use a NAT Gateway with appropriate routing, or another supported connectivity design.

### 10. What is the difference between a Security Group and a Network ACL?

A Security Group is stateful and applies to network interfaces, while a Network ACL is stateless and applies at the subnet level.

## 📝 Quick Revision

```text
                 AWS VPC
                    |
       ┌────────────┼────────────┐
       |            |            |
       v            v            v
    Subnets     Route Tables   Security
                                Groups
       |
       ├── Public Subnet
       |
       └── Private Subnet
              |
              └── NAT Gateway

Internet Gateway
       |
       └── Internet Connectivity
```

### Remember These Points

```text
VPC       → Virtual Network
CIDR      → IP Address Range
Subnet    → Network Division
IGW       → Internet Connectivity
NAT       → Private Subnet Outbound Access
Route     → Traffic Direction
SG        → Stateful Firewall
NACL      → Stateless Firewall
AZ        → Isolated Location
```

## 🔑 One-Line Interview Answer

> Amazon VPC is a logically isolated virtual network in AWS that allows you to organize resources using subnets, configure routing, and control network connectivity and security.