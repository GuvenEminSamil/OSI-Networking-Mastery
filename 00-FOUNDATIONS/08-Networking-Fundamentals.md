# 00-08 — Networking Fundamentals

> **Prerequisite:** 00-01 to 00-07 — Foundations  
> **CCNA 200-301 v1.1 connection:** Exam objective 1.1 — Network Components.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain what a computer network is.
- Distinguish LAN, WLAN, and WAN.
- Identify common network devices and their roles.
- Compare client-server and peer-to-peer communication.
- Understand protocols, standards, and key networking organizations.
- Explain bandwidth, throughput, latency, jitter, and packet loss.
- Recognize the difference between MAC addresses and IP addresses.

## 1. What Is a Network?

A **computer network** is a group of connected devices that can exchange data and share resources.

For example, when your phone streams a video:

1. Your phone connects to a local network through Wi-Fi or a cable.
2. A router forwards traffic toward your internet provider.
3. Other networks carry the traffic toward the video service.
4. The video server sends data back to your phone.

The **Internet** is a global network of interconnected networks. It is not one single network owned by one company.

## 2. Common Network Types

**LAN (Local Area Network):** A network covering a limited area, such as a home, office, or school.

**WLAN (Wireless Local Area Network):** A LAN that uses wireless communication, usually Wi-Fi.

**WAN (Wide Area Network):** A network that connects locations over a large geographic area. A company may use a WAN to connect offices in different cities.

| Type | Example |
|---|---|
| LAN | Computers connected inside an office |
| WLAN | Laptops and phones connected through Wi-Fi |
| WAN | A company connecting offices in different cities |

## 3. Network Devices and Their Roles

These devices are important for the CCNA exam.

| Device | Main role | Information commonly used |
|---|---|---|
| **Router** | Connects different IP networks and forwards packets between them | IP addresses and routing table |
| **Layer 2 switch** | Connects devices within a local Ethernet network | MAC addresses |
| **Layer 3 switch** | Performs switching and can also route between IP networks | MAC and IP information |
| **Access point (AP)** | Connects wireless clients to a network | Wireless association and link information |
| **Firewall** | Allows or blocks traffic according to security rules | Addresses, ports, protocols, and configured policies |
| **IPS** (Intrusion Prevention System) | Detects and can block suspicious traffic | Traffic patterns and security rules |
| **Wireless LAN controller (WLC)** | Centrally manages supported wireless access points | Wireless configuration and client state |
| **End device** | Creates or receives user data | Depends on the application |
| **Server** | Provides services such as web pages, files, or DNS | Application and network protocols |
| **PoE switch** | Can provide electrical power to compatible devices over Ethernet | Power negotiation and Ethernet link |

A **routing table** is a list of network destinations and the next steps a router can use to reach them.

A **MAC address** identifies a network interface on a local link. An **IP address** is a logical address used to deliver packets across IP networks. You will study their relationship in more detail later.

## 4. Client-Server and Peer-to-Peer

In a **client-server model**, one device requests a service and another device provides it.

Example: Your browser (the client) requests a web page from a web server.

In a **peer-to-peer (P2P) model**, devices can communicate and share resources directly without relying on one central server for every exchange.

Example: Two computers sharing files directly over a local network.

Many real systems combine both models.

## 5. Protocols and Standards

A **protocol** is a set of rules that devices follow to communicate. It defines things such as message format, meaning, timing, and expected actions.

A **standard** is an agreed technical specification that helps products from different manufacturers work together.

Examples:

- Ethernet is defined by IEEE 802.3.
- Wi-Fi is defined by the IEEE 802.11 family.
- IP and TCP are specified in documents called RFCs, published through the IETF process.

Important organizations:

| Organization | Main area |
|---|---|
| **IEEE** (Institute of Electrical and Electronics Engineers) | Ethernet and Wi-Fi standards |
| **IETF** (Internet Engineering Task Force) | Internet protocols such as IP, TCP, and DNS |
| **ISO** (International Organization for Standardization) | International standards, including the OSI reference model |
| **ITU-T** (International Telecommunication Union — Telecommunication Standardization Sector) | Telecommunications standards |
| **IANA** (Internet Assigned Numbers Authority) | Coordinates protocol numbers, port registries, and other Internet identifiers |

You do not need to memorize every detail of these organizations now. Remember the examples shown in the table.

## 6. Measuring Network Performance

These measurements describe how well a network is working.

**Bandwidth** is the maximum data-carrying capacity of a link, usually expressed in bits per second.

**Throughput** is the actual rate of successful data delivery.

**Latency** is the time it takes data to travel from one point to another.

**Jitter** is variation in packet delay. It matters for real-time voice and video because packets should arrive at a steady rate.

**Packet loss** happens when packets fail to reach their destination.

Four components contribute to network delay:

- **Processing delay:** Time spent examining and handling a packet.
- **Queuing delay:** Time spent waiting in a queue.
- **Transmission delay:** Time required to put all packet bits onto a link.
- **Propagation delay:** Time for the signal to travel through the physical medium.

Example: A 1,500-byte packet contains 12,000 bits.

On a 10 Mbps link:

[
12,000div10,000,000=0.0012 s=1.2 ms
]

On a 1 Gbps link:

[
12,000div1,000,000,000=0.000012 s=12 mu s
]

A faster link reduces transmission delay. It does not make the physical signal travel faster through the cable.

## 7. MAC Address and IP Address: A First Look

A **MAC address** is used for delivery on a local network link.

An **IP address** identifies a source or destination in an IP network.

When a packet travels through a router to another network:

- The source and destination IP addresses normally remain the same, unless a feature such as NAT changes them.
- The Ethernet source and destination MAC addresses are replaced for the next link.
- The IP Time to Live (TTL) field is reduced by a router.

**NAT** (Network Address Translation) is a function that changes IP address information as traffic passes through a device. You will study it later.

This is why MAC and IP addresses have different jobs.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| A switch and a router do the same job. | A Layer 2 switch forwards frames within a LAN; a router forwards packets between IP networks. |
| Bandwidth and throughput are identical. | Bandwidth is capacity; throughput is the actual achieved rate. |
| Higher bandwidth always means lower latency. | It can reduce transmission delay, but not necessarily propagation or processing delay. |
| MAC addresses replace IP addresses. | They serve different roles at different parts of communication. |
| A WLAN and a WAN are the same. | WLAN means wireless LAN; WAN means wide area network. |

## 9. Knowledge Check

1. What does LAN stand for?
   <details><summary>Answer</summary>Local Area Network — a network covering a limited area.</details>

2. Which device commonly forwards Ethernet frames using MAC addresses?
   <details><summary>Answer</summary>A Layer 2 switch.</details>

3. Which device connects different IP networks?
   <details><summary>Answer</summary>A router.</details>

4. What is the main difference between a protocol and a standard?
   <details><summary>Answer</summary>A protocol defines communication rules. A standard is an agreed specification that helps different implementations work together.</details>

5. What is the difference between bandwidth and throughput?
   <details><summary>Answer</summary>Bandwidth is the link's capacity; throughput is the actual successful data rate.</details>

6. Which delay component is affected by increasing link speed: transmission delay or propagation delay?
   <details><summary>Answer</summary>Transmission delay decreases. Propagation delay is determined mainly by the medium and distance.</details>

7. When a router forwards an ordinary packet without NAT, which addresses usually change for the next Ethernet link?
   <details><summary>Answer</summary>The source and destination MAC addresses change. The source and destination IP addresses normally remain the same.</details>

## 10. Practice

On your computer, find:

- Your IP address.
- Your MAC address.
- Your default gateway.

A **default gateway** is the router or Layer 3 device a host sends traffic to when the destination is outside its local IP network.

On Windows, use:

```powershell
ipconfig /all
```

On Linux, use:

```bash
ip addr
ip route
```

Find the default route and identify the gateway address.

## 11. CCNA Takeaways

- Know the roles of routers, switches, Layer 3 switches, APs, firewalls, IPS, WLCs, endpoints, and servers.
- Understand LAN, WLAN, and WAN.
- Distinguish protocols from standards.
- Understand bandwidth, throughput, latency, jitter, and packet loss.
- Know why MAC addresses and IP addresses are both needed.

## Self-Check

- [ ] I can describe the main network device roles.
- [ ] I can distinguish LAN, WLAN, and WAN.
- [ ] I can explain the difference between client-server and peer-to-peer.
- [ ] I can define bandwidth, throughput, latency, jitter, and packet loss.
- [ ] I understand the basic difference between MAC and IP addresses.

**Next lesson:** 00-09 — Layered Models: OSI and TCP/IP.
