# 🖼️ Amazon Machine Image (AMI)

![AWS](https://img.shields.io/badge/AWS-AMI-orange?logo=amazon-aws&logoColor=white)
![Compute](https://img.shields.io/badge/Service-Compute-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What is an AMI?

**Amazon Machine Image (AMI)** is a template used to create an EC2 instance.

An AMI contains the information required to launch an EC2 instance, such as:

- Operating system
- Application server
- Applications
- Configuration
- Required software

**In simple words:**

> AMI is a pre-configured template from which EC2 instances can be launched.

---

## 🏗️ How AMI Works

```text
AMI
 │
 ├── Operating System
 ├── Software
 ├── Configuration
 └── Application
       │
       ▼
   Launch EC2
       │
       ▼
   EC2 Instance
   
----

🚀 Real-World Example

Suppose you have configured an EC2 instance with:

Java 21
Spring Boot environment
Required system packages
Application configuration

Instead of configuring every new EC2 instance manually, you can create a custom AMI.

Then use that AMI to launch additional instances.