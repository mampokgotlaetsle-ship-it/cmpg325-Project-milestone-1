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
