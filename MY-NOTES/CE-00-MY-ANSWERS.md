# CE-00 — My Answers

> These are the answers from the original diagnostic attempt. They are preserved as a historical record; corrections and feedback are listed below.

**Start time:** Not recorded  
**Finish time:** Not recorded

## Section A (1 point each)

1. 7
2. Physical, Application
3. Layer 4
4. Layer 3
5. Layer 2
6. Layer 3
7. Layer 2
8. Packet
9. Layer 2
10. One process prepares data to be sent; the other decodes the packet.

## Section B (2 points each)

11. Check Layer 1 first. There may be a cable problem.
12. There may be a switch problem. I would check Layers 1 and 2.
13. Check Layer 3. There may be a connection problem with the DNS server.
14. Because the data is going outside the LAN, it should first go to the router.
15. Flood the frame to all devices on the LAN.
16. Source IP and MAC addresses, and destination IP and MAC addresses.
17. ?
18. ?
19. For encryption and security.
20. ARP?

## Section C (2 points each)

21. To avoid confusion about which two devices are communicating.
22. Because of speed.
23. Frames do not have a TTL field, or the TTL value is high. “TTL protocol.”
24. Use `192.168.1.0/24` because the destination IP is in the same network.
25. In the first scenario, the destination is on the same network and the Layer 2 switch knows the MAC addresses in that network. In the second scenario, the data goes through the WAN, so the computer needs the router's MAC address (the default gateway).

## Scoring

> Scored on 2026-11-20 using the criteria in `10-QUESTION-BANK/COMPREHENSIVE-EXAMS/answers/CE-00-ANSWERS.md`.

| Section | Score |
|---|---:|
| A (out of 10) | 10 |
| B (out of 20) | 6 |
| C (out of 10) | 5 |
| **Total (out of 40)** | **21** |

**Feedback summary:** Layer-to-concept matching was strong (Section A was full marks). The main gaps were in mechanisms and practical detail. The redesigned course is intended to build those mechanisms step by step.

## Incorrect or Incomplete Answers

Bold rows below indicate answers that were given confidently but contained a misconception.

| Question | Score | Revisit | Feedback |
|---:|---:|---|---|
| 10 | 1/1 | 08-01 | The overall direction was right. The missing detail is that each layer adds its own header and removes it at the receiving side. |
| 11 | 1/2 | 01-10, 11-01 | Layer 1 was correct. Add why the link light matters (the two PHYs detect each other) and name at least one additional physical check. |
| 12 | 0/2 | 03-06, 11-03, 02-15 | If Internet access works, the sender's L1–L3 path is probably functional. The target may block ICMP, have incorrect IP settings, belong to another VLAN, or be isolated by the wireless network. |
| 13 | 1/2 | 07-02, 08-10 | DNS was a good guess, but **DNS is Layer 7**, not Layer 3. A successful ping to 8.8.8.8 indicates that basic Layer 3 reachability is working. |
| 14 | 2/2 | 03-06 | Correct. State explicitly that the destination MAC is the router's (default gateway's) MAC address. |
| 15 | 1/2 | 02-06 | Flooding was correct. The switch floods only within the same VLAN and excludes the port on which the frame arrived. |
| **16** | 1/2 | 03-07 | The MAC-address change was correct, but **IP addresses do not normally change during routing** (unless NAT is used). TTL is reduced and the IPv4 header checksum is recalculated. |
| 17 | 0/2 | 04-03 | The TCP handshake is SYN, SYN-ACK, ACK. |
| 18 | 0/2 | 07-03 | DHCP uses Discover, Offer, Request, Acknowledge (DORA). |
| 19 | 0/2 | 06-05, 06-06 | TLS provides confidentiality (encryption), integrity, and server authentication. |
| **20** | 0/2 | 03-10 | **ARP is not enough** for communication between different VLANs. Layer 3 routing is required, using router-on-a-stick or a Layer 3 switch with an SVI. |
| 21 | 1/2 | 03-07, 08-04 | The end-to-end IP role was right. The missing detail is that MAC addresses are used only on the current link and are replaced at each routed hop. |
| 22 | 1/2 | 04-06 | “Speed” is too general. Old game updates may no longer be useful; TCP retransmission and head-of-line blocking can delay newer data. |
| **23** | 1/2 | 02-11, 02-12 | It is correct that Ethernet frames have no TTL field. But there is no “TTL protocol” for this problem. STP prevents Layer 2 loops. |
| 24 | 1/2 | 03-08 | The selected route was correct, but explain longest prefix match. Both routes cover the destination; /24 is more specific than /16. |
| **25** | 1/2 | 00-03, 03-06 | The result was right, but **the host uses ARP to learn the MAC address**. The host uses its own subnet mask to decide local versus remote. A local destination needs its own MAC; a remote destination needs the default gateway's MAC. |
