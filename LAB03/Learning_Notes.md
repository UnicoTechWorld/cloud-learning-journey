# 📘 Learning Notes — LAB03

This file contains the questions I had during the lab, along with the answers and the reasoning behind them.

---

## ❓ Q1 — Why couldn’t I RDP into my VM? (My reasoning process)

During this lab, I initially struggled to connect to my VM using RDP.  
Here is the exact reasoning path I followed to identify the root cause:

### 1. I received an RDP connection error  
Remote Desktop could not connect to my VM.

<img width="562" height="220" alt="image" src="https://github.com/user-attachments/assets/e4ff459c-3c3e-484e-9184-c912fc49b098" />

### 2. I remembered that I selected **“Public inbound ports: None”** during VM creation  
This meant Azure didn’t automatically open RDP (port 3389).

### 3. I assumed there was **no NSG** because I didn’t manually configure one  
But this assumption turned out to be incorrect.

### 4. After checking the VM’s “Networking” tab, I noticed Azure **automatically created an NSG** on the NIC  
Even if you don’t select an NSG during deployment, Azure assigns a default one when a public IP is present.

<img width="1209" height="443" alt="image" src="https://github.com/user-attachments/assets/d2aefe02-22af-480f-aceb-fcfcb012019b" />

### 5. I checked the NSG rules and noticed there was **no rule allowing RDP**  
The NSG only contained:
- AllowVnetInBound  
- AllowAzureLoadBalancerInBound  
- **DenyAllInBound** (this blocks all traffic unless explicitly allowed)

<img width="949" height="341" alt="image" src="https://github.com/user-attachments/assets/8ad1a75d-3f66-4b88-816e-c4f72fb93ab4" />

### 6. I realized RDP comes from outside the VNet  
So it was hitting the **DenyAllInBound** rule and getting blocked.

### 7. I concluded that I needed to add an inbound RDP rule  

After adding an inbound rule for port 3389, RDP worked immediately


### ✅ Summary

I discovered the issue through my own reasoning:

- No inbound ports selected → no RDP rule  
- Azure still created a default NSG  
- Default NSG blocked all inbound connections  
- Without an explicit RDP rule, RDP was denied  
- Adding a custom inbound RDP rule fixed the issue  
