# CE-00 — Answer Key

> Questions: `../CE-00.md`. Complete the test before opening this file.

## Score Interpretation

| Score (out of 40) | Interpretation |
|---:|---|
| 34–40 | Your overall model is strong. Focus on the mechanisms and details in the relevant lessons. |
| 24–33 | You have a basic framework, but there are gaps. Review the linked lessons for incorrect answers. |
| 0–23 | This is a starting point, not a failure. The curriculum is designed to build the concepts from the beginning. |

For every answer, “Lesson links” identifies where the concept is studied in more detail. Review those lessons for incorrect or uncertain answers.

## Section A — Basic Knowledge

| # | Answer | Lesson links |
|---:|---|---|
| 1 | Seven | 00-09 |
| 2 | Highest: Application (L7). Lowest: Physical (L1). | 00-09 |
| 3 | Transport (L4) | 04-03 |
| 4 | Network (L3) | 03-01 |
| 5 | Data Link (L2), more precisely its MAC sublayer | 02-02 |
| 6 | L3. A router interface also performs L1 and L2 functions, and a router can run management protocols such as SSH and SNMP. | 03-07 |
| 7 | L2. A Layer 3 switch can also perform routing. | 02-06, 03-10 |
| 8 | Packet (IP packet) | 00-09, 08-01 |
| 9 | L2, Data Link | 02-03 |
| 10 | Encapsulation adds protocol information as data moves down the sender's stack. Decapsulation processes and removes that information as data moves up the receiver's stack. | 08-01 |

For question 10: encapsulation adds a header at each layer (and a trailer at Layer 2, such as the Ethernet FCS). Decapsulation processes those fields and passes the payload to the next layer. A router performs part of this process: it removes the incoming Layer 2 frame, processes the Layer 3 packet, and encapsulates it in a new Layer 2 frame for the next link.

## Section B — Scenarios

**11.** Check Layer 1 (Physical) first.

- **Why:** A link light indicates that the physical interfaces at both ends detect a link. Without a physical link, higher-layer communication cannot work.
- **Checks:** Ensure the cable is seated at both ends; check the cable and cable type; verify that the remote device and port are powered on; check whether the switch port is administratively shut down or in an error-disabled state.
- **Scoring:** 1 point for Layer 1; 1 point for the reasoning and at least two checks.
- **Lesson links:** 01-10, 11-01

**12.** Your local configuration is probably mostly working because you can reach the Internet. Possible causes include:

- The destination computer's firewall blocks incoming ICMP Echo requests.
- The destination is powered off, has an incorrect IP configuration, or has a broken return path.
- The computers are in different VLANs or subnets without routing between them.
- Wireless client isolation prevents wireless clients from communicating directly.

Check the destination's IP configuration, ARP information (for example, `arp -a`), VLAN/subnet placement, and host firewall.
- **Scoring:** 1 point for two plausible causes; 1 point for sensible layer-based reasoning.
- **Lesson links:** 03-06, 11-03, 02-15

**13.** If `8.8.8.8` responds, the path to an Internet IP address is working. Likely causes include:

- **DNS failure:** The domain name cannot be resolved. Test with `nslookup <site>`.
- A firewall or proxy blocks TCP 80/443 or UDP 443 (HTTP/3). On Windows, test TCP 443 with `Test-NetConnection <site> -Port 443`.
- The website is unavailable, the TLS certificate is invalid, or the browser's proxy settings are wrong.

- **Scoring:** 1 point for DNS; 1 point for another plausible cause and a suitable test.
- **Lesson links:** 07-02, 08-10

**14.** The destination MAC address should be the MAC address of the default gateway, router `192.168.1.1`.

Assuming a /24 local network, `8.8.8.8` is remote. The host sends the Ethernet frame to its next hop (the router). The IP packet's destination remains `8.8.8.8`.
- **Scoring:** 1 point for the correct MAC; 1 point for the explanation.
- **Lesson links:** 03-06, 08-03

**15.** The switch performs **unknown unicast flooding**: it sends the frame out all ports in the same VLAN except the port on which the frame arrived. It also learns the source MAC address and associates it with the incoming port. When the destination replies, the switch can learn its location too.
- **Scoring:** 1 point for flooding; 1 point for the same-VLAN / ingress-port exclusion or the learning behaviour.
- **Lesson links:** 02-06

**16.** During normal routing without NAT:

- The entire Layer 2 header is replaced. The source MAC becomes the router's outgoing-interface MAC, and the destination MAC becomes the next-hop MAC. The new frame gets a new FCS.
- The IP TTL is reduced by one. The IPv4 header checksum is recalculated because the header changed.
- The source and destination IP addresses remain unchanged.

- **Scoring:** 1 point for the MAC-address change; 1 point for TTL and checksum.
- **Lesson links:** 03-07

**17.** SYN, SYN-ACK, ACK.  
**Scoring:** 2 points for all three in the correct order; 1 point if the order is incorrect.  
**Lesson links:** 04-03

**18.** Discover, Offer, Request, Acknowledge (DORA).  
**Scoring:** 2 points for all four in the correct order; 1 point if one item is missing or the order is incorrect.  
**Lesson links:** 07-03

**19.** TLS provides three main security properties:

- **Confidentiality:** Traffic is encrypted.
- **Integrity:** Modification in transit can be detected.
- **Authentication:** The client can verify the server's identity using its certificate.

The TLS handshake establishes the keys and parameters used to provide these properties.
- **Scoring:** 1 point for two properties; 2 points for all three.
- **Lesson links:** 06-05, 06-06

**20.** Layer 3 routing is required. Each VLAN is a separate broadcast domain and normally has its own IP subnet and default gateway.

Common implementations:
- **Router-on-a-stick:** An 802.1Q trunk and one router subinterface per VLAN.
- **Layer 3 switch:** An SVI for each VLAN and IP routing enabled.
- Separate physical router interfaces for each VLAN (an older and less scalable design).

- **Scoring:** 1 point for identifying Layer 3 routing; 1 point for a valid implementation.
- **Lesson links:** 03-10

## Section C — Deeper Reasoning

**21.** MAC and IP addresses serve different purposes.

- A **MAC address** is used to deliver a frame across a local link to the next device. A router terminates the incoming frame and creates a new frame for the outgoing link. MAC addresses therefore change at each routed hop.
- An **IP address** identifies the source and destination across the routed path. Routers use the destination IP address to make forwarding decisions, so the IP addresses normally remain the same end to end.
- **Exception:** NAT intentionally changes IP addresses (and PAT also changes port numbers).

- **Scoring:** 1 point for the link-local role of MAC; 1 point for the end-to-end role of IP and routing.
- **Lesson links:** 03-07, 08-04

**22.** In many games, old data is no longer useful. If a position update is lost, retransmitting that old update may be worse than using a newer update that is already on its way.

With TCP, a missing segment can delay delivery of later data (head-of-line blocking), and retransmission or congestion control can add delay. UDP does not provide those reliability mechanisms by default, so the application can decide which data needs recovery and which data can simply be replaced by a newer update.
- **Scoring:** 1 point for latency / stale data; 1 point for head-of-line blocking or retransmission overhead.
- **Lesson links:** 04-06

**23.** The likely issue is a **Layer 2 loop** causing a **broadcast storm**. Ethernet frames do not have a hop counter like IP's TTL, so a broadcast frame can circulate indefinitely and be replicated by switches. The **Spanning Tree Protocol (STP)** prevents switching loops by blocking redundant paths when necessary and forming a loop-free logical topology. A faulty device generating excessive broadcasts is another possibility; storm control can limit that traffic.
- **Scoring:** 1 point for identifying the loop/storm; 1 point for STP.
- **Lesson links:** 02-11, 02-12

**24.** Select `192.168.1.0/24`. This is the **longest prefix match** rule. Both routes cover `192.168.1.10`, but /24 matches 24 leading bits while /16 matches only 16. The more specific /24 route is preferred. Administrative distance and metric do not decide between these two different prefix lengths; they are used when comparing routes to the same prefix.
- **Scoring:** 1 point for the route; 1 point for the longest-prefix explanation.
- **Lesson links:** 03-08

**25.** The host makes the local-versus-remote decision using its own subnet mask.

- For `192.168.1.50`, both the source and destination are in `192.168.1.0/24`. The destination is local, so the host uses ARP to learn the destination computer's MAC address.
- For `8.8.8.8`, the destination network is different. The host sends the frame to its default gateway and uses ARP to learn the gateway's MAC address. The IP packet's destination remains `8.8.8.8`.
- The **sending host**, not the router, makes this initial local-versus-remote decision.

- **Scoring:** 1 point for the subnet-mask decision; 1 point for identifying which MAC address is resolved in each case.
- **Lesson links:** 00-03, 03-06
