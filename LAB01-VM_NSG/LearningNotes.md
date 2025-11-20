📘 Learning Notes — LAB01 VM + NSG
----------------------------------------
This file contains the questions I had during the lab, along with the answers and reasoning behind them.

----------------------------------------

❓ Questions I Had During the Lab
1️⃣ What should I choose for Availability Zones?

Answer:
✔️ None (for labs and small test environments)

Reasoning:
Availability Zones are designed for high-availability, production workloads.
They increase cost and complexity and are not needed for practice labs.

----------------------------------------
2️⃣ Which security type should I choose for the VM?

Answer:
✔️ Standard

Reasoning:
Trusted Launch and Confidential VMs are advanced security features that provide additional hardware-based protections (Secure Boot, vTPM, DMA protection).
However, they also introduce more configuration steps and limitations.
For foundational labs, Standard is the simplest and most compatible choice.

----------------------------------------
3️⃣ There is already a default DenyAllInbound rule. Why do I still need my own deny rule?

Answer:
Because Azure evaluates default Allow rules before the default deny.

Azure includes system-defined rules such as:

| Priority | Rule Name                     | Action |
| -------- | ----------------------------- | ------ |
| 65000    | AllowVnetInBound              | Allow  |
| 65001    | AllowAzureLoadBalancerInBound | Allow  |
| 65500    | DenyAllInbound                | Deny   |


Reasoning:

-The system Allow rules (65000 and 65001) are matched before the DenyAllInbound rule.

-This means internal VNet traffic can still be allowed even if you didn't configure it.

-To take full control of inbound traffic, you must create your own explicit deny rule (e.g., priority 4000).

With a custom deny rule:

➡️ You guarantee that only the traffic you allow (3389) reaches the VM

➡️ You take full control instead of relying on system behavior
