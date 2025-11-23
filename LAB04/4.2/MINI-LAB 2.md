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

I will document **how this issue was identified and resolved** in a separate page.

After fixing the routing issue (details documented on the *Troubleshooting – RDP Issue* page), I was able to successfully RDP back into my VM.

From that point on:

- Outbound rules through the Azure Firewall worked as expected  
- HTTPS traffic was allowed  
- All validation tests for Mini-Lab 2 were successful  

✅ **Conclusion:**  
The connectivity issue was resolved, and Mini-Lab 2 was fully completed without further problems.

---
## 🎓 What I Learned

This mini-lab helped me understand several key Azure Firewall and routing concepts:

### 🔹 1. How outbound traffic flows through the Azure Firewall  
I now understand how a firewall sitting in a dedicated subnet (AzureFirewallSubnet) inspects and controls outbound L3/L4 traffic using Network Rules.

### 🔹 2. Why User-Defined Routes (UDRs) are required  
Without a UDR pointing `0.0.0.0/0 → Firewall`, the VM would bypass the firewall and go directly to the Internet.  
The lab showed me how to enforce traffic through the firewall using UDRs.

### 🔹 3. How to troubleshoot RDP failures caused by routing  
I learned that:
- A default route (`0.0.0.0/0`) to the firewall forces *all* traffic through the firewall  
- The firewall blocks inbound RDP unless DNAT rules exist  
- Therefore, applying a UDR can unintentionally break RDP  

I now fully understand why RDP timed out and how to fix it (either remove the UDR temporarily or configure DNAT).


### 🔹 4. Real-world enterprise firewall design basics  
I gained hands-on experience with:
- Firewall policies  
- Rule collections  
- Network rules  
- Default routes  
- Troubleshooting network flows  

These are core skills for real Azure networking and security designs.

---

