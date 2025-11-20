Project 1 – Deploy a secure Windows VM in Azure
Goal: Provide a VM accessible via RDP while blocking all other inbound traffic.

✔️ Steps Completed

Created a Resource Group

Deployed a Windows Server VM (no open inbound ports)

Created a Network Security Group (NSG)

Associated the NSG with the VM’s NIC

Configured inbound rules:

Allow TCP/3389 (RDP)

Deny all other inbound traffic

Tested RDP successfully
