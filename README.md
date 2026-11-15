<div align="center">

# 🌐 3-Tier Enterprise Network

**Core • Distribution • Access design built in Cisco Packet Tracer**

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Routing](https://img.shields.io/badge/Routing-OSPF%20Area%200-success?style=for-the-badge)
![VLANs](https://img.shields.io/badge/VLANs-7-orange?style=for-the-badge)
![Devices](https://img.shields.io/badge/Devices-8%20+%20PCs-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)


</div>

---

## 📑 Table of Contents

- [🎯 Overview](#-overview)
- [🗺️ Topology Layers](#️-topology-layers)
- [🏷️ VLAN & IP Plan](#️-vlan--ip-plan)
- [🔗 Inter-Device Links](#-inter-device-links)
- [🖥️ Device List](#️-device-list)
- [⚙️ Configuration Files](#️-configuration-files)
- [🧪 Testing & Verification](#-testing--verification)
- [🚀 How to Open](#-how-to-open)
- [📁 Repository Structure](#-repository-structure)
- [👤 Author](#-author)

---

## 🎯 Overview

| | Feature | Details |
|---|---|---|
| 🏢 | **Design** | 3-tier hierarchical campus network |
| 🔀 | **Routing** | OSPF process 10, Area 0 |
| 🧩 | **Inter-VLAN routing** | SVIs on Layer 3 switches |
| 📶 | **Wi-Fi** | Guest wireless AP on VLAN 60 |
| 🌍 | **Internet** | ISP uplink via `203.113.0.0/30` (test target `8.8.8.8`) |
| 🔒 | **Native VLAN** | VLAN 99 on all trunks |

---

## 🗺️ Topology Layers

| Layer | Icon | Devices | Role |
|-------|:----:|---------|------|
| **Internet / Edge** | 🌍 | ISP (2911), CORE R1 (2911) | WAN uplink and edge routing |
| **Core** | 🔴 | CORE SW1, CORE SW2 (3560-24PS) | High-speed L3 backbone |
| **Distribution** | 🟠 | DIST SW1, DIST SW2 (3560-24PS) | VLAN gateways (SVIs), OSPF |
| **Access** | 🟢 | ACCESS SW2, ACCESS SW3 (2960-24TT) | End-device connectivity |
| **End devices** | 💻 | PCs, AP1-WIRELESS | Users and Wi-Fi clients |

---

## 🏷️ VLAN & IP Plan

| VLAN | Department | Network | Gateway (SVI) |
|:----:|------------|---------|---------------|
| 🟦 **10** | 👥 HR | `192.168.10.0/24` | `192.168.10.1` |
| 🟩 **20** | 💰 Finance | `192.168.20.0/24` | `192.168.20.1` |
| 🟨 **30** | 🛠️ Management | `192.168.30.0/24` | `192.168.30.1` |
| 🟧 **40** | 🖥️ IT | `192.168.40.0/24` | `192.168.40.1` |
| 🟥 **50** | 📈 Sales | `192.168.50.0/24` | `192.168.50.1` |
| 🟪 **60** | 📶 Guest Wi-Fi | `192.168.60.0/24` | `192.168.60.1` |
| ⬜ **99** | 🔐 Native / Management | `192.168.99.0/24` | `192.168.99.1` |

---

## 🔗 Inter-Device Links

| # | From | Port | ➜ | To | Port | Network |
|:-:|------|:----:|:-:|----|:----:|---------|
| 1 | 🌍 ISP | G0/0 | ➜ | 🔀 R1 | G0/0 | `203.0.113.0/30` |
| 2 | 🔀 R1 | G0/0 | ➜ | 🔴 CORE SW1 | G0/1 | `10.0.0.0/30` |
| 3 | 🔀 R1 | G0/2 | ➜ | 🔴 CORE SW2 | G0/1 | `10.0.0.4/30` |
| 4 | 🔴 CORE SW1 | G0/2 | ➜ | 🔴 CORE SW2 | G0/2 | `10.2.0.0/30` |
| 5 | 🔴 CORE SW1 | G0/3 | ➜ | 🟠 DIST SW1 | G0/1 | `10.1.0.0/30` |
| 6 | 🔴 CORE SW2 | G0/3 | ➜ | 🟠 DIST SW2 | G0/1 | `10.1.4.0/30` |

---

## 🖥️ Device List

| Icon | Name | Model | Role |
|:----:|------|-------|------|
| 🌍 | ISP | 2911 | ISP router |
| 🔀 | CORE R1 | 2911 | Edge / core router |
| 🔴 | CORE SW1 | 3560-24PS | Core switch 1 (L3) |
| 🔴 | CORE SW2 | 3560-24PS | Core switch 2 (L3) |
| 🟠 | DIST SW1 | 3560-24PS | Distribution switch 1 |
| 🟠 | DIST SW2 | 3560-24PS | Distribution switch 2 |
| 🟢 | ACCESS SW2 | 2960-24TT | Access switch (IT / Sales) |
| 🟢 | ACCESS SW3 | 2960-24TT | Access switch (HR / Finance) |
| 📶 | AP1-WIRELESS | AccessPoint-PT | Wireless AP (VLAN 60) |
| 💻 | PCs | PC-PT | End devices |

---

## ⚙️ Configuration Files

Apply them in this order. Click a device to expand its config.

| Step | Device | File |
|:----:|--------|------|
| 1️⃣ | ISP | [`configs/01-ISP.txt`](configs/01-ISP.txt) |
| 2️⃣ | CORE R1 | [`configs/02-CORE-R1.txt`](configs/02-CORE-R1.txt) |
| 3️⃣ | CORE SW1 | [`configs/03-CORE-SW1.txt`](configs/03-CORE-SW1.txt) |
| 4️⃣ | CORE SW2 | [`configs/04-CORE-SW2.txt`](configs/04-CORE-SW2.txt) |
| 5️⃣ | DIST SW1 | [`configs/05-DIST-SW1.txt`](configs/05-DIST-SW1.txt) |
| 6️⃣ | DIST SW2 | [`configs/06-DIST-SW2.txt`](configs/06-DIST-SW2.txt) |
| 7️⃣ | ACCESS SW2 | [`configs/07-ACCESS-SW2.txt`](configs/07-ACCESS-SW2.txt) |
| 8️⃣ | ACCESS SW3 | [`configs/08-ACCESS-SW3.txt`](configs/08-ACCESS-SW3.txt) |

<details>
<summary>🔀 <b>Example: CORE R1 config</b> (click to expand)</summary>

```
enable
conf t
hostname CORE R1
interface g0/0
 ip address 203.0.113.2 255.255.255.252
 no shut
interface g0/2
 ip address 10.0.0.6 255.255.255.252
 no shut
router ospf 10
 network 10.0.0.0 0.0.0.3 area 0
 network 10.0.0.4 0.0.0.3 area 0
exit
```
</details>

<details>
<summary>🟢 <b>Example: ACCESS SW2 config</b> (click to expand)</summary>

```
enable
conf t
hostname ACCESS SW2
vlan 40
 name IT
vlan 50
 name SALES
vlan 60
 name GUEST
vlan 99
 name MANAGEMENT
interface g0/1
 switchport mode trunk
 switchport trunk allowed vlan 40,50,60,99
 switchport trunk native vlan 99
interface range g0/2-24
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
```
</details>

---

## 🧪 Testing & Verification

### 🔍 Useful commands

```
show ip route
show ip ospf neighbor
show ip ospf interface brief
show vlan brief
```

### ✅ Checklist

- [x] 🟢 All interfaces are **up/up**
- [x] 🤝 OSPF neighbors form between R1, Core and Distribution switches
- [x] 📡 PCs get correct IPs from DHCP (if configured)
- [x] 🏷️ All VLANs can reach their gateways
- [x] 🔁 PCs can ping other VLANs
- [x] 🌍 PCs can ping `8.8.8.8` (Internet)
- [x] 📶 Wireless clients (VLAN 60) can access the network

---

## 🚀 How to Open

1. 📥 Install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
2. ⬇️ Download [`3-Tier_EN.pkt`](3-Tier_EN.pkt)
3. 📂 Double-click it, or go to **File ➜ Open**
4. ▶️ Switch to **Simulation** or **Realtime** mode and test the pings

---

## 📁 Repository Structure

```
📦 3-tier-enterprise-network
 ┣ 📜 README.md
 ┣ 🧩 3-Tier_EN.pkt        ← Packet Tracer project
 ┣ 📂 images
 ┃ ┗ 🖼️ topology.png
 ┗ 📂 configs
   ┣ 📄 01-ISP.txt
   ┣ 📄 02-CORE-R1.txt
   ┣ 📄 03-CORE-SW1.txt
   ┣ 📄 04-CORE-SW2.txt
   ┣ 📄 05-DIST-SW1.txt
   ┣ 📄 06-DIST-SW2.txt
   ┣ 📄 07-ACCESS-SW2.txt
   ┗ 📄 08-ACCESS-SW3.txt
```

---

## 👤 Author

**Shane Steve** · [GitHub](https://github.com/steve3301)

<div align="center">

⭐ If this project helped you, give it a star! ⭐

</div>
