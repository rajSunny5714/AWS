# 💾 Amazon EBS (Elastic Block Store)

![AWS](https://img.shields.io/badge/AWS-EBS-orange?logo=amazon-aws&logoColor=white)
![Storage](https://img.shields.io/badge/Service-Storage-blue)
![Level](https://img.shields.io/badge/Level-Beginner-success)

## 📌 What Is Amazon EBS?

**Amazon Elastic Block Store (EBS)** is a block storage service designed for use with Amazon EC2.

It provides persistent storage volumes that can store operating systems, applications, files, and databases.

**In simple words:**

> EBS is like a virtual hard disk that you can attach to an EC2 instance.

## 🎯 Why Do We Need EBS?

EBS is useful for:

- 💾 Storing application files
- 🖥️ Storing an EC2 operating system
- 🗄️ Running databases
- 📦 Storing application data
- 🔄 Retaining data independently of an EC2 instance's running state

## 🏗️ How EBS Works

```text
        Amazon EC2
            |
            | Attached Volume
            |
            v
        Amazon EBS
            |
     ┌──────┴──────┐
     |             |
 Operating      Application
  System           Data
```

An EBS volume is created in a specific Availability Zone and attached to a compatible EC2 instance in that same Availability Zone.

## 🧩 Important EBS Concepts

### 1. EBS Volume

An EBS volume is a virtual block storage device.

It can store:

- Operating system files
- Application data
- Database files
- Logs and other persistent files

### 2. Persistence

EBS storage persists independently of the EC2 instance's running state.

For example, stopping and restarting an EC2 instance normally does not delete its attached EBS volumes.

**Important:** If an instance is terminated, whether its root EBS volume is deleted depends on the volume's `DeleteOnTermination` setting. Other attached EBS volumes are generally retained unless configured otherwise.

### 3. Snapshots

An EBS snapshot is a point-in-time backup of an EBS volume.

Snapshots can help you:

- Back up important data
- Restore data after a failure
- Create new volumes
- Maintain recovery copies

```text
       EBS Volume
            |
            v
         Snapshot
            |
       ┌────┴────┐
       |         |
   Backup      Restore
                 |
                 v
            New EBS Volume
```

Snapshots are stored in Amazon S3-managed infrastructure; they are not ordinary files that you browse directly in an S3 bucket.

## 📦 Types of EBS Volumes

EBS provides different volume types for different workloads.

### 1. General Purpose SSD

Common volume types include:

- `gp3`
- `gp2`

Suitable for:
- Boot volumes
- General applications
- Development environments
- Many transactional workloads

### 2. Provisioned IOPS SSD

Common volume types include:

- `io2`
- `io1`

Suitable for workloads requiring consistently high I/O performance, such as demanding databases.

### 3. Throughput Optimized HDD

Volume type:

- `st1`

Suitable for throughput-intensive workloads, such as large sequential data processing.

### 4. Cold HDD

Volume type:

- `sc1`

Suitable for less frequently accessed data where low storage cost is a priority.

**Note:** HDD volume types are not supported as boot volumes. Choose a suitable SSD volume for an EC2 boot volume.

## 📊 EBS Volume Comparison

| Volume Type | Storage Media | Typical Use |
|---|---|---|
| gp3 | SSD | General-purpose applications |
| gp2 | SSD | General-purpose applications |
| io2 | SSD | High-performance databases |
| io1 | SSD | I/O-intensive workloads |
| st1 | HDD | High-throughput sequential workloads |
| sc1 | HDD | Infrequently accessed data |

## 🔄 EBS vs EC2 Instance Store

EC2 can provide storage through EBS volumes or instance store volumes, depending on the instance type.

| Feature | EBS | Instance Store |
|---|---|---|
| Storage | Network-attached block storage | Physically attached host storage |
| Persistence | Designed to persist independently of instance state | Ephemeral; data may be lost when the instance stops, terminates, or the underlying host fails |
| Detachable | Can be detached from an instance | Cannot be detached like an EBS volume |
| Use case | Persistent application and database data | Temporary data and workloads needing local storage |

**Remember:** Do not rely on instance store for your only copy of important data.

## 🔄 EBS vs EBS Snapshot

| Feature | EBS Volume | EBS Snapshot |
|---|---|---|
| Purpose | Provides block storage | Provides a point-in-time backup |
| Used directly by an EC2 instance | Yes, when attached | No |
| Main role | Store and access data | Backup and recovery |
| Can create another volume | Not its primary purpose | Yes |

## ☕ Spring Boot Example

Suppose you deploy a Spring Boot application on EC2.

```text
          EC2 Instance
               |
       ┌───────┴────────┐
       |                |
       v                v
  Spring Boot       EBS Volume
  Application       Application Data
                         |
                         v
                    EBS Snapshot
                         |
                         v
                    Backup Copy
```

EBS can store application files, logs, or self-managed database files.

For a production application, consider managed storage and database services when appropriate instead of keeping all persistent data on the application server.

## 🛡️ EBS Best Practices

- Take regular snapshots of important volumes.
- Test restoration procedures instead of assuming backups work.
- Encrypt EBS volumes containing sensitive data.
- Monitor storage capacity and performance.
- Choose a volume type based on workload requirements.
- Review snapshot retention and deletion policies.
- Follow least-privilege access for EBS and snapshot operations.

## 🎤 Interview Questions

### 1. What is Amazon EBS?

Amazon EBS is a block storage service that provides persistent storage volumes for EC2 instances.

### 2. What happens to EBS data when an EC2 instance is stopped?

The data generally remains available when the instance is restarted.

### 3. What is an EBS snapshot?

An EBS snapshot is a point-in-time backup used for recovery and creating additional volumes.

### 4. What is the difference between EBS and instance store?

EBS is persistent block storage independent of an instance's running state, while instance store provides temporary local storage.

### 5. Can you attach an EBS volume to an EC2 instance in another Availability Zone?

Not directly. The volume and instance must be in the same Availability Zone. You can create a snapshot and use it to create a volume in another Availability Zone.

### 6. Which EBS volume type is suitable for general-purpose workloads?

`gp3` is a common general-purpose SSD choice.

### 7. What happens to the root EBS volume when an EC2 instance is terminated?

It depends on the `DeleteOnTermination` setting. The root volume is commonly configured for deletion on termination, but this can be changed.

### 8. Why should EBS volumes be encrypted?

Encryption helps protect data at rest and supports protection of data moving between the EC2 instance and the EBS volume.

## 📝 Quick Revision

```text
Amazon EBS
    |
    ├── Block Storage
    ├── Persistent Volumes
    ├── Snapshots
    ├── Encryption
    └── Backup and Recovery
```

**One-line interview answer:**

> Amazon EBS is a persistent block storage service for EC2 that provides storage volumes for operating systems, applications, and databases.