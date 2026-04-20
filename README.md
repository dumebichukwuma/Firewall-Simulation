# Firewall-Simulation
<img width="902" height="430" alt="image" src="https://github.com/user-attachments/assets/8170a604-dbd8-4337-b598-0c7496a2ffd0" />

This project demonstrates the implementation of a **Secure Network Architecture** using a Cisco 2911 Router to segment traffic between an **Internal LAN**, a **DMZ (Demilitarized Zone)**, and an **External Network**.

The core of the project focuses on **Stateless Firewalling** using Extended Access Control Lists (ACLs) to enforce the Principle of Least Privilege.

## Network Topology
* **Internal LAN (G0/0):** `192.168.1.0/24` - Private host zone (PC0).
* **DMZ (G0/1):** `192.168.2.0/24` - Public-facing services zone (Server0).
* **External Network (G0/2):** `10.10.10.0/24` - Untrusted/Outside network (Server1).

## Security Features
* **Traffic Segmentation:** Distinct security zones prevent direct, unfiltered communication between the internal network and the outside world.
* **Established Session Handling:** Utilizes the `established` keyword in TCP ACLs to allow return traffic only for connections initiated from within the trusted zones.
* **ICMP Management:** Granular control over ICMP traffic, allowing `echo` and `echo-reply` for troubleshooting while maintaining a secure posture.
* **Service Filtering:** Limits access strictly to Web protocols (**HTTP/80** and **HTTPS/443**), adhering to a "Deny All" default policy for all other ports.

## Configuration Overview
The implementation follows a standard Cisco IOS approach:
1.  **Interface Configuration:** IP assignment and state initialization (`no shutdown`).
2.  **Extended ACL Definition:** Creation of named access lists (`INTERNAL`, `DMZ`, `EXTERNAL`) to handle complex traffic patterns.
3.  **Access-Group Application:** Applying filters `inbound` on interfaces to drop unauthorized traffic at the earliest possible point.

## How to Use
1.  Load the project in **Cisco Packet Tracer**.
2.  Verify the configuration using `show ip access-lists` and `show run`.
3.  Perform connectivity tests (Ping and Web Browser) to observe the ACLs permitting and denying traffic based on the source/destination rules.
