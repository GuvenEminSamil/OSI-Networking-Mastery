# Curriculum and Content Catalogue

> **Single source of truth for planned course content.** Lesson, lab, host-lab, and code-exercise identifiers are defined here. `STUDY-ROADMAP.md` describes learning order; `PROGRESS.md` records production and learner progress.
>
> **Target:** CCNA 200-301 v1.1. **Curriculum scope:** unchanged from the approved syllabus. The v2.0-only topics are retained as post-exam extensions where marked.

## 1. Design Principles

1. **Build from fundamentals toward applications.** Start with data and bits, then physical communication, frames, switching, routing, transport, applications, and integrated scenarios.
2. **Use spiralled practice.** Earlier concepts reappear in later lessons and troubleshooting scenarios.
3. **Keep one primary home for each concept.** Other files link to that lesson rather than repeating the full explanation.
4. **Respect prerequisites.** A topic appears after the concepts needed to understand it.
5. **Keep the teaching style practical and approachable.** Avoid unnecessary theoretical depth. Define new terms when first introduced.
6. **Make simulator limitations explicit.** Packet Tracer (PT) is used where it represents the behaviour; real-host labs or conceptual exercises cover gaps.
7. **Use two kinds of PT practice.** Short drills let the learner design the topology and configuration. Full labs are reserved for break-fix, integration, and exam-style tasks.
8. **Separate core and extension material.** The CCNA v1.1 core is prioritised. Items marked `[v2.0 EXTENSION]`, advanced coding exercises, and non-essential host labs are secondary or post-exam material.
9. **Track learning separately from writing.** Publishing a file does not mark the learner as having studied it.

## 2. Module Prerequisites

| Module | Prerequisite | Reason |
|---|---|---|
| 00 — Foundations | None | Starting point |
| 01 — Physical Layer | 00 | Basic electricity, transistors, and digital representation support signal concepts |
| 02 — Data Link | 01 and 00-03 | Frames carry bits; CRC uses XOR |
| 03 — Network | 02 and 00-03 | Subnet masks use Boolean operations; forwarding relies on ARP and switching |
| 04 — Transport | 03 and 00-07 | Ports identify processes; sockets are operating-system concepts |
| 05 — Session | 04 | Modern session functions use transport and application protocols |
| 06 — Presentation | 00-06, 04, 05 | Encoding depends on data representation; TLS uses transport services |
| 07 — Application | 04 and 06 | Application protocols use TCP/UDP; HTTPS uses TLS |
| 08 — Cross-layer communication | Relevant layers | Each scenario lists its own prerequisites |
| 11 — Troubleshooting | Introduced progressively | Methodology is introduced early; advanced cases follow the relevant layers |
| 14 — Security | 02, 03, 04, 07 | ACLs use ports; Layer 2 defenses depend on DHCP, ARP, and NDP |
| 15 — Operations, automation, and AI | 03 and 07 | Requires routing, control/data plane, REST, SNMP, and syslog concepts |

## 3. Theory Lessons

The lesson filenames below are the canonical names. CCNA references refer to the v1.1 blueprint unless explicitly marked as v2.0. Prerequisites are lesson IDs.

### 3.1 Foundations — `00-FOUNDATIONS/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 00-01 | `01-Information-and-Data.md` | Data versus information; analog and digital representation; bits; signal thresholds and noise margin; why digital systems use discrete states | — |
| 00-02 | `02-Number-Systems-and-Units.md` | Decimal, binary, hexadecimal; conversions; powers of two; bits, nibbles, bytes, octets; SI/IEC prefixes; Mbps versus MB/s | 00-01 |
| 00-03 | `03-Binary-Arithmetic-and-Boolean-Logic.md` | Binary addition, overflow, two's complement; AND, OR, NOT, XOR; bitwise operations and masking; logic gates; links to subnetting and CRC | 00-02 |
| 00-04 | `04-Electricity-Fundamentals.md` | Voltage, current, resistance, Ohm's law, power, circuits, ground, DC and AC; impedance/capacitance intuition is optional depth | — |
| 00-05 | `05-Transistors-and-Digital-Logic.md` | MOSFET as a switch; CMOS gates; logic levels and thresholds; flip-flops and memory; clock signals | 00-03, 00-04 |
| 00-06 | `06-Data-Representation.md` | Integers, endianness and network byte order; text encoding; pixels and RGB; sound sampling and PCM; video frames and codecs; files as byte sequences | 00-02 |
| 00-07 | `07-Computer-Architecture-for-Networking.md` | CPU, RAM, buses; NIC, DMA, interrupts, ring buffers and drivers; operating-system network stack; introduction to sockets | 00-05, 00-06 |
| 00-08 | `08-Networking-Fundamentals.md` | LAN/WAN/WLAN; hosts, NICs, hubs, switches, routers, APs, WLCs, firewalls, servers and PoE; client-server and P2P; protocols and standards; bandwidth, delay, throughput; MAC/IP introduction | 00-07 |
| 00-09 | `09-Layered-Models-OSI-and-TCPIP.md` | Why layered models exist; OSI and TCP/IP models; PDU names; encapsulation overview; practical limits of strict layering | 00-08 |

### 3.2 Physical Layer — `01-PHYSICAL-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 01-01 | `01-Physical-Layer-Purpose.md` | Physical-layer responsibilities and boundaries; path from bits to signals; PHY and MAC interface | 00-09 |
| 01-02 | `02-Signals-and-Bandwidth.md` | Frequency, amplitude, phase, period; analog/digital signals; bandwidth in Hz versus bit rate; practical Nyquist/Shannon overview | 00-04, 01-01 |
| 01-03 | `03-Line-Coding-and-Modulation.md` | NRZ, Manchester, MLT-3, PAM; block coding; bit rate versus baud; ASK, FSK, PSK, QAM, OFDM | 01-02, 00-05 |
| 01-04 | `04-Bit-Synchronization-and-Reception.md` | Sampling, decision thresholds, clock recovery, preamble/SFD, equalisation, decoding, bit error rate | 01-03 |
| 01-05 | `05-Signal-Impairments.md` | Attenuation, dB/dBm, noise and SNR, EMI/RFI, crosstalk, reflection, impedance mismatch, dispersion, jitter | 01-02 |
| 01-06 | `06-Copper-Cabling.md` | Twisted pair, UTP/STP, cable categories, coax, RJ-45/8P8C, T568A/B, straight/crossover/rollover, Auto-MDIX, 100 m limit, PoE | 01-05, 00-04 |
| 01-07 | `07-Fiber-Optics.md` | Refraction and total internal reflection; core/cladding; SMF/MMF; wavelengths; dispersion; LC/SC; SFP families; transmitters and receivers | 01-05 |
| 01-08 | `08-Wireless-RF-Fundamentals.md` | Electromagnetic waves; 2.4/5/6 GHz bands; channels and channel width; RSSI, dBm, SNR, interference, multipath, MIMO | 01-02, 01-05 |
| 01-09 | `09-Ethernet-Physical-Standards.md` | IEEE 802.3 naming; auto-negotiation; speed; half/full duplex | 01-03, 01-06, 01-07 |
| 01-10 | `10-Topologies-Devices-and-Interface-Issues.md` | Physical/logical topology; repeaters, hubs, media converters, transceivers; interface counters and troubleshooting | 01-09 |

### 3.3 Data Link Layer — `02-DATA-LINK-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 02-01 | `01-Data-Link-Layer-Purpose.md` | Layer 2 responsibilities; LLC/MAC; framing; media access; LAN/WAN data-link examples including PPP/HDLC | 00-09, 01-01 |
| 02-02 | `02-MAC-Addresses-and-NICs.md` | 48-bit MAC format, OUI, I/G and U/L bits; unicast/multicast/broadcast; MAC randomisation; NIC filtering and offload | 00-02, 02-01 |
| 02-03 | `03-Ethernet-Frame-Structure.md` | Preamble/SFD; frame fields; EtherType versus Length; frame size and padding; MTU/jumbo frames; IFG | 02-02 |
| 02-04 | `04-Error-Detection-FCS-and-CRC.md` | Parity, checksums, CRC and XOR; FCS; error detection versus correction; handling corrupted frames | 00-03, 02-03 |
| 02-05 | `05-Media-Access-CSMA-CD-and-Duplex.md` | Shared media and collisions; CSMA/CD; exponential backoff; slot time; full-duplex Ethernet | 01-09, 02-03 |
| 02-06 | `06-Switch-Operation.md` | FCS check, source MAC learning, destination lookup, forwarding/filtering/flooding, aging, CAM/TCAM, ASICs, switching methods and buffers | 02-03, 02-04, 02-05 |
| 02-07 | `07-Collision-and-Broadcast-Domains.md` | Collision and broadcast domains; effect of hubs, switches, and routers | 02-06 |
| 02-08 | `08-VLANs.md` | Why VLANs exist; VLAN ID ranges; access ports; default/data/voice VLANs; VLAN database | 02-07 |
| 02-09 | `09-Trunking-8021Q-and-DTP.md` | 802.1Q tags; native VLAN; allowed VLAN list; DTP modes and security; VTP is optional depth | 02-08 |
| 02-10 | `10-ARP.md` | ARP format, request/reply, cache, gratuitous/proxy ARP, Layer 2/Layer 3 relationship | 02-03, 03-03 |
| 02-11 | `11-Spanning-Tree-STP.md` | Switching loops and broadcast storms; bridge ID and root election; path cost; port roles/states; BPDU; timers | 02-06, 02-09 |
| 02-12 | `12-Rapid-PVST-and-STP-Protection.md` | RSTP, Rapid PVST+, root primary/secondary, PortFast, BPDU Guard/Filter, Root Guard, Loop Guard | 02-11 |
| 02-13 | `13-EtherChannel-LACP.md` | Link aggregation; LACP, PAgP and static mode; compatibility; load-distribution hash; Layer 2/Layer 3 port channels | 02-11 |
| 02-14 | `14-CDP-and-LLDP.md` | Neighbour discovery, TLVs, and verifying network documentation | 02-03 |
| 02-15 | `15-Wireless-LAN-MAC-802-11.md` | 802.11 frame types; CSMA/CA, RTS/CTS; SSID/BSSID; BSS/ESS; association, roaming, address fields | 01-08, 02-05 |
| 02-16 | `16-Wireless-Architectures-and-WLC.md` | Autonomous, controller-based and cloud-managed WLANs; CAPWAP; AP modes; AP/WLC switch connections | 02-15, 02-09, 03-03 |

### 3.4 Network Layer — `03-NETWORK-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 03-01 | `01-Network-Layer-Purpose.md` | Why logical addresses are needed; connectionless best-effort delivery; control, data and management planes | 00-09, 02-01 |
| 03-02 | `02-IPv4-Header.md` | IPv4 header fields, DSCP/ECN, TTL, protocol number, fragmentation fields and header checksum | 03-01, 00-02 |
| 03-03 | `03-IPv4-Addressing.md` | Dotted decimal, network/host portions, masks, CIDR, private and special-use ranges | 03-02, 00-03 |
| 03-04 | `04-Subnetting-Binary-Method.md` | Binary subnetting, network/broadcast/host range, FLSM, quick method | 03-03 |
| 03-05 | `05-VLSM-and-Summarization.md` | VLSM, /31 and /32, route summarisation | 03-04 |
| 03-06 | `06-Host-Forwarding-and-Default-Gateway.md` | Host local/remote decision, gateway ARP, host route table, Windows/macOS/Linux checks | 03-04, 02-10 |
| 03-07 | `07-Router-Packet-Forwarding.md` | Router ingress processing, decapsulation, TTL/checksum update, route lookup, ARP/adjacency, new frame, CEF/FIB | 03-06, 02-06 |
| 03-08 | `08-Routing-Table-LPM-AD-Metric.md` | Route sources/codes, connected/local routes, longest-prefix match, administrative distance, metric, default route, `show ip route` | 03-07 |
| 03-09 | `09-Static-Routing.md` | Network, host, default and floating routes; next hop and exit interface; recursive lookup | 03-08 |
| 03-10 | `10-Inter-VLAN-Routing.md` | Router-on-a-stick, SVI, routed port, `ip routing` | 03-09, 02-09 |
| 03-11 | `11-ICMP-Ping-and-Traceroute.md` | ICMP message types, ping, extended ping, traceroute and ICMPv6 differences | 03-02, 03-07 |
| 03-12 | `12-MTU-and-Fragmentation.md` | MTU, IPv4 fragmentation, DF, PMTUD, black-hole problems, IPv6 router behaviour, TCP MSS | 03-02, 02-03 |
| 03-13 | `13-Dynamic-Routing-Concepts.md` | Distance vector/link state, convergence, IGP/EGP, loop prevention, routed versus routing protocols; RIP, EIGRP, IS-IS, BGP overview | 03-08 |
| 03-14 | `14-OSPF-Concepts.md` | Neighbour states, Hello/Dead, LSA/LSDB, SPF, cost, network types, DR/BDR, router ID | 03-13 |
| 03-15 | `15-OSPFv2-Configuration.md` | Single-area configuration and verification, passive interface, reference bandwidth, default route advertisement, neighbour troubleshooting | 03-14 |
| 03-16 | `16-IPv6-Fundamentals.md` | IPv6 purpose/header, notation, GUA/ULA/link-local/multicast/anycast/loopback, EUI-64, prefix sizing | 03-02, 00-02 |
| 03-17 | `17-IPv6-NDP-SLAAC-DHCPv6.md` | NDP, DAD, SLAAC, stateless/stateful DHCPv6, privacy addresses | 03-16, 02-10 |
| 03-18 | `18-IPv6-Routing-and-OSPFv3.md` | IPv6 routing and static routes; single-area OSPFv3 is a v2.0 extension | 03-17, 03-09, 03-15 |
| 03-19 | `19-First-Hop-Redundancy-HSRP-VRRP.md` | Default-gateway redundancy; virtual IP/MAC; HSRP; VRRP extension; priority and preemption | 03-07, 02-10 |
| 03-20 | `20-NAT-and-PAT.md` | Inside/outside and local/global terms; static/dynamic NAT, PAT, translation table, IOS XE configuration | 03-08, 04-01 |
| 03-21 | `21-QoS-Fundamentals.md` | Per-hop behaviour, classification, marking (DSCP/CoS), queues, congestion, policing and shaping | 03-02, 02-09 |

### 3.5 Transport Layer — `04-TRANSPORT-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 04-01 | `01-Transport-Layer-Purpose-Ports-Sockets.md` | Process delivery, port ranges, sockets, 5-tuple, multiplexing/demultiplexing, Layer 4 middleboxes | 00-07, 03-01 |
| 04-02 | `02-UDP.md` | UDP header and checksum; why minimal transport can be useful; DNS, VoIP, gaming, QUIC | 04-01 |
| 04-03 | `03-TCP-Header-and-Connection-Lifecycle.md` | TCP header/flags, three-way handshake, sequence numbers, states, FIN/RST/TIME-WAIT | 04-01 |
| 04-04 | `04-TCP-Reliability.md` | Sequence numbers, cumulative ACK, RTT/RTO, fast retransmit, SACK, ordering | 04-03 |
| 04-05 | `05-TCP-Flow-and-Congestion-Control.md` | Receive window, window scaling, sliding window, BDP, slow start, congestion avoidance, AIMD, ECN | 04-04 |
| 04-06 | `06-TCP-vs-UDP-and-Modern-Transport.md` | TCP/UDP comparison, MSS, segmentation, TSO, QUIC, optional SCTP overview and applications | 04-02, 04-05, 03-12 |
| 04-07 | `07-Application-to-Application-Communication.md` | Socket API, kernel buffers, application-to-network and network-to-application data path | 04-03, 00-07 |

### 3.6 Session Layer — `05-SESSION-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 05-01 | `01-OSI-Session-Layer-Theory.md` | OSI session establishment, maintenance, release, dialogue control and synchronisation points | 00-09 |
| 05-02 | `02-Session-Functions-in-Modern-Protocols.md` | Where session functions appear today: TCP, TLS resumption, HTTP sessions, WebSocket, SSH channels, RPC, SMB | 05-01, 04-03 |

### 3.7 Presentation Layer — `06-PRESENTATION-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 06-01 | `01-Presentation-Layer-Purpose.md` | Abstract/transfer syntax, ASN.1 introduction, OSI theory versus TCP/IP practice | 00-06, 00-09 |
| 06-02 | `02-Character-Encoding-ASCII-Unicode-UTF8.md` | ASCII, code pages, Unicode code points, UTF-8/UTF-16, BOM, character corruption, HTTP charset | 06-01, 00-06 |
| 06-03 | `03-Serialization-and-Data-Formats.md` | JSON, XML, YAML, Protocol Buffers, ASN.1/BER, MIME, Base64 | 06-02 |
| 06-04 | `04-Compression.md` | Lossless and lossy compression; Huffman, LZ77, DEFLATE, gzip, Brotli, JPEG, H.264, HTTP content encoding | 06-01 |
| 06-05 | `05-Cryptography-Fundamentals.md` | Confidentiality, integrity, authentication, AES, RSA/ECC, key exchange, hashes, HMAC, signatures, certificates and PKI | 00-03 |
| 06-06 | `06-TLS-and-the-OSI-Model.md` | TLS 1.3 handshake, record layer, SNI, ALPN, why TLS does not map neatly to one OSI layer | 06-05, 04-03, 05-02 |

### 3.8 Application Layer — `07-APPLICATION-LAYER/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 07-01 | `01-Application-Layer-Concepts.md` | Applications versus application protocols, client-server/P2P, request-response, stateful/stateless, ports, proxies and L7 load balancers | 04-01 |
| 07-02 | `02-DNS.md` | DNS hierarchy, recursive/iterative queries, record types, caching/TTL, UDP/TCP 53, DoT/DoH, Cisco client configuration | 07-01, 04-02 |
| 07-03 | `03-DHCPv4.md` | DORA, broadcast, options, leases, relay agent and Cisco DHCP configuration | 07-01, 04-02, 03-06 |
| 07-04 | `04-HTTP-and-HTTPS.md` | HTTP messages, methods, status codes, headers, persistent connections, HTTP/2/3, cookies, HTTPS and TLS | 07-01, 04-03, 06-06 |
| 07-05 | `05-Email-SMTP-POP3-IMAP.md` | Email sending and retrieval, MX records, ports and STARTTLS | 07-02, 07-04 |
| 07-06 | `06-Remote-Access-Telnet-SSH.md` | Telnet security, SSH architecture and Cisco configuration, console and web management | 04-03, 06-05 |
| 07-07 | `07-File-Transfer-FTP-TFTP-SCP-SFTP.md` | FTP control/data channels, active/passive modes, TFTP, SCP/SFTP extension, IOS file management | 07-06, 04-02 |
| 07-08 | `08-NTP.md` | Why time matters, stratum, NTP client/server modes | 04-02 |
| 07-09 | `09-SNMP-and-Syslog.md` | SNMP manager/agent/MIB/OID, operations, v2c/v3; syslog message fields and severity | 04-02, 06-03 |
| 07-10 | `10-REST-APIs.md` | REST principles, CRUD/HTTP mapping, authentication, JSON and network APIs | 07-04, 06-03 |
| 07-11 | `11-Browser-to-Website-Application-View.md` | Browser-to-website sequence: URL, cache, HSTS, DNS, TCP, TLS, HTTP and rendering | 07-02, 07-04 |

### 3.9 Cross-Layer Communication — `08-CROSS-LAYER-COMMUNICATION/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 08-01 | `01-Encapsulation-Master-Model.md` | Full encapsulation model; headers; per-hop MAC/TTL/checksum/FCS changes; NAT exception for IP addresses | 03-07 |
| 08-02 | `02-Same-LAN-File-Transfer.md` | File transfer on one LAN: ARP, switching, TCP and application | 04-07, 02-06 |
| 08-03 | `03-Different-Subnet-Communication.md` | Ping to another subnet: gateway decision, ARP and router reframing | 03-07 |
| 08-04 | `04-Multiple-Router-Path.md` | Multi-router path, per-hop header changes, TTL and routing decisions | 03-09 |
| 08-05 | `05-WiFi-Communication.md` | Wi-Fi association, 802.11/802.3 bridging, AP and DHCP | 02-15, 07-03 |
| 08-06 | `06-DNS-Resolution-End-to-End.md` | Stub resolver, recursive resolver, root/TLD/authoritative servers and caching | 07-02 |
| 08-07 | `07-TCP-Connection-End-to-End.md` | TCP setup, data transfer and shutdown, with packet-level view | 04-05 |
| 08-08 | `08-HTTPS-to-Remote-Server.md` | Remote HTTPS access including home-router PAT, Internet path, TLS and HTTP | 06-06, 03-20 |
| 08-09 | `09-Opening-a-Website-Full-Journey.md` | Full journey from a Wi-Fi laptop to a data-centre web server, including all devices and layers | 08-02–08-08 |
| 08-10 | `10-When-Connections-Fail.md` | Failure cases: cable, VLAN, gateway, DNS, TCP reset, firewall drop, MTU black hole | 08-09, 11-01 |

### 3.10 Troubleshooting — `11-TROUBLESHOOTING/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 11-01 | `01-Troubleshooting-Methodology.md` | Top-down, bottom-up, divide-and-conquer, path tracing, comparison, hypothesis-test loop and documentation | 00-09 |
| 11-02 | `02-Cisco-Show-and-Debug-Toolkit.md` | Show commands, logging, ping, extended ping, traceroute, debug precautions and packet captures | 03-11 |
| 11-03 | `03-Host-Side-Troubleshooting-Windows-macOS-Linux.md` | Verify host IP configuration, reachability and wireless settings on three operating systems | 03-06 |
| 11-04 | `04-Layer-by-Layer-Fault-Catalog.md` | Symptom → likely cause → verification command table for L1–L7 | Units 01–07 |
| 11-05 | `05-Case-Studies.md` | Realistic fault tickets and diagnosis workflows | 11-04 |

### 3.11 Revision — `12-REVISION/`

| ID | File | Scope |
|---|---|---|
| 12-01 | `01-Spaced-Repetition-Guide.md` | Optional retrieval practice and spaced-review guidance |
| 12-02 | `02-Flashcards-by-Module.md` | Module-by-module review cards; grows with lesson production |
| 12-03 | `03-Cheat-Sheets.md` | Subnet tables, ports, header fields and common commands |

### 3.12 CCNA Exam Preparation — `13-CCNA-EXAM-PREPARATION/`

| ID | File | Scope |
|---|---|---|
| 13-01 | `01-Exam-Blueprint-Mapping.md` | Final mapping of course coverage to the target exam blueprint |
| 13-02 | `02-Exam-Strategy-and-Question-Types.md` | Exam strategy, time management and question types |
| 13-03 | `03-Gap-Analysis-and-Next-Modules.md` | Deeply covered, introductory, and out-of-scope topics; suggested next study areas |
| 13-04 | `04-Final-Readiness-Checklist.md` | Exam-readiness checklist |

### 3.13 Security Fundamentals — `14-SECURITY-FUNDAMENTALS/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 14-01 | `01-Security-Concepts.md` | Threats, vulnerabilities, exploits, mitigation, security awareness, physical access, passwords, MFA, certificates and biometrics | 00-08 |
| 14-02 | `02-Device-Access-Control-and-AAA.md` | Local credentials, AAA, RADIUS/TACACS+ and fallback | 07-06 |
| 14-03 | `03-Access-Control-Lists.md` | Standard/extended, numbered/named ACLs, wildcard masks, order and implicit deny | 03-08, 04-01 |
| 14-04 | `04-Layer2-Attacks-and-Defenses.md` | MAC flooding, VLAN hopping, DHCP attacks, ARP spoofing, rogue RA, broadcast storms; port security, DHCP snooping, DAI; storm control/RA Guard extension | 02-12, 02-10, 07-03, 03-17 |
| 14-05 | `05-VPNs-and-IPsec.md` | Site-to-site and remote access VPNs; IKE, ESP, AH, tunnel/transport mode, GRE | 06-05, 03-09 |
| 14-06 | `06-Wireless-Security.md` | WPA/WPA2/WPA3, PSK, Enterprise, 802.1X/EAP and SAE | 02-15, 06-05 |

### 3.14 Network Operations, Automation, and AI — `15-NETWORK-OPERATIONS-AUTOMATION-AI/`

| ID | File | Scope | Prerequisite |
|---|---|---|---|
| 15-01 | `01-Network-Architectures.md` | Two-/three-tier campus, spine-leaf, WAN, SOHO, on-premises and cloud | 03-19, 02-12 |
| 15-02 | `02-Virtualization-VMs-Containers-VRFs.md` | Type 1/2 hypervisors, virtual switches, container networking, VRF; Kubernetes is optional depth | 02-08, 03-07 |
| 15-03 | `03-Network-Management-Approaches.md` | Device-, cloud-, controller- and automation-based management; infrastructure as code | 07-09 |
| 15-04 | `04-Controller-Based-and-SDN.md` | Control/data plane, underlay/overlay/fabric, northbound/southbound APIs | 03-07, 07-10 |
| 15-05 | `05-Configuration-Management-Ansible-Terraform.md` | Ansible/Terraform capabilities and differences; agentless/push and declarative/procedural approaches | 15-03, 06-03 |
| 15-06 | `06-AI-in-Network-Operations.md` | Predictive/generative AI, machine learning, agentic AI extension, and safe prompt selection | 15-03 |

**Total planned theory lessons: 116.**

## 4. Packet Tracer Labs — 100 Labs

**Target environment:** Packet Tracer 9.0.0 on Windows. Device-model and command support must be checked when each lab is written and tested.

### 4.1 Lab Types

- **Drill (Y):** A short task, success criteria, optional hints, and related theory. The learner designs the topology, addressing, and configuration. A phase-level answer file contains a concise solution and simulator limitations.
- **Full lab (T):** A structured topology, addressing table, detailed task list, and (where appropriate) intentionally incorrect configurations for break-fix practice. It has a separate solution file.

The design target is **69 drills and 31 full labs**. A full lab is used when a fixed topology or a broken configuration is valuable, rather than for every simple task.

### 4.2 Packet Tracer Support Labels

| Label | Meaning |
|---|---|
| ✅ | Known to be supported; verify commands when the lab is written |
| ⚠️ | Partial or uncertain support; verify before relying on it |
| ❌ | Not available; use a host lab, code exercise, or conceptual alternative |

### 4.3 Lab Catalogue

| ID | Type | Topic |
|---|---|---|
| LAB-001 | Y | First network in Packet Tracer; Realtime and Simulation modes |
| LAB-002 | Y | Inspect a PDU in Simulation Mode |
| LAB-003 | Y | Cable types and link states |
| LAB-004 | Y | Hub, switch, and collision domains |
| LAB-005 | Y | Console access and IOS command modes |
| LAB-006 | Y | Basic device configuration and configuration files |
| LAB-007 | Y | Interface states and counters |
| LAB-008 | Y | Speed, duplex, and auto-negotiation |
| LAB-009 | Y | Serial WAN link, DCE/DTE and clock rate |
| LAB-010 | Y | Home wireless network |
| LAB-011 | T | Physical-layer break-fix |
| LAB-012 | Y | Inspect an Ethernet frame |
| LAB-013 | Y | MAC address learning, aging and flooding |
| LAB-014 | Y | Switch management SVI and Telnet |
| LAB-015 | Y | VLANs and access ports |
| LAB-016 | Y | VLANs across switches using 802.1Q trunks |
| LAB-017 | Y | Native VLAN, allowed VLANs and DTP |
| LAB-018 | Y | Voice VLAN, IP phone and edge-port settings |
| LAB-019 | Y | Verify network documentation with CDP and LLDP |
| LAB-020 | T | VLAN and trunk break-fix |
| LAB-021 | Y | ARP in action |
| LAB-022 | Y | Host IPv4 configuration and default gateway |
| LAB-023 | Y | Two LANs connected by a router; MAC rewrite |
| LAB-024 | Y | FLSM subnet design and implementation |
| LAB-025 | Y | VLSM plan for a multi-branch organisation |
| LAB-026 | Y | STP loops, broadcast storms and root election |
| LAB-027 | Y | Rapid PVST+ root and port states |
| LAB-028 | Y | PortFast, BPDU Guard, Root Guard and Loop Guard |
| LAB-029 | Y | EtherChannel: LACP, PAgP and static mode |
| LAB-030 | T | STP and EtherChannel break-fix |
| LAB-031 | Y | Static routing across three routers |
| LAB-032 | Y | Default route and floating static backup |
| LAB-033 | Y | Host routes, summary routes and longest-prefix match |
| LAB-034 | Y | Inter-VLAN routing with router-on-a-stick |
| LAB-035 | Y | Layer 3 switch: SVI, routed port and Layer 3 EtherChannel |
| LAB-036 | Y | ICMP, ping, extended ping, traceroute and TTL |
| LAB-037 | Y | MTU and fragmentation |
| LAB-038 | Y | Interpret a routing table |
| LAB-039 | T | Static-routing break-fix |
| LAB-040 | Y | OSPFv2 point-to-point adjacency and router ID |
| LAB-041 | Y | OSPFv2 DR/BDR election on broadcast networks |
| LAB-042 | Y | OSPF cost, passive interfaces and default-route advertisement |
| LAB-043 | T | OSPF adjacency break-fix |
| LAB-044 | Y | Interpret HSRP/FHRP state |
| LAB-045 | Y | IPv6 addressing: GUA, link-local and EUI-64 |
| LAB-046 | Y | NDP, SLAAC and DHCPv6 |
| LAB-047 | Y | IPv6 static routing |
| LAB-048 | Y, extension | Single-area OSPFv3 |
| LAB-049 | T | Dual-stack network and IPv6 break-fix |
| LAB-050 | Y | TCP handshake and connection termination |
| LAB-051 | Y | TCP and UDP: DNS and HTTP traffic |
| LAB-052 | Y | DHCPv4 server and DORA |
| LAB-053 | Y | DHCP relay and router DHCP client |
| LAB-054 | T | DHCPv4 break-fix |
| LAB-055 | Y | DNS server and name-resolution faults |
| LAB-056 | Y | HTTP and HTTPS request across layers |
| LAB-057 | Y | File transfer and backup with TFTP/FTP |
| LAB-058 | Y | Email: SMTP and POP3 |
| LAB-059 | Y | Secure remote management with SSH |
| LAB-060 | Y | NTP and syslog |
| LAB-061 | Y | SNMP communities and MIB queries |
| LAB-062 | Y | Publish a server using static NAT |
| LAB-063 | Y | Dynamic NAT pool and PAT |
| LAB-064 | Y | Standard ACL |
| LAB-065 | Y | Extended ACL |
| LAB-066 | Y | Named ACLs and VTY access control |
| LAB-067 | Y | Port security |
| LAB-068 | Y | DHCP snooping and Dynamic ARP Inspection |
| LAB-069 | Y, extension | Storm control and RA Guard |
| LAB-070 | Y | AAA: local users, RADIUS and TACACS+ |
| LAB-071 | Y | Enterprise wireless: WLC, lightweight APs and WPA2 |
| LAB-072 | Y | Site-to-site VPN with GRE and IPsec |
| LAB-073 | T | NAT and ACL break-fix |
| LAB-074 | Y | Controller-based network and REST API |
| LAB-075 | T | Build a small office network end to end |
| LAB-076 | T | Complete journey of opening a website |
| LAB-077 | T | Redundant two-tier campus design |
| LAB-078 | T | Multi-branch WAN with OSPF and central services |
| LAB-079 | Y | Dual-stack enterprise services |
| LAB-080 | T | Secure the management plane |
| LAB-081 | T | Wired and wireless integration |
| LAB-082 | T | Correct an inaccurate network diagram using CDP/LLDP |
| LAB-083 | T | Troubleshooting ticket: “I cannot access a website” |
| LAB-084 | T | Multi-fault Layer 2 scenario |
| LAB-085 | T | Multi-fault Layer 3 scenario |
| LAB-086 | T | DHCP, DNS and NAT service faults |
| LAB-087 | T | Security faults |
| LAB-088 | T | IPv6 faults |
| LAB-089 | T | Interface and performance faults |
| LAB-090 | T | Troubleshoot using packet capture |
| LAB-091 | T | Capstone: build an SMB network from scratch |
| LAB-092 | T | Capstone: high-availability campus |
| LAB-093 | Y | Capstone: dual-stack multi-branch OSPF network |
| LAB-094 | T | Capstone: services and security hardening |
| LAB-095 | Y | Capstone: branch, wireless and VPN |
| LAB-096 | T | CCNA-style configuration task 1 |
| LAB-097 | T | CCNA-style configuration task 2 |
| LAB-098 | T | CCNA-style troubleshooting task 1 |
| LAB-099 | T | CCNA-style troubleshooting task 2 |
| LAB-100 | T | Final design, build, document, break and repair |

The full lab files use the folder and answer-file structure defined in `09-PACKET-TRACER-LABS/README.md`. Full labs are divided into Beginner (001–025), Intermediate (026–061), Advanced (062–082), and Expert (083–100).

## 5. Real-Host and Code Exercises

### 5.1 Real-host labs — `16-REAL-HOST-LABS/HOST/`

| ID | Topic | Related theory |
|---|---|---|
| H01 | Verify IP configuration on Windows, macOS and Linux | 03-06, 11-03 |
| H02 | First Wireshark capture; Ethernet fields, FCS and checksum-offload warning | 00-09, 02-03 |
| H03 | Capture ARP and IPv6 NDP | 02-10, 03-17 |
| H04 | Wireless survey: band, channel, RSSI and interference | 01-08 |
| H05 | MTU and PMTUD using DF-bit ping | 03-12 |
| H06 | Compare traceroute types on Windows, Linux and macOS | 03-11 |
| H07 | Inspect TCP in Wireshark; handshake, window, retransmission, `ss`, `netstat` | 04-03–04-05 |
| H08 | Observe UDP and QUIC traffic | 04-02, 04-06 |
| H09 | TLS 1.3 handshake with Wireshark and `openssl s_client` | 06-06 |
| H10 | Inspect HTTP with `curl -v` | 07-04 |
| H11 | Inspect DNS records with `dig` and `nslookup` | 07-02 |
| H12 | Observe DHCP release/renew and DORA | 07-03 |
| H13 | SSH, SCP and SFTP | 07-06, 07-07 |
| H14 | Linux syslog and SNMP | 07-09 |
| H15 | VirtualBox NAT, bridged, host-only and internal networks | 15-02 |
| H16 | Build a virtual switch/router with Linux namespaces, veth and bridges | 15-02, 02-06, 03-07 |
| H17 | Docker bridge networks, port publishing and NAT | 15-02, 03-20 |
| H18 | Run network-device commands using Ansible | 15-05 |
| H19 | Select a generative-AI prompt for network operations | 15-06 |

Linux host labs use Fedora. The environment and commands are verified when each lab is written.

### 5.2 Code exercises — `16-REAL-HOST-LABS/CODE/`

These optional Python exercises use the standard library and are intended to make a mechanism concrete. They are secondary to the CCNA core.

| ID | Exercise | Related theory |
|---|---|---|
| K01 | Number-system converter and bitwise operations | 00-02, 00-03 |
| K02 | Line-coding simulator: NRZ, Manchester, MLT-3 | 01-03 |
| K03 | Calculate CRC-32 and detect a damaged frame | 02-04 |
| K04 | Toy switch: MAC learning and flooding | 02-06 |
| K05 | IPv4 header checksum and subnet calculator | 03-02, 03-04 |
| K06 | Mini-router lookup using longest-prefix match | 03-08 |
| K07 | TCP and UDP echo servers with sockets | 04-07 |
| K08 | UTF-8 encoder/decoder and Base64 | 06-02, 06-03 |

## 6. Question Bank

### 6.1 Categories

| Code | Category | Measures |
|---|---|---|
| B | Basic understanding | Correct definition and role |
| O | Intermediate technical | Field values, behaviour, calculations, command output |
| I | Advanced reasoning | Cause/effect and “what changes if…” |
| S | Real-world scenario | Applying knowledge to a described network |
| A | Troubleshooting | Moving from symptom to likely cause |
| MC | Multiple choice | CCNA-style single- or multiple-answer questions |
| K | Explain in your own words | Open-ended answer scored with a rubric |
| KK | Compare | When and why two technologies are chosen |

Difficulty levels range from 1 (basic) to 3 (challenging). Question files and answer keys are stored separately.

### 6.2 Indicative Question Targets

Targets are guides, not quotas. Quality and coverage take priority over quantity.

| Area | Target | Area | Target |
|---|---:|---|---:|
| FND | ~40 | PRS | ~30 |
| PHY | ~40 | APP | ~60 |
| DL | ~70 | SEC | ~50 |
| NET | ~120 | OPS | ~30 |
| TRN | ~40 | SES | ~10 |

### 6.3 Comprehensive Exams

CE-01–CE-06 are cumulative and include mixed review from earlier units. CE-00 is a historical starting-point diagnostic and does not count toward mastery.

| ID | Intended point | Coverage | Approx. questions |
|---|---|---|---:|
| CE-00 | Baseline diagnostic | 25 questions from the earlier OSI notes | 25 |
| CE-01 | After early Network Layer topics | Foundations, L1, early L2 and IPv4 | 40 |
| CE-02 | After IPv6 and routing foundations | L1–L3 | 50 |
| CE-03 | After Application Layer | All seven layers | 60 |
| CE-04 | After operations/security | All topics, including security and operations | 60 |
| CE-05 | Final exam practice | CCNA-style mock exam 1 | 100 |
| CE-06 | Final exam practice | CCNA-style mock exam 2 | 100 |

## 7. Diagram Plan

The intended diagrams include binary place values (00-02), transistor switching (00-05), bit-to-signal path (01-01), line coding (01-03), differential signalling (01-06), fibre reflection (01-07), Ethernet/VLAN frame fields (02-03/02-09), switching and VLAN flows (02-06/02-08), STP (02-11), IPv4/IPv6 headers (03-02/03-16), subnetting (03-04), host forwarding (03-06), router pipeline (03-07), OSPF states (03-14), NAT (03-20), TCP (04-03), congestion window (04-05), TLS (06-06), DNS/DHCP (07-02/07-03), encapsulation (08-01), and the end-to-end website journey (08-09).

## 8. Packet Tracer Limitations and Alternatives

| Topic | PT support | Alternative |
|---|---|---|
| Signal, attenuation, EMI and distance | Not realistically simulated | 01-05 concepts, K02 and real output interpretation |
| Duplex-mismatch symptoms | Partial | Interpret real command output in LAB-008/LAB-089 |
| Real host operating systems | Not a general-purpose host environment | H01, H04 and 11-03 |
| Raw packet bytes | PDU details available; raw bytes limited | H02, H07–H12 |
| MTU and PMTUD | Partial | H05 |
| TCP congestion control | Not fully represented | H07 and 04-05 |
| TLS handshake details | HTTPS available; handshake detail limited | H09 |
| DNS MX/PTR records | Partial | H11 |
| SCP/SFTP | Partial | H13 |
| SNMP | Partial | H14 |
| VRRP | Partial | Interpret output in 03-19 |
| DAI, storm control and RA Guard | Partial | Concepts and output interpretation in 14-04 |
| Hypervisor/container networking | Not represented sufficiently | H15–H17 |
| Ansible | Not represented | H18 |
| Agentic/generative AI | Not represented | 15-06 and H19 |

## 9. CCNA 200-301 Blueprint Mapping

The primary target is the **v1.1 exam blueprint**. Topic labels below are concise paraphrases; consult Cisco's official exam-topic document in `SOURCES.md` for the authoritative wording. The detailed exam mapping is also planned for lesson 13-01.

### 9.1 v1.1 Domains and Topics (53 topics)

| Objective | Topic summary | Theory / practice |
|---|---|---|
| **1.0 Network Fundamentals (20%)** | | |
| 1.1 | Roles of network components: routers, L2/L3 switches, NGFW/IPS, APs/controllers, endpoints, servers and PoE | 00-08, 01-06; LAB-001, 018 |
| 1.2 | Network topologies: two-/three-tier, spine-leaf, WAN, SOHO, on-premises and cloud | 15-01; LAB-077 |
| 1.3 | Physical interfaces and cable types; shared media and point-to-point | 01-06, 01-07, 01-09, 02-05; LAB-003, 004 |
| 1.4 | Interface/cable issues: collisions, errors, speed and duplex mismatch | 01-10, 02-05; LAB-007, 008, 011, 089 |
| 1.5 | Compare TCP and UDP | 04-01–04-06; LAB-050, 051; H07 |
| 1.6 | Configure and verify IPv4 addressing and subnetting | 03-03–03-06; LAB-022, 024, 025, 085 |
| 1.7 | Explain the need for private IPv4 addressing | 03-03, 03-20; LAB-063 |
| 1.8 | Configure and verify IPv6 addressing and prefixes | 03-16, 03-17; LAB-045, 046, 049, 088 |
| 1.9 | IPv6 address types: GUA, ULA, link-local, anycast, multicast, EUI-64 | 03-16; LAB-045 |
| 1.10 | Verify host IP parameters on client operating systems | 03-06, 11-03; H01 |
| 1.11 | Wireless principles: non-overlapping channels, SSID, RF and encryption | 01-08, 02-15, 14-06; LAB-010, H04 |
| 1.12 | Virtualisation basics: server virtualisation, containers and VRF | 15-02; conceptual |
| 1.13 | Switching concepts: MAC learning/aging, forwarding, flooding and MAC table | 02-06, 02-07; LAB-012, 013 |
| **2.0 Network Access (20%)** | | |
| 2.1 | VLANs: data/voice access ports, default VLAN and inter-VLAN connectivity | 02-08, 03-10; LAB-015, 018, 034, 035 |
| 2.2 | Switch interconnection: trunks, 802.1Q and native VLAN | 02-09; LAB-016, 017, 020, 084 |
| 2.3 | CDP and LLDP | 02-14; LAB-019, 082 |
| 2.4 | Layer 2/Layer 3 EtherChannel using LACP | 02-13; LAB-029, 035, 084 |
| 2.5 | Rapid PVST+: root, port roles/states, PortFast, guards and BPDU protection | 02-11, 02-12; LAB-026–030, 077 |
| 2.6 | Cisco wireless architectures and AP modes | 02-16; LAB-071 |
| 2.7 | Physical connections of WLAN components: AP, WLC, access/trunk, LAG | 02-16; LAB-071, 081 |
| 2.8 | Device management access: Telnet, SSH, HTTP/HTTPS, console, TACACS+/RADIUS and cloud management | 07-06, 14-02, 15-03; LAB-005, 014, 059, 070, 080 |
| 2.9 | Interpret WLAN GUI configuration | 02-16, 14-06; LAB-071 |
| **3.0 IP Connectivity (25%)** | | |
| 3.1 | Routing-table components | 03-08; LAB-023, 038 |
| 3.2 | Router forwarding decision: LPM, AD and metric | 03-07, 03-08; LAB-023, 033, 038 |
| 3.3 | IPv4/IPv6 static routes: default, network, host and floating | 03-09, 03-18; LAB-031–033, 039, 047, 049, 085, 088 |
| 3.4 | Single-area OSPFv2: adjacency, point-to-point, broadcast DR/BDR and router ID | 03-14, 03-15; LAB-040–043, 078, 085 |
| 3.5 | First-hop redundancy protocols (FHRP) | 03-19; LAB-044, 077 |
| **4.0 IP Services (10%)** | | |
| 4.1 | Inside source NAT (static and pool) | 03-20; LAB-062, 063, 073, 078, 086 |
| 4.2 | NTP client and server modes | 07-08; LAB-060, 080 |
| 4.3 | Roles of DHCP and DNS | 07-02, 07-03; LAB-052, 055, 086; H11/H12 |
| 4.4 | SNMP function | 07-09; LAB-061, 080 |
| 4.5 | Syslog facilities and severity levels | 07-09; LAB-060, 080 |
| 4.6 | DHCP client and relay | 07-03; LAB-053, 054, 078 |
| 4.7 | QoS per-hop behaviour | 03-21; conceptual |
| 4.8 | Remote access using SSH | 07-06; LAB-059, 080; H13 |
| 4.9 | TFTP and FTP | 07-07; LAB-057 |
| **5.0 Security Fundamentals (15%)** | | |
| 5.1 | Security concepts: threats, vulnerabilities, exploits and mitigation | 14-01; conceptual |
| 5.2 | Security programme: awareness, training and physical access | 14-01; conceptual |
| 5.3 | Device access control using local passwords | 14-02; LAB-006, 080 |
| 5.4 | Password policy: management, complexity, MFA, certificates and biometrics | 14-01; conceptual |
| 5.5 | IPsec remote-access and site-to-site VPNs | 06-05, 14-05; LAB-072 |
| 5.6 | Configure and verify ACLs | 14-03; LAB-064–066, 073, 080 |
| 5.7 | Layer 2 security: DHCP snooping, DAI and port security | 14-04; LAB-067, 068, 087 |
| 5.8 | AAA concepts | 14-02; LAB-070, 080 |
| 5.9 | WPA, WPA2 and WPA3 | 14-06; LAB-071 |
| 5.10 | Configure a WPA2-PSK WLAN using a GUI | 14-06; LAB-010, 071 |
| **6.0 Automation and Programmability (10%)** | | |
| 6.1 | Impact of automation on network management | 15-03; conceptual |
| 6.2 | Traditional versus controller-based networking | 03-01, 15-04; LAB-074 |
| 6.3 | Controller-based and software-defined architecture: overlay/underlay/fabric, control/data planes, northbound/southbound APIs | 15-04; conceptual |
| 6.4 | Predictive/generative AI and machine learning in network operations | 15-06; conceptual |
| 6.5 | REST API characteristics: authentication, CRUD, HTTP methods and data encoding | 07-10; LAB-074 |
| 6.6 | Configuration-management tools: Ansible and Terraform | 15-05; H18 is an extension |
| 6.7 | JSON data components | 06-03, 07-10; LAB-074 |

### 9.2 v2.0 Extensions

If the exam target changes to v2.0, review the additional/expanded topics below. These are retained in the curriculum but are not part of the current v1.1 core priority:

| v2.0 objective | Topic | Course location |
|---|---|---|
| 1.2 | Hypervisors, VMs and container networking | 15-02; H15–H17 |
| 1.7 | DHCPv4 troubleshooting | 07-03; LAB-054, LAB-086 |
| 2.2 | Endpoint port profiles | LAB-018 |
| 2.4 | Troubleshooting tools including packet capture | 11-02; LAB-090; H02 |
| 3.3 | Single-area OSPFv3 | 03-18; LAB-048 |
| 3.4 | Interpret VRRP state | 03-19 |
| 4.2 | SFTP and SCP file management | 07-07; H13 |
| 4.4 | Diagnose DNS record faults | 07-02; LAB-055; H11 |
| 4.7 | Storm control and RA Guard | 14-04; LAB-069 |
| 5.1–5.2 | Agentic AI and prompt selection for generative AI | 15-06; H19 |
| 5.3 | Network-management approaches and infrastructure as code | 15-03 |
| 5.5 | Execute commands with Ansible | 15-05; H18 |

### 9.3 Initial Out-of-Scope List

The following are not core CCNA v1.1 topics in this plan: multi-area OSPF configuration, EIGRP/BGP configuration beyond conceptual examples, MPLS, detailed SD-WAN, multicast routing, advanced QoS configuration, cloud-provider networking in depth, Kubernetes CNI internals, and advanced Python network automation. The final scope review belongs in 13-03.

## 10. Design Notes and Corrections

- The course target was changed to CCNA v1.1 by decision; v2.0 differences remain listed as extensions.
- Lesson 00-09 was added to introduce OSI and TCP/IP before studying each layer.
- Security has its own module because ACLs, Layer 2 defenses, and VPNs rely on multiple earlier layers.
- Operations, automation, and AI have their own module because these topics do not belong to one OSI layer.
- Real-host labs cover features Packet Tracer cannot represent accurately.
- Optional code exercises use the learner's software background to make mechanisms tangible; they are not a prerequisite for the exam.
- Troubleshooting methodology is introduced early, then applied in later layer-specific and integrated scenarios.

## 11. Relationship to the Earlier OSI Notes

The earlier user notes (`USR-OSI-NOTES`) are a high-level overview and a source for the historical CE-00 diagnostic test. They are not a substitute for the current lesson sequence and are not copied wholesale into this curriculum.

| Earlier notes section | Topic | Current lessons |
|---|---|---|
| 1–2 | OSI introduction, TCP/IP, PDU, headers and trailers | 00-09, 08-01 |
| 3 | Application protocols | 07-01–07-09, 06-06 |
| 4 | Presentation, encoding, formats, encryption and compression | 06-01–06-06 |
| 5 | Session layer | 05-01, 05-02 |
| 6.1–6.5 | Ports, TCP and UDP | 04-01–04-06 |
| 6.6 | SCTP | 04-06 |
| 6.7 | Layer 4 firewalls and load balancers | 04-01, 14-03 |
| 7.1–7.4 | IP addressing and routing | 03-01–03-08 |
| 7.5–7.6 | TTL and ICMP | 03-02, 03-11 |
| 7.7 | Routing protocols | 03-13–03-15 |
| 7.8 | ARP | 02-10 |
| 8.1–8.4 | MAC, Ethernet and switches | 02-02–02-07 |
| 8.5–8.6 | VLANs, trunks and STP | 02-08, 02-09, 02-11, 02-12 |
| 8.7 | Wi-Fi | 01-08, 02-15, 02-16, 14-06 |
| 8.8 | PPP | 02-01 |
| 9 | Physical layer | 01-01–01-10 |
| 10 | Encapsulation and decapsulation | 08-01 |
| 11 | Packet journey, HTTPS and NAT | 08-03, 08-04, 08-08, 08-09 |
| 12–13 | Switch/router roles, MAC/IP/ports | 02-06, 03-07, 08-01 |
| 14–15 | TCP/UDP, VLANs, subnetting, ARP and NAT | 04-06, 02-08, 03-04, 02-10, 03-20 |
| 16 | Troubleshooting and host commands | 11-01, 11-03, 11-04, H01 |
| 17 | Common mistakes | “Common Misunderstandings” sections in relevant lessons |
| 19 | Original 25-question self-test | CE-00 |

### 11.1 Corrections to Carry into the Lessons

| Earlier note | Correction | Current lessons |
|---|---|---|
| The home-router packet example shows an unchanged source IP before mentioning NAT later | If that same home router performs NAT, the WAN packet already has the translated public source address. IP addresses stay unchanged only across hops where NAT is not performed. | 03-20, 08-08 |
| The router decides whether the destination is local | The **sending host** uses its own IP address and mask to decide local versus remote. A router uses its routing table and longest-prefix match. | 03-06, 03-08 |
| IPv6 routers update an IPv4-like header checksum | IPv6 has no header checksum field. Integrity checks are provided at other layers. | 03-16 |
| Ethernet has no TTL field, described as a router TTL issue | TTL is a field in the IP header, not a router feature. Ethernet has no hop counter, which is why Layer 2 loops need STP. | 02-11 |
| Routed and routing protocols are not clearly distinguished | IP is a routed protocol. OSPF, RIP and BGP are routing protocols that distribute route information. | 03-13 |
