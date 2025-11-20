# 🚀 LAB 03 — VNet Peering + Multi-Subnet Architecture (Frontend ↔ Backend)

## 🎯 Scenario
You are tasked with building a simple two-tier application architecture:
- A **frontend server** in one VNet  
- A **backend server** in a separate VNet  
- The two networks must be isolated  
- BUT still able to communicate using **private IP addresses only**  
- Communication is enabled using **VNet Peering**

This lab simulates a real production environment where frontend and backend workloads live in separate networks for security.

---

## 🛠 Steps Performed

## 📌 Step 1 — Create the Resource Group

<img width="407" height="122" alt="image" src="https://github.com/user-attachments/assets/b5a1fbc7-6b94-4bfa-96c9-879a9e3bb154" />

## 📌 Step 2 — Create VNet-A (Frontend)

<img width="450" height="330" alt="image" src="https://github.com/user-attachments/assets/7e1ee0d0-1e14-4005-80e2-d91b5a671035" />

## 📌 Step 3 — Create VNet-B (Backend)

<img width="389" height="331" alt="image" src="https://github.com/user-attachments/assets/67477eed-dfa7-4350-83ba-db9e838fbc9e" />

## 📌 Step 4 — Deploy VM1 in Frontend Subnet

<img width="636" height="311" alt="image" src="https://github.com/user-attachments/assets/0370d6b3-694f-4aa0-a13c-34701c485c19" />

## 📌 Step 5 — Deploy VM2 in Backend Subnet

<img width="631" height="327" alt="image" src="https://github.com/user-attachments/assets/eb69abfe-f6c9-4d62-987a-29854c2f2bbd" />

## 📌 Step 6 — Configure VNet Peering (Both Directions)

<img width="1046" height="911" alt="image" src="https://github.com/user-attachments/assets/1e540bfc-e484-48bd-9dfe-b237b3519663" />

<img width="1894" height="406" alt="image" src="https://github.com/user-attachments/assets/77f0413c-00c3-45ea-b8e2-c76cabcf153b" />

<img width="1855" height="357" alt="image" src="https://github.com/user-attachments/assets/f35d88fa-fac7-4ab7-9941-07a72bef16b2" />

## 📌 Step 7 — Test Connectivity Between the Two VMs

<img width="691" height="245" alt="image" src="https://github.com/user-attachments/assets/7985b310-74df-432e-b435-3e0faf6cec32" />

