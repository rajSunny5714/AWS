# 🖥️ EC2 Instance Types

![AWS](https://img.shields.io/badge/AWS-EC2-orange?logo=amazon-aws\&logoColor=white)
![Compute](https://img.shields.io/badge/Service-Compute-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What are EC2 Instance Types?

An **EC2 Instance Type** defines the hardware resources available to an EC2 instance.

It determines:

* 🧠 CPU / vCPU
* 💾 Memory (RAM)
* 🌐 Network performance
* 💿 EBS bandwidth
* ⚡ Processing capability
* 🏗️ CPU architecture

**In simple words:**

> Instance type = The size and capability of an EC2 server.

---

## 🏗️ EC2 Instance Type Structure

Example:

```text
t3.medium

│
├── t3       → Instance family
└── medium   → Instance size
```

Another example:

```text
m6i.large

│
├── m6i      → Instance family
└── large    → Instance size
```

---

# 🧩 Major EC2 Instance Families

## 1️⃣ General Purpose

Designed for workloads requiring a balanced combination of:

* CPU
* Memory
* Network

Common families:

```text
T
M
```

### Example

```text
t3.micro
t3.medium
m6i.large
```

### Suitable for

* 🌐 Web applications
* 🔌 REST APIs
* 🖥️ Application servers
* 🧪 Development environments
* 🗄️ Small databases

---

# 2️⃣ Compute Optimized

Designed for workloads that require high CPU performance.

Common family:

```text
C
```

### Example

```text
c6i.large
c6i.2xlarge
```

### Suitable for

* CPU-intensive applications
* Batch processing
* High-performance APIs
* Scientific computing
* Video processing

```text
High CPU requirement
       ↓
Compute Optimized
       ↓
C Family
```

---

# 3️⃣ Memory Optimized

Designed for applications that require large amounts of RAM.

Common families:

```text
R
X
```

### Suitable for

* 🗄️ Large databases
* ⚡ In-memory processing
* 📊 Big data workloads
* 🧠 Caching
* Analytics

Example:

```text
r6i.large
```

---

# 4️⃣ Storage Optimized

Designed for workloads requiring high-speed local storage and high I/O performance.

Common families include:

```text
I
D
H
```

### Suitable for

* Large-scale databases
* Data warehousing
* Log processing
* High I/O workloads
* Distributed file systems

---

# 5️⃣ Accelerated Computing

Uses specialized hardware such as GPUs or other accelerators.

Common families include:

```text
G
P
Inf
Trn
```

### Suitable for

* 🤖 Machine Learning
* 🧠 AI workloads
* 🎮 Graphics processing
* 🖼️ Video processing
* High-performance computing

---

# ⚡ T-Series: Burstable Instances

T-series instances are **burstable performance instances**.

They provide a baseline CPU performance and can temporarily burst above that baseline when required.

```text
Normal workload
      ↓
Baseline CPU
      ↓
CPU credits available
      ↓
Traffic increases
      ↓
CPU bursts
```

### Example

```text
t3.micro
t3.small
t3.medium
```

---

# 🪙 CPU Credits

T-series instances use **CPU credits** to handle bursts.

When CPU usage is below the baseline:

```text
CPU usage ↓
    ↓
Credits accumulate
```

When CPU usage exceeds the baseline:

```text
CPU usage ↑
    ↓
Credits are consumed
```

**Best suited for:**

> Applications with variable CPU usage rather than continuously high CPU workloads.

---

# 🧠 Important Instance Characteristics

When selecting an EC2 instance, consider:

### 1. vCPU

Number of virtual CPUs available.

```text
More vCPU
   ↓
More parallel processing capability
```

### 2. Memory

RAM available to the application.

```text
More memory
   ↓
Better for memory-intensive workloads
```

### 3. Network Performance

Determines how much network traffic the instance can handle.

Important for:

* APIs
* Microservices
* Distributed systems

### 4. EBS Bandwidth

Determines how quickly the instance can communicate with EBS storage.

### 5. CPU Architecture

Common architectures include:

```text
x86
Arm
```

AWS also provides **AWS Graviton** processors based on Arm architecture.

---

# 📊 General Comparison

| Family | Main Focus      | Typical Workload           |
| ------ | --------------- | -------------------------- |
| T      | Burstable       | Small apps, dev/test       |
| M      | General purpose | Web/API servers            |
| C      | CPU             | CPU-intensive workloads    |
| R      | Memory          | Databases, caching         |
| I      | Storage/I/O     | High I/O workloads         |
| G      | GPU             | Graphics, ML               |
| P      | GPU             | AI/ML training             |
| Inf    | AI inference    | Machine learning inference |
| Trn    | ML training     | Deep learning              |

---

# 🎯 How to Choose an Instance Type?

Use the workload to decide.

### 🌐 Web Application

```text
Spring Boot Application
        ↓
General Purpose
        ↓
M / T family
```

### 🔥 CPU-Intensive Application

```text
Heavy computation
        ↓
Compute Optimized
        ↓
C family
```

### 🧠 Memory-Intensive Application

```text
Large in-memory dataset
        ↓
Memory Optimized
        ↓
R family
```

### 🤖 Machine Learning

```text
ML workload
    ↓
Accelerated Computing
    ↓
G / P / Inf / Trn
```

---

# ☕ Spring Boot Example

Suppose you deploy a Spring Boot REST API:

```text
Users
  ↓
Load Balancer
  ↓
EC2 Instances
  ↓
Spring Boot
  ↓
RDS
```

For a normal backend workload, a **General Purpose** instance may be a good starting point.

If CPU usage becomes consistently high:

```text
High CPU
   ↓
Compute Optimized
```

If memory usage becomes the bottleneck:

```text
High RAM usage
   ↓
Memory Optimized
```

---

# 🔄 Scaling Instance Size

If an application needs more resources, you can change to a larger instance size.

Example:

```text
t3.small
    ↓
t3.medium
    ↓
t3.large
```

This is called **vertical scaling (scaling up)**.

---

# 📈 Vertical vs Horizontal Scaling

### Vertical Scaling

Increase resources of an existing instance.

```text
Small EC2
   ↓
Larger EC2
```

### Horizontal Scaling

Add more EC2 instances.

```text
EC2
EC2
EC2
EC2
```

Usually combined with:

```text
Application Load Balancer
          ↓
   Multiple EC2
```

---

# 🎤 Interview Questions

### 1. What is an EC2 instance type?

> An EC2 instance type defines the compute resources such as vCPU, memory, network performance, and storage capabilities of an EC2 instance.

### 2. What is the difference between T and M instances?

> T instances are burstable and use CPU credits, while M instances provide balanced general-purpose compute resources.

### 3. When would you use C instances?

> When the workload is CPU-intensive and requires high compute performance.

### 4. When would you use R instances?

> For memory-intensive workloads such as large databases, caching, and in-memory analytics.

### 5. What is vertical scaling?

> Increasing the resources of an existing instance, such as moving from a smaller instance size to a larger one.

### 6. What is horizontal scaling?

> Adding more instances to distribute workload across multiple servers.

### 7. What are CPU credits?

> CPU credits allow burstable T-series instances to temporarily use CPU performance above their baseline.

---

# 📝 Quick Revision

```text
EC2 Instance Type
       ↓
Defines server resources
       ↓
┌───────────────────────┐
│ CPU                   │
│ Memory                │
│ Network               │
│ EBS Bandwidth         │
│ Architecture          │
└───────────────────────┘
```

### Remember:

```text
T → Burstable
M → General Purpose
C → Compute
R → Memory
I/D/H → Storage
G/P → GPU
Inf/Trn → AI/ML
```

---

## 🔑 One-Line Interview Answer

> **EC2 instance types define the hardware configuration of an EC2 instance and are selected based on workload requirements such as CPU, memory, storage, and network performance.**

---
