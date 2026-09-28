# 🖥️ Amazon EC2 (Elastic Compute Cloud)

![AWS](https://img.shields.io/badge/AWS-EC2-orange?logo=amazon-aws&logoColor=white)
![Compute](https://img.shields.io/badge/Service-Compute-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What is Amazon EC2?

**Amazon Elastic Compute Cloud (EC2)** is a cloud computing service that provides **virtual servers (instances)** on demand.

Instead of buying and maintaining physical servers, you can launch an EC2 instance within minutes and pay only for the resources you use.

**In simple words:**

> EC2 is a virtual computer running inside AWS that hosts your applications, APIs, websites, databases, or services.

---

## 🎯 Why Do We Use EC2?

EC2 is commonly used to run:

- 🌐 Spring Boot applications
- ⚛️ React / Angular frontend
- 🔌 REST APIs
- 🗄️ Backend servers
- 🤖 AI & ML workloads
- 🐳 Docker containers
- ☸️ Kubernetes worker nodes

---

## 🏗️ How EC2 Works

```text
User
   │
   ▼
Internet
   │
   ▼
Elastic IP / Load Balancer
   │
   ▼
EC2 Instance
   │
   ▼
Spring Boot / Node.js / Python App
   │
   ▼
RDS / S3 / Redis
```

---

## ⚙️ Key EC2 Components

| Component | Description |
|-----------|-------------|
| **Instance** | Virtual machine running in AWS. |
| **AMI** | Pre-configured operating system template. |
| **Instance Type** | CPU, RAM, storage configuration. |
| **Security Group** | Firewall controlling inbound/outbound traffic. |
| **Key Pair** | SSH authentication for Linux instances. |
| **EBS** | Persistent storage attached to EC2. |
| **Elastic IP** | Static public IP address. |

---

## 💻 EC2 Instance Lifecycle

```text
Launch
   │
Running
   │
Stop
   │
Start
   │
Reboot
   │
Terminate
```

**Important:** After **Terminate**, the instance cannot be recovered.

---

## 📦 Common Instance Types

| Instance Family | Used For |
|-----------------|----------|
| **t2 / t3** | Learning, small applications. |
| **m5** | General-purpose applications. |
| **c5** | CPU-intensive workloads. |
| **r5** | Memory-intensive applications. |
| **g4 / p3** | GPU & Machine Learning. |

---

## 🔐 Security in EC2

EC2 security mainly depends on:

### Security Groups

Acts like a firewall.

Example rules:

| Type | Port |
|------|------|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |
| Spring Boot API | 8080 |

### Key Pair

- Public Key
- Private Key (`.pem`)
- Used to securely connect using SSH.

---

## 💾 Storage Options

### EBS (Elastic Block Store)

- Persistent storage.
- Attached to an EC2 instance.
- Data remains after stopping the instance.

### Instance Store

- Temporary storage.
- Data is lost if the instance is terminated.

---

## 🌐 Public IP vs Elastic IP

| Public IP | Elastic IP |
|-----------|------------|
| Changes after restart (sometimes). | Static IP address. |
| Automatically assigned. | Manually allocated. |
| Temporary. | Persistent. |

---

## 🚀 Real-World Example

Deploying a Spring Boot backend.

1. Launch EC2.
2. Install Java.
3. Upload JAR file.
4. Open port **8080** in Security Group.
5. Access using Public IP.

```text
Browser
   │
Public IP:8080
   │
EC2
   │
Spring Boot Application
```

---

## 📚 Important Interview Questions

### Beginner

- What is Amazon EC2?
- What is an AMI?
- What is an EC2 instance?
- What is a Security Group?

### Intermediate

- Difference between Security Group and NACL?
- Difference between EBS and Instance Store?
- Public IP vs Elastic IP?
- Stop vs Terminate an instance?

### Scenario-Based

- How would you deploy a Spring Boot application on EC2?
- How do you allow HTTP but block SSH from everyone except your IP?

---

## 📝 Summary

- EC2 is AWS's virtual server service.
- Launch instances on demand.
- Choose an AMI and instance type.
- Secure access using Security Groups and Key Pairs.
- Store data using EBS.
- Use Elastic IP for a static public address.
