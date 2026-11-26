# FND-HW — Electricity, Transistors, and Computer Architecture

> **Coverage:** 00-04, 00-05, 00-07 | **Questions:** 9 | **Suggested time:** 30 minutes  
> Answers: `answers/A-FND-HW.md`. See `10-QUESTION-BANK/README.md` for scoring rules. No calculator.

---

### FND-HW-001
**Category:** O · **Difficulty:** 1 · **Lesson:** 00-04

An IP camera uses PoE at 48 V and draws 0.25 A. The cable's total loop resistance is 10 Ω.

a) How much power does the camera receive?  
b) How much power is lost as heat in the cable?

### FND-HW-002
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-04

In a factory, an Ethernet cable runs in the same cable tray as the power cable for a large motor. CRC errors increase on the connected switch port. Which **two** actions directly address the likely problem? (Select two.)

- A) Route the data cable separately from the power cable.
- B) Use a longer Ethernet cable.
- C) Replace the Ethernet connection with fiber.
- D) Increase the port speed from 100 Mbps to 1 Gbps.
- E) Restart the switch.

### FND-HW-003
**Category:** I · **Difficulty:** 2 · **Lesson:** 00-05

A logic family datasheet lists: VOH = 3.0 V, VIH = 2.3 V, VIL = 1.0 V, VOL = 0.4 V.

a) Calculate the high-level and low-level noise margins.  
b) The line may experience 0.65 V of noise. Which logic level is at risk, and why?

### FND-HW-004
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-05

On a Cisco router, where are changes made with `configure terminal` first stored, and what happens if power is lost before saving?

- A) In startup-config in NVRAM; the changes remain.
- B) In running-config in RAM; the unsaved changes are lost.
- C) In the IOS image in flash; the changes remain.
- D) In the bootstrap program in ROM; the changes remain.

### FND-HW-005
**Category:** S · **Difficulty:** 2 · **Lesson:** 00-05

In a lab, you enter `hostname SW-LAB` and create VLANs 10 and 20 on a Catalyst switch. You remove power without saving the configuration. After reboot, VLANs 10 and 20 still exist, but the prompt is back to `Switch>`.

Explain why these two results are different.

### FND-HW-006
**Category:** MC · **Difficulty:** 2 · **Lesson:** 00-07

A Linux server is connected to a switch port with no CRC errors. During busy periods, the server's `ethtool -S` output shows a rapidly increasing `rx_missed_errors` counter. What is the most likely cause?

- A) A faulty cable is corrupting frames.
- B) The RX ring buffer is full because the driver and CPU cannot process incoming frames quickly enough.
- C) The server and switch have a duplex mismatch.
- D) Another device is using the server's IP address.

### FND-HW-007
**Category:** O · **Difficulty:** 2 · **Lesson:** 00-07

A 100 Mbps Ethernet link carries only minimum-size 64-byte frames.

a) Approximately how many frames per second can it transmit? Include preamble, SFD, and interframe gap (IFG).  
b) How long does each frame occupy the link?

### FND-HW-008
**Category:** KK · **Difficulty:** 2 · **Lesson:** 00-07

Compare interrupts and polling.

- Which is generally more suitable at low traffic rates, and why?
- Which can be more suitable at high traffic rates, and why?
- How does Linux NAPI combine the two approaches?

### FND-HW-009
**Category:** A · **Difficulty:** 2 · **Lesson:** 00-07

A student captures traffic with Wireshark on a laptop. Outgoing TCP packets are marked with an `incorrect` checksum, but incoming packets look correct. The student concludes that the cable is faulty and packets are being transmitted with errors.

a) Is the student correct? What is the most likely explanation?  
b) Give two ways to verify your explanation.
