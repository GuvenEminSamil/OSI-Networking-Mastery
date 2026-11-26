# Sources and Research Methodology

> This file defines (1) how course content is researched and verified and (2) the source register. Lesson files cite sources by the identifiers recorded here.
>
> **Register created:** 2026-11-19. Source access states reflect the original research notes unless updated below.

## 1. Research Methodology

### 1.1 Source Hierarchy

| Level | Source type | Use |
|---:|---|---|
| 1 | Cisco official documentation and CCNA exam topics | Exam scope, Cisco commands, Cisco-specific behaviour and defaults |
| 2 | IEEE and other technical standards (TIA, ISO/IEC, ITU-T) | Layer 1/Layer 2 behaviour, frame formats and cabling |
| 3 | IETF RFCs and IANA registries | IP and upper-layer protocol behaviour, address blocks and port numbers |
| 4 | Official documentation from other vendors (operating systems, Wireshark, Ansible, OpenSSL) | Host labs and tool usage |
| 5 | Reputable textbooks | Conceptual explanations and further reading |
| 6 | Reliable educational resources | Cross-checking and teaching examples only |

### 1.2 Verification Workflow

1. Every important technical claim should be supported by at least one Level 1–3 source. Cite a section or clause number where possible.
2. Numeric values (field sizes, timers, defaults, port numbers) should come from primary sources. Cisco-specific defaults must be supported by Cisco documentation and marked `[CISCO-SPECIFIC]`.
3. Commands should be checked against Cisco command references and assigned a Packet Tracer support label (Section 3). Note syntax differences between IOS and IOS XE.
4. Secondary sources (Levels 5–6) are not the sole evidence for a technical claim; use them for cross-checking or explanation.
5. If sources conflict, prefer the primary source and note the discrepancy in the relevant lesson.
6. Mark intentional simplifications with `[SIMPLIFIED]` and briefly describe the real behaviour.
7. Do not present unverified information as fact. Mark it “not verified” and add it to the open validation list in `PROGRESS.md`.
8. Do not force a protocol into one OSI layer when its functions span multiple layers (for example, ARP, TLS, DHCP, and OSPF). Distinguish OSI theory (`[OSI-THEORY]`) from practical TCP/IP implementation (`[TCP/IP-PRACTICE]`).

### 1.3 Known Limitations

- **Packet Tracer:** This environment cannot run Packet Tracer. Simulator support is labelled from documented or known behaviour; the learner must verify it in their installed version. A learner-tested feature is labelled 🧪 and recorded with the version in `PROGRESS.md`.
- **IEEE standards:** Full standards may require payment or controlled access. Do not cite an unverified clause number.
- **Textbooks:** Full textbook contents may not be available. They are recommended for further reading and are not the only evidence for a claim.
- **Dynamic web pages:** Some Cisco pages load with JavaScript and may not be directly readable. Use an official PDF or mark the item open for verification.

## 2. Citation Format in Lesson Files

| Source type | Format | Example |
|---|---|---|
| RFC | `[RFC number §section]` | `[RFC 9293 §3.5]` |
| IEEE | `[IEEE number, Clause]` | `[IEEE 802.3, Clause 25]` (only when verified) |
| Cisco document | `[CISCO: identifier, section]` | `[CISCO: CISCO-V2, 3.3]` |
| Textbook | `[identifier, chapter]` | `[TXT-STEVENS, Chapter 13]` |
| CCNA exam objective | `[CCNA version code]` | `[CCNA v2.0 3.3]` |

Every lesson ends with a “Sources” section listing the identifiers it uses. Add a source here before citing it from a lesson.

## 3. Status Labels

### 3.1 Packet Tracer Support

| Label | Meaning |
|---|---|
| ✅ | Known to be supported in Packet Tracer; verify command-level details when writing the lab |
| ⚠️ | Partial or uncertain support; verify before relying on it and use an alternative if needed |
| ❌ | Not available; use a host lab, code exercise, or conceptual task |
| 🧪 | Tested by the learner in Packet Tracer; record the exact version in `PROGRESS.md` |

### 3.2 Source Access Status

| Status | Meaning |
|---|---|
| Read | Source material was directly inspected; record the access date |
| Search summary | Relevant result/snippet was inspected, but not the complete source |
| Planned | To be read while writing the relevant lesson |
| Open | Not accessible or not yet verified |

## 4. Source Register

### 4.1 Planning-Stage Sources (access recorded: 2026-11-19)

| ID | Source | Level | Status | Use |
|---|---|---:|---|---|
| USR-OSI-NOTES | User-provided notes: *OSI Model (Open Systems Interconnection) — The Seven-Layer Structure of Computer Networks* (`OSI.docx`, 20 sections) | — | Read | Starting-point reference, CE-00 diagnostic, common-mistake list and section mapping in `CURRICULUM.md` §11. This is user material, not primary technical evidence. |
| CISCO-V2 | Cisco, *Implementing and Administering Cisco Solutions (200-301 CCNA) v2.0 — Exam Topics* (PDF). https://learningcontent.cisco.com/documents/marketing/exam-topics/200-301_CCNA_v2.0_Exam_Topics_PDF.pdf | 1 | Read | v2.0 domains, weighting and 29 topics |
| CISCO-V2-PAGE | Cisco Learning Network, CCNA v2.0 Exam Topics. https://learningnetwork.cisco.com/s/ccna-v2-exam-topics | 1 | Search summary | v2.0 first exam date: 3 February 2027. Page body was JavaScript-loaded; details were taken from CISCO-V2. |
| CISCO-V11 | Cisco, *CCNA Exam v1.1 (200-301)* (PDF). https://learningcontent.cisco.com/documents/marketing/exam-topics/200-301-CCNA-v1.1.pdf | 1 | Read | **Primary exam target.** Six v1.1 domains, their weightings, 53 topics and subtopics |
| CISCO-V11-PAGE | Cisco Learning Network, CCNA Exam Topics (v1.1). https://learningnetwork.cisco.com/s/ccna-exam-topics | 1 | Search summary | Final v1.1 exam date recorded as 2 February 2027 |
| CISCO-POLICY | Cisco, *Exam, Testing, and Certification Policies*. https://www.cisco.com/site/us/en/learn/training-certifications/exams/policies.html | 1 | Search summary | Restrictions relating to candidates residing in sanctioned countries |
| SEC-PV-RU | The Open Group, *FAQ — Exam Based Certifications*. https://www.opengroup.org/certifications/faqs | 6 | Search summary | Background on Pearson VUE's suspension of exam services in Russia from 7 March 2022 |
| SEC-V11-LIST | ComputingForGeeks, *CCNA 200-301 Exam Topics: The Complete v1.1 List Explained*. https://computingforgeeks.com/ccna-exam-topics/ | 6 | Read | Cross-check of v1.1 topic list and domain weightings; this is an independent summary, not Cisco wording |
| SEC-V2-DATES | NetworkLessons, *CCNA 200-301*. https://networklessons.com/cisco/ccna-200-301 ; Cisnet, *CCNA v2.0 vs v1.1*. https://www.cisnet.ca/blog/ccna-v2-0-vs-v1-1 | 6 | Read | Announcement and transition dates; comparison of topics added or removed |
| SEC-V2-LIST | CertRamp Learning, *CCNA 200-301 Exam Guide*. https://certramplearning.com/guides/ccna-200-301/ | 6 | Read | Cross-check of the v2.0 topic list |
| SEC-OCG-V11 | Cisco Press, *CCNA 200-301 Official Cert Guide, Volume 2, 2nd Edition* (Odom, Hucaby, Gooley), 22 July 2024. https://www.ciscopress.com/title/0138215049 | 5 | Publisher page read | Confirms the official v1.1 study-guide publication and scope |
| SEC-PT-VER | Packet Tracer version references: https://packettracernetwork.com/ ; https://www.computernetworkingnotes.com/ccna-study-guide/download-packet-tracer-for-windows-and-linux.html | 6 | Read | Background on Packet Tracer 9.0.0 and 8.2.2. Confirm version details against official NetAcad release information when available. |

### 4.2 Cisco Primary Sources

| ID | Source | Use |
|---|---|---|
| CISCO-CFG | Configuration guides and command references for Catalyst 2960, 3650 and 9000 series and ISR 1900, 2900 and 4000 series (IOS 15 and IOS XE). Add exact URLs when a lesson is written. | Commands, defaults and verification output |
| CISCO-PT | Cisco Packet Tracer official documentation and NetAcad release notes | Device models and supported features |
| CISCO-NETACAD | Cisco Networking Academy (NetAcad) CCNA course material. https://www.netacad.com | Packet Tracer setup and Simulation Mode |
| CISCO-WLC | Cisco WLC configuration guides | 02-16, LAB-071 |
| CISCO-DESIGN | Cisco campus design guides | 15-01 |

### 4.3 IETF RFCs

RFCs are available at `https://www.rfc-editor.org/rfc/rfcNNNN`. Use the current RFC where a specification has been updated (for example, RFC 9293 rather than RFC 793 for the current TCP specification).

| Area | RFCs | Related lessons |
|---|---|---|
| Architecture and layers | 1122 (host requirements), 1123 (application/support requirements), 3439 (architectural principles and limits of layering) | 00-09, 05-02 |
| ARP and Layer 2 | 826 (ARP), 5227 (IPv4 address conflict detection and gratuitous ARP), 1661 (PPP) | 02-01, 02-10 |
| IPv4 | 791, 792, 1071, 1191, 1812, 1918, 3021, 3927, 4632, 5737, 6598, 6890 | 03-02–03-12 |
| QoS and ECN | 2474 (DSCP), 3168 (ECN) | 03-02, 03-21, 04-05 |
| Routing and FHRP | 2328 (OSPFv2), 5340 (OSPFv3), 2453 (RIPv2), 4271 (BGP-4), 2281 (HSRP, informational), 5798 (VRRPv3) | 03-13–03-19 |
| NAT | 2663 (NAT terminology), 3022 (traditional NAT) | 03-20 |
| IPv6 | 8200, 4291, 5952, 4193, 3849, 4443, 4861, 4862, 8981, 8415, 8201, 6105 | 03-16–03-18, 14-04 |
| Transport | 768 (UDP), 9293 (TCP), 5681 (congestion control), 6298 (RTO), 7323 (TCP extensions/window scaling), 2018 (SACK), 9000 (QUIC), 9260 (SCTP), 6335 (port procedures) | 04-* |
| Presentation and security | 8446 (TLS 1.3), 3629 (UTF-8), 8259 (JSON), 4648 (Base64), 1951 (DEFLATE), 1952 (gzip), 5280 (X.509 PKI), 4301 (IPsec architecture), 4303 (ESP), 7296 (IKEv2), 2784 (GRE) | 06-*, 14-05 |
| DNS | 1034, 1035, 3596 (AAAA), 7858 (DNS over TLS), 8484 (DNS over HTTPS) | 07-02 |
| DHCP | 2131, 2132, 1542 (BOOTP relay) | 07-03 |
| Web | 9110, 9112, 9113, 9114, 3986, 6265, 6797 | 07-04, 07-11 |
| Email | 5321 (SMTP), 6409 (message submission), 8314 (implicit TLS), 1939 (POP3), 9051 (IMAP4rev2) | 07-05 |
| Remote access and file transfer | 854 (Telnet), 4251–4254 (SSH), 959 (FTP), 1350 (TFTP) | 07-06, 07-07 |
| Management | 5905 (NTPv4), 3411–3418 (SNMPv3 framework), 5424 (syslog), 2865 (RADIUS), 8907 (TACACS+) | 07-08, 07-09, 14-02 |

**Note:** SFTP and SCP do not have published RFC specifications in this register. SFTP is described using the IETF `draft-ietf-secsh-filexfer` work and OpenSSH documentation.

### 4.4 IEEE and Other Standards

| ID | Standard | Related lessons |
|---|---|---|
| IEEE-8023 | IEEE 802.3 Ethernet (PHYs, auto-negotiation, MAC and PoE) | 01-03, 01-06, 01-09, 02-03, 02-05 |
| IEEE-8021Q | IEEE 802.1Q VLAN bridging; current editions also cover bridging and spanning-tree material | 02-06, 02-08, 02-09, 02-11, 02-12 |
| IEEE-8021D | IEEE 802.1D-2004 (historical STP/RSTP; 802.1w was incorporated) | 02-11, 02-12 |
| IEEE-8021AX | IEEE 802.1AX Link Aggregation and LACP (formerly 802.3ad) | 02-13 |
| IEEE-8021AB | IEEE 802.1AB LLDP | 02-14 |
| IEEE-8021X | IEEE 802.1X port-based network access control | 14-06 |
| IEEE-8022 | IEEE 802.2 LLC | 02-01 |
| IEEE-80211 | IEEE 802.11 and related amendments (n, ac, ax) | 01-08, 02-15 |
| TIA-568 | ANSI/TIA-568 structured cabling standards, including T568A/B; verify the current edition | 01-06 |
| ISO-7498 | ISO/IEC 7498-1:1994 / ITU-T X.200 (OSI Basic Reference Model) | 00-09 |
| ISO-8327 | ISO 8327 / ITU-T X.225 (OSI session protocol) | 05-01 |
| ISO-8823 | ISO 8823 / ITU-T X.226 (OSI presentation protocol) | 06-01 |
| ITU-ASN1 | ITU-T X.680 (ASN.1), X.690 (BER/DER), X.509 (certificates) | 06-01, 06-03, 06-05 |
| ISO-10589 | ISO/IEC 10589 (IS-IS) | 03-13 |
| STD-IEC80000 | IEC 80000-13 (quantities and units in information technology, including binary prefixes such as kibi and mebi) | 00-02 |

### 4.5 Registries and Reference Data

| ID | Source | Use |
|---|---|---|
| IANA-PORTS | IANA Service Name and Transport Protocol Port Number Registry | Port numbers |
| IANA-PROTO | IANA Protocol Numbers | IPv4 Protocol and IPv6 Next Header values |
| IANA-SPECIAL | IANA IPv4 and IPv6 Special-Purpose Address Registries | Special-use address ranges |
| IEEE-RA | IEEE Registration Authority (OUI and EtherType registrations) | 02-02, 02-03 |
| UNICODE | The Unicode Standard (unicode.org) | 06-02 |

### 4.6 Textbooks (Further Reading)

| ID | Book | Most relevant lessons |
|---|---|---|
| TXT-PETZOLD | Charles Petzold, *Code: The Hidden Language of Computer Hardware and Software*, 2nd ed., Microsoft Press | 00-01–00-05 |
| TXT-HARRIS | David M. Harris and Sarah L. Harris, *Digital Design and Computer Architecture*, Morgan Kaufmann | 00-03–00-07, optional depth |
| TXT-KUROSE | James F. Kurose and Keith W. Ross, *Computer Networking: A Top-Down Approach*, 8th ed., Pearson | All layers |
| TXT-TANENBAUM | Andrew S. Tanenbaum, Nick Feamster and David J. Wetherall, *Computer Networks*, 6th ed., Pearson | L1–L2 and general networking |
| TXT-STEVENS | Kevin R. Fall and W. Richard Stevens, *TCP/IP Illustrated, Volume 1: The Protocols*, 2nd ed., Addison-Wesley | 03-*, 04-*, 07-* |
| TXT-SPURGEON | Charles E. Spurgeon and Joann Zimmerman, *Ethernet: The Definitive Guide*, 2nd ed., O'Reilly | 01-06, 01-09, 02-03 |
| TXT-PERLMAN | Radia Perlman, *Interconnections*, 2nd ed., Addison-Wesley | 02-11, 03-13, optional depth |
| TXT-ODOM | Wendell Odom et al., *CCNA 200-301 Official Cert Guide*, Volumes 1 and 2, 2nd ed., Cisco Press (v1.1). Update if a new v2.0 edition is published. | CCNA preparation |

### 4.7 Educational Resources and Tool Documentation

| ID | Source | Use |
|---|---|---|
| EDU-JITL | Jeremy's IT Lab, free CCNA course | Cross-check only (Level 6) |
| TOOL-WIRESHARK | Wireshark User's Guide and sample captures. https://www.wireshark.org/docs/ | H02, H07–H12 |
| TOOL-ANSIBLE | Ansible documentation, including the `cisco.ios` collection. https://docs.ansible.com | 15-05, H18 |
| TOOL-LINUX | iproute2 and Linux manual pages (`ip`, `ss`, `ip netns`). https://man7.org/linux/man-pages/ | H01, H07, H16 |
| TOOL-OPENSSL | OpenSSL documentation (`s_client`) | H09 |
| TOOL-OPENSSH | OpenSSH documentation (`ssh`, `scp`, `sftp`) | H13 |

### 4.8 Foundational Papers and Learning Science

| ID | Source | Use |
|---|---|---|
| PAPER-SHANNON | C. E. Shannon, “A Mathematical Theory of Communication,” *Bell System Technical Journal*, 27 (1948) | 00-01: bits, information and entropy |
| LRN-ROEDIGER | H. L. Roediger and J. D. Karpicke, “Test-Enhanced Learning,” *Psychological Science*, 17(3), 2006 | 12-01: retrieval practice |
| LRN-CEPEDA | N. J. Cepeda et al., “Distributed Practice in Verbal Recall Tasks,” *Psychological Bulletin*, 132(3), 2006 | 12-01: spaced practice |
| LRN-DUNLOSKY | J. Dunlosky et al., “Improving Students' Learning With Effective Learning Techniques,” *Psychological Science in the Public Interest*, 14(1), 2013 | 12-01: comparison of learning techniques |

### 4.9 Sources Used for Foundations Lessons 00-05–00-09 and Foundations Questions

Access notes below refer to the research checkpoint recorded on 2026-11-20. “Search summary” means only relevant search-result material was inspected, not necessarily the complete source.

| ID | Source | Level | Status | Use |
|---|---|---:|---|---|
| CISCO-V11 | Cisco official CCNA v1.1 exam-topics PDF, Section 4.1 | 1 | Search summary rechecked | 00-08: objective 1.1 subtopics |
| CISCO-NETACAD | Cisco Networking Academy CCNA material (University of Tartu mirror, module 6.3.1.3) and NSRC workshop notes for cross-checking | 1 | Search summary | 00-05: router memory types (RAM, ROM, NVRAM, flash) |
| CISCO-PCM | Cisco, *Waveform Coding Techniques*, document 8123. https://www.cisco.com/c/en/us/support/docs/voice/h323/8123-waveform-coding.html | 1 | Search summary | 00-06: pre-sampling filtering, PCM and 64 kbps |
| CISCO-VOIP-BW | Cisco, *Voice Over IP – Per Call Bandwidth Consumption*, document 7934. https://www.cisco.com/c/en/us/support/docs/voice/voice-quality/7934-bwidth-consume.html | 1 | Search summary | 00-06: G.711, 20 ms packetisation, 50 packets/s, 87.2 kbps per call over Ethernet under the stated header assumptions |
| CISCO-IFCOUNT | Cisco documents and Cisco Community discussions, including *Troubleshoot Ignored Errors*, document 18003 | 1 / 6 | Search summary | 00-07: overrun, ignored and no-buffer counters |
| STD-TI-LOGIC | Texas Instruments, *Logic Guide* (SDYU001, 2017). https://www.ti.com/lit/sdyu001 | 4 | Search summary | 00-05: 5 V TTL and 3.3 V LVTTL thresholds |
| STD-JEDEC-DDR4 | JEDEC JESD79-4, DDR4 SDRAM | 2 | Open; primary text is paid and was not read | 00-05: 64 ms refresh window; cross-checked against secondary sources |
| SEC-DRAM | *HiRA: Hidden Row Activation for Reducing Refresh Latency of Off-the-Shelf DRAM Chips* (arXiv:2209.10198), arXiv:2303.07445, and University of Maine ECE 571 notes | 5–6 | Search summary | 00-05: DDR4 tREFW/tREFI values and temperature-related refresh behaviour |
| PAPER-COHEN | D. Cohen, “On Holy Wars and a Plea for Peace,” IEN 137, 1 April 1980. https://www.ietf.org/rfc/ien/ien137.txt | 3 | Search summary | 00-06: origin of the terms big-endian and little-endian |
| RFC-791 | RFC 791, Appendix B, *Data Transmission Order* | 3 | Search summary | 00-06: octet transmission order; 00-09: “Internet datagram” term |
| ITU-G711 | ITU-T G.711, *Pulse code modulation (PCM) of voice frequencies*. https://www.itu.int/rec/T-REC-G.711 | 2 | Search summary / Blue Book extract | 00-06: 8,000 samples/s and 8 bits per sample |
| STD-PNG | W3C, *Portable Network Graphics (PNG) Specification*, 3rd ed., §5.2. https://www.w3.org/TR/png/ | 2 | Search summary | 00-06: PNG signature bytes |
| LNX-NAPI | Linux kernel documentation, *NAPI*. https://docs.kernel.org/networking/napi.html | 4 | Search summary | 00-07: interrupt/polling sequence, budget, interrupt masking and IRQ coalescing |
| TOOL-WINNET | Microsoft NetAdapter PowerShell documentation (`Get-NetAdapter`, `Get-NetAdapterStatistics`, `Get-NetAdapterAdvancedProperty`). https://learn.microsoft.com/powershell/module/netadapter/ | 4 | Planned; verify on a real host in H01 | 00-07: Windows NIC statistics and driver settings |
| RFC-1122 | RFC 1122, §§1.1.3 and 1.3.1 | 3 | Read | 00-09: four-layer model, ICMP and limits of strict layering |
| RFC-3439 | RFC 3439, §3 “Layering Considered Harmful” | 3 | Search summary | 00-09: limitations of layering |
| ITU-X200 | ITU-T X.200 (07/1994), *OSI Basic Reference Model: The basic model*, equivalent to ISO/IEC 7498-1:1994. https://www.itu.int/rec/T-REC-X.200-199407-I | 2 | Registration page read; full text not opened in that session | 00-09: authoritative OSI model reference and history |

### 4.10 References Added for Physical Layer Lessons

| ID | Source | Used in |
|---|---|---|
| CISCO-CCNA-EXAM-TOPICS-V11 | [Cisco 200-301 CCNA v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics) | 01-06: objective 1.3, fibre/copper and shared-media/point-to-point connections |
| CISCO-POE-INDUSTRIAL | [Cisco — PoE for Industrial Automation](https://www.cisco.com/c/en/us/products/collateral/networking/industrial-switches/poe-ind-data-control-single-cable-so.html) | 01-06: 802.3af/at/bt PSE and PD power levels |
| CISCO-POE-IOSXE | [Cisco IOS XE PoE Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/c9000/infra/poe/poe-configuration-guide/g-poe/c-poe.html) | 01-06: PoE classification and power capability |
| ANSI-TIA-568-E-REFERENCE | [ANSI/TIA-568-E cabling reference table](https://imlive.s3.amazonaws.com/Federal%20Government/ID62048956821926688123123361973875756393/Attachment%201i%20TIA-568%20Telecomm%20Cabling%20Standard.pdf) | 01-06: balanced twisted-pair categories and application distances |
| CISCO-GIG-SFP-DATA-SHEET | [Cisco — Gigabit Ethernet SFP Transceiver Data Sheet](https://www.cisco.com/c/en/us/products/collateral/interfaces-modules/gigabit-ethernet-gbic-sfp-modules/datasheet-c78-366584.html) | 01-07: example 1000BASE-SX and 1000BASE-LX/LH wavelengths, fibre types and reach |
| CISCO-CPWE-FIBER-GUIDE | [Cisco — Physical Infrastructure Design Guide (Fiber Optics)](https://www.cisco.com/c/en/us/td/docs/solutions/Verticals/CPwE/5-1/Phy_Arch/CPwE-Physical-Infrastructure_Feb2023.pdf) | 01-07: core size, SMF/MMF overview and OM/OS fibre categories |
| CISCO-WIRELESS-RF-GUIDE | [Cisco Wireless RF Reference Guide](https://www.cisco.com/c/en/us/td/docs/wireless/controller/9800/technical-reference/wireless-rf-reference-guide.html) | 01-08: bands, channel overlap, RSSI/dBm, attenuation, multipath and MIMO |
| CISCO-WIRELESS-DESIGN-LARGE | [Cisco Design Guide — Wireless for Large Public Networks](https://www.cisco.com/c/en/us/support/docs/wireless/catalyst-9800-series-wireless-controllers/222000-design-guide-cx-wireless-for-large-pub.html) | 01-08: channel width and 2.4/5/6 GHz planning |
| CISCO-ETHERNET-AUTONEG | [Cisco Configure and Verify Ethernet Auto-Negotiation](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/10561-3.html) | 01-09: auto-negotiation, speed/duplex and mismatch |
| CISCO-LAN-TROUBLESHOOT | [Cisco Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 01-10: collisions, late collisions, errors and Ethernet troubleshooting |

### 4.11 References Added for Data Link Lessons

| ID | Source | Used in |
|---|---|---|
| IEEE-802-LLC-REFERENCE | [IEEE 802 overview and standards references](https://www.ieee802.org/) | 02-01: LLC/MAC sublayers and IEEE 802 architecture |
| RFC-9724-MAC-RANDOMIZATION | [RFC 9724 — State of Affairs for Randomized and Changing MAC Addresses](https://www.rfc-editor.org/rfc/rfc9724.html) | 02-02: MAC format, OUI, I/G and U/L bits, local/randomised addresses |
| IEEE-EUI-OUI-GUIDELINES | [IEEE — Guidelines for EUI, OUI, and CID](https://standards-support.ieee.org/hc/en-us/articles/4888705676564-Guidelines-for-Use-of-Extended-Unique-Identifier-EUI-Organizationally-Unique-Identifier-OUI-and-Company-ID-CID) | 02-02: OUI and special MAC-address bits |
| RFC-7042-IEEE-802-IDENTIFIERS | [RFC 7042 — IANA Considerations and IEEE 802 Parameters](https://www.rfc-editor.org/rfc/rfc7042.html) | 02-02: EUI-48 format, group and local bits |
| CISCO-ETHERNET-FRAME-TR | [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf) | 02-03: frame fields, preamble, SFD, Type/Length, FCS, minimum size and padding |
| CISCO-NETFLOW-L2-FRAME | [Cisco — NetFlow Layer 2 and Ethernet Frame Formats](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_pi/configuration/15-s/nf-15-s-book.pdf) | 02-03: Ethernet II and IEEE 802.3 frame fields |
| CISCO-PRESS-ETHERNET-FRAME | [Cisco Press — Ethernet Frames](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4) | 02-03: standard and VLAN-tagged Ethernet frame sizes |
| CISCO-ETHERNET-ERROR-DETECTION | [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf) | 02-04: Ethernet FCS and frame integrity |
| CISCO-LAN-TROUBLESHOOT-ERRORS | [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 02-04: CRC/FCS errors and interface troubleshooting |
| CISCO-ETHERNET-CSMA-CD | [Cisco Press — Ethernet Frames and Shared Ethernet](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4) | 02-05: half-duplex shared Ethernet and CSMA/CD |
| CISCO-LAN-TROUBLESHOOT-CSMA | [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 02-05: collisions, late collisions, duplex mismatch and troubleshooting |
