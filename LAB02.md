🌐 LAB 02 — Deploy Azure VM with VNet + Subnet + NSG + Bastion (or RDP)

## 🌍 Scenario

You are working in the **Infra/Cloud team**.

An internal application needs to be tested on an isolated Windows Server.  
For this task, you must:

1. Create a **dedicated network** (VNet + Subnet).
2. Configure a **strict firewall** (NSG):
   - Allow RDP (TCP/3389)
   - Block all other inbound traffic
3. Deploy a **Windows Server VM**.
4. Securely connect to the machine using **RDP** or **Azure Bastion** (recommended).
--------------------------------------------------

## 🛠 Steps Performed


☑️ Create Resource Group  
Name: Lab02-RG  
Region: West Europe  

<img width="784" height="143" alt="image" src="https://github.com/user-attachments/assets/e86d7177-46f0-4fa2-8ad2-9c440c677344" />


--------------------------------------------------
☑️ Create Virtual Network  
Name: lab02-vnet  
Address space: 10.0.0.0/16  

☑️ Create Subnet  
Name: vm-subnet  
Address range: 10.0.1.0/24  


<img width="690" height="712" alt="image" src="https://github.com/user-attachments/assets/f891cc36-e4aa-49bd-b2c0-b8db041a26fb" />

--------------------------------------------------
☑️ Create Network Security Group  
Name: lab02-nsg  
Inbound rule:  
- Name: Allow-RDP  
- Port: 3389 (TCP)  
- Priority: 100  
- Source: Any  

<img width="472" height="380" alt="image" src="https://github.com/user-attachments/assets/5a4fed98-2c14-4e55-8724-8aaa9f495aaa" />

<img width="1903" height="472" alt="image" src="https://github.com/user-attachments/assets/2d078bfb-9b35-4347-9cda-ee63381660e8" />


--------------------------------------------------
☑️ Associate NSG to Subnet  
Subnet: vm-subnet  
Associated NSG: lab02-nsg  

<img width="1364" height="624" alt="image" src="https://github.com/user-attachments/assets/b1334254-820a-4e22-942e-75545b886e75" />


--------------------------------------------------
☑️ Deploy Virtual Machine  
Name: lab02-vm  
Image: Windows Server 2022 Datacenter  
VNet/Subnet: lab02-vnet / vm-subnet  

<img width="1889" height="1005" alt="image" src="https://github.com/user-attachments/assets/d1a27e7f-f03c-4382-8d70-25152f31d9db" />



--------------------------------------------------
☑️ Deploy Azure Bastion  
Name: lab02-bastion  
Subnet: AzureBastionSubnet 
Connection: RDP over port 3389 via browser

<img width="1742" height="985" alt="image" src="https://github.com/user-attachments/assets/f59c8750-aded-43c3-9a2b-ba30c9fb7363" />


--------------------------------------------------------------

✔️ Result

A fully secured Azure environment where:

- The VM is deployed inside a custom VNet & subnet  
- RDP works securely through Azure Bastion  
- No public IP exposure  
- NSG correctly blocks all inbound traffic except RDP  
- Network segmentation and security are configured at subnet level

--------------------------------------------------------------

🎓 Skills Learned

- Creating VNets and Subnets
- Planning address spaces (CIDR)
- Building and configuring NSGs
- Understanding inbound/outbound rules & priorities
- Subnet-level security best practices
- Deploying Windows Server 2022 in Azure
- Using Azure Bastion for secure RDP access
- Network and VM connectivity validation
- Zero Trust access principles in practice

--------------------------------------------------------------
