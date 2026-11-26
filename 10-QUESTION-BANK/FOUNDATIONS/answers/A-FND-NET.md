# FND-NET — Answer Key

> Questions: `../Q-FND-NET.md`. Complete the questions before opening this file. Scoring rules: `10-QUESTION-BANK/README.md`.

---

### FND-NET-001
**Answer:** B — Layer 2 switch.

**Explanation:** A Layer 2 switch looks up the destination MAC address in its MAC address table and forwards the frame toward the associated port. If the destination is unknown, the switch floods the frame within the VLAN, excluding the ingress port.

**Why the other options are wrong:** A hub repeats signals to all ports without making a MAC-based forwarding decision. A router forwards between IP networks. An AP bridges wireless clients to a wired network, but it is not the multiport Layer 2 switch described here.

**Lesson links:** 00-08 §3.3; 02-06

### FND-NET-002
**Answer:** C.

**Explanation:** An NGFW adds application identification and capabilities such as integrated intrusion prevention (IPS) to traditional IP/port filtering and stateful inspection. This allows policies to distinguish applications even when they use the same TCP or UDP port.

**Why the other options are wrong:** IP filtering, port filtering, and stateful inspection are also available on traditional firewalls.

**Lesson links:** 00-08 §3.3; further detail in 14-01

### FND-NET-003
**Answer:** B — Wireless LAN controller (WLC).

**Explanation:** A WLC centrally manages controller-based access points, including channel and power settings, SSIDs, and security policies.

**Lesson links:** 00-08 §3.3; 02-16

### FND-NET-004
**Answer:** A and C.

**Explanation:** Power sourcing equipment (PSE) supplies power; a powered device (PD) receives it. A switch has a finite total PoE power budget. When that budget is exhausted, additional devices may not receive power.

**Why the other options are wrong:** PoE sends data and power over the same copper cable; it uses DC; fiber does not carry the electrical power used by PoE.

**Lesson links:** 00-08 §3.3; 00-04 §§4.1 and 5

### FND-NET-005
**Answer:** a) **3 ms**. b) **12 microseconds**.

**Explanation:** 1,500 bytes = 12,000 bits.
- At 4 Mbps: (12,000/(4\times10^6)=0.003\text{ s}=3\text{ ms}).
- At 1 Gbps: (12,000/10^9=12\times10^{-6}\text{ s}=12\ \mu s).

This is transmission (serialization) delay: the time needed to put all packet bits onto the link.

**Scoring:** 0.5 for each part.  
**Lesson links:** 00-08 §§3.6 and 4

### FND-NET-006
**Answer:** a) Most of the 180 ms is likely **propagation delay**. b) A faster link can reduce ping time when congestion and queueing delay are significant.

**Explanation:** The four common components are transmission delay, propagation delay, queueing delay, and processing delay. The long physical distance to another continent causes propagation delay, which does not fall simply because the link's bit rate increases. A small ping packet already takes very little time to transmit over a 100 Mbps link.

A capacity upgrade can help when the link is congested and packets spend significant time waiting in output queues. Compare latency during quiet and busy periods and inspect link utilisation. If the delay is high even when the link is quiet, distance is a more likely explanation.

**Scoring:** 0.5 for propagation delay and why bandwidth does not remove it; 0.5 for queueing/congestion and a suitable measurement.  
**Lesson links:** 00-08 §§3.6 and 4

### FND-NET-007
**Answer:**

| Traffic on link | Source MAC | Destination MAC | Source IP | Destination IP |
|---|---|---|---|---|
| a) Request, SW2–Server | CCCC | DDDD | 10.1.1.10 | 10.2.2.20 |
| b) Reply, SW1–PC | BBBB | AAAA | 10.2.2.20 | 10.1.1.10 |

**Explanation:** MAC addresses are used for delivery across a local link. Router R1 creates a new frame for each outgoing link. On the request's final link, the source MAC is R1's G0/1 address (CCCC), and the destination MAC is the server's address (DDDD). On the reply's final link, the source MAC is R1's G0/0 address (BBBB), and the destination MAC is the PC's address (AAAA). The IP addresses remain end-to-end addresses because no NAT is used.

**Scoring:** 0.5 for each complete row.  
**Lesson links:** 00-08 §3.7

### FND-NET-008
**Example answer:** A client-server design gives central control, monitoring, and a single trusted source for the update. Its weakness is that the central server must deliver 5,000 copies of a 2 GB file — 10 TB in total — and may become a bandwidth or storage bottleneck. In a P2P design, computers can share pieces of the update, increasing aggregate distribution capacity as more peers participate. However, distribution, security, and integrity are harder to control. A hybrid design is a reasonable choice: the central server authenticates and signs the update, while local peers share verified pieces.

**Scoring rubric (1 point total):**

| Criterion | Points |
|---|---:|
| One client-server strength | 0.25 |
| One client-server weakness (server load / bottleneck) | 0.25 |
| One P2P strength and one weakness | 0.25 |
| A justified recommendation; a hybrid approach is acceptable | 0.25 |

**Lesson links:** 00-08 §3.4; further detail in 07-01

### FND-NET-009
**Answer:** D.

**Explanation:** RFC 791 specifies IPv4. RFCs are part of the Internet standards process associated with the IETF, not IEEE. IEEE publishes standards such as 802.3 Ethernet, 802.11 wireless LAN, and 802.1Q VLAN bridging.

**Why the other options are correct:** 802.11 is an IEEE standard; RFC 9293 specifies TCP; G.711 is an ITU-T recommendation.

**Lesson links:** 00-08 §3.5
