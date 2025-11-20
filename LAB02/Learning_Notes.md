# 📘 Learning Notes — LAB02 VNet + Subnet + NSG + Bastion

This file contains the questions I had during the lab, along with the answers and the reasoning behind them.



---

## ❓ 1. Why didn’t we need to explicitly add a “Deny All” rule like in Lab01?

### ✔️ Short Answer
Because Azure NSGs already include a **built-in default Deny rule** at the bottom of every NSG.  
We only need to add custom *Allow* rules — everything else is automatically blocked.

### 🧠 Detailed Explanation
Every Network Security Group comes with system-defined rules:

| Priority | Rule Name                   | Action |
|---------|------------------------------|--------|
| 65000   | AllowVNetInbound             | Allow  |
| 65001   | AllowAzureLoadBalancerInbound| Allow  |
| **65500** | **DenyAllInbound**         | **Deny** |

This final rule blocks all inbound traffic unless you explicitly allow it.

In **Lab01**, we added a deny rule manually only because it was part of the *training objective* — not because it was required technically.

### ⭐ Best Practice
In real Azure environments:
> **You only create the allow rules you need.  
Everything else is automatically denied.**

This keeps NSGs clean, predictable, and secure.



---

## ❓ 2. What exactly is Azure Bastion and why is it recommended?

### ✔️ Short Answer
Azure Bastion is a fully managed **secure jump-host** that lets you connect to VMs using **RDP or SSH over the browser**, without exposing the VM to the internet.

### 🧠 Detailed Explanation
Without Bastion, you must use:
- a **public IP** on the VM  
- open ports like **3389 (RDP)** or **22 (SSH)**  
- which exposes the VM to the public internet  
- leading to brute-force attacks within minutes  

Azure Bastion removes all of this:

- Your VM stays **private**  
- No public IP needed  
- No inbound ports opened  
- You connect safely through **HTTPS (443)**  
- You log in directly in the browser  
- Microsoft maintains, patches, and secures the Bastion host

This follows Azure's **Zero Trust** security model.

### ⭐ Best Practice
> **Use Azure Bastion instead of opening RDP/SSH to the public Internet.**  
It eliminates attack surface and is the recommended approach for production environments.



---

