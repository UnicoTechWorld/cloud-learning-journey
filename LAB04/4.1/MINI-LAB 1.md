## 🔵 Scenario – Mini-Lab 1: Azure Firewall Basic Setup

You are working as a junior Cloud Engineer in a team that is setting up a new, secure network architecture in Azure.  
Until now, developers have been using a simple virtual network (VNet) with a single subnet that hosts their test VMs.  
These VMs can reach the internet without any restrictions because no firewall or routing has been configured yet.

The security team requests that **all outbound traffic from the VMs must now pass through a central Azure Firewall**, so that:

- network traffic is monitored and logged,
- only allowed protocols can leave the network,
- the company can gradually evolve into a proper **hub-and-spoke** model.

For this mini-lab, your task is to build the foundation:

1. Create a virtual network with two subnets:
   - **AzureFirewallSubnet** (required for the firewall)
   - **WorkloadSubnet** (where VMs will later be deployed)

2. Deploy an **Azure Firewall** inside AzureFirewallSubnet.

3. Create a **Public IP** and attach it to the firewall.

4. Attach a **Firewall Policy**, which will later be used to configure rules.

The goal of this mini-lab is to make you familiar with the fundamentals:  
**how an Azure Firewall is correctly deployed and what network structure is required for it.**

## 🔵 Mini-Lab 1 — Overview of All Steps

### **Step 1 — Create Resource Group**
You create a dedicated Resource Group for this lab so that everything stays clean and organized.

<img width="820" height="160" alt="image" src="https://github.com/user-attachments/assets/03213535-66d3-4643-9017-b8db8e86be1f" />

---

### **Step 2 — Create Virtual Network (VNet)**
You create a VNet where both the firewall and future workload VMs will be deployed.

<img width="694" height="769" alt="image" src="https://github.com/user-attachments/assets/ae36128f-e930-4152-9b3b-2a06b19be58a" />

---

### **Step 3 — Create Subnets**
Inside the VNet, you create two subnets:

- **AzureFirewallSubnet** (required for Azure Firewall)
- **WorkloadSubnet** (for VMs and later routing configuration)

<img width="1887" height="364" alt="image" src="https://github.com/user-attachments/assets/19112475-ceea-4269-bfb3-ed53f9ff9baa" />


---

### **Step 4 — Create Public IP for the Firewall**
The firewall needs a static Public IP for management and outbound internet connectivity.

<img width="1445" height="427" alt="image" src="https://github.com/user-attachments/assets/271d0096-1a34-4f71-9e16-d13c9ac5ae41" />

---

### **Step 5 — Create Firewall Policy**
You create the policy so you can later add rules (network, application, DNAT).

<img width="849" height="547" alt="image" src="https://github.com/user-attachments/assets/375900e9-ee30-4bdd-aa92-75e236d3e6e2" />


---

### **Step 6 — Deploy Azure Firewall into AzureFirewallSubnet**
You deploy the firewall and attach the Public IP and the Firewall Policy.

<img width="648" height="528" alt="image" src="https://github.com/user-attachments/assets/0e6cef8e-f388-4dc3-983c-aa25d5e5406b" />

---

### **Step 7 — Validation**
You verify that:

- the firewall is up & running,
- the policy is attached,
- routing is not yet active (that comes in the next mini-labs).

<img width="1550" height="466" alt="image" src="https://github.com/user-attachments/assets/7b714f0d-1367-4da4-a0f5-b904328e08be" />


---

## ✅ Results

By the end of this mini-lab, the following components were successfully deployed:

- A dedicated Resource Group for the lab  
- A Virtual Network (`FW-VNET`) with two subnets:  
  - **AzureFirewallSubnet** (required for Azure Firewall)  
  - **WorkloadSubnet** (for future VMs)  
- A **Public IP (Standard, Static, Zone-redundant)** assigned to the firewall  
- A **Firewall Policy** created for future rule configuration  
- An **Azure Firewall** successfully deployed inside the AzureFirewallSubnet and linked to both the Public IP and Firewall Policy  
- Validation confirmed that:  
  - The firewall deployment succeeded  
  - The policy was attached correctly  
  - No routing was active yet (expected — comes in next labs)

This completes the foundational setup for all upcoming firewall, DNAT, routing, and DNS labs.

---

## 📘 What I Learned

During this mini-lab, I learned the core fundamentals of how Azure Firewall is deployed and how its network structure works:

- Azure Firewall **requires a dedicated subnet** named exactly `AzureFirewallSubnet`
- The firewall should be deployed in a **zone-redundant** configuration for high availability
- A **Standard static public IP** is necessary for outbound traffic, DNAT, and rule processing
- Firewall Policies are used to manage all rule collections:
  - Network rules (L3/L4)
  - Application rules (HTTP/HTTPS)
  - DNAT rules (inbound translations)
- VNets must be intentionally designed before deploying a firewall:
  - Proper address spacing
  - Subnet separation
  - Clear network hierarchy
- This deployment becomes the base for:
  - Forced tunneling (UDR)
  - Network segmentation
  - Secure inbound RDP via DNAT (Mini-Lab 3)
  - DNS resolution across VNets (Mini-Lab 5)

This mini-lab builds the foundation for the complete firewall architecture I will configure in the next exercises.

