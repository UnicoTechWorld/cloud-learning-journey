🌐 LAB 01 — Secure Azure VM with NSG

## 🌍 Scenario

You are tasked with deploying a Windows Server VM that must remain secure and isolated.  
To follow best practices for Infrastructure/Cloud administration, the VM must:

1. Be reachable **only via RDP** (TCP/3389) for remote management.
2. Block **all other inbound traffic** using a Network Security Group (NSG).
3. Demonstrate basic Azure VM deployment and firewall configuration.
4. Follow the principle of **least privilege** by exposing only the minimum required port.
--------------------------------------------------

🛠 Steps Performed
1️⃣ Create Resource Group

Name: rg-level1-project1

Region: West Europe

<img width="992" height="506" alt="image" src="https://github.com/user-attachments/assets/d5a3d041-9191-4d6c-81f1-6a2eff3e3409" />

--------------------------------------------------
2️⃣ Deploy Virtual Machine

Name: vm-level1

Image: Windows Server

No inbound ports

<img width="1867" height="495" alt="image" src="https://github.com/user-attachments/assets/c1d2e988-1e73-449d-a442-0e45fc946d01" />

--------------------------------------------------
3️⃣ Create Network Security Group

Name: nsg-level1

<img width="1203" height="142" alt="image" src="https://github.com/user-attachments/assets/fb9daff5-8a4e-4f1f-9580-91c75e028294" />

--------------------------------------------------
4️⃣ Associate NSG to VM's NIC

<img width="1336" height="559" alt="image" src="https://github.com/user-attachments/assets/7d1fa0c6-45a4-4e59-8af9-c781f7638ee4" />

--------------------------------------------------
5️⃣ Configure NSG Inbound Rules

Allow 3389 (priority 100)

Deny all inbound (priority 4000)

<img width="1331" height="499" alt="image" src="https://github.com/user-attachments/assets/7d834616-5835-4224-b9e8-ef4f6d01a3b7" />

--------------------------------------------------
6️⃣ Test RDP

<img width="1376" height="816" alt="image" src="https://github.com/user-attachments/assets/ab22bb98-8fb8-4323-a241-0558f851d01f" />


--------------------------------------------------
✔️ Result

A fully secured Azure VM where:

  -RDP works

  -All other inbound traffic is blocked

  -NSG is correctly applied at NIC level
  
--------------------------------------------------
📚 Skills Learned

  -Azure VM deployment

  -NSG firewall basics

  -Prioritizing rules

  -Public IP configuration

  -NIC & VNet fundamentals

  -RDP connectivity troubleshooting
