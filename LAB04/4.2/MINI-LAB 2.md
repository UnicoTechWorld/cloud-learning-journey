# 🔵 Scenario — MINI-LAB 2: Network Rules (L3/L4)

You have an Azure Firewall deployed in its own dedicated subnet  
(**AzureFirewallSubnet**).

In the same virtual network, there is a virtual machine (**VM1**) located in a different subnet  
(for example: **WorkloadSubnet**).

At this moment, VM1 cannot send **any outbound traffic** to the internet:  
no ping, no RDP, no access to websites.

Using **Network Rules (Layer 3/4)**, you must ensure that:

## 1. VM1 outbound traffic is allowed through the Azure Firewall
- ICMP (Ping)  
- TCP 3389 (RDP outbound)  
- TCP 443 (HTTPS outbound)

## 2. You must test from inside VM1  
Validate that outbound traffic works after applying the rules.

---

# ✅ Overview of All Steps

## **Step 1 — Verify all base resources exist**

Check that you have:
- Azure Firewall  
- Firewall Policy  
- Virtual Network (VNet)  
- WorkloadSubnet + AzureFirewallSubnet  
- Virtual Machine (VM)  

<img width="333" height="78" alt="image" src="https://github.com/user-attachments/assets/63fbf7a7-405d-4df6-8551-447489578f6c" />

➡️ **Why:** You want to be sure you can continue building on top of Mini-Lab 1.

---

## **Step 2 — Force VM outbound traffic through the firewall**

Check the **effective routes** and ensure that outbound traffic flows through the Azure Firewall.

<img width="620" height="462" alt="image" src="https://github.com/user-attachments/assets/681b01d7-5373-41f1-985f-a3e712c91576" />

<img width="574" height="560" alt="image" src="https://github.com/user-attachments/assets/21a55664-03d3-40e1-949c-c1d46984b5a8" />

<img width="605" height="220" alt="image" src="https://github.com/user-attachments/assets/83f8a235-04bf-4fe5-a596-838c15e4982a" />

<img width="1362" height="432" alt="image" src="https://github.com/user-attachments/assets/036d17a3-7600-4034-ba9b-20275abe80b3" />

➡️ **Why:** Without a UDR or correct subnet/firewall association, the VM will send traffic directly to the internet instead of passing through the firewall.

---

## **Step 3 — Create a Network Rule Collection in the Firewall Policy**

Create a new **Network Rule Collection** that allows:

- ICMP outbound 
- HTTPS outbound (TCP 443)  

➡️ **Why:** Network Rules control Layer 3/4 traffic such as ping and RDP.

<img width="1900" height="318" alt="image" src="https://github.com/user-attachments/assets/843cc66c-fa25-49b0-8a7a-4f2e8afac0f8" />

---

## **Step 4 — Test from the VM**

From inside VM1, test:

- Ping to `8.8.8.8`  
- RDP to a public server or a machine in the same VNet  
- Browsing / HTTPS traffic (port 443)  

➡️ **Why:** This confirms that outbound traffic is allowed through the firewall.

### ⚠️ Note: RDP Connectivity Issue (initial problem)

At the beginning of this mini-lab, I could not RDP into my VM.  
I repeatedly received the following error:

> “Remote Desktop can’t connect to the remote computer…”
> <img width="598" height="242" alt="image" src="https://github.com/user-attachments/assets/ddee3eff-3f3f-48e2-998d-047675b44c3c" />


This issue was related to the fact that my VM’s outbound traffic was not yet correctly routed through the Azure Firewall, and the necessary firewall rules were not configured at that moment.

I will document **how this issue was identified and resolved** in a separate page

---

