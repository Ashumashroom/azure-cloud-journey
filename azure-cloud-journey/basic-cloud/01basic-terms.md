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

# Today's Azure Concepts

## Infrastructure as a Service (IaaS)

Raw compute, storage, and networking resources you manage at the OS level.

* **You manage:** OS, middleware, runtime, applications, data, security.
* **Azure manages:** Physical hosts, hypervisor, network fabric.
* **Examples:** Azure Virtual Machines, Azure Disks, Azure Virtual Network.

## Platform as a Service (PaaS)

Managed platform for building, deploying, and scaling apps.

* **You manage:** Application code, configuration, data.
* **Azure manages:** OS, runtime, middleware, scaling, high availability.
* **Examples:** Azure App Service, Azure Functions, Azure SQL Database, Azure Kubernetes Service (AKS).

## Software as a Service (SaaS)

Fully managed applications delivered over the Internet.

* **You manage:** User settings, data inside the app.
* **Azure/Microsoft manages:** Application code, runtime, infrastructure.
* **Examples:** Microsoft 365, Dynamics 365, Power BI, Azure DevOps Services, GitHub.

## Azure Resource

An individual service instance in Azure.

* Each resource has its own configuration, billing meter, and lifecycle.
* **Examples:** Virtual Machine, Storage Account, App Service, SQL Database.

## Azure Resource Group

A logical container for grouping related resources.

* Resources in a group share lifecycle operations (deploy, update, delete).
* Enables unified management, RBAC, tagging, and policy enforcement.
* **Example:** Resource group `rg-webapp-prod` containing a VM, Storage Account, App Service, and SQL Database.

## Azure Resource Manager (ARM)

The deployment and management control plane for Azure.

* All resource operations (create/update/delete) go through ARM APIs.
* Supports declarative templates (ARM templates/Bicep).
* Provides role-based access control (RBAC), tagging, policy enforcement, and dependency resolution.
* **Usage:** Azure Portal, Azure CLI/PowerShell, ARM templates.

### Quick Reference

| Model/Concept              | You Manage                        | Azure Manages                            | Examples                                 |
| -------------------------- | --------------------------------- | ---------------------------------------- | ---------------------------------------- |
| **IaaS**                   | OS, runtime, apps, data, security | Physical infrastructure & virtualization | Virtual Machines, Disks, Virtual Network |
| **PaaS**                   | App code, configuration, data     | OS, runtime, middleware, scaling, HA     | App Service, Functions, SQL DB, AKS      |
| **SaaS**                   | User settings & data              | Entire application stack                 | Microsoft 365, Dynamics 365, Power BI    |
| **Azure Resource**         | Service configuration & data      | Underlying infrastructure via ARM        | VM, Storage Account, SQL Database        |
| **Resource Group**         | Organization, RBAC, tags          | None (logical container)                 | `rg-<app>-<env>`                         |
| **Azure Resource Manager** | Deployment templates & RBAC       | ARM service control plane                | ARM Templates, CLI/PowerShell commands   |

## Azure Resources Overview

Below is a categorized list of core Azure resources:

### Compute

* Virtual Machines
* App Services (Web Apps)
* Azure Functions
* Azure Kubernetes Service (AKS)

### Storage

* Azure Blob Storage
* Azure File Storage
* Azure Disks
* Azure Data Lake Storage

### Networking

* Virtual Network (VNet)
* Load Balancer
* Application Gateway
* Azure DNS
* VPN Gateway
* ExpressRoute

### Databases

* Azure SQL Database
* Azure Cosmos DB
* Azure Database for MySQL/PostgreSQL
* Azure Table Storage

### Identity & Access

* Azure Active Directory (AAD)
* Role-Based Access Control (RBAC)
* Managed Identities

### Monitoring & Management

* Azure Monitor
* Azure Log Analytics
* Azure Application Insights
* Azure Policy

### Developer & Integration Tools

* Azure DevOps
* Azure Repos
* Azure Pipelines
* GitHub (Microsoft owned)

### AI & Machine Learning

* Azure Machine Learning
* Cognitive Services
* Azure Bot Services

These resources are accessible via Azure Portal, CLI, SDKs, and ARM/Bicep templates.
