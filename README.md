
# 🎓 University Campus Network System (UCNS)

![Network](https://img.shields.io/badge/Project-Networking-blue) ![Cisco](https://img.shields.io/badge/Tools-CiscoPacketTracer-green) ![Status](https://img.shields.io/badge/Status-Completed-success)

A **secure, scalable, and smart university campus network** built using **Cisco Packet Tracer**, featuring VLAN segmentation, centralized server farm, IoT automation, and access control for enhanced campus management.

---

## 🔹 Table of Contents

- [About the Project](#about-the-project)
- [Problem Statement](#problem-statement)
- [Network Architecture](#network-architecture)
- [Configuration Details](#configuration-details)
- [Services Implemented](#services-implemented)
- [Testing & Results](#testing--results)
- [Protocol Analysis](#protocol-analysis)
- [Future Enhancements](#future-enhancements)
- [Contributors](#contributors)
- [License](#license)

---

## 📝 About the Project

The **University Campus Networking System (UCNS)** provides:

- VLAN-based traffic segmentation for different departments.
- Centralized server farm with DHCP, DNS, Email, FTP, and Web Portal.
- IoT automation for lighting, security, and alerts.
- Extended ACLs for network security.

> This project simulates a real-world university network, making it ideal for academic labs and professional demonstrations.

---

## ❗ Problem Statement

The existing campus network faced multiple challenges:

- Inefficient traffic routing across buildings
- Lack of VLANs for departmental isolation
- No dynamic IP assignment in some areas
- Limited internal communication (email/alerts)
- Poor scalability and maintainability

**Goal:** Build a secure, scalable, and manageable network.

---

## 🏛️ Network Architecture

### VLAN Segmentation

| VLAN | Department           | Subnet          |
|------|--------------------|----------------|
| 10   | Faculty            | 192.168.10.0/24 |
| 20   | Labs               | 192.168.20.0/24 |
| 30   | Admissions         | 192.168.30.0/24 |
| 40   | Library            | 192.168.40.0/24 |
| 50   | Student Services   | 192.168.50.0/24 |
| 60   | Server Farm        | 192.168.60.0/24 |

### Centralized Server Farm (VLAN 60)

- **DHCP & DNS:** Assigns IPs & resolves internal domain names (portal.gamingzone.com)  
- **Email (SMTP/POP3):** Cross-VLAN communication & IoT alert notifications  
- **FTP & Web Portal:** Secure file transfer & internal web services

### IoT & Security Features

- Smoke & trip sensors for real-time alerts  
- RFID-based access control  
- Extended ACLs to protect critical servers

> ![IoT Security](https://img.shields.io/badge/IoT-Secure-orange)

---

## ⚙️ Configuration Details

### Core Switch (Inter-VLAN Routing + EIGRP)

```text
vlan 10,20,30,40,50,60

interface Vlan10
 ip address 192.168.10.1 255.255.255.0

interface Vlan20
 ip address 192.168.20.1 255.255.255.0
 ip helper-address 192.168.60.2

interface Vlan30
 ip address 192.168.30.1 255.255.255.0
 ip helper-address 192.168.60.2

interface Vlan40
 ip address 192.168.40.1 255.255.255.0
 ip helper-address 192.168.60.2

interface Vlan50
 ip address 192.168.50.1 255.255.255.0
 ip helper-address 192.168.60.2

interface Vlan60
 ip address 192.168.60.1 255.255.255.0

router eigrp 100
 network 192.168.10.0 0.0.0.255
 network 192.168.20.0 0.0.0.255
 network 192.168.30.0 0.0.0.255
 network 192.168.40.0 0.0.0.255
 network 192.168.50.0 0.0.0.255
 network 192.168.60.0 0.0.0.255
 network 10.0.0.0 0.0.0.3
 no auto-summary
````

### IoT Security ACL

```text
ip access-list extended IOT_SERVER_RESTRICTION
 permit ip 192.168.10.0 0.0.0.255 host 192.168.50.10
 deny ip 192.168.20.0 0.0.0.255 host 192.168.50.10
 deny ip 192.168.30.0 0.0.0.255 host 192.168.50.10
 deny ip 192.168.40.0 0.0.0.255 host 192.168.50.10
 permit ip any any
interface Vlan50
 ip access-group IOT_SERVER_RESTRICTION in
```

---

## 💻 Services Implemented

* DHCP: Auto IP assignment for all VLANs
* DNS: Internal name resolution
* SMTP/POP3: Email & automated IoT alerts
* FTP: File sharing between VLANs
* IoT Logic: Automated alarms & monitoring

---

## ✅ Testing & Results

* **Connectivity:** Ping tests across VLANs & buildings ✅
* **Routing:** EIGRP neighbor verification ✅
* **IoT Devices:** Smoke/Trip sensors & RFID access ✅
* **Security:** ACL enforcement for restricted access ✅
* **Email & Web Portal:** Cross-VLAN communication verified ✅
* **FTP:** Successful file transfer between VLANs ✅

---

## 📡 Protocol Analysis

* **EIGRP:** Fast, loop-free dynamic routing
* **Inter-VLAN Routing:** Secure communication between departments
* **SMTP/POP3:** Reliable internal messaging & IoT alert delivery

---

## 🚀 Future Enhancements

* Network redundancy & failover
* VPN for remote access
* IPv6 adoption
* Advanced monitoring tools (SNMP, NetFlow)
* Expanded IoT automation

