# 01-10 — Topologies, Devices, and Interface Issues

> **Prerequisites:** 01-06 — Copper Cabling; 01-07 — Fiber Optics; 01-09 — Ethernet Physical Standards  
> **CCNA 200-301 v1.1 connection:** Exam objective 1.4 — Identify interface and cable issues, such as collisions, errors, and duplex or speed mismatches.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Distinguish physical and logical network topologies.
- Recognize star, bus, ring, and mesh layouts.
- Explain the roles of repeaters, hubs, media converters, and transceivers.
- Recognize common Ethernet interface error counters.
- Use a structured method to troubleshoot physical and interface problems.

## 1. What Is a Network Topology?

A **network topology** describes how network devices and connections are arranged.

There are two useful views:

- **Physical topology:** The actual placement of devices, cables, and connections.
- **Logical topology:** How data flows between devices, regardless of the exact physical layout.

A network can have one physical arrangement and a different logical communication pattern.

## 2. Common Topology Types

### Star

In a **star topology**, devices connect to a central device, commonly a switch.

If one workstation cable fails, the other workstations can continue working. If the central switch fails, many devices may lose connectivity.

Modern office Ethernet commonly uses a physical star topology.

### Bus

In a **bus topology**, devices share one main communication cable.

Traditional coaxial Ethernet used a bus layout. A break or termination problem could affect the shared segment.

### Ring

In a **ring topology**, each device connects to two neighbors, forming a loop.

Some technologies use a ring for resilience or predictable forwarding. Ethernet networks can also use logical ring-like forwarding designs, but a modern switched Ethernet LAN is not normally a physical ring at the access layer.

### Mesh

In a **mesh topology**, devices have multiple paths between them.

A **full mesh** has a direct link between every pair of devices. A **partial mesh** provides multiple paths for selected devices.

Mesh designs can provide redundancy but require more links and configuration.

## 3. Common Physical-Layer Devices

### Repeater

A **repeater** receives a signal and regenerates it so it can travel farther.

It operates at the Physical layer. It does not read MAC or IP addresses.

### Hub

A **hub** is a multiport repeater. It repeats incoming bits out of its other ports rather than forwarding frames based on MAC addresses.

All devices connected to a traditional hub share the same collision domain.

A **collision domain** is a network segment in which simultaneous transmissions can collide when using half-duplex shared Ethernet.

Hubs are legacy devices and are not normally used in modern switched Ethernet networks.

### Media Converter

A **media converter** changes one physical media type into another, such as copper Ethernet to fiber Ethernet.

It does not normally perform routing or Layer 2 switching. It simply connects compatible physical media interfaces.

### Transceiver

A **transceiver** is a component that can both transmit and receive signals.

Examples include optical SFP modules and copper transceiver modules. A transceiver must match the device interface, medium, wavelength, speed, and supported reach.

## 4. Collision and Error Counters

Cisco interfaces can display several counters. Learn what they suggest, but remember that a counter alone may not identify the root cause.

| Counter | Meaning |
|---|---|
| CRC / FCS errors | Received frames fail the error check; investigate cable quality, interference, connectors, or the physical link. |
| Runts | Frames shorter than the minimum valid Ethernet frame size; can occur with collisions or physical/interface problems. |
| Giants | Frames larger than the supported maximum frame size; investigate MTU, jumbo-frame settings, or malformed traffic. |
| Input errors | A summary counter that can include several receive-side errors, depending on platform. |
| Output errors | Problems while transmitting frames from the interface. |
| Collisions | Transmissions collided on a half-duplex shared Ethernet segment. |
| Late collisions | Collisions detected after the normal collision window; may indicate a duplex mismatch or physical cabling problem. |
| Interface resets | The interface has been reset; repeated resets can indicate link instability or other problems. |

**FCS** means *Frame Check Sequence*. It is the error-detection value carried at the end of an Ethernet frame.

A **runt** is a frame that is shorter than the Ethernet minimum, excluding certain special cases. A **giant** is a frame larger than the interface's supported frame size.

## 5. Why Do Collisions Matter?

In half-duplex Ethernet, two devices may try to transmit at the same time on the shared medium.

A collision occurs when the transmissions interfere with one another.

Traditional shared Ethernet used CSMA/CD to detect collisions and recover.

In modern switched full-duplex Ethernet, each link is normally point-to-point and collisions should not occur. If collision counters appear unexpectedly, check the interface mode, connected devices, and whether the link is operating in half-duplex.

## 6. A Structured Troubleshooting Example

A user reports slow file transfers. The switch port is up.

Use this sequence:

1. **Check the physical connection.** Inspect the cable, connectors, and link indicators.
2. **Check interface state.** Run `show interfaces status`.
3. **Check speed and duplex.** Confirm that the interface is operating as expected.
4. **Check error counters.** Run `show interfaces` and note CRC, input errors, output errors, runts, giants, and collisions.
5. **Check both ends.** A mismatch can exist between the switch and the connected host or another switch.
6. **Test with a known-good cable or port.** Change one thing at a time so you can identify the cause.
7. **Compare counters after the test.** Determine whether errors continue increasing.

Do not clear counters before recording their original values. Counters help you compare before and after a troubleshooting change.

## 7. Useful Cisco Commands

```
Switch# show interfaces status
Switch# show interfaces
Switch# show interfaces gigabitEthernet 1/0/1
Switch# show logging
```

- `show interfaces status` gives a quick port summary.
- `show interfaces` displays detailed interface information and counters.
- `show logging` displays system messages that may mention link changes or duplex issues.

The interface name and command output vary between Cisco models and operating-system versions.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| A repeater understands MAC addresses. | A repeater regenerates physical signals; it does not make forwarding decisions based on MAC addresses. |
| A hub is the same as a switch. | A hub repeats bits to other ports; a switch forwards frames using MAC-address information. |
| Every CRC error proves that the cable is bad. | A cable is one possible cause; interference, connectors, transceivers, and other physical problems may also be involved. |
| Collisions are normal on a full-duplex link. | Normal full-duplex switched Ethernet should not have collisions. |
| Input errors identify one exact problem. | Input errors can summarize multiple receive-side problems. Inspect the detailed counters. |
| A link being up proves the cable is perfect. | A link can remain up while errors increase or performance is poor. |

## 9. Knowledge Check

1. What is a physical topology?
   <details><summary>Answer</summary>The actual arrangement of devices, cables, and physical connections.</details>

2. What is the difference between physical and logical topology?
   <details><summary>Answer</summary>Physical topology describes actual connections; logical topology describes how data flows.</details>

3. What does a repeater do?
   <details><summary>Answer</summary>It regenerates a signal so it can travel farther.</details>

4. How is a hub different from a switch?
   <details><summary>Answer</summary>A hub repeats incoming bits to other ports; a switch forwards Ethernet frames using MAC-address information.</details>

5. What does a media converter do?
   <details><summary>Answer</summary>It converts between compatible physical media types, such as copper Ethernet and fiber Ethernet.</details>

6. What might an increasing CRC counter indicate?
   <details><summary>Answer</summary>Received frames are being corrupted. Possible causes include damaged cable, interference, bad connectors, or transceiver problems.</details>

7. What is a late collision?
   <details><summary>Answer</summary>A collision detected after the normal collision window; it can indicate duplex mismatch or a physical cabling problem.</details>

8. Should normal full-duplex switched Ethernet have collisions?
   <details><summary>Answer</summary>No. Collisions should not occur on a normal full-duplex point-to-point link.</details>

## 10. Practice

Scenario:

A switch port is connected to a workstation. The port is up, but the user reports intermittent network problems. The interface counters show increasing CRC errors.

Write a short troubleshooting plan:

1. What would you inspect first?
2. Which command would you use?
3. What two causes would you investigate?
4. How would you test whether the cable is responsible?
5. What would you compare after replacing the cable?

A good answer uses evidence from the interface counters and changes one variable at a time.

## 11. CCNA Takeaways

- Physical topology describes real cables and device placement.
- Logical topology describes how data flows.
- Repeater and hub are Physical-layer devices.
- A media converter changes physical media; a transceiver sends and receives signals.
- Know CRC/FCS, runts, giants, input errors, output errors, collisions, and late collisions.
- Full-duplex switched Ethernet should not have collisions.
- Use interface status, counters, logs, and known-good replacements to troubleshoot methodically.

## Self-Check

- [ ] I can compare star, bus, ring, and mesh topologies.
- [ ] I can distinguish physical and logical topology.
- [ ] I can explain repeater, hub, media converter, and transceiver.
- [ ] I can explain CRC errors, runts, giants, and collisions.
- [ ] I can use Cisco interface commands to investigate a physical link issue.
- [ ] I can propose a structured troubleshooting sequence.

**You have completed the Physical Layer lesson sequence.** The next module begins with the Data Link layer and Ethernet frames.

## References

- [Cisco — CCNA 200-301 v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics)
- [Cisco — Configure and Verify Ethernet Auto-Negotiation](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/10561-3.html)
- [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html)
