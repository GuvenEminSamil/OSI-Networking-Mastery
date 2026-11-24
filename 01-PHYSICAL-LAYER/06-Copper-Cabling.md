# 01-06 — Copper Cabling

> **Prerequisites:** 01-05 — Signal Impairments; 00-04 — Electricity Fundamentals  
> **CCNA 200-301 v1.1 connection:** Exam objective 1.3 — Compare physical interface and cabling types; copper media and connections.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain how twisted-pair copper cabling works.
- Distinguish UTP and shielded cable types.
- Recognize common cable categories.
- Identify Ethernet connector and wiring standards.
- Understand straight-through, crossover, and rollover cables.
- Explain Auto-MDIX and the common 100-meter cable limit.
- Recognize the main PoE standards and roles.

## 1. What Is Twisted-Pair Copper Cable?

A **copper cable** carries electrical signals through copper conductors.

Ethernet commonly uses **twisted-pair cable**. It contains pairs of insulated copper wires twisted around one another.

Why are the wires twisted?

Twisting helps reduce the effect of external noise and crosstalk. The two wires in a pair are used together, allowing the receiver to detect a difference between their electrical signals.

A common Ethernet twisted-pair cable contains four pairs, or eight individual wires.

## 2. UTP and Shielded Cable

**UTP** means *Unshielded Twisted Pair*. It uses twisted pairs without an additional metallic shield.

Shielded cable adds a conductive layer to help reduce interference.

| Type | Meaning | Basic idea |
|---|---|---|
| UTP | Unshielded Twisted Pair | Twisted pairs without a cable shield |
| STP | Shielded Twisted Pair | General term for twisted-pair cable with shielding |
| F/UTP | Foiled/Unshielded Twisted Pair | An overall foil shield surrounds the unshielded pairs |

Shielding is useful only when the cable, connectors, and installation are designed and installed correctly. A shield does not automatically make a poor installation reliable.

For typical office Ethernet, UTP is common and often sufficient.

## 3. Cable Categories

A cable **category** describes the transmission performance requirements of a cable, including the frequency range it is designed to support.

Common categories include:

| Category | General use |
|---|---|
| Cat5e | Widely used for Gigabit Ethernet over copper |
| Cat6 | Higher performance than Cat5e; commonly used in office networks |
| Cat6A | Designed to support 10GBASE-T up to 100 meters |
| Cat7 | A higher-performance shielded cabling class used in some installations |
| Cat8 | Designed for very high-speed, short-distance data-center connections |

For common balanced twisted-pair Ethernet cabling:

- 1000BASE-T can operate over Cat5e, Cat6, Cat6A, and Cat8 up to 100 meters when the installed channel meets the relevant requirements.
- 10GBASE-T can operate over Cat6A up to 100 meters.
- Cat8 supports 25GBASE-T and 40GBASE-T up to 30 meters.

The actual result depends on the cable, connectors, installation quality, and the Ethernet standard. Do not assume that any cable with an RJ-45-style connector supports every speed.

## 4. Ethernet Connector: RJ-45 and 8P8C

The connector commonly called **RJ-45** is an eight-position, eight-contact modular connector, often described as **8P8C**.

- 8P = eight positions.
- 8C = eight electrical contacts.

It is widely used for copper Ethernet connections.

The connector must be terminated correctly. A poorly installed connector can cause errors, reduced link speed, or no link at all.

## 5. T568A and T568B Wiring

**T568A** and **T568B** are two wiring schemes that define which colored wire goes to each connector pin.

The two schemes use the same eight wires but place the green and orange pairs in different positions.

| Pin | T568A | T568B |
|---:|---|---|
| 1 | White/Green | White/Orange |
| 2 | Green | Orange |
| 3 | White/Orange | White/Green |
| 4 | Blue | Blue |
| 5 | White/Blue | White/Blue |
| 6 | Orange | Green |
| 7 | White/Brown | White/Brown |
| 8 | Brown | Brown |

Use the same wiring scheme at both ends for a straight-through cable:

- T568A at both ends, or
- T568B at both ends.

A cable wired with T568A at one end and T568B at the other is a traditional crossover cable.

## 6. Straight-Through, Crossover, and Rollover

### Straight-through cable

Both ends use the same wiring scheme (A-A or B-B).

It is the normal cable type used for most Ethernet connections.

### Crossover cable

One end uses T568A and the other uses T568B. The transmit and receive pairs are crossed.

Older Ethernet devices sometimes needed crossover cables when connecting similar device types, such as switch to switch.

### Rollover cable

A **rollover cable** reverses the pin order from one end to the other. It is traditionally used for connecting a computer to a Cisco console port, not for ordinary Ethernet data communication.

## 7. Auto-MDIX

**MDI** (Medium Dependent Interface) describes the transmit and receive pin arrangement of an Ethernet interface.

**MDI-X** is the crossed version of that arrangement.

**Auto-MDIX** allows supported interfaces to detect the required transmit and receive pair arrangement automatically.

This means modern switches and network adapters often work with either a straight-through or crossover cable.

You should still recognize the cable types, but do not assume that every device supports Auto-MDIX.

## 8. Why Is 100 Meters Important?

For common Ethernet balanced twisted-pair cabling, the maximum channel length is typically 100 meters.

A structured-cabling channel commonly consists of:

- Up to 90 meters of permanent horizontal cable.
- Up to 10 meters of patch cords combined.

A **patch cord** is a short flexible cable used to connect a device to a wall outlet or patch panel.

Longer runs may exceed the supported electrical limits and cause unreliable communication. Fiber is often chosen when a longer distance is required.

## 9. Power over Ethernet (PoE)

**PoE** means *Power over Ethernet*. It allows a compatible Ethernet cable to carry both data and electrical power.

PoE can power devices such as:

- Wireless access points.
- IP phones.
- Security cameras.

Two important roles:

- **PSE** (Power Sourcing Equipment): the device that supplies power, such as a PoE switch.
- **PD** (Powered Device): the device that receives power, such as an access point.

Common IEEE PoE standards:

| Standard | Common name | Maximum power from PSE | Maximum power available at PD |
|---|---|---:|---:|
| 802.3af | PoE | 15.4 W | 12.95 W |
| 802.3at | PoE+ | 30 W | 25.5 W |
| 802.3bt Type 3 | PoE++ | 60 W | 51 W |
| 802.3bt Type 4 | 4-pair PoE / PoE++ | 90 W | 71.3 W |

The PSE power is higher than the power available at the PD because some energy is lost in the cable.

The switch and powered device must support compatible PoE capabilities. The switch detects and classifies supported devices before providing the required power.

## 10. Real-World Troubleshooting

A user reports that an Ethernet connection only negotiates at 100 Mbps, even though both devices support 1 Gbps.

Possible causes include:

- One or more cable pairs are damaged.
- A connector is terminated incorrectly.
- The cable is damaged or does not meet the required category.
- The installed cable channel is too long or poorly installed.
- A port has been manually configured to a lower speed.

A practical first check is to replace the cable with a known-good cable of the correct category and inspect the interface status and counters.

Useful Cisco commands:

```
Switch# show interfaces status
Switch# show interfaces
```

## 11. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Every twisted-pair cable supports every Ethernet speed. | Cable category, installation, distance, and the Ethernet standard determine what is supported. |
| Shielding always improves a cable. | Shielding helps only when the cable and installation are designed and grounded correctly. |
| T568A and T568B are different Ethernet protocols. | They are two pin-wiring schemes for the connector. |
| A rollover cable is an Ethernet crossover cable. | A rollover cable is traditionally used for console connections. |
| A PoE switch delivers all source power to the end device. | Some power is lost along the cable, so the PD receives less than the PSE supplies. |
| 100 meters is the maximum for every copper technology. | The limit depends on the Ethernet standard and cable type; 100 m is common for balanced twisted-pair BASE-T links. |

## 12. Knowledge Check

1. Why are the wires twisted in twisted-pair cable?
   <details><summary>Answer</summary>Twisting helps reduce the effects of external noise and crosstalk.</details>

2. What does UTP stand for?
   <details><summary>Answer</summary>Unshielded Twisted Pair.</details>

3. Which cable category is designed to support 10GBASE-T up to 100 meters?
   <details><summary>Answer</summary>Cat6A.</details>

4. What does 8P8C mean?
   <details><summary>Answer</summary>Eight positions and eight electrical contacts.</details>

5. What wiring schemes are used at the two ends of a traditional crossover cable?
   <details><summary>Answer</summary>T568A at one end and T568B at the other.</details>

6. What does Auto-MDIX do?
   <details><summary>Answer</summary>It detects and adapts to the transmit and receive pair arrangement required by the connection.</details>

7. What is the common maximum channel length for balanced twisted-pair Ethernet cabling?
   <details><summary>Answer</summary>100 meters, when the installation meets the relevant cabling requirements.</details>

8. What is the difference between PSE and PD?
   <details><summary>Answer</summary>PSE supplies PoE power; PD receives it.</details>

9. How much power can an 802.3at PSE supply, and how much is available at the PD?
   <details><summary>Answer</summary>Up to 30 W from the PSE and up to 25.5 W at the PD.</details>

## 13. Practice

Look at an Ethernet cable or a cabling diagram.

1. Identify whether it is twisted-pair copper or another medium.
2. Find its category marking, if visible.
3. Check both connector ends and identify whether they follow T568A or T568B.
4. Decide whether the cable is straight-through or crossover.
5. Explain whether it would be suitable for a typical Gigabit Ethernet connection.

If you have a PoE switch and an access point in Packet Tracer, identify which device acts as the PSE and which is the PD.

## 14. CCNA Takeaways

- Twisted-pair copper uses pairs of wires to carry electrical signals.
- Twisting helps reduce noise and crosstalk.
- Know UTP and the general role of shielding.
- Recognize Cat5e, Cat6, Cat6A, Cat7, and Cat8.
- Understand the purpose of RJ-45/8P8C, T568A, and T568B.
- Know straight-through, crossover, rollover, and Auto-MDIX.
- Remember the common 100-meter channel limit for balanced twisted-pair Ethernet.
- Know the PSE and PD roles and the major PoE standards.

## Self-Check

- [ ] I can explain why copper pairs are twisted.
- [ ] I can distinguish UTP from shielded cable.
- [ ] I can recognize the purpose of common cable categories.
- [ ] I can identify T568A and T568B wiring.
- [ ] I can explain straight-through, crossover, and rollover cables.
- [ ] I understand Auto-MDIX and the common 100-meter limit.
- [ ] I can explain PoE, PSE, and PD.

**Next lesson:** 01-07 — Fiber Optics.

## References

- [Cisco — CCNA 200-301 v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics)
- [Cisco — Power over Ethernet standards and power levels](https://www.cisco.com/c/en/us/products/collateral/networking/industrial-switches/poe-ind-data-control-single-cable-so.html)
- [Cisco — PoE Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/c9000/infra/poe/poe-configuration-guide/g-poe/c-poe.html)
- [ANSI/TIA-568 cabling standard reference table](https://imlive.s3.amazonaws.com/Federal%20Government/ID62048956821926688123123361973875756393/Attachment%201i%20TIA-568%20Telecomm%20Cabling%20Standard.pdf)
