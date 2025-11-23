## 🔵 Scenario – Mini-Lab 3: DNAT (Inbound RDP via Azure Firewall)

Your team is using a **hub-and-spoke architecture**, where *all* access to internal workloads must pass through a **central Azure Firewall**.

👉 **Rule:** In the workload subnet, only **one** VM is allowed to have a Public IP.  
All other workloads **must** be reachable only through the firewall.

The dev team lead asks:

> “Can we temporarily allow RDP access to a specific VM in the WorkloadSubnet,  
but **without giving it a public IP**?”

Your task:

➡️ **Make secure inbound RDP possible using DNAT rules on Azure Firewall.**

---

## 🌸 What you will do

1. Deploy a **Windows VM without a Public IP** in the WorkloadSubnet.
2. Create a **DNAT rule** inside the Firewall Policy:
   - When someone opens RDP to the **Firewall Public IP** on **port 50001**,  
   - The firewall must NAT the traffic to the internal VM on **port 3389**.
3. Test if you can connect via the firewall’s Public IP.
4. Verify in Firewall Logs that the DNAT rule was actually triggered.

---

## ✅ Overview of all steps (short & simple)

### 1. Check Resource Group & Networking
Make sure your hub-and-spoke environment is ready (Firewall, VNets, subnets).  

<img width="789" height="267" alt="image" src="https://github.com/user-attachments/assets/0a1d51b3-1572-4fc6-bc35-40a73a6125a4" />

<img width="748" height="751" alt="image" src="https://github.com/user-attachments/assets/069603b9-544c-4926-968a-f60f8866e4f4" />

<img width="630" height="689" alt="image" src="https://github.com/user-attachments/assets/a3405991-0cd6-4b1b-93de-4143963cab2d" />

<img width="829" height="899" alt="image" src="https://github.com/user-attachments/assets/22de4919-6536-46ad-98fc-a25671c80a7a" />

<img width="534" height="718" alt="image" src="https://github.com/user-attachments/assets/c16848e6-400b-44d1-bf29-203c9ca66b45" />

<img width="1514" height="486" alt="image" src="https://github.com/user-attachments/assets/e3fed142-aef2-43fb-bae2-7090f35bf5dc" />

---

### 2. Deploy Windows VM (without Public IP)
Create an internal VM inside the WorkloadSubnet.  

<img width="1875" height="971" alt="image" src="https://github.com/user-attachments/assets/ce162e36-7906-4542-b2c4-0968c5a1d5d3" />

---

### 3. Create a Log Analytics Workspace (for Firewall logs)
Create a Log Analytics Workspace that will receive Azure Firewall diagnostics.

<img width="816" height="608" alt="image" src="https://github.com/user-attachments/assets/eae85136-bd32-47b6-8694-e0e308ace4b9" />

<img width="1887" height="743" alt="image" src="https://github.com/user-attachments/assets/2a804fd4-46e3-4d8e-bc3b-194ddaeabf65" />


✔️ *Why?* Azure Firewall does not log anything by default —  
you need a LAW to collect DNAT, network, and application rule logs.

---

### 4. Create DNAT Rule in the Firewall Policy
Forward traffic from **FW-Public-IP:50001 → Internal VM:3389**.  
✔️ *Why?* DNAT safely exposes RDP without giving the VM a Public IP.

<img width="1901" height="354" alt="image" src="https://github.com/user-attachments/assets/18b244ca-afa0-40a0-8274-1ccb71f2660c" />

---

### 5. Test via Remote Desktop
Open RDP to: **Firewall-Public-IP:50001**.  
✔️ *Why?* This confirms that the firewall is correctly NAT-ing the traffic.

<img width="874" height="443" alt="image" src="https://github.com/user-attachments/assets/85c313bd-c430-4678-9325-be8d0d32b72d" />

<img width="1406" height="854" alt="image" src="https://github.com/user-attachments/assets/185c1ef7-0875-42e4-938f-90a863020abe" />

---

### 7. Open Firewall Logs
Verify that the DNAT rule was actually used.  
✔️ *Why?* Logs prove the traffic flowed through the firewall as expected.

> Note: At first, I couldn’t see any DNAT logs.  
> In the **Questions / Problems Encountered** section, I will show exactly what was wrong  
> and how I eventually fixed it so the logs appeared correctly.

<img width="1663" height="504" alt="image" src="https://github.com/user-attachments/assets/76f40601-38e0-46df-9092-0abd40761ba4" />

<img width="1599" height="371" alt="image" src="https://github.com/user-attachments/assets/14bbce39-f63f-4341-84ea-4ca9fabeb5a9" />

---

## 🎉 Results

By the end of this mini-lab, I successfully achieved:

- ✔️ RDP access to an internal VM **without a Public IP**
- ✔️ Fully functional **DNAT rule** on Azure Firewall  
  (FW-Public-IP:50001 → VM-Private-IP:3389)
- ✔️ Verified the DNAT traffic flow through Azure Firewall using **Log Analytics**
- ✔️ Confirmed proper **Firewall Policy** configuration and rule ordering
- ✔️ Corrected diagnostic settings to ensure **DNAT logs** were properly collected
- ✔️ Demonstrated a secure way to expose internal workloads through a firewall

This lab successfully reproduces a real-world hub-and-spoke scenario  
used in enterprise Azure environments.

---

## 📘 What I Learned

Here are the main insights I gained during this lab:

- 🔹 **How DNAT works** inside Azure Firewall and why it is essential for secure inbound access  
- 🔹 The difference between **DNAT rules**, **Network rules**, and **Application rules**
- 🔹 Why internal VMs should **not** have Public IPs in secure architectures
- 🔹 How to properly configure the **Firewall Policy** and avoid rule conflicts
- 🔹 That Azure Firewall does *not* log anything by default —  
  **diagnostic settings must be configured correctly**  
- 🔹 How to enable and use **Log Analytics Workspace** to analyze firewall traffic
- 🔹 How to troubleshoot missing firewall logs (legacy vs modern categories)
- 🔹 How to test real inbound flows from an external machine using `FW-Public-IP:50001`

Overall, this lab gave me a deeper understanding of  
**secure inbound connectivity**, **Azure Firewall behavior**, and  
**real-world troubleshooting** in Azure networking.



