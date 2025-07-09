# ☁️ Azure Cloud Basics – Core Concepts

This document summarizes the essential cloud computing concepts with a focus on Azure. It covers foundational knowledge like virtualization, hypervisors, scalability, availability, fault tolerance, and disaster recovery — all crucial for building resilient, scalable cloud-native applications.

---

## 📘 Table of Contents
- [1. Virtualization](#1-virtualization)
- [2. Hypervisor](#2-hypervisor)
- [3. API (Application Programming Interface)](#3-api-application-programming-interface)
- [4. Load Balancer](#4-load-balancer)
- [5. Regions and Availability Zones](#5-regions-and-availability-zones)
- [6. Core Cloud Concepts](#6-core-cloud-concepts)
  - [6.1 Scalability](#61-scalability)
  - [6.2 Auto-Scaling](#62-auto-scaling)
  - [6.3 Manual Scalability](#63-manual-scalability)
  - [6.4 Elasticity](#64-elasticity)
  - [6.5 Agility](#65-agility)
  - [6.6 High Availability (HA)](#66-high-availability-ha)
  - [6.7 Fault Tolerance](#67-fault-tolerance)
  - [6.8 Disaster Recovery](#68-disaster-recovery)

---

## 1. Virtualization

Virtualization is the process of creating a virtual (software-based) version of a physical resource like CPU, memory, or storage. It allows multiple **Virtual Machines (VMs)** to run on a single physical host.

> Example: One physical server can host multiple OS like Windows, Linux, etc., each isolated from the other.

---

## 2. Hypervisor

A **hypervisor** is software that enables virtualization. It abstracts the underlying physical hardware and allows multiple VMs to run on it.

### Types of Hypervisors:
| Type        | Description                      | Example               |
|-------------|----------------------------------|------------------------|
| Type 1      | Bare-metal, runs on hardware     | Hyper-V, ESXi, Xen     |
| Type 2      | Runs on top of OS                | VirtualBox, VMware     |

Azure uses **Type 1 (Hyper-V)** for performance and isolation.

---

## 3. API (Application Programming Interface)

An API defines how two applications or services communicate. APIs are used everywhere in cloud platforms for automation, service access, and integration.

> Example: A weather app uses a weather API to get temperature data.

Common methods: `GET`, `POST`, `PUT`, `DELETE`

---

## 4. Load Balancer

A **Load Balancer** distributes incoming traffic across multiple servers to ensure:
- No single server is overwhelmed
- High availability and reliability
- Better performance

### Azure Load Balancer Types:
| Type                  | Protocol | Use Case             |
|-----------------------|----------|----------------------|
| Azure Load Balancer   | Layer 4  | TCP/UDP-based apps   |
| Application Gateway   | Layer 7  | Web apps, HTTP/HTTPS |
| Azure Front Door      | Global   | Geo-based traffic    |

---

## 5. Regions and Availability Zones

### 🌍 Region:
A **region** is a geographical area with one or more data centers. Example: `East US`, `Central India`.

### 🏢 Availability Zone (AZ):
An AZ is an isolated datacenter within a region. Azure regions with AZs offer high availability by replicating across multiple physical zones.

Benefits:
- Fault isolation
- Redundancy
- High availability

---

## 6. Core Cloud Concepts

### 6.1 Scalability
Ability to handle growing workloads.
- **Vertical**: Increase resources on a single instance
- **Horizontal**: Add more instances

### 6.2 Auto-Scaling
Automatically adds/removes compute resources based on traffic.

### 6.3 Manual Scalability
User-triggered resizing or scaling.

### 6.4 Elasticity
Ability to scale **dynamically** in real-time based on workload changes.

### 6.5 Agility
Speed at which applications can be deployed, tested, and scaled.

### 6.6 High Availability (HA)
Ensures services are accessible 99.99%+ of the time using redundancy and failover mechanisms.

### 6.7 Fault Tolerance
System continues operating even when components fail.

### 6.8 Disaster Recovery
Ability to restore services after a catastrophic event.

---

## ✅ Summary Table

| Concept             | Purpose                           | Azure Tools/Features              |
|---------------------|-----------------------------------|-----------------------------------|
| Scalability         | Add resources as needed           | VM resize, Scale Sets             |
| Elasticity          | Dynamic real-time scaling         | Auto-scaling                      |
| Agility             | Rapid dev/test/deploy             | ARM, DevOps, Functions            |
| High Availability   | 99.99% uptime                     | Availability Zones, Load Balancer |
| Fault Tolerance     | Operate despite failures          | Availability Sets, ZRS            |
| Disaster Recovery   | Recover from system-wide failure  | Azure Site Recovery, GRS          |

---

> 🧠 Next up: Learn about **Azure Virtual Machines (VMs)** and deploy your first VM with CLI and Portal!

