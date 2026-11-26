# FND-OSI — Answer Key

> Questions: `../Q-FND-OSI.md`. Complete the questions before opening this file. Scoring rules: `10-QUESTION-BANK/README.md`.

---

### FND-OSI-001
**Answer:** C.

**Explanation:** The Transport layer PDU for TCP is commonly called a segment; the UDP PDU is a datagram.

**Why the other options are wrong:** The Data Link layer uses frames, the Network layer uses packets, and the Physical layer transmits bits.

**Lesson links:** 00-09 §3.4

### FND-OSI-002
**Answer:** A and D — DNS and DHCP.

**Explanation:** DNS (UDP/TCP 53) and DHCP (UDP 67/68) are application-layer protocols, even though DHCP provides network-layer configuration to a host.

**Why the other options are wrong:** ICMP is carried within IP; ARP is carried directly in an Ethernet frame and supports local address resolution; OSPF is carried directly over IP (protocol number 89). These are not Layer 7 protocols.

**Lesson links:** 00-09 §3.6

### FND-OSI-003
**Answer:** In the OSI model, encryption and compression are presentation-layer (Layer 6) functions. In TCP/IP implementations, these functions are usually provided within applications or libraries used by applications.

**Explanation:** TLS is commonly used to provide encryption and integrity for application traffic. HTTP can use `Content-Encoding: gzip` for compression, and media applications use codecs such as H.264.

**Scoring:** 0.5 for Layer 6; 0.5 for explaining where the functions appear in TCP/IP and giving at least one valid example.  
**Lesson links:** 00-09 §§3.2 and 3.6; 06-01, 06-04, 06-06

### FND-OSI-004
**Answer:**
a) **ARP**. The frame payload contains an ARP message, not an IP header.  
b) Ethernet (EtherType 0x0800) → IPv4 (Protocol 17) → UDP (destination port 53) → DNS application.

**Explanation:** Each protocol header contains information that helps the receiver identify the next protocol. EtherType identifies the payload protocol at Ethernet, the IPv4 Protocol field identifies the transport protocol, and the UDP port identifies the receiving service.

**Scoring:** 0.5 for each part. For part (b), deduct 0.25 if one link in the protocol chain is missing.  
**Lesson links:** 00-09 §§3.5–3.6; 00-06 §4

### FND-OSI-005
**Answer:**
a) A Layer 2 switch normally uses Layer 2 information, especially the destination MAC address. An NGFW can inspect information up to Layer 7, including the application.  
b) A switch makes forwarding decisions using MAC addresses and does not normally understand the application payload. An NGFW can recognise an application and apply a more specific security policy, such as blocking an unauthorised file-sharing application even when it uses TCP port 443.

**Explanation:** The higher the layer a device can inspect, the more detailed the policy may be, though deeper inspection requires additional processing.

**Scoring:** 0.5 for each part.  
**Lesson links:** 00-09 §3.5; 00-08 §3.3

### FND-OSI-006
**Answer:**
a) G0/1 is down/down, which normally points to a physical-link (Layer 1) issue. G0/2 is administratively down/down, which means the interface has been disabled by configuration.  
b) For G0/1, check the cable, remote device, and remote port. For G0/2, enter interface configuration mode and use `no shutdown`.

```text
Router(config)# interface GigabitEthernet0/2
Router(config-if)# no shutdown
```

**Explanation:** In `show ip interface brief`, the status and protocol columns indicate the interface's physical and line-protocol states. “Administratively down” explicitly identifies a configuration shutdown.

**Scoring:** 0.5 for each correctly diagnosed interface.  
**Lesson links:** 00-09 §§7 and 9; further detail in 01-10

### FND-OSI-007
**Answer:** a) Ethernet frame: **1,518 bytes**; link occupancy: **1,538 byte-times**. b) **About 95.7%**. c) **About 95.7 Mbps**.

**Explanation:**
- UDP payload 1,472 + UDP header 8 + IPv4 header 20 = 1,500-byte IP packet.
- Ethernet header and FCS add 18 bytes, producing a 1,518-byte frame.
- Preamble/SFD (8 byte-times) and IFG (12 byte-times) bring link occupancy to 1,538 byte-times.
- Efficiency is (1,472/1,538\approx95.7\%). On a 100 Mbps link, the approximate application rate is 95.7 Mbps.

**Scoring:** One third per part.  
**Lesson links:** 00-09 §4.1

### FND-OSI-008
**Example answer:** At the sender, data moves down the protocol stack. Each layer adds its own header and treats the data from the layer above as its payload. The Data Link layer also adds a trailer, such as the Ethernet FCS, to form a frame. The receiver works in the opposite direction: each layer checks its header, processes it, and passes the payload upward. Fields such as EtherType, the IP Protocol field, and transport ports help the receiver identify the next protocol. A router removes the incoming Layer 2 frame, examines the IP packet, makes a forwarding decision, and sends the packet in a new Layer 2 frame.

**Scoring rubric (1 point total):**

| Criterion | Points |
|---|---:|
| Explains that each layer adds its own header | 0.25 |
| Explains the Data Link trailer / FCS | 0.25 |
| Identifies protocol fields used to pass data upward | 0.25 |
| Explains that a router processes the packet and creates a new Layer 2 frame | 0.25 |

**Note:** Encapsulation is not the same as encryption or compression.  
**Lesson links:** 00-09 §3.5

### FND-OSI-009
**Example answer:** The OSI model has seven layers, while the common TCP/IP model has four. TCP/IP combines OSI's top three layers into its Application layer and combines the lower Physical and Data Link functions into its Link layer. Another difference is historical: the OSI model was designed as a reference model, whereas the TCP/IP protocols were developed and used in practice before the model became a common teaching description. Today's network protocols belong mainly to the TCP/IP suite, but the OSI layer numbers remain useful shared language. For example, “Layer 2 switch” and “Layer 4 load balancer” describe the kind of information a device uses.

**Scoring rubric (1 point total):**

| Criterion | Points |
|---|---:|
| Correct layer counts and mapping | 0.25 |
| A second valid difference | 0.25 |
| Recognises that real-world protocols are mainly TCP/IP protocols | 0.25 |
| Explains why OSI layer numbers remain useful, with an example | 0.25 |

**Lesson links:** 00-09 §§3.2 and 3.3

### FND-OSI-010
**Answer:** a) **Layer 7, DNS**. b) Use `nslookup` to test name resolution and inspect the configured DNS server with `ipconfig /all`. You can also query a known alternative resolver for comparison.

**Explanation:** The link is active, the host has valid IP settings, and it can reach both its gateway and an Internet IP address. The failing step is translating the domain name into an IP address. The message “could not find host” means the name could not be resolved before ping was sent. DNS is an application-layer protocol.

**Scoring:** 0.5 for identifying DNS/Layer 7; 0.5 for two valid checks (one check earns 0.25).  
**Lesson links:** 00-09 §§3.6 and 9; further detail in 07-02
