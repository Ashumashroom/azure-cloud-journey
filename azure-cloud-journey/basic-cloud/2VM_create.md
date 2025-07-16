# Azure Virtual Machine Creation Guide

This document provides four common methods to create an Azure Virtual Machine (VM). Copy and paste this into your GitHub repository.

---

## 1. Using the Azure Portal

1. Sign in at [https://portal.azure.com](https://portal.azure.com)
2. Click **Create a resource** → **Compute** → **Virtual Machine**
3. **Basics** tab:

   * **Subscription** + **Resource group** (create or select existing)
   * **Region** (e.g., Central India)
   * **Image** (e.g., Ubuntu 20.04 LTS, Windows Server 2022)
   * **Size** (vCPU/RAM selection)
   * **Authentication**: SSH public key or password
4. **Disks** tab:

   * OS disk type (Premium SSD, Standard HDD, etc.)
   * (Optional) add data disks
5. **Networking** tab:

   * Virtual Network/subnet
   * Public IP (yes/no)
   * Network Security Group (open ports: 22, 80, 443…)
6. **Management**, **Advanced**, **Tags** tabs:

   * Enable monitoring, boot diagnostics, add extensions, tags
7. Click **Review + create**, then **Create**

Once deployment succeeds, view the VM’s public IP on the Overview page and SSH (Linux) or RDP (Windows) into it.

---

## 2. Using the Azure CLI

Make sure you have the Azure CLI installed and have run `az login`.

```bash
# Variables
RG="myResourceGroup"
LOCATION="centralindia"
VM_NAME="myVM"
IMAGE="UbuntuLTS"
SIZE="Standard_D2s_v3"
ADMIN_USER="azureuser"
SSH_KEY_PATH="$HOME/.ssh/id_rsa.pub"

# Create a resource group
az group create \
  --name $RG \
  --location $LOCATION

# Create the VM
az vm create \
  --resource-group $RG \
  --name $VM_NAME \
  --image $IMAGE \
  --size $SIZE \
  --admin-username $ADMIN_USER \
  --ssh-key-value $SSH_KEY_PATH \
  --output table

# Open port 22 for SSH
az vm open-port \
  --resource-group $RG \
  --name $VM_NAME \
  --port 22
```

SSH into the VM:

```bash
ssh azureuser@<public-ip-address>
```

---

## 3. Using Azure PowerShell

Install the Az module (`Install-Module -Name Az`) and run `Connect-AzAccount`.

```powershell
# Variables
$rg      = "myResourceGroup"
$loc     = "CentralIndia"
$vmName  = "myVM"
$image   = "Win2022Datacenter"
$cred    = Get-Credential  # enter username/password

# Create resource group
New-AzResourceGroup -Name $rg -Location $loc

# Define VM configuration
$vmConfig = New-AzVMConfig -VMName $vmName -VMSize "Standard_D2s_v3" |
  Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred |
  Set-AzVMSourceImage -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" `
                       -Skus "2022-Datacenter" -Version "latest" |
  Add-AzVMNetworkInterface -Id (
    New-AzNetworkInterface -Name "$($vmName)-nic" -ResourceGroupName $rg `
      -Location $loc -SubnetId (
        (New-AzVirtualNetwork -Name "$($rg)-vnet" -ResourceGroupName $rg `
          -Location $loc -AddressPrefix "10.0.0.0/16" |
         Add-AzVirtualNetworkSubnetConfig -Name "default" -AddressPrefix "10.0.0.0/24" |
         Set-AzVirtualNetwork).Subnets[0].Id) |
      New-AzPublicIpAddress -Name "$($vmName)-pip" -ResourceGroupName $rg `
        -Location $loc -AllocationMethod Dynamic).Id

# Create the VM
New-AzVM -ResourceGroupName $rg -Location $loc -VM $vmConfig
```

---

## 4. Using an ARM Template

Save this as `azuredeploy.json`:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName":      { "type": "string", "defaultValue": "myVM" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "secureString" },
    "location":    { "type": "string", "defaultValue": "centralindia" },
    "vmSize":      { "type": "string", "defaultValue": "Standard_D2s_v3" },
    "imagePublisher": { "type": "string", "defaultValue": "Canonical" },
    "imageOffer": { "type": "string", "defaultValue": "UbuntuServer" },
    "imageSku":   { "type": "string", "defaultValue": "18.04-LTS" }
  },
  "resources": [
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2021-07-01",
      "name": "[parameters('vmName')]",
      "location": "[parameters('location')]",
      "properties": {
        "hardwareProfile": {
          "vmSize": "[parameters('vmSize')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[parameters('imagePublisher')]",
            "offer": "[parameters('imageOffer')]",
            "sku": "[parameters('imageSku')]",
            "version": "latest"
          },
          "osDisk": {
            "createOption": "FromImage"
          }
        },
        "osProfile": {
          "computerName": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(parameters('vmName'),'-nic'))]"
            }
          ]
        }
      }
    }
    // ... add NIC, VNet, PublicIP resources here
  ]
}
```

Deploy with:

```bash
az group create --name myRG --location centralindia
az deployment group create \
  --resource-group myRG \
  --template-file azuredeploy.json \
  --parameters adminUsername=azureuser adminPassword="P@ssw0rd!"
```

---

## 5. Azure VM Series and Types

Azure VMs are grouped into series, each optimized for specific workloads:

### General Purpose (Balanced CPU/Memory)

* **Av2 family**: Entry-level, cost-effective; dev/test and low-traffic web servers.
* **Dv5/Dsv5/Ddv5 series**: Latest generation balanced VMs; typical enterprise workloads and small databases.
* **B series (Burstable)**: Baseline CPU with burst credits; suitable for intermittent workloads with occasional spikes.

### Compute Optimized

* **Fsv2 family**: High CPU-to-memory ratio; ideal for batch processing, analytics, gaming servers, and web front-ends.
* **FX series**: Enhanced Fsv2 with larger local SSD; compute-heavy tasks requiring fast temp storage.

### Memory Optimized

* **Ev5/Esv5 series**: High memory-to-CPU; memory-intensive relational databases, in-memory caches like Redis.
* **Ebds\_v5/Ebsv5**: Similar to Ev5 with premium SSD bursting for improved IOPS.
* **M series**: Massive memory (up to multiple TB); SAP HANA, large-scale in-memory analytics.

### Storage Optimized

* **Ls series**: High disk throughput & IOPS; big data, NoSQL databases like Cassandra.
* **Lsv2 series**: Latest generation with NVMe SSD for ultra-low latency storage workloads.

### GPU Accelerated

* **NC/ND series**: NVIDIA GPUs for compute and AI training/inference (CUDA, Tensor Cores).
* **NV series**: GPUs optimized for visualization and graphics rendering workloads.

### High Performance Compute (HPC)

* **H series**: Low-latency network and RDMA; parallel simulations, molecular modeling, CFD.
* **Hb/Hc series**: Latest Mellanox HDR Infiniband for ultra-high throughput and low latency in HPC clusters.

*Select the series based on your workload’s CPU, memory, disk I/O, and network needs, ensuring regional availability.*

## Next Steps

* Automate deployments with Terraform or Bicep
* Lock down your NSG rules
* Enable Azure Backup & Azure Monitor
* Explore VM extensions and custom scripts

---

*End of guide.*

also 
