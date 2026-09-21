# 🚀 Multi-VLAN  Enterprise Network Infrastructure Design & Verification

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-v8.x-blue?style=for-the-badge&logo=cisco)
![Network Architecture](https://img.shields.io/badge/Architecture-Enterprise%20Multi--VLAN-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Verified%20%26%20Tested-success?style=for-the-badge)

## 📌 Project Overview
This project presents a scalable, redundant, and highly available **Enterprise Network Infrastructure** designed and implemented using **Cisco Packet Tracer**. It simulates a complete multi-department corporate environment featuring segmented VLANs, Layer 3 Inter-VLAN routing, dynamic link aggregation, OSPF routing, enterprise wireless connectivity, and centralized network services (DHCP, DNS, Web).

---

## 🏗️ Topology & Architectural Highlights

- **Core & Distribution Layer:** Driven by Multilayer Switches (3560 Series) using Switch Virtual Interfaces (SVI) to achieve full wire-speed Inter-VLAN routing.
- **Access Layer:** Layer 2 Switches (2960 Series) enforcing strict VLAN segmentation to isolate departmental broadcast domains.
- **Redundancy & Aggregation:** EtherChannel (LACP/PAgP) configured on core trunk links for dynamic bandwidth scaling and fault-tolerant link redundancy.
- **Dynamic Routing:** OSPF routing protocol deployed for automated route discovery across Core Routers and L3 Switches.
- **Centralized Enterprise Services:** Isolated Server Room hosting centralized DHCP (with L3 Relay Agent), DNS Server, and HTTP Web Server.
- **Wireless Infrastructure:** Enterprise Access Points providing secure wireless connectivity for Admin and Staff segments.

---

## 🛠️ Key Technologies & Protocols

| Protocol / Technology | Implementation Details |
| :--- | :--- |
| **VLSM & Subnetting** | Custom `/28` & `/30` subnets for IPv4 address optimization. |
| **802.1Q VLAN Trunking** | 12+ segmented VLANs for departmental isolation across access switches. |
| **Inter-VLAN Routing** | Hardware-accelerated SVI routing on Multilayer Switches with `ip routing`. |
| **EtherChannel (LACP)** | Multi-link aggregation ensuring higher throughput and link failure backup. |
| **OSPF Dynamic Routing** | Single-area OSPF for seamless routing between L3 switches and core routers. |
| **DHCP Relay Agent** | Centralized DHCP allocation using `ip helper-address` on SVI gateways. |
| **DNS & Web Hosting** | Local domain name resolution (`www.lab.com`) pointing to the local Web Server. |
| **Enterprise Wi-Fi** | Secure WPA2-PSK Access Points integrated with local subnets. |

---

## 📊 Subnetting & VLAN Addressing Table

| VLAN ID | Department / Zone | IP Subnet | Default Gateway (SVI) | Subnet Mask |
| :---: | :--- | :--- | :--- | :--- |
| **10** | GUEST | `192.168.1.0/28` | `192.168.1.1` | `255.255.255.240` |
| **20** | STAFF | `192.168.1.16/28` | `192.168.1.17` | `255.255.255.240` |
| **30** | SALES | `192.168.1.32/28` | `192.168.1.33` | `255.255.255.240` |
| **40** | FINANCE | `192.168.1.48/28` | `192.168.1.49` | `255.255.255.240` |
| **50** | HR | `192.168.1.64/28` | `192.168.1.65` | `255.255.255.240` |
| **60** | OPERATIONS | `192.168.1.80/28` | `192.168.1.81` | `255.255.255.240` |
| **70** | MARKETING | `192.168.1.96/28` | `192.168.1.97` | `255.255.255.240` |
| **80** | IT | `192.168.1.112/28` | `192.168.1.113` | `255.255.255.240` |
| **90** | ENGINEERING | `192.168.1.128/28` | `192.168.1.129` | `255.255.255.240` |
| **100** | ELECTRIC | `192.168.1.144/28` | `192.168.1.145` | `255.255.255.240` |
| **110** | ADMIN | `192.168.1.160/28` | `192.168.1.161` | `255.255.255.240` |
| **120** | SERVER ROOM | `192.168.1.176/28` | `192.168.1.177` | `255.255.255.240` |

---

## ⚙️ Essential CLI Configuration Snippets

<details>
<summary><b>1. Layer 3 Switch Inter-VLAN Routing & DHCP Relay</b></summary>

```text
MultilayerSwitch# configure terminal
MultilayerSwitch(config)# ip routing
MultilayerSwitch(config)# vlan 120
MultilayerSwitch(config-vlan)# name SERVER_ROOM
MultilayerSwitch(config-vlan)# exit

MultilayerSwitch(config)# interface vlan 120
MultilayerSwitch(config-if)# ip address 192.168.1.177 255.255.255.240
MultilayerSwitch(config-if)# no shutdown

MultilayerSwitch(config)# interface vlan 110
MultilayerSwitch(config-if)# ip address 192.168.1.161 255.255.255.240
MultilayerSwitch(config-if)# ip helper-address 192.168.1.178
MultilayerSwitch(config-if)# no shutdown
```
</details>

<details>
<summary><b>2. Trunking & EtherChannel Configuration</b></summary>

```text
MultilayerSwitch(config)# interface range FastEthernet 0/4 - 5
MultilayerSwitch(config-if-range)# switchport trunk encapsulation dot1q
MultilayerSwitch(config-if-range)# switchport mode trunk
MultilayerSwitch(config-if-range)# channel-group 1 mode active
MultilayerSwitch(config-if-range)# no shutdown
```
</details>

---

## ✅ Verification & Testing Results

- **Dynamic IP Allocation:** Verified across all VLANs via DHCP Relay Agent (`ip helper-address`).
- **End-to-End Connectivity:** ICMP ping verified from all host subnets to the Server Room (`192.168.1.178`).
- **DNS & Web Services:** End-user browser testing confirms successful HTTP web page loading using `www.lab.com`.
- **Trunk & EtherChannel Health:** Confirmed operational state via `show etherchannel summary` and `show interface trunk`.

---

## 👤 Author
**Yadigarzade Ceyhun**
- **Project:** Wireless Enterprise Networking Lab
- **Environment:** Cisco Packet Tracer v8.x
```
