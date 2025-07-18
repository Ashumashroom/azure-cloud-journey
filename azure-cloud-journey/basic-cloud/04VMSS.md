# ☁️ Azure Virtual Machine Scale Set (VMSS) Guide

This guide explains what Azure VMSS (Virtual Machine Scale Set) is, its features, use cases, and how to create one using the Azure Portal and CLI.

---

## 📘 What is VMSS?

**Azure Virtual Machine Scale Set (VMSS)** is an Azure compute service that allows you to deploy and manage a group of identical, auto-scaling virtual machines. It is ideal for high-availability and large-scale applications.

---

## 🌟 Key Features

| Feature               | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **Auto-scaling**      | Automatically scale VM instances in or out based on demand                  |
| **Load Balancing**    | Integrated with Azure Load Balancer or Application Gateway                  |
| **High Availability** | Spreads instances across Fault Domains or Availability Zones                |
| **Rolling Updates**   | Enables safe, batch-based VM image or configuration updates                 |
| **Stateless Support** | Ideal for stateless workloads like web servers, containers, and microservices |
| **Uniform or Flexible** | Choose identical VMs (Uniform) or mixed VM types (Flexible orchestration)  |

---

## 🛠️ How to Create VMSS (Azure Portal)

### Step 1: Open Azure Portal

Visit: https://portal.azure.com

### Step 2: Search for “Virtual Machine Scale Sets”  
Click **Create** ➜ **Virtual Machine Scale Set**

### Step 3: Configure Basics
- Subscription
- Resource Group
- Scale Set Name
- Region
- Availability Zone (optional)

### Step 4: Instance Settings
- Orchestration Mode: **Uniform** or **Flexible**
- Image: Ubuntu, Windows, or custom image
- Size: e.g., `Standard_B1s`

### Step 5: Scaling
- Enable Autoscale
- Set rules based on CPU or memory usage

### Step 6: Networking
- Attach to a Virtual Network
- Optionally connect to a Load Balancer

### Step 7: Review and Create

---

## 📈 Autoscale Rule Example

| Metric      | Condition             | Action           |
|-------------|------------------------|------------------|
| CPU Usage   | > 70% for 5 minutes    | Add 1 instance   |
| CPU Usage   | < 30% for 10 minutes   | Remove 1 instance|

---

## 🚀 Azure CLI Command Example

```bash
az vmss create \
  --resource-group myResourceGroup \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --admin-username azureuser \
  --generate-ssh-keys
