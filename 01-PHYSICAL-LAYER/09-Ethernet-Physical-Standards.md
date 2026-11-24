# 01-09 — Ethernet Physical Standards

> **Prerequisites:** 01-03 — Line Coding and Modulation; 01-06 — Copper Cabling; 01-07 — Fiber Optics  
> **CCNA 200-301 v1.1 connection:** Ethernet physical interfaces, media, speed, duplex, and link negotiation.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Read common Ethernet standard names.
- Recognize common Ethernet speeds and media.
- Explain auto-negotiation.
- Distinguish half-duplex and full-duplex operation.
- Identify speed or duplex mismatches.
- Use Cisco commands to check Ethernet interface status.

## 1. What Is an Ethernet Physical Standard?

**Ethernet** is a family of wired LAN technologies standardized mainly through IEEE 802.3.

An Ethernet physical standard defines how data is transmitted over a particular medium. It can specify:

- Data rate.
- Copper or fiber medium.
- Signal encoding and signaling.
- Maximum supported reach.
- Connector and physical interface requirements.

A device's Ethernet interface and the connected cable or transceiver must support compatible standards.

## 2. Reading Ethernet Names

Ethernet standards often use names such as:

`10BASE-T`

The parts give useful information:

- `10` = 10 Mbps data rate.
- `BASE` = baseband signaling.
- `T` = twisted-pair copper.

Here are common examples:

| Ethernet standard | Speed | Medium | General use |
|---|---:|---|---|
| 10BASE-T | 10 Mbps | Twisted-pair copper | Legacy Ethernet |
| 100BASE-TX | 100 Mbps | Twisted-pair copper | Fast Ethernet |
| 1000BASE-T | 1 Gbps | Four-pair twisted-pair copper | Gigabit Ethernet |
| 1000BASE-SX | 1 Gbps | Multimode fiber | Short-range optical links |
| 1000BASE-LX | 1 Gbps | Mainly single-mode fiber | Longer optical links |
| 10GBASE-T | 10 Gbps | Twisted-pair copper | 10 Gigabit Ethernet over copper |
| 10GBASE-SR | 10 Gbps | Multimode fiber | Short-range optical links |
| 10GBASE-LR | 10 Gbps | Single-mode fiber | Longer optical links |

The maximum distance is not determined by the speed alone. It depends on the specific Ethernet standard, cable or fiber type, transceiver, and installation.

## 3. What Is Auto-Negotiation?

**Auto-negotiation** is a process in which two connected Ethernet interfaces exchange information about their capabilities and select a compatible operating mode.

Depending on the technology, they may negotiate:

- Speed.
- Duplex mode.
- Flow-control capabilities.

For example, a 10/100/1000 Mbps switch port may connect to a device that supports only 100 Mbps. Auto-negotiation can select 100 Mbps if both ends support it.

The two ends must operate compatibly. A link light alone does not prove that the speed and duplex settings are correct.

On many modern Ethernet copper interfaces, auto-negotiation is enabled by default. The exact behavior depends on the interface and transceiver type.

## 4. Half-Duplex and Full-Duplex

**Duplex** describes whether a link can send and receive at the same time.

### Half-Duplex

In half-duplex operation, a device can send or receive at a given time, but not both simultaneously.

If two devices share the same medium and transmit at the same time, their signals can collide.

**CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) is the traditional Ethernet method for detecting and handling collisions on shared half-duplex Ethernet.

You will study CSMA/CD in the Data Link module.

### Full-Duplex

In full-duplex operation, both ends can send and receive at the same time.

Modern switched Ethernet links normally use full-duplex operation. Because each direction can transmit at the same time, collisions do not occur on a normal full-duplex point-to-point link.

## 5. Speed and Duplex Mismatch

A **duplex mismatch** occurs when the two ends of an Ethernet link use different duplex settings.

Example:

- Switch port: full-duplex.
- Connected device: half-duplex.

The link may appear to be up, but performance can be poor. You may see errors, collisions on the half-duplex side, or retransmissions and throughput problems.

A common cause is manually configuring one end while leaving the other end to auto-negotiate.

Best practice for supported modern Ethernet interfaces is generally to keep auto-negotiation enabled at both ends unless the equipment documentation or network design requires a specific configuration.

If a setting must be forced, make sure both ends are configured consistently.

## 6. Checking Speed and Duplex on Cisco Devices

Use:

```
Switch# show interfaces status
```

This command gives a quick view of connected ports, their speed, and duplex state on supported switches.

For more detail:

```
Switch# show interfaces gigabitEthernet 1/0/1
```

The output includes information such as:

- Interface status.
- Speed and duplex.
- Input and output errors.
- CRC errors.
- Traffic counters.

The interface name and available commands depend on the switch model.

You may see a prefix such as `a-` before speed or duplex in some command outputs. This commonly indicates that the value was auto-negotiated.

## 7. Practical Troubleshooting Example

A switch is connected to a server. The link is up, but file transfers are much slower than expected.

Check the following:

1. Is the interface operating at the expected speed?
2. Is it full-duplex?
3. Are both ends configured compatibly?
4. Are CRC, alignment, or other input errors increasing?
5. Is the cable category and length suitable for the speed?

Use `show interfaces status` for a quick check, then `show interfaces` for detailed counters.

Do not change speed or duplex settings blindly. First identify the supported capabilities of both link partners.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| 1000BASE-T means 100 Mbps. | 1000 means 1,000 Mbps, or 1 Gbps. |
| Auto-negotiation is the same as DHCP. | Auto-negotiation selects Ethernet link capabilities; DHCP provides IP configuration. |
| Full-duplex Ethernet has collisions. | Normal full-duplex point-to-point Ethernet does not have collisions. |
| A link light proves correct duplex. | A link can be up even when speed or duplex is misconfigured. |
| One side can be forced and the other left at auto without risk. | This can create a duplex mismatch, especially on 10/100 Mbps links. |
| Every Ethernet standard supports the same cable and distance. | Media, cable category, transceiver, and reach depend on the specific standard. |

## 9. Knowledge Check

1. What does the number in 1000BASE-T represent?
   <details><summary>Answer</summary>1000 Mbps, or 1 Gbps.</details>

2. What medium does the final T in 1000BASE-T indicate?
   <details><summary>Answer</summary>Twisted-pair copper.</details>

3. What is auto-negotiation?
   <details><summary>Answer</summary>A process in which two Ethernet interfaces exchange capabilities and select a compatible operating mode.</details>

4. Can a half-duplex device send and receive at the same time?
   <details><summary>Answer</summary>No. It can send or receive at a given time, but not both simultaneously.</details>

5. Why do normal full-duplex switched Ethernet links not have collisions?
   <details><summary>Answer</summary>Both directions can transmit at the same time on separate transmit and receive paths; they do not share a collision domain in the half-duplex sense.</details>

6. What is a duplex mismatch?
   <details><summary>Answer</summary>The two ends of a link operate with different duplex settings.</details>

7. Which Cisco command gives a quick view of port speed and duplex?
   <details><summary>Answer</summary>`show interfaces status`.</details>

## 10. Practice

On a Cisco switch in Packet Tracer:

1. Run `show interfaces status`.
2. Identify a connected port.
3. Note its speed and duplex.
4. Run `show interfaces` for that port.
5. Identify its input errors and CRC counters.

Explain why you should check both ends before forcing a speed or duplex setting.

## 11. CCNA Takeaways

- Ethernet physical standards specify media, speed, signaling, and reach.
- Read common names such as 10BASE-T, 100BASE-TX, 1000BASE-T, and 10GBASE-T.
- Auto-negotiation exchanges interface capabilities.
- Half-duplex cannot send and receive simultaneously.
- Full-duplex supports simultaneous transmission and reception.
- A duplex mismatch can cause poor performance and interface errors.
- Use Cisco interface commands to inspect operational speed, duplex, and counters.

## Self-Check

- [ ] I can interpret common Ethernet standard names.
- [ ] I can explain auto-negotiation.
- [ ] I can distinguish half-duplex and full-duplex.
- [ ] I can explain how a duplex mismatch affects a link.
- [ ] I can inspect speed, duplex, and errors with Cisco commands.

**Next lesson:** 01-10 — Topologies, Devices, and Interface Issues.

## References

- [Cisco — CCNA 200-301 v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics)
- [Cisco — Configure and Verify Ethernet Auto-Negotiation](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/10561-3.html)
- [Cisco — Configure Interface Characteristics](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3850/software/release/3se/consolidated_guide/configuration_guide/b_consolidated_3850_3se_cg/b_consolidated_3850_3se_cg_chapter_0101.pdf)
