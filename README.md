# Hotel-Management-Network
Vic Modern Hotel Network - Enterprise Network Design with OSPF, VLANs, DHCP, SSH & Port Security

A complete three-floor hotel network implementation in Cisco Packet Tracer. Each floor has its own router (connected via serial DCE links), switch, and wireless access point. Departments are separated using VLANs with inter-VLAN routing. OSPF handles dynamic routing, DHCP servers assign IP addresses automatically, SSH enables secure remote management, and port security restricts access to the IT department's test PC.

# 🏨 Vic Modern Hotel Network Design

## 📌 Project Overview

This project implements a complete enterprise network for **Vic Modern Hotel** using Cisco Packet Tracer. The hotel has three floors, each with its own router, switch, wireless AP, and multiple departments separated by VLANs.

All devices can communicate with each other across floors using OSPF routing. IP addresses are assigned dynamically via DHCP, and SSH is configured on all routers for secure remote login.

---

## 🏢 Floor & VLAN Mapping

| Floor | Department      | VLAN ID | Subnet           | Devices in Topology        |
|-------|----------------|---------|------------------|----------------------------|
| 1st   | Reception       | 80      | 192.168.8.0/24   | PC1, Reception Printer     |
| 1st   | Store           | 70      | 192.168.7.0/24   | PC3, Store Printer         |
| 1st   | Logistics       | 60      | 192.168.6.0/24   | (configured, ready)        |
| 2nd   | Finance         | 50      | 192.168.5.0/24   | PC2, Fin-Printer           |
| 2nd   | HR              | 40      | 192.168.4.0/24   | PC0                        |
| 2nd   | Sales/Marketing | 30      | 192.168.3.0/24   | SocialMedia PC1, s/m-Printer |
| 3rd   | Admin           | 20      | 192.168.2.0/24   | PC6, Admin-Printer         |
| 3rd   | IT              | 10      | 192.168.1.0/24   | PC7, Test-PC (port fa0/1)  |

---

## 🧱 Network Topology

### Floor 1
- F1-Router → F1-Switch → F1-AP
- VLANs: 60, 70, 80
- Printers: Store-Printer, Reception-Printer
- Wireless: Laptops, Smartphones

### Floor 2
- F2-Router → F2-Switch → F2-AP
- VLANs: 30, 40, 50
- Printers: Fin-Printer, s/m-Printer

### Floor 3
- F3-Router → F3-Switch → F3-AP
- VLANs: 10, 20
- Printers: Admin-Printer
- **Test-PC** connected to F3-Switch port fa0/1 (port security enabled)

### Router-to-Router Connections (Serial DCE)

| Link                    | Network        |
|-------------------------|----------------|
| F1-Router ↔ F2-Router   | 10.10.10.0/30  |
| F2-Router ↔ F3-Router   | 10.10.10.4/30  |
| F1-Router ↔ F3-Router   | 10.10.10.8/30  |

All three routers are placed in the IT department server room (Floor 3).

---

## 🔧 Technologies & Features

| Feature               | Implementation                                   |
|-----------------------|--------------------------------------------------|
| Routing Protocol      | OSPF (advertises all VLANs and serial links)     |
| VLAN Segmentation     | 802.1Q trunking between router and switch       |
| Inter-VLAN Routing    | Router-on-a-stick on each floor                 |
| DHCP                  | Each router configured as DHCP server           |
| Wireless Access       | APs connected to switches (Laptops/Phones)      |
| Remote Management     | SSH version 2 on all routers                    |
| Port Security         | F3-Switch fa0/1 – sticky MAC, shutdown violation|

---

## 🔒 Port Security Configuration (IT Switch - Floor 3)

On **F3-Switch**, port `fa0/1` (connected to Test-PC):

