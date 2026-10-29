# CCNA-Labs-Notes
# 🌐 Multi-Router Network Design with DHCP & Custom Subnetting

## 📌 Project Overview
This project demonstrates a fully functional enterprise-level network architecture simulated in **Cisco Packet Tracer**. The network spans across four routers interconnected using serial interfaces, featuring dynamic host configuration (**DHCP**), customized subnetting for optimal efficiency, and security hardening on inter-router links.

---

## 🛠️ Network Architecture & Design Topology

### 1. Advanced VLSM / Subnetting Strategy
The base network **192.168.1.0/24** was logically segmented into **7 distinct subnets** using Variable Length Subnet Masking (VLSM). This approach caters exactly to the required host density while strictly mitigating IP broadcast waste and strengthening edge security.

* **LAN Subnets (4 Networks):** Tailored to support up to **30 hosts** each (using `/27` masks, e.g., `255.255.255.224`). 
* **Inter-Router WAN Links (3 Networks):** Tailored strictly as Point-to-Point networks to support only **2 hosts** each (using `/30` masks, e.g., `255.255.255.252`). 

> **🔒 Security Impact:** Using a `/30` subnet mask on inter-router links restricts the network segment from accommodating any accidental or malicious unauthorized hosts, drastically minimizing the attack surface.

### 2. Centralized DHCP Service Configuration
Instead of tedious manual static indexing, a dedicated centralized **DHCP Server** was implemented and deployed in the topology. 
* Multiple IP Pools (`serverPool`, `serverPool1`, `serverPool2`, `serverPool3`) were built with specified **Start IP Addresses** and customized Subnet Masks (`255.255.255.224`).
* Hosts automatically acquire their Layer 3 configurations smoothly across the architecture.

---

## 🔧 Engineering & Implementation Steps

1. **Hardware Customization (WIC Modules):** 
   Physical router chassis were expanded by integrating **WIC (WAN Interface Card)** hardware expansion modules into the empty slots. This provided the necessary high-speed Serial ports to stitch the 4-router core network together.
   
2. **Layer 3 Interface Provisioning:**
   Configured administrative status, IP assignments, and clock rates on appropriate Serial and FastEthernet ports:
   ```cisco
   Router(config)# interface Serial 0/0/0
   Router(config-if)# ip address 192.168.1.65 255.255.255.252
   Router(config-if)# no shutdown
   ```

3. **Routing Table Establishment:**
   Constructed a unified routing architecture ensuring complete end-to-end connectivity across all segments, verifying optimal next-hop paths.

4. **DHCP Relay & Verification:**
   Ensured client workstations on distinct LAN subnets successfully broadcasted discover packets and pulled accurate lease metadata from the centralized repository server.

---

## 📊 Verification & Screenshots

### Core Network Topology Diagram
Below is the implemented physical/logical blueprint showing the interconnected routers, switching fabric, server architectures, and user endpoints:

![Network Topology](https://githubusercontent.com) *(Note: Replace with your actual image path later)*

### DHCP Server Scope Pools Configuration
The snapshot below highlights the active concurrent DHCP scoping parameters deployed within the infrastructure:

![DHCP Pools Setup](https://githubusercontent.com) *(Note: Replace with your actual image path later)*

---
🚀 *Deployed by [Abdelwahab-soc](https://github.com) as part of the specialized Cisco CCNA hands-on security and core routing curriculum.*
