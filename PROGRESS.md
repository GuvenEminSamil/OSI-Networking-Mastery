# Project Progress

> **Last updated:** 2026-11-26  
> **Course language:** English  
> **Exam target:** CCNA 200-301 v1.1, with the previously agreed target date of 2027-02-02.  
> **Curriculum:** The approved syllabus scope is unchanged.

## Current Snapshot

- **Last lesson completed by the learner:** 00-02 — Number Systems and Units (2026-11-26).
- **Next learner lesson:** 00-03 — Binary Arithmetic and Boolean Logic.
- **Next content-production lesson:** 02-07 — Collision and Broadcast Domains.
- **Learner progress and content-production progress are separate.** A lesson being written or published does not mean it has been studied.
- The teaching standard is clear, beginner-friendly English. Explain new technical terms when they first appear; do not assume prior knowledge.
- No fixed daily schedule, study-hour quota, mandatory Anki routine, daily log, or forced teach-back is required.

## A. Content Production

| Area | Planned lessons | Published | Current state |
|---|---:|---:|---|
| 00 — Foundations | 9 | 9 | 00-01 has now been rewritten in English; 00-02–00-09 are in English. Formal technical audit remains pending. |
| 01 — Physical Layer | 10 | 10 | All lessons published in English. Formal audit remains pending. |
| 02 — Data Link Layer | 16 | 6 | 02-01–02-06 published in English; next authoring item is 02-07. |
| 03 — Network Layer | 21 | 0 | Not yet produced. |
| 04 — Transport Layer | 7 | 0 | Not yet produced. |
| 05 — Session Layer | 2 | 0 | Not yet produced. |
| 06 — Presentation Layer | 6 | 0 | Not yet produced. |
| 07 — Application Layer | 11 | 0 | Not yet produced. |
| 08 — Cross-Layer Communication | 10 | 0 | Not yet produced. |
| 11 — Troubleshooting | 5 | 0 | Not yet produced. |
| 12 — Revision | 3 | 2 | 12-01 and 12-02 are published; 12-03 remains pending. |
| 13 — CCNA Exam Preparation | 4 | 0 | Not yet produced. |
| 14 — Security Fundamentals | 6 | 0 | Not yet produced. |
| 15 — Network Operations, Automation, and AI | 6 | 0 | Not yet produced. |
| **Total** | **116** | **27** | Production continues independently of learner progress. |

### Question Bank and Supporting Material

- Foundations question bank: 40 questions across FND-DAT, FND-HW, FND-NET, and FND-OSI.
- CE-00: 25-question diagnostic test with a separate answer key.
- English Anki decks are available for lessons 00-01–00-09, 01-01–01-10, and 02-01–02-06.
- `GLOSSARY.md`, `SOURCES.md`, revision flashcards, and question-bank material support the lesson files.
- Packet Tracer drills, full labs, real-host labs, and code exercises remain to be produced according to the curriculum.

## B. Learner Progress

### Confirmed Record

| Date | Item | Status |
|---|---|---|
| 2026-11-20 | CE-00 diagnostic test | Completed: 21/40. This is a historical baseline, not a mastery result. |
| 2026-11-26 | 00-02 — Number Systems and Units | Completed. The learner pushed commit `da47e41` with all five lesson self-check items checked. |
| Current | 00-03 — Binary Arithmetic and Boolean Logic | Next lesson; not yet marked complete. |

No other lesson is marked complete by this update.

### Unit-Level Target Deadlines

> Set on 2026-11-26 against the agreed 2027-02-02 exam target. These are unit completion milestones, not daily schedules or required study hours.

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

These dates are targets, not reasons to rush. If a target is missed, review the remaining plan and exam readiness rather than skipping concepts.

## C. Current Study and Production Decisions

| Topic | Current decision |
|---|---|
| Syllabus | CCNA 200-301 v1.1; curriculum scope unchanged. |
| Language | English for lessons, practice, questions, and explanations. |
| Teaching style | Clear and practical; avoid unnecessary scientific depth. Define every new technical term in plain English at first use. |
| Lesson flow | Explanation, examples, practical scenario, relevant commands or lab where useful, then questions. |
| Questions | Usually 10–15, adjusted to lesson complexity; progress from easier to more exam-like questions when appropriate. |
| Practical work | Use Packet Tracer or real-host labs when they add useful experience. |
| Schedule | Flexible. No fixed daily hours, daily study targets, weekly routine, or mandatory flashcard use. |
| Progress tracking | Record only lessons and assessments the learner has actually completed. |
| Repository | GitHub is the project source of truth. Keep the handoff documents in `ai-workspace` current at meaningful checkpoints. |

## D. Open Technical Validation Items

These items should be verified before the associated labs are treated as technically audited:

- **Physical / Ethernet:** Auto-MDIX behaviour; duplex-mismatch simulation and interface error counters; exact supported Packet Tracer device models and commands.
- **Hardware and operating systems:** DDR4 refresh details against the primary JEDEC text; Windows NetAdapter command output on a real host.
- **Layer 3 and IPv6:** /31 lab support; MTU and fragmentation behaviour; VRRP; stateful DHCPv6.
- **Services and management:** DNS MX/PTR exercises; SCP/SFTP behaviour; SNMP features; Network Controller and REST API behaviour.
- **Security:** Dynamic ARP Inspection (DAI); storm control and RA Guard; IPsec site-to-site VPN behaviour.
- **Packet Tracer environment:** PoE demonstration and Sniffer device support.

The v1.1 exam-objective mapping has already been checked against Cisco's published exam topics (recorded in `SOURCES.md`).

## E. Change Log

| Date | Change |
|---|---|
| 2026-11-19 | Initial course structure, curriculum, source list, progress tracker, diagnostic test, and Foundations material created. |
| 2026-11-20 | CE-00 diagnostic completed and scored 21/40. The learner's original answers and feedback are preserved in `MY-NOTES/CE-00-MY-ANSWERS.md`. |
| 2026-11-24 | Learner confirmed that 00-02 was the last completed lesson and that the previous course depth felt overwhelming. The course was redesigned for a clearer, more practical English-first approach. |
| 2026-11-24 | Published the ten English Physical Layer lessons and Data Link lessons 02-01–02-06, with supporting review material. |
| 2026-11-26 | Learner completed redesigned lesson 00-02 and pushed commit `da47e41`. Next learner lesson: 00-03. Unit-level milestones were added, retaining the agreed exam target. |
| 2026-11-26 | Repository language audit started. Turkish lesson, question-bank, answer-key, revision, and personal-note files are being translated. Conflicting fixed-schedule sections are being retired. Learner completion status is unchanged. |
