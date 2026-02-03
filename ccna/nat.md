---
title: Static NAT Configuration in Cisco Packet Tracer (Two Routers)
layout: page
parent: CCNA — Networking Fundamentals
nav_order: 2
---

# Static NAT Configuration in Cisco Packet Tracer (Two Routers)

In this lab, I configured **Static NAT** between two networks using two routers in Cisco Packet Tracer.

This helped me understand how private IP addresses are mapped to public IP addresses and how communication happens across networks using NAT.

---

## Topology Overview

- PC1 → Router A → Router B → PC2
- Both routers are connected using a serial link
- Static NAT is configured on both routers

---

## IP Addressing

| Device | Interface | IP Address |
|---|---|---|
| PC1 | — | 10.0.0.2 |
| Switch0 | - | - |
| Router A | Fa0/0 | 10.0.0.1 |
| Router A | S0/0/0 | 20.0.0.1 |
| Router B | S0/0/0 | 20.0.0.2 |
| Router B | Fa0/0 | 192.168.0.1 |
| Switch0 | - | - |
| PC2 | — | 192.168.0.2 |

---

## Goal of This Lab

- Map **10.0.0.2 → 50.0.0.3** on Router A
- Map **192.168.0.2 → 30.0.0.1** on Router B
- Allow both PCs to communicate using the mapped (public) addresses

---

## Router A Configuration

```bash
enable
conf t

interface fastethernet0/0
ip address 10.0.0.1 255.255.255.0
ip nat inside
no shutdown

interface serial0/0/0
ip address 20.0.0.1 255.255.255.0
ip nat outside
no shutdown

ip nat inside source static 10.0.0.2 50.0.0.3
```

## Router B Configuration

```bash
enable
conf t

interface fastethernet0/0
ip address 192.168.0.1 255.255.255.0
ip nat inside
no shutdown

interface serial0/0/0
ip address 20.0.0.2 255.255.255.0
ip nat outside
no shutdown

ip nat inside source static 192.168.0.2 30.0.0.1
```
---

## PC1 Configuration

IP Address: 10.0.0.2

Default Gateway: 10.0.0.1

## PC2 Configuration

IP Address: 192.168.0.2

Default Gateway: 192.168.0.1

---

## How Static NAT Works Here

When PC1 sends traffic:

Source IP 10.0.0.2 is translated to 50.0.0.3 by Router A

Packet travels to Router B

Router B translates destination from 30.0.0.1 to 192.168.0.2

This allows private IPs to communicate using public mapped addresses.

--- 

Verification Commands:

Use these on both routers:

show ip nat translations
show ip nat statistics

You will see the static mappings in the NAT table.

---

## What I Learned

From this lab, I understood:

Difference between inside and outside NAT interfaces

How static mapping works

How routers translate IP addresses during packet forwarding

Why NAT is important in real networks

## Key Takeaway

Static NAT creates a one-to-one mapping between private and public IP addresses.

This is commonly used when an internal device must be reachable from another network using a fixed public IP.
