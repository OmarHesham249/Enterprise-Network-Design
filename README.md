# 🌐 Multi-Branch Enterprise Network Design & Implementation

> A large-scale enterprise network connecting 4 geographical branches, built and simulated using **Cisco Packet Tracer v8.2.2**

---

## 🗺️ Network Topology

![Network Topology](https://github.com/OmarHesham249/Enterprise-Network-Design/blob/main/Network%20Topology.png)

> *Place your Packet Tracer topology screenshot here*

---

## 📋 Project Overview

This project represents the comprehensive design, implementation, and documentation of a full enterprise network infrastructure. The topology connects multiple branches across different geographical areas while providing centralized services, high availability, and secure manageable access.

| Detail | Info |
|--------|------|
| 🛠️ Tool | Cisco Packet Tracer v8.2.2 |
| 📍 Branches | Cairo · Alexandria · Zagazig · Port Said |
| 🏗️ Architecture | Multi-Area OSPF (3 Areas) |
| 👥 Team | Omar Hesham · Ahmed Mahmoud |
| 👨‍🏫 Supervisor | Eng. Ekram |

---

## ⚙️ Core Technologies

### 🔀 Routing — Multi-Area OSPF
- **Area 0** (Backbone) — core of the network
- **Area 1** — Alexandria & Zagazig branches
- **Area 2** — Cairo & Port Said branches
- ABRs handle route summarization to reduce overhead and speed up convergence

### 🔌 Network Segmentation — VLANs & ROAS
Each branch is segmented into 4 departmental VLANs:

| VLAN | Department |
|------|-----------|
| 10 | IT |
| 20 | Sales |
| 30 | HR |
| 40 | Marketing |

- Inter-VLAN routing via **Router-on-a-Stick (802.1Q sub-interfaces)**
- Dedicated **Native VLAN (60)** per branch trunk link
- All VLAN subnets advertised into OSPF for full enterprise-wide reachability

### 🔁 High Availability & Redundancy

**HSRP (Hot Standby Router Protocol)**
- Virtual gateway IP presented to end devices
- Automatic failover if the primary router goes down
- Priority `105` + preempt configured on active routers

**EtherChannel (Link Aggregation)**
- Physical links bundled into logical Port-Channels between switches
- Provides fault tolerance and increased bandwidth
- Configured using **LACP (mode active)**

### 🖥️ Centralized Services

**DHCP Server (Area 0)**
- Separate IP pool per VLAN per branch
- `ip helper-address` configured on all sub-interfaces as DHCP relay agents

**AAA / RADIUS Server**
- Centralized authentication for all routers and switches
- Routers: RADIUS enforced on both `line con 0` and `line vty`
- Switches: RADIUS enforced on `line vty`
- Local `admin` account configured as fallback

**FTP Server (Area 0)**
- Central repository for configuration backups
- Routers and switches push configs via `copy startup-config ftp`

### 🔒 Security & Public Access

**Static NAT**
- Internal Web Server: `10.10.10.2` (private)
- Public IP: `50.50.50.2`
- Configured on edge router (Router 11) with `ip nat inside / outside`

**SSH (Secure Shell)**
- Enabled on all routers and switches
- Replaces insecure Telnet
- Integrated with RADIUS for centralized authentication

---

## 🔐 Access Credentials

> ⚠️ *For lab/simulation use only*

| Method | Username | Password |
|--------|----------|----------|
| AAA (RADIUS) | `omar` | `123` |
| Local Fallback | `admin` | `123` |
| Enable Password | — | `123` |
| FTP | `omar` | `123` |

---

## 🏢 Branch Summary

| Branch | OSPF Area | Router IPs (Serial) |
|--------|-----------|---------------------|
| Alexandria | Area 1 | `11.11.11.2` / `11.11.11.6` |
| Zagazig | Area 1 | `20.20.20.2` / `20.20.20.6` |
| Port Said | Area 2 | `30.30.30.2` / `30.30.30.6` |
| Cairo | Area 2 | `40.40.40.2` / `40.40.40.6` |

---

## 📝 Important Notes

- **Initial ping timeouts** are expected — ARP and STP need time to converge on first boot
- **Packet Tracer instability**: the simulator may occasionally fail to reload saved configs after a crash; this is a known tool limitation, not a design failure
- All devices have been **fully configured and tested** — end-to-end connectivity and all services are verified as operational

---

## 👥 Team

<table>
  <tr>
    <td align="center"><b>Omar Hesham Mohamed Elhady</b></td>
    <td align="center"><b>Ahmed Mahmoud Amer</b></td>
  </tr>
</table>

**Supervised by:** Eng. Ekram

---

<p align="center">
  Made with 💙 as part of the CCNA Final Project — ITI
</p>
