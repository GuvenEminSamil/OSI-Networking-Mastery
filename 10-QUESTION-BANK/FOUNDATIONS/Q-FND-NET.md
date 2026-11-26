# FND-NET — Networking Fundamentals

> **Coverage:** 00-08 | **Questions:** 9 | **Suggested time:** 25 minutes  
> Answers: `answers/A-FND-NET.md`. See `10-QUESTION-BANK/README.md` for scoring rules. No calculator.

---

### FND-NET-001
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-08

Which device forwards frames between devices on a local network by examining the destination MAC address and sending the frame out the appropriate port?

- A) Hub
- B) Layer 2 switch
- C) Router
- D) Access point (AP)

### FND-NET-002
**Category:** MC · **Difficulty:** 2 · **Lesson:** 00-08

Which feature distinguishes a next-generation firewall (NGFW) from a traditional firewall?

- A) Filtering by source and destination IP address
- B) Filtering by TCP and UDP port number
- C) Identifying applications and providing integrated intrusion prevention (IPS)
- D) Tracking connection state (stateful operation)

### FND-NET-003
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-08

Which component centrally manages the channel, power, and security settings of 200 access points across a university campus?

- A) Layer 3 switch
- B) Wireless LAN controller (WLC)
- C) NGFW
- D) PoE switch

### FND-NET-004
**Category:** MC · **Difficulty:** 2 · **Lessons:** 00-08, 00-04

Which **two** statements about Power over Ethernet (PoE) are correct? (Select two.)

- A) A PoE switch is the power sourcing equipment (PSE); an IP phone is a powered device (PD).
- B) A PoE cable carries only power; a separate cable is required for data.
- C) If the switch's total PoE budget is exceeded, some ports may not be able to power their devices.
- D) PoE uses alternating current (AC), like mains electricity.
- E) PoE works only over fiber-optic cables.

### FND-NET-005
**Category:** O · **Difficulty:** 1 · **Lesson:** 00-08

A router sends a 1,500-byte packet over a 4 Mbps WAN interface.

a) What is the packet's serialization (transmission) delay?  
b) What would the transmission delay be if the same packet were sent over a 1 Gbps LAN interface?

### FND-NET-006
**Category:** I · **Difficulty:** 3 · **Lesson:** 00-08

The ping time from an office to a cloud server on another continent is consistently about 180 ms. A manager suggests upgrading the Internet connection from 100 Mbps to 1 Gbps and expects the ping time to fall to 18 ms.

a) Why is this expectation incorrect? Explain the four components of network delay.  
b) Under what condition could a faster link genuinely reduce ping time? How would you identify that condition?

### FND-NET-007
**Category:** S · **Difficulty:** 2 · **Lesson:** 00-08

Consider this topology:

```text
  PC ──── SW1 ──── G0/0 [R1] G0/1 ──── SW2 ──── Server
  10.1.1.10           10.1.1.1   10.2.2.1           10.2.2.20
  MAC: AAAA           MAC: BBBB  MAC: CCCC          MAC: DDDD
```

The PC sends a ping (ICMP Echo Request) to the server. There is no NAT.

a) On the link between SW2 and the server, write the request's source MAC, destination MAC, source IP, and destination IP.  
b) On the link between the PC and SW1, write the same four values for the server's Echo Reply.

### FND-NET-008
**Category:** KK · **Difficulty:** 2 · **Lesson:** 00-08

A company wants to distribute a 2 GB software update to 5,000 employees on the same day. Compare distributing the update from one central server (client-server) with having employee computers share the update with one another (peer-to-peer, or P2P).

Give one strength and one weakness of each approach, then recommend an approach for this situation.

### FND-NET-009
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-08

Which organisation–document pairing is incorrect?

- A) IEEE — 802.11 (Wi-Fi)
- B) IETF — RFC 9293 (TCP)
- C) ITU-T — G.711 (PCM voice coding)
- D) IEEE — RFC 791 (IPv4)
