# cisco_packet_tracer_project
# Enterprise Network Architecture & Design (Cisco Packet Tracer)

A comprehensive, large-scale enterprise network simulation designed in Cisco Packet Tracer. This project demonstrates high-availability routing, structured LAN segmentation, end-user mobility, centralized server infrastructure, and robust administrative access controls.

---

## 🌐 Network Topology Overview

The infrastructure simulates a multi-department enterprise environment with the following hardware footprint:
* **Core/Distribution Routing:** 10 Cisco Routers running Dynamic Routing.
* **Access Layer Switches:** 10 Managed Switches facilitating wired connectivity.
* **Wired Endpoints:** 50 Host PCs (Distributed evenly with 5 PCs per Switch).
* **Wireless Infrastructure:** 1 Home/Enterprise Wireless Router supporting 10 Mobile Cell Phones.
* **Centralized Server Farm:** 3 Dedicated Servers managing infrastructure services:
    * **DNS Server:** Domain Name Resolution (`www.bank.com`).
    * **Web Server:** Main enterprise HTTP portal hosting corporate files.
    * **FTP Server:** Secure centralized storage for file backup and transfer.

---

## 🔢 Subnetting & IP Addressing Strategy

To maximize IPv4 efficiency and limit broadcast domains, Variable Length Subnet Masking (VLSM) is systematically applied across the entire topology. 
* The infrastructure utilizes custom-calculated subnets to isolate the Server Farm (DMZ), the Wireless local area network, and individual departmental Switch LANs.
* This tiered addressing hierarchy prevents unnecessary broadcast traffic from traversing the core routers and allows for seamless network scaling.

---

## 🛠️ Core Configurations & Protocols

### 1. Dynamic Routing: Open Shortest Path First (OSPF)
To ensure optimal path calculation and fast convergence across the 10 routers, multi-area OSPF is deployed as the interior gateway protocol.
```text
Router(config)# router ospf 1
Router(config-router)# network [network-address] [wildcard-mask] area 0
Remote Management & Access Control
Enables secure administrative remote control and privilege verification over network infrastructure using a localized user database and encrypted passwords:

Plaintext
Switch(config)# username admin password cisco123
Switch(config)# enable secret class
Switch(config)# line vty 0 4
Switch(config-line)# login local
Switch(config-line)# transport input telnet
