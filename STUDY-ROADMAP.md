# Study Roadmap and Topic Dependencies

> This file describes the recommended learning order and dependencies. It is not a daily schedule. The syllabus target is CCNA 200-301 v1.1, and the course language is English.

## 1. How to Use This Roadmap

- Follow the lesson order and prerequisite links in `CURRICULUM.md`.
- Complete the knowledge checks and practical activities that are useful for the topic.
- Move forward when the current concepts are understood. Do not rush to meet a date.
- Unit deadlines are milestones, not daily targets. There are no required study hours, study days, or mandatory weekly routines.
- Optional flashcards and spaced review can support learning, but they are not compulsory.
- Keep actual learner progress in `PROGRESS.md`. Publishing a lesson is content-production progress, not learner completion.

## 2. Curriculum Sequence

| Unit | Area | Main focus |
|---|---|---|
| 00 | Foundations | Data, number systems, Boolean logic, hardware basics, networking fundamentals, OSI and TCP/IP |
| 01 | Physical Layer | Signals, encoding, copper, fiber, wireless, Ethernet physical standards |
| 02 | Data Link Layer | Ethernet frames, MAC addresses, switching, collision/broadcast domains, VLANs, STP, wireless LAN |
| 03 | Network Layer | IPv4/IPv6, subnetting, forwarding, routing, ICMP, OSPF, NAT, QoS |
| 04 | Transport Layer | Ports, sockets, UDP, TCP, reliability, flow and congestion control |
| 05 | Session Layer | OSI session concepts and where session functions appear in modern protocols |
| 06 | Presentation Layer | Encoding, formats, compression, cryptography, TLS |
| 07 | Application Layer | DNS, DHCP, HTTP(S), email, remote access, file transfer, NTP, SNMP, syslog, REST |
| 08 | Cross-Layer Communication | End-to-end scenarios that combine the layers |
| 11 | Troubleshooting | Methodology, diagnostic commands, host troubleshooting, fault catalogue, case studies |
| 14 | Security Fundamentals | Security concepts, AAA, ACLs, Layer 2 defenses, VPNs, wireless security |
| 15 | Network Operations, Automation, and AI | Architectures, virtualisation, management, SDN, automation, AI |
| 12 | Revision | Optional spaced review, flashcards, and reference sheets |
| 13 | Exam Preparation | Blueprint mapping, exam strategy, gap analysis, readiness |

Packet Tracer labs (Unit 09), the question bank (Unit 10), and real-host labs (Unit 16) are companion resources used alongside the relevant theory. They are not additional sequential theory units.

## 3. Important Prerequisite Relationships

The full prerequisite list is maintained in `CURRICULUM.md`. The following chain highlights relationships that affect several later topics:

- **Number systems → Boolean logic → subnetting and CRC.** Binary arithmetic and logic operations support subnet masks, bit-level reasoning, and error detection.
- **Electricity → transistors → digital logic and signalling.** These topics provide the minimum background needed to understand how devices represent and transmit bits.
- **Ethernet frame → MAC learning → switching → VLANs and STP.** A switch's behaviour is easier to understand once frame fields and MAC addresses are familiar.
- **IPv4 addressing → subnetting → host forwarding → router forwarding → routing tables.** A host first decides whether a destination is local; routers then forward packets between networks.
- **TCP fundamentals → application protocols and TLS.** Ports, connections, and transport behaviour are prerequisites for several application-layer topics.
- **DHCP and ARP → Layer 2 security.** DHCP snooping and Dynamic ARP Inspection rely on understanding the underlying protocols.
- **Related layers → cross-layer scenarios and troubleshooting.** Real faults often span multiple layers, so integrated diagnosis comes after the relevant basics.

## 4. Practical Learning Approach

Use practical work when it clarifies a mechanism or builds a useful troubleshooting skill.

- **Packet Tracer:** Use it for device configuration, switching, VLANs, routing, and supported protocol behaviour.
- **Real-host tools:** Use operating-system commands and Wireshark when actual host behaviour or packet bytes matter.
- **Troubleshooting scenarios:** Start from the symptom, form a hypothesis, run a test, interpret the result, and then choose a correction.
- **Question bank:** Use questions to find gaps. Review explanations for incorrect or uncertain answers rather than memorising answer letters.

Packet Tracer's known limitations and alternatives are listed in `CURRICULUM.md`.

## 5. Mastery Levels

Reading a lesson alone does not demonstrate mastery. Use these levels only when the evidence is available:

| Level | Name | Evidence |
|---:|---|---|
| 0 | Not started | The lesson has not been studied. |
| 1 | Read | The lesson has been studied and its self-check attempted. |
| 2 | Explains | The learner can explain the concept and how/why it works without relying on the lesson text. |
| 3 | Applies | Relevant practical work is completed and topic questions are answered correctly. |
| 4 | Troubleshoots | The learner can identify likely causes, verify them, and explain a suitable correction. |
| 5 | Mastered | The relevant knowledge gate is passed and later recall is demonstrated. |

Do not assign a level based only on the fact that a file exists or has been published.

## 6. Unit-Level Target Deadlines

> Targets set on 2026-11-26 against the previously agreed CCNA 200-301 v1.1 exam target of **2027-02-02**. These are unit completion milestones, not a day-by-day timetable. Some later topics may be studied alongside earlier units once their prerequisites are complete.

| Unit | Unit name | Target completion |
|---|---|---:|
| 00 | Foundations | **2026-12-03** |
| 01 | Physical Layer | **2026-12-10** |
| 02 | Data Link Layer | **2026-12-20** |
| 03 | Network Layer | **2027-01-07** |
| 04 | Transport Layer | **2027-01-13** |
| 05 | Session Layer | **2027-01-15** |
| 06 | Presentation Layer | **2027-01-20** |
| 07 | Application Layer | **2027-01-28** |
| 08 | Cross-Layer Communication | **2027-01-31** |
| 11 | Troubleshooting | **2027-01-31** |
| 14 | Security Fundamentals | **2027-01-31** |
| 15 | Network Operations, Automation, and AI | **2027-02-01** |
| 12 | Revision resources and final review | **2027-02-01** |
| 13 | CCNA Exam Preparation | **2027-02-01** |

A unit is complete when its lessons have been studied, the relevant checks have been attempted, and required practical tasks have been completed. If a target is missed, shift the remaining milestones and reassess exam readiness rather than skipping important concepts.

## 7. Current Checkpoint

- Last completed lesson: **00-02 — Number Systems and Units** (2026-11-26).
- Next learner lesson: **00-03 — Binary Arithmetic and Boolean Logic**.
- Next content-production lesson: **02-07 — Collision and Broadcast Domains**.
- The learner's diagnostic baseline is recorded in `MY-NOTES/RESULTS.md`.
- The current state and confirmed completion record are maintained in `PROGRESS.md`.
