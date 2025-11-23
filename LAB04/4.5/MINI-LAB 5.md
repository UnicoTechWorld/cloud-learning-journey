# 🔵 MINI-LAB 5 — Scenario: Private DNS Zones

You are working for an organization where several virtual machines exist inside the same virtual network.  
Until now, these VMs could only reach each other using **private IP addresses**, which is inconvenient and error-prone.

Your task is to configure an **internal DNS solution** so the VMs can resolve each other using a **friendly hostname**, for example:

## 🔹 Overview of all steps 

### Step 1 — Create a Private DNS Zone

<img width="631" height="497" alt="image" src="https://github.com/user-attachments/assets/329b7621-b2aa-4e9e-8f19-8718f547c635" />

### Step 2 — Create a VNet Link

<img width="963" height="364" alt="image" src="https://github.com/user-attachments/assets/2eb7a192-c03a-4470-aae0-6df24c3a238f" />


### Step 3 — Add an A-Record

<img width="1916" height="349" alt="image" src="https://github.com/user-attachments/assets/be99647d-9c05-4153-8334-b64dfd3b306b" />


### Step 4 — Test from your VM

<img width="512" height="124" alt="image" src="https://github.com/user-attachments/assets/67dcea6c-a3e3-4ae9-a803-448793d70c5e" />


---

## ✅ Results

- The Private DNS Zone was successfully created and linked to the existing VNet.
- The A-record for the VM (e.g., `VM2.private.unico.lab`) was added correctly.
- DNS resolution from inside the VM worked as expected:
  - `nslookup` returned the private IP of the VM.
- All components (DNS Zone, VNet Link, A-record) functioned together to provide internal name resolution.
- The lab demonstrated that Azure VMs can resolve each other using friendly hostnames instead of IP addresses.


---

## 🧠 Skills Learned

- Understanding the purpose of **Private DNS Zones** and when to use them.
- Knowing the difference between **public DNS** and **private/internal DNS** in Azure.
- How to:
  - Create a Private DNS Zone.
  - Link a VNet to a DNS Zone using a **VNet Link** so VMs can use it for name resolution.
  - Add a manual **A-record** for a VM.
  - Validate DNS resolution using `nslookup` from inside an Azure VM.
- Improved understanding of Azure internal DNS behavior (168.63.129.16 resolver).
- Learned how name resolution works between VMs without relying on IP addresses.

