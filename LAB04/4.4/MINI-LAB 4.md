# 🔥 MINI-LAB 4 — Scenario (UDR + Force Traffic Through Firewall)

You are working in an environment where:

- A **Hub-VNet** exists containing an **Azure Firewall**.
- A **Workload-VNet** exists with a VM inside it.
- The Hub and Workload VNets are **peered**.
- The VM currently has **direct internet access** via Azure’s default routing (system routes).

## 🟡 What are we trying to achieve?

### 🎯 Goal: **Force ALL outbound traffic from the Workload-VM to go through the Azure Firewall.**

No more direct internet access.

All traffic must pass through:
VM → Workload subnet → UDR → Firewall → Internet

## What do you need to do?

---

### 🟦 1. Create a Route Table (UDR)

<img width="734" height="416" alt="image" src="https://github.com/user-attachments/assets/722e045a-af9c-419f-9739-374da0f71a42" />

---

### 🟦 2. Link the Route Table to the Workload Subnet

This ensures that **all VMs** inside that subnet will use the new route.

<img width="1906" height="420" alt="image" src="https://github.com/user-attachments/assets/297a2b63-74df-41c2-a482-9de1b70f6159" />

<img width="1902" height="934" alt="image" src="https://github.com/user-attachments/assets/c13ea1a9-3111-43ae-842c-522a56f726a2" />


---

### 🟦 3. Check Effective Routes (on the NIC of the Workload VM)

<img width="1128" height="493" alt="image" src="https://github.com/user-attachments/assets/dc5c1bf3-e20a-4515-9bae-b82c60891a6f" />

---

### 🟦 4. Test Traffic

- ❌ First: Try to ping an external IP from the VM or surf to the internet → should **not** work

<img width="1477" height="967" alt="image" src="https://github.com/user-attachments/assets/4c79c4c0-3e2b-4b65-8224-fb03a1982190" />


- ✔️ Then: Add an **outbound rule** on the firewall to Allow Internet

### 📝 How I configured the outbound rule (no screenshot available)

Since I forgot to take a screenshot during this step, here is exactly how I configured the Network Rule Collection in the Azure Firewall Policy:

1. Open **Fw-Policy-Lab4**  
2. Navigate to **Network rules → Add Network Rule Collection**
3. Configure the collection with:
   - **Name:** `Allow-Internet`
   - **Priority:** `100`
   - **Rule type:** `Network`
   - **Action:** `Allow`
4. Add the following rule:
   - **Source:** Workload subnet (`10.20.0.0/24`)
   - **Protocol:** `Any`
   - **Destination:** `*`
   - **Destination ports:** `*`

This rule allowed outbound traffic from my workload VM to reach the internet **only through the Azure Firewall**.

  
- ✔️ Test again  
- ➜ Now traffic works **only** through the firewall

<img width="1479" height="968" alt="image" src="https://github.com/user-attachments/assets/1579e38f-3189-4821-8830-03bc8dffb9ad" />

---

### 🟦 5. Firewall Logs (Diagnostics / Log Analytics Workspace)

Verify that outbound traffic is visible in the firewall logs.

<img width="1875" height="955" alt="image" src="https://github.com/user-attachments/assets/a3a68323-d7ec-494f-927f-9063c701dcd5" />

---

## ✅ Final Result

By the end of this mini-lab:

- The Workload VM no longer had direct internet access.
- All outbound traffic was successfully **forced through the Azure Firewall**.
- After adding the `Allow-Internet` rule, the VM regained internet access — but only **via the firewall**.
- The UDR (`0.0.0.0/0 → Firewall Private IP`) correctly replaced Azure’s default system route.
- Firewall logs in Log Analytics confirmed that all outbound traffic was being inspected.
- The routing design and firewall enforcement worked exactly as intended.

---

## 📘 What I Learned

During this lab, I learned how Azure User Defined Routes (UDRs) influence routing behavior and how they can be used to force traffic through a security appliance.  
Key takeaways:

- How to create a custom route table and associate it with a subnet.
- How UDRs override Azure’s default outbound routing.
- How to use **Effective Routes** on a NIC to troubleshoot routing issues.
- Why outbound traffic fails when no firewall rule allows it.
- How to configure a Network Rule Collection inside an Azure Firewall Policy.
- How outbound connections appear in Log Analytics using AzureDiagnostics.

This lab helped me better understand how organizations control egress traffic and ensure that all outbound flows pass through centralized security controls.


