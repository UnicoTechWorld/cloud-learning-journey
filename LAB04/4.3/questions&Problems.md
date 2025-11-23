## ❓ Questions / Problems Encountered

### 🔸 1. I could not see any DNAT logs at first
When I opened the Log Analytics Workspace and ran my query,  
I saw **zero results**, even though DNAT was clearly working.

This was confusing at first, because my DNAT rule was correct  
and the RDP test was successful.

<img width="1346" height="521" alt="image" src="https://github.com/user-attachments/assets/21aa4acf-f8d2-482a-834c-4f1b390a8860" />


#### ✔️ Root cause
I had only enabled the **legacy diagnostic categories**  
inside the Azure Firewall Diagnostic Settings:

- Azure Firewall Application Rule (Legacy)
- Azure Firewall Network Rule (Legacy)
- Azure Firewall DNS Proxy (Legacy)

These categories **do NOT include DNAT logging**,  
so the firewall was not sending DNAT logs to the workspace at all.

<img width="694" height="474" alt="image" src="https://github.com/user-attachments/assets/474d4ae9-dc33-44bf-ac6c-14c21f925d15" />


#### ✔️ How I solved it
I edited the diagnostic settings and enabled the **new** firewall log categories:

- **Azure Firewall Nat Rule**  ← (required for DNAT)
- Azure Firewall Network Rule
- Azure Firewall Application Rule
- Azure Firewall Nat Rule Aggregation (Policy Analytics)

<img width="1162" height="971" alt="image" src="https://github.com/user-attachments/assets/9e0ffbbd-0714-4166-b536-b483d6a24d54" />


After saving the updated diagnostic settings,  
I waited a few minutes and ran my query again.

This time, the DNAT logs appeared immediately.

<img width="1663" height="504" alt="image" src="https://github.com/user-attachments/assets/93834420-123f-4915-bfbb-6e3f31e2de59" />

<img width="1599" height="371" alt="image" src="https://github.com/user-attachments/assets/fca3b4f8-2e6c-427d-8753-06586e8bfc54" />


#### ✔️ Why this happens
Azure Firewall does not log to Log Analytics by default.  
If you only enable the legacy categories, DNAT traffic is not captured.  
You must enable the **modern diagnostic categories** for DNAT to show up.
