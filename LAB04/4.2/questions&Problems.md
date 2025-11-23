## 🔧 RDP Troubleshooting — Short Summary (What caused it & how I fixed it)

**Problem:**  
I was unable to RDP into my VM, even though the NIC-NSG had an inbound allow rule for TCP 3389.  
Every attempt resulted in a *timeout*.

**Root Cause:**  
I had applied a **UDR `0.0.0.0/0 → Firewall`** on the WorkloadSubnet.  
This forced **all** traffic (including inbound RDP return traffic) to go **through the firewall**.

But the firewall only had **outbound network rules**, no inbound RDP rule.  
So the firewall **dropped the return traffic**, causing RDP to fail.

**Fix (Option I used): DNAT**  
I configured DNAT so the firewall correctly handles inbound RDP:

- Associated a **Public IP** to the Firewall  
- Created a **DNAT rule**:
  - `Firewall-PIP:3389 → VM-PrivateIP:3389`
- Connected using the **firewall’s public IP**, *not* the VM public IP

**Result:**  
RDP worked again because inbound RDP was now explicitly forwarded by the firewall, and the return path was allowed.

