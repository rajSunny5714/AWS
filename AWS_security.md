# 🔐 AWS Security Groups

![AWS](https://img.shields.io/badge/AWS-Security%20Groups-orange?logo=amazon-aws&logoColor=white)
![Networking](https://img.shields.io/badge/Category-Networking-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What Is a Security Group?

An **AWS Security Group** acts as a virtual firewall that controls inbound and outbound traffic for resources such as EC2 instances.

It defines which network traffic is allowed to reach or leave a resource.

**In simple words:**

> A Security Group controls which connections are allowed to access your EC2 instance.

## 🎯 Why Do We Need Security Groups?

Security Groups help you:

- 🔐 Restrict unauthorized access
- 🌐 Allow only required network traffic
- 🛡️ Protect application servers
- 🔌 Control access to application ports
- 🧱 Apply network-level security rules

## 🏗️ How Security Groups Work

```text
             Internet
                 |
                 v
          Security Group
                 |
         Allowed Traffic?
                 |
                 v
             EC2 Instance
                 |
           Spring Boot API
```

Traffic allowed by the Security Group can reach the instance, subject to other network and operating-system controls.

## 🚪 Inbound Rules

**Inbound rules** control traffic entering a resource.

Example rules for a web application:

| Type | Protocol | Port | Purpose |
|---|---|---:|---|
| SSH | TCP | 22 | Remote Linux administration |
| HTTP | TCP | 80 | Web traffic |
| HTTPS | TCP | 443 | Secure web traffic |
| Custom TCP | TCP | 8080 | Spring Boot application |

Only add the ports your application actually needs.

### Example

To allow HTTPS traffic:

```text
Type: HTTPS
Protocol: TCP
Port: 443
Source: Approved IP range or security group
```

**Security best practice:** Avoid opening SSH (port 22) to the entire internet unless there is a specific, justified need.

## 📤 Outbound Rules

**Outbound rules** control traffic leaving a resource.

For example, an EC2 application may need outbound access to:

- A database
- An external API
- Package repositories
- Other application services

New Security Groups commonly allow all outbound traffic by default. Review and restrict this when your architecture requires tighter control.

## 🧠 Stateful Firewall

Security Groups are **stateful**.

This means that when an inbound connection is allowed, its response traffic is automatically permitted, even if a separate outbound rule does not explicitly allow that response.

```text
Client
  |
  | Allowed request
  v
EC2 Application
  |
  | Response to that request
  v
Client
```

You do not need to create a separate inbound rule just for the response to an allowed inbound connection.

## 🚫 Security Groups vs Network ACLs

| Feature | Security Group | Network ACL |
|---|---|---|
| Applied to | Network interfaces/resources | Subnets |
| Stateful | Yes | No |
| Rules | Allow rules | Allow and deny rules |
| Rule evaluation | All applicable rules are evaluated | Rules evaluated by rule number |
| Response traffic | Automatically tracked | Must be allowed by applicable rules |

**Remember:** Security Groups are stateful; Network ACLs are stateless.

## ☕ Spring Boot Example

Suppose you deploy a Spring Boot API on EC2.

```text
Users
  |
  | HTTPS :443
  v
Load Balancer
  |
  | Application traffic
  v
EC2 Security Group
  |
  | Allowed application port
  v
Spring Boot API
  |
  v
Database
```

A secure design could use these rules:

1. Allow public HTTPS traffic to the load balancer.
2. Allow application traffic to EC2 only from the load balancer's Security Group.
3. Allow database traffic only from the application server's Security Group.

This avoids exposing the application server and database directly to the public internet.

## 🔗 Security Group References

A Security Group can reference another Security Group as a rule's source or destination where supported.

Example:

```text
Load Balancer SG
       |
       | Allowed application traffic
       v
Application EC2 SG
       |
       | Allowed database traffic
       v
Database SG
```

This is often easier to maintain than allowing fixed IP addresses for every component.

## 🛡️ Best Practices

- Allow only the ports required by your workload.
- Avoid unrestricted SSH access from `0.0.0.0/0`.
- Do not expose databases publicly unless absolutely necessary.
- Use separate Security Groups for different application tiers.
- Prefer Security Group references for communication between tiers.
- Review rules periodically and remove unused permissions.
- Remember that Security Groups do not replace IAM permissions or application authentication.

## 🎤 Interview Questions

### 1. What is an AWS Security Group?

An AWS Security Group is a stateful virtual firewall that controls allowed inbound and outbound network traffic for associated resources.

### 2. Are Security Groups stateful or stateless?

Security Groups are stateful, so response traffic for an allowed connection is automatically permitted.

### 3. What is the difference between inbound and outbound rules?

Inbound rules control incoming traffic, while outbound rules control outgoing traffic.

### 4. What is the difference between a Security Group and a Network ACL?

A Security Group applies to network interfaces and is stateful. A Network ACL applies at the subnet level and is stateless.

### 5. Should port 8080 be open to everyone for a Spring Boot application?

Usually not. Prefer allowing application traffic only from the intended load balancer or trusted source.

### 6. Can an EC2 instance have multiple Security Groups?

Yes. Multiple Security Groups can be associated with an instance's network interface, and their allow rules are combined.

### 7. Does a Security Group replace IAM?

No. Security Groups control network traffic, while IAM controls access to AWS resources and actions.

## 📝 Quick Revision

```text
Security Group
      |
      ├── Inbound Rules
      ├── Outbound Rules
      ├── Stateful
      └── Allow Rules
```

**One-line interview answer:**

> An AWS Security Group is a stateful virtual firewall that controls allowed inbound and outbound traffic for resources such as EC2 instances.