---
title: OSI vs TCP/IP — Understanding with a Real Packet Flow
layout: page
parent: CCNA
nav_order: 3
---

# OSI vs TCP/IP — Understanding with a Real Packet Flow

Many beginners memorize the OSI layers and TCP/IP model but struggle to understand **where they apply in real life**.

In this post, we will follow a **real example**:

> What happens inside the network when you open `https://google.com` in a browser?

By the end, OSI and TCP/IP will feel practical — not theoretical.

---

## The Two Models

| OSI Model (7 Layers) | TCP/IP Model (4 Layers) | Purpose |
|---|---|---|
| Application | Application | User interaction, data formatting |
| Presentation | Application | Encryption, encoding |
| Session | Application | Session handling |
| Transport | Transport | End-to-end communication |
| Network | Internet | Logical addressing (IP) |
| Data Link | Network Access | MAC addressing, switching |
| Physical | Network Access | Bits on the wire |

---

## Real Scenario: Opening a Website

You type `https://google.com` into your browser and press Enter.

Let’s track the packet from top to bottom.

---

## 1) Application Layer (OSI 7,6,5) / Application Layer (TCP/IP)

- Browser creates an **HTTP request**
- Data may be **encrypted using TLS (HTTPS)**
- A session is established between your system and the server

**What lives here:** HTTP, HTTPS, DNS, FTP

---

## 2) Transport Layer (OSI 4) / Transport Layer (TCP/IP)

- TCP is used for reliable communication
- A **TCP 3-way handshake** happens:
  - SYN → SYN-ACK → ACK
- Port numbers are added:
  - Source Port: random
  - Destination Port: 443 (HTTPS)

**What lives here:** TCP, UDP, Ports

---

## 3) Network Layer (OSI 3) / Internet Layer (TCP/IP)

- Your system checks: “Is this IP in my network?”
- If not, packet is sent to the **default gateway**
- **IP address** is attached:
  - Source IP: Your system
  - Destination IP: Google server

**What lives here:** IP, Routing

---

## 4) Data Link Layer (OSI 2) / Network Access (TCP/IP)

- Your PC needs the **MAC address** of the gateway
- ARP request is sent: “Who has this IP?”
- Switch forwards frames using MAC table

**What lives here:** MAC, ARP, Switching, Frames

---

## 5) Physical Layer (OSI 1)

- Bits travel through cable/Wi-Fi as electrical/radio signals

---

## Encapsulation (How data is wrapped)

| Layer | What is added | Name |
|---|---|---|
| Application | Data | Data |
| Transport | TCP Header | Segment |
| Network | IP Header | Packet |
| Data Link | MAC Header/Trailer | Frame |
| Physical | Bits | Bits |

This wrapping is called **Encapsulation**.

---

## Why This Matters for Networking and Security

Understanding this flow helps you:

- Configure ACLs (Network layer filtering)
- Troubleshoot connectivity issues
- Understand how VLANs and routing work
- Understand how attackers scan networks (Nmap works at these layers)
- Understand how firewalls filter traffic

---

## Key Takeaway

OSI is a **teaching model**.  
TCP/IP is a **practical model**.

But real networking happens when you can imagine:

> How a packet travels layer by layer from your system to a server.

---

## Where DNS Happens (Before Everything)

Before any packet is sent, your system must convert `google.com` into an IP address.

1. Browser checks local DNS cache
2. If not found, a query is sent to the configured DNS server
3. DNS server replies with Google’s IP address
4. Only after this, TCP/IP communication begins

**Layer:** Application Layer (OSI) / Application Layer (TCP/IP)

Without DNS resolution, none of the steps in this article can happen.

---

## How Your System Decides to Use the Default Gateway

After receiving Google’s IP, your PC performs a simple check:

> “Is this IP inside my subnet?”

- If **yes** → packet is sent directly to the destination
- If **no** → packet is sent to the **default gateway (router)**

Since Google is on the internet, the packet always goes to the router.

**Layer involved:** Network Layer (IP logic)

---

## The Return Journey (Server → Your PC)

Communication on a network is always two-way.

When Google responds:

1. Server sends packet to your public IP
2. Your router forwards it to your PC
3. Your PC removes headers layer by layer

This process is called **Decapsulation**.

---

## Encapsulation vs Decapsulation

| Sending (Your PC) | Receiving (Your PC) |
|---|---|
| Data → Segment → Packet → Frame → Bits | Bits → Frame → Packet → Segment → Data |

Understanding this is very helpful while analyzing packets and troubleshooting issues.

---

## Quick Layer Responsibility Table (Troubleshooting Guide)

| Problem | Layer to Check |
|---|---|
| Website not opening | Application / Transport |
| Port blocked | Transport |
| Cannot reach outside network | Network (IP / Gateway) |
| Same network device not reachable | Data Link (ARP / MAC) |
| Cable unplugged | Physical |

This is how real network engineers isolate problems.

---

## Why Attackers and Firewalls Care About These Layers

- Network scanners like Nmap operate at **Transport & Network layers**
- ACLs and Firewalls filter traffic at **Network & Transport layers**
- ARP spoofing attacks occur at the **Data Link layer**
- SSL/TLS inspection happens at the **Application layer**

Security becomes easier to understand when you know how layers work.

---

## Final Mental Picture

When you open a website, imagine this complete flow:

> DNS → TCP Handshake → IP Routing → ARP → Frame Switching → Bits on wire → Server → Back to you

This is OSI and TCP/IP working together in real life.
