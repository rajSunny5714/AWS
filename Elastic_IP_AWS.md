# 🌐 Elastic IP (EIP) in AWS

![AWS](https://img.shields.io/badge/AWS-Elastic%20IP-orange?logo=amazon-aws&logoColor=white)
![Networking](https://img.shields.io/badge/Category-Networking-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What Is an Elastic IP?

An **Elastic IP (EIP)** is a static public IPv4 address designed for use with AWS resources.

You can associate it with an EC2 instance or another supported resource. When your architecture changes, you can often remap the address to another resource.

**In simple words:**

> An Elastic IP is a public IPv4 address that you can keep and reassign instead of relying on a changing public IP address.

## 🎯 Why Do We Need Elastic IP?

Elastic IPs are useful when you need:

- 🌐 A consistent public IPv4 address
- 🔄 The ability to remap an address to another resource
- 🖥️ A stable endpoint for certain applications
- 🛠️ A known IP address for network allowlists

## 🏗️ How Elastic IP Works

```text
             Internet
                 |
                 v
           Elastic IP
                 |
                 v
            EC2 Instance
                 |
                 v
          Application Server
```

You allocate an Elastic IP to your AWS account and associate it with a supported resource.

## 🔄 Public IP vs Elastic IP

| Feature | Automatically Assigned Public IP | Elastic IP |
|---|---|---|
| Address stability | Can change after stop/start | Designed to remain allocated to your account |
| Reassignment | Not retained as a reusable allocation in the same way | Can be reassociated with another supported resource |
| Typical use | General internet access | A stable public IPv4 endpoint |
| Cost | Depends on AWS pricing rules | Charges may apply; check current pricing |

**Important:** AWS charges for public IPv4 addresses, including Elastic IPs, under its public IPv4 pricing policy. Check current pricing before allocating one.

## ⚙️ How to Allocate and Associate an Elastic IP

### Step 1: Open the EC2 Console

Open the AWS Management Console and navigate to EC2.

### Step 2: Find Elastic IP Addresses

In the EC2 navigation menu, select **Elastic IP addresses**.

### Step 3: Allocate an Elastic IP

Choose **Allocate Elastic IP address** and confirm the allocation.

### Step 4: Associate the Address

Select the allocated address and choose **Associate Elastic IP address**.

### Step 5: Select the Resource

Choose the appropriate EC2 instance or supported network interface and complete the association.

```text
Allocate Elastic IP
        |
        v
Select Elastic IP
        |
        v
Associate with Resource
        |
        v
Use Stable Public IPv4
```

## 🔁 Remapping an Elastic IP

Suppose your application server fails and you need to move its public address to a replacement instance.

```text
Before:

Elastic IP
    |
    v
EC2 Instance A


After:

Elastic IP
    |
    v
EC2 Instance B
```

You can reassociate the Elastic IP with the replacement resource, subject to AWS configuration and networking requirements.

**Note:** Remapping the address does not automatically migrate your application, files, or database. Those must be handled separately.

## ☕ Spring Boot Example

Suppose you deploy a Spring Boot application on EC2.

```text
Users
  |
  v
Elastic IP
  |
  v
EC2 Instance
  |
  v
Spring Boot API
```

An Elastic IP can provide a consistent public IPv4 address for the server.

However, for production applications, a DNS name with a load balancer is often a better design because it supports traffic distribution and improved availability.

## 🔐 Elastic IP Best Practices

- Release Elastic IPs that are no longer needed.
- Monitor public IPv4 address charges.
- Restrict inbound traffic with appropriate Security Group rules.
- Avoid exposing application and database ports unnecessarily.
- Use a load balancer for applications requiring high availability.
- Do not assume an Elastic IP provides automatic failover or data recovery.

## 📊 Elastic IP vs DNS

| Feature | Elastic IP | DNS Name |
|---|---|---|
| Purpose | Provides a static public IPv4 address | Maps a name to one or more network endpoints |
| Example | `203.0.113.10` | `api.example.com` |
| Can be used in a browser | Yes, if the service and network configuration allow it | Yes |
| Simplifies endpoint changes | Requires address reassociation when changing resources | DNS records can be updated to point to new endpoints |

## 🎤 Interview Questions

### 1. What is an Elastic IP?

An Elastic IP is a static public IPv4 address allocated to an AWS account that can be associated with supported AWS resources.

### 2. Why would you use an Elastic IP?

To maintain a consistent public IPv4 address or remap that address to another supported resource when needed.

### 3. What happens to an Elastic IP when an EC2 instance stops?

The Elastic IP remains allocated to your account and generally remains associated with the instance unless you disassociate or reassign it.

### 4. Does an Elastic IP automatically provide high availability?

No. It provides a stable address, but failover requires additional configuration and operational steps.

### 5. Is an Elastic IP free?

Not necessarily. AWS applies public IPv4 address charges, so check the current pricing policy.

### 6. What happens if you release an Elastic IP?

The address returns to AWS's address pool. You generally cannot guarantee that you will receive the same address again.

### 7. What is the difference between an Elastic IP and a private IP?

An Elastic IP is a public IPv4 address, while a private IP is used for communication within private networks and other connected networks.

## 📝 Quick Revision

```text
Elastic IP
    |
    ├── Static Public IPv4
    ├── Allocated to AWS Account
    ├── Can Be Reassociated
    ├── Useful for Stable Endpoints
    └── Public IPv4 Charges May Apply
```

**One-line interview answer:**

> An Elastic IP is a static public IPv4 address in AWS that can be associated with supported resources and reassigned when required.