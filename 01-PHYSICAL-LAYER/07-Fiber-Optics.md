# 01-07 — Fiber Optics

> **Prerequisites:** 01-05 — Signal Impairments; 01-06 — Copper Cabling  
> **CCNA 200-301 v1.1 connection:** Exam objective 1.3.a — Compare single-mode fiber, multimode fiber, and copper.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain how light carries data through optical fiber.
- Identify the core, cladding, and outer jacket.
- Compare single-mode and multimode fiber.
- Recognize common wavelengths and fiber types.
- Understand modal and chromatic dispersion.
- Identify LC and SC connectors.
- Recognize SFP, SFP+, and QSFP transceiver modules.

## 1. How Does Fiber Carry Data?

**Optical fiber** is a thin strand of glass or plastic that carries information using light.

A transmitter converts electrical data into optical signals. Light travels through the fiber, and a receiver converts the received light back into an electrical signal.

Fiber is useful because it can support high data rates over long distances and is not affected by electromagnetic interference in the same way as copper cable.

## 2. Core, Cladding, and Jacket

A fiber strand has several layers:

- **Core:** The central part of the fiber through which light travels.
- **Cladding:** The glass layer around the core. It has a lower refractive index than the core and helps keep light inside.
- **Coating and jacket:** Protective layers that help prevent physical damage and moisture.

**Refractive index** describes how much light slows down when it travels through a material.

### Total Internal Reflection

When light travels from the higher-index core toward the lower-index cladding at a suitable angle, it can reflect back into the core instead of escaping. This is called **total internal reflection**.

Repeated internal reflections help the light remain inside the fiber as it travels.

The exact light path depends on the fiber design. The important idea is that the core and cladding are designed to guide light along the fiber.

## 3. Single-Mode and Multimode Fiber

There are two main types of optical fiber used in networking.

### Single-Mode Fiber (SMF)

**Single-mode fiber (SMF)** has a very small core, typically around 9 micrometers in common telecom designs.

It carries light in one propagation mode. A **mode** is a possible path or pattern in which light travels through the fiber.

Because it avoids the multiple paths found in multimode fiber, SMF can support longer distances and high data rates.

SMF commonly uses laser-based transmitters and wavelengths such as 1310 nm and 1550 nm.

### Multimode Fiber (MMF)

**Multimode fiber (MMF)** has a larger core, commonly 50 or 62.5 micrometers.

It allows multiple light paths (modes) to travel through the fiber. It is often used for shorter links inside buildings and data centers.

MMF commonly uses 850 nm optical transmitters, including VCSEL-based devices.

**VCSEL** means *Vertical-Cavity Surface-Emitting Laser*. It is a type of laser commonly used with multimode fiber.

### Quick Comparison

| Property | Single-mode (SMF) | Multimode (MMF) |
|---|---|---|
| Core | Smaller, commonly about 9 μm | Larger, commonly 50 or 62.5 μm |
| Light paths | One mode | Multiple modes |
| Common wavelengths | 1310 nm and 1550 nm | 850 nm; other designs may use additional wavelengths |
| Typical use | Longer distances | Shorter building and data-center links |
| Transmitter | Commonly laser | Commonly LED or VCSEL, depending on technology |

The fiber type and the transceiver must be compatible. A connector that physically fits does not guarantee that the optical modules are compatible.

## 4. OM and OS Fiber Categories

Multimode fiber types are commonly identified with **OM** labels, while single-mode fiber types use **OS** labels.

| Type | Category | Common description |
|---|---|---|
| OM1 | Multimode | Legacy 62.5 μm core |
| OM2 | Multimode | 50 μm core |
| OM3 | Multimode | Laser-optimized 50 μm fiber |
| OM4 | Multimode | Higher performance than OM3 for supported applications |
| OM5 | Multimode | Wideband multimode fiber for specified wavelength ranges |
| OS1 / OS2 | Single-mode | Single-mode fiber categories; OS2 is widely used for outdoor/longer-reach cabling |

A **micrometer (μm)** is one millionth of a meter. A **nanometer (nm)** is one billionth of a meter.

You do not need to memorize every category specification in this lesson. Recognize the names and understand that OM refers to multimode and OS to single-mode fiber.

## 5. Wavelengths: 850 nm, 1310 nm, and 1550 nm

A **wavelength** is the distance between repeating points on a wave, such as one peak to the next peak. It is commonly measured in nanometers for optical communication.

Common optical wavelengths include:

- 850 nm: widely used with multimode fiber.
- 1310 nm: commonly used with single-mode fiber and some other optical designs.
- 1550 nm: commonly used for longer-reach single-mode links.

These are common examples, not universal rules. Always check the transceiver specifications.

## 6. Dispersion in Fiber

**Dispersion** means that parts of a light pulse can arrive at different times. The pulse spreads out as it travels.

Two forms are especially useful to recognize:

### Modal Dispersion

**Modal dispersion** occurs in multimode fiber because different light paths can have different travel times.

Some light paths are longer than others. Their pulses may arrive at different times, spreading the received pulse.

Single-mode fiber avoids this particular multiple-path effect.

### Chromatic Dispersion

**Chromatic dispersion** occurs because different wavelengths (colors) of light can travel at slightly different speeds in the fiber.

If a transmitted pulse contains a range of wavelengths, the components may spread apart over distance.

You do not need to calculate dispersion values for this lesson. Understand that pulse spreading can limit the distance and data rate of an optical link.

## 7. Fiber Connectors: LC and SC

Fiber connectors align the fiber end so that light can pass between devices with low loss.

Two common connector types are:

- **LC (Lucent Connector):** A small connector with a latch. It is widely used on modern transceivers.
- **SC (Subscriber Connector):** A larger, square connector that uses a push-pull mechanism.

A **duplex connector** carries two separate fiber strands: one for transmit and one for receive.

Many Ethernet fiber links use two strands. Some technologies use a single strand with different wavelengths in each direction, but that requires compatible transceivers.

## 8. SFP, SFP+, and QSFP Modules

A **transceiver** can both transmit and receive signals.

Network devices often use removable optical or copper transceiver modules.

| Module name | General purpose |
|---|---|
| SFP | Small Form-Factor Pluggable; commonly used for Gigabit Ethernet |
| SFP+ | Enhanced SFP form factor; commonly used for 10 Gigabit Ethernet |
| QSFP | Quad Small Form-Factor Pluggable; supports multiple data lanes for higher-speed links |

A **data lane** is one independent stream of transmitted data within a multi-lane interface.

The transceiver determines the supported medium, wavelength, connector, and distance. Check the exact module data sheet before connecting a link.

## 9. Example: 1000BASE-SX and 1000BASE-LX

These examples help you recognize common Gigabit Ethernet fiber standards.

| Standard | Typical fiber | Common wavelength | Example reach |
|---|---|---:|---|
| 1000BASE-SX | Multimode | 850 nm | Up to about 550 m on suitable 50 μm MMF |
| 1000BASE-LX/LH | Single-mode | 1310 nm | Up to about 10 km on supported SMF |

These distances are examples for particular Cisco transceiver families. Exact reach depends on the transceiver model, fiber grade, connectors, splices, and the optical link budget.

## 10. Fiber Safety and Troubleshooting

Never look directly into the end of a fiber cable or an optical transceiver. Some optical signals are infrared and may not be visible to the human eye.

Common fiber problems include:

- Dirty connector end faces.
- Incorrect fiber type or transceiver.
- Incorrect transmit/receive polarity.
- Excessive bending or physical damage.
- Optical signal that is too weak or too strong for the receiver.

A **link budget** is the allowed range of optical power loss between transmitter and receiver.

For troubleshooting:

1. Verify that the transceivers at both ends are compatible.
2. Confirm that the fiber type and connector match.
3. Check that transmit and receive strands are connected correctly.
4. Inspect and clean connectors using the correct cleaning tools.
5. Check optical power and interface counters where supported.

## 11. Knowledge Check

1. What carries information through optical fiber?
   <details><summary>Answer</summary>Light signals.</details>

2. What are the core and cladding?
   <details><summary>Answer</summary>The core guides the light; the surrounding cladding has a lower refractive index and helps keep light inside the core.</details>

3. What is total internal reflection?
   <details><summary>Answer</summary>A condition where light reflects back into the higher-index core rather than passing into the lower-index cladding.</details>

4. Which fiber type is normally used for longer distances: SMF or MMF?
   <details><summary>Answer</summary>Single-mode fiber (SMF).</details>

5. Which fiber type commonly uses 850 nm in Ethernet links?
   <details><summary>Answer</summary>Multimode fiber (MMF).</details>

6. What causes modal dispersion?
   <details><summary>Answer</summary>Different light paths in multimode fiber can have different travel times, spreading the pulse.</details>

7. What do LC and SC identify?
   <details><summary>Answer</summary>Two types of fiber-optic connector.</details>

8. What is the general difference between SFP and SFP+?
   <details><summary>Answer</summary>SFP is commonly used for Gigabit Ethernet; SFP+ is commonly used for 10 Gigabit Ethernet.</details>

## 12. Practice

A switch has a 1000BASE-SX module, but the connected fiber link does not come up.

Check the following:

1. Is the fiber multimode?
2. Does the remote device use a compatible transceiver?
3. Are the transmit and receive strands crossed correctly?
4. Are the connectors clean?
5. Does the actual cable length fit the transceiver specifications?

Explain which check you would perform first and why.

## 13. CCNA Takeaways

- Fiber carries data using light.
- The core guides light; the cladding supports total internal reflection.
- SMF has a smaller core and is commonly used for longer links.
- MMF has a larger core and is commonly used for shorter links.
- Recognize 850 nm, 1310 nm, and 1550 nm.
- OM identifies multimode categories; OS identifies single-mode categories.
- Know LC and SC connectors.
- Recognize SFP, SFP+, and QSFP transceiver modules.
- Always match transceiver type, wavelength, fiber, connector, and reach.

## Self-Check

- [ ] I can explain how fiber guides light.
- [ ] I can compare SMF and MMF.
- [ ] I recognize common fiber wavelengths and OM/OS categories.
- [ ] I can explain modal and chromatic dispersion.
- [ ] I can identify LC, SC, SFP, SFP+, and QSFP.
- [ ] I can suggest basic troubleshooting checks for a fiber link.

**Next lesson:** 01-08 — Wireless RF Fundamentals.

## References

- [Cisco — CCNA 200-301 v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics)
- [Cisco — Gigabit Ethernet SFP Transceiver Data Sheet](https://www.cisco.com/c/en/us/products/collateral/interfaces-modules/gigabit-ethernet-gbic-sfp-modules/datasheet-c78-366584.html)
- [Cisco — Physical Infrastructure Design Guide (Fiber Optics)](https://www.cisco.com/c/en/us/td/docs/solutions/Verticals/CPwE/5-1/Phy_Arch/CPwE-Physical-Infrastructure_Feb2023.pdf)
