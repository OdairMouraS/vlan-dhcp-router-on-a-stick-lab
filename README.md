# vlan-dhcp-router-on-a-stick-lab


# VLAN + DHCP Network Lab (Packet Tracer)

## 📌 Project Overview

This project demonstrates the implementation of a **segmented network using VLANs**, **Router-on-a-Stick**, and **DHCP per VLAN**, simulated in **Cisco Packet Tracer**. The goal was to build a small enterprise-style network where different departments are isolated at Layer 2 but can communicate through Layer 3 routing.

This lab simulates a common real-world scenario used in corporate environments and is aligned with **junior IT support / network technician roles**.

---

## 🧱 Network Topology

* 1 Cisco Router
* 1 Cisco Switch (Layer 2)
* 4 End Devices (PCs)
* Trunk link between Switch and Router

### VLAN Structure

| VLAN ID | Name  | Purpose              |
| ------- | ----- | -------------------- |
| 10      | ADMIN | Administrative users |
| 20      | SALES | Sales department     |

---

## ⚙️ Configuration Summary

### 1️⃣ VLAN Configuration (Switch)

* VLAN 10 (ADMIN)
* VLAN 20 (SALES)
* Access ports assigned per department

```bash
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 10

interface range fa0/3 - 4
 switchport mode access
 switchport access vlan 20
```

---

### 2️⃣ Trunk Configuration (Switch → Router)

```bash
interface fa0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

---

### 3️⃣ Router-on-a-Stick (Inter-VLAN Routing)

```bash
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

---

### 4️⃣ DHCP Configuration per VLAN

```bash
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp excluded-address 192.168.20.1 192.168.20.10

ip dhcp pool ADMIN
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8

ip dhcp pool SALES
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8
```

---

## 🧪 Testing & Validation

### ✔ DHCP Assignment

* PCs in VLAN 10 received IPs in `192.168.10.0/24`
* PCs in VLAN 20 received IPs in `192.168.20.0/24`

### ✔ Connectivity Tests

* PC → Gateway ping: **Success**
* Inter-VLAN ping (ADMIN ↔ SALES): **Success**
* Router → PCs ping: **Success**

These tests confirm proper VLAN segmentation, trunking, DHCP operation, and Layer 3 routing.

---

## 🛠 Tools Used

* Cisco Packet Tracer
* Cisco IOS CLI

---

## 📚 Skills Demonstrated

* VLAN creation and management
* Trunk configuration (802.1Q)
* Router-on-a-Stick
* DHCP server configuration
* Inter-VLAN routing
* Network troubleshooting

---

## 🚀 Next Improvements

* Implement ACLs to control inter-VLAN traffic
* Add NAT and Internet access
* Simulate DNS and Web servers
* Expand topology with multiple switches

---

## 👤 Author

**Odair da Silva Moura**
Computer Networks Student (Final Semester)
Fluent English | Entry-Level IT & Networking
