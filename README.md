# CMPG 325 — Computer Networks: Individual Project

**Project ID:** CMPG325-2026-043  
**Student Name:** MAMPO, EXCELLENCY  
**Student Number:** 35987774  
**Client Organisation:** Leeto Freight & Logistics (Mahikeng)  
**Industry:** Logistics  
**Assigned IP Addressing Block:** `172.30.20.0/23`  

---

## 1. Project Overview & Milestone 1: Client Design Review

This repository contains the design, IP addressing scheme, and implementation files for the Leeto Freight & Logistics computer network simulation built in Cisco Packet Tracer.

### Key Requirements & Constraints
* **Assigned Networking Challenge:** Wireless Security (WPA2-PSK hardening with optional Enterprise extension).
* **Design Constraint:** Pre-allocate logical and physical resources for a new department to be added next year.
* **Client Change Request (CR5):** User numbers grow by 25%. The IP addressing scheme must absorb this expansion without requiring network re-numbering.
* **Physical Topology:** Star Topology (Hub-and-Spoke model centered on core switching infrastructure).

---

## 2. Physical & Logical Network Design

### Physical Star Topology Structure
The physical architecture follows a central Star Topology layout:
* **Central Hub:** Core Switch (`SW-Core-01`) directly linked to the edge router (`RTA-Mahikeng-Core`).
* **Spoke Access Nodes:**
  * `SW-Logistics-01` & Wireless Access Point (`WAP-Logistics`) — Warehouse & Operations.
  * `SW-Admin-01` — Administration & Finance.
  * `SW-IT-01` — IT Infrastructure, Management PCs, and Servers (DHCP/DNS/Web).
  * `SW-Future-01` — Pre-provisioned trunk port/switch reserved for next year's department expansion.

### Logical VLAN Segmentation
* **VLAN 10 (Management & IT):** Switches, router management interfaces, and administrative servers.
* **VLAN 20 (Logistics & Operations):** Warehouse tracking terminals, handheld scanners, and hardened WPA2-PSK WAPs.
* **VLAN 30 (Administration & Finance):** General office workstations and shared network printers.
* **VLAN 40 (Drivers & Guest Wi-Fi):** Isolated access point for delivery drivers and contractors.
* **VLAN 50 (Future Department):** Pre-assigned logical VLAN ID and sub-interface reserved for annual expansion.

---

## 3. IP Addressing Plan (VLSM with +25% CR5 Growth Absorption)

* **Base Subnet:** `172.30.20.0/23` (Total IP Pool: `172.30.20.0` – `172.30.21.255`)

| Subnet / VLAN | Base Hosts | +25% CR5 Growth | Subnet Mask | CIDR | Usable IP Range | Network / Broadcast Address |
| :--- | :---: | :---: | :--- | :---: | :--- | :--- |
| **VLAN 20: Logistics & Ops** | 80 | 100 | `255.255.255.128` | `/25` | `172.30.20.1` – `172.30.20.126` | `172.30.20.0` / `172.30.20.127` |
| **VLAN 30: Admin & Finance** | 40 | 50 | `255.255.255.192` | `/26` | `172.30.20.129` – `172.30.20.190` | `172.30.20.128` / `172.30.20.191` |
| **VLAN 10: IT & Core Infrastructure** | 20 | 25 | `255.255.255.224` | `/27` | `172.30.20.193` – `172.30.20.222` | `172.30.20.192` / `172.30.20.223` |
| **VLAN 40: Drivers / Guest Wi-Fi** | 20 | 25 | `255.255.255.224` | `/27` | `172.30.20.225` – `172.30.20.254` | `172.30.20.224` / `172.30.20.255` |
| **VLAN 50: Reserved New Department** | 60 | 75 | `255.255.255.128` | `/25` | `172.30.21.1` – `172.30.21.126` | `172.30.21.0` / `172.30.21.127` |
| **Unallocated / Reserve Block** | — | — | `255.255.255.128` | `/25` | `172.30.21.129` – `172.30.21.254` | `172.30.21.128` / `172.30.21.255` |

---

## 4. Repository Structure

```text
├── README.md
├── 01-Requirements/
│   └── Client_Brief_Summary.md
├── 02-Design-and-Addressing/
│   ├── Physical_Star_Topology.png
│   ├── Logical_VLAN_Topology.png
│   └── IP_Addressing_Plan.xlsx
├── 03-PacketTracer/
│   └── Leeto_Freight_Star_Network.pkt
└── 04-Evidence-and-Testing/

# Leeto Freight and Logistics Network Implementation
**Course:** CMPG 325 - Computer Networks  
**Student:** K E Mampo (35987774)  
**Date:** October 2, 2026[cite: 1, 4]  
**Repository:** [cmpg325-Project-milestone-1](https://github.com/mampokgotlaetsle-ship-it/cmpg325-Project-milestone-1.git)[cite: 1]

---

## Milestone 2: Client Implementation & Verification Review

### 1. Executive Summary
Milestone 2 transitions the initial conceptual design into a fully functional Cisco Packet Tracer simulation for **Leeto Freight and Logistics**[cite: 1, 4]. The topology follows a central **Hierarchical Star Architecture** with segmented logical traffic, inter-VLAN routing, link aggregation (EtherChannel), and wireless security hardening[cite: 1, 2, 3].

---

### 2. Physical & Logical Topology Overview

#### Physical Star Architecture
- **Central Core Node:** `SW-Core-01` directly linked to edge router `RTA-Mahikeng-Core`.
- **Spoke Access Switch Nodes:**
  - `SW-IT-01` — Core servers (DHCP, DNS, Web) and network administration.
  - `SW-Logistics-01` — Warehouse floor terminals, tracking devices, and wireless access point (`WAP-Logistics`)[cite: 1].
  - `SW-Admin-01` — Workstations for administrative and finance staff[cite: 1].
  - `SW-Future-01` — Pre-provisioned switch trunk reserved for next year's expansion[cite: 1].

#### Logical VLAN Segmentation & VLSM Addressing Scheme (`172.30.20.0/23` Base)[cite: 1]

| Department / VLAN | Assigned CIDR | Subnet Mask | Usable IP Range | Network / Broadcast Address |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 20:** Logistics & Ops | `/25` | `255.255.255.128` | `172.30.20.1 – 172.30.20.126` | `172.30.20.0 / 172.30.20.127` |
| **VLAN 30:** Admin & Finance | `/26` | `255.255.255.192` | `172.30.20.129 – 172.30.20.190` | `172.30.20.128 / 172.30.20.191` |
| **VLAN 10:** IT & Infrastructure | `/27` | `255.255.255.224` | `172.30.20.193 – 172.30.20.222` | `172.30.20.192 / 172.30.20.223` |
| **VLAN 40:** Drivers / Guest Wi-Fi | `/27` | `255.255.255.224` | `172.30.20.225 – 172.30.20.254` | `172.30.20.224 / 172.30.20.255` |
| **VLAN 50:** Future Expansion | `/25` | `255.255.255.128` | `172.30.21.1 – 172.30.21.126` | `172.30.21.0 / 172.30.21.127` |

---

### 3. Implemented Core Configurations

#### A. Router-on-a-Stick Inter-VLAN Routing (`RTA-Mahikeng-Core`)[cite: 1]
```text
enable
configure terminal
hostname RTA-Mahikeng-Core

interface GigabitEthernet0/0/0
 no shutdown

interface GigabitEthernet0/0/0.10
 encapsulation dot1Q 10
 ip address 172.30.20.193 255.255.255.224

interface GigabitEthernet0/0/0.20
 encapsulation dot1Q 20
 ip address 172.30.20.1 255.255.255.128

interface GigabitEthernet0/0/0.30
 encapsulation dot1Q 30
 ip address 172.30.20.129 255.255.255.192

interface GigabitEthernet0/0/0.40
 encapsulation dot1Q 40
 ip address 172.30.20.225 255.255.255.224

interface GigabitEthernet0/0/0.50
 encapsulation dot1Q 50
 ip address 172.30.21.1 255.255.255.128
end
