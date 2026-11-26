# FND-HW — Answer Key

> Questions: `../Q-FND-HW.md`. Complete the questions before opening this file. Scoring rules: `10-QUESTION-BANK/README.md`.

---

### FND-HW-001
**Answer:** a) **12 W**. b) **0.625 W**.

**Explanation:** Camera power is (P=V\times I=48\times0.25=12\text{ W}). Cable loss is (P=I^2R=0.25^2\times10=0.625\text{ W}).

**Scoring:** 0.5 for each part.  
**Lesson links:** 00-04 §§3.5 and 4.1

### FND-HW-002
**Answer:** A and C.

**Explanation:** The motor's changing magnetic field can induce electromagnetic interference (EMI) in a nearby data cable. If the interference is strong enough, the receiver may misread bits and the Ethernet FCS check can fail. Separating the cable reduces exposure; fiber uses light and is not affected by electromagnetic interference.

**Why the other options are wrong:**
- B) A longer cable generally increases attenuation.
- D) Increasing speed does not remove the interference and may make the link less tolerant of signal problems.
- E) Restarting may reset counters but does not remove the interference source.

**Lesson links:** 00-04 §§3.6, 5, and 9

### FND-HW-003
**Answer:** a) High noise margin = **0.7 V**; low noise margin = **0.6 V**. b) The low (0) level is at risk.

**Explanation:**
- (NM_H=V_{OH}-V_{IH}=3.0-2.3=0.7\text{ V}).
- (NM_L=V_{IL}-V_{OL}=1.0-0.4=0.6\text{ V}).

A 0.65 V disturbance can raise a low output from 0.4 V to 1.05 V, beyond the 1.0 V low-input limit. A high output reduced by 0.65 V would be 2.35 V, still above the 2.3 V high-input limit.

**Scoring:** 0.5 for both margins; 0.5 for the level and explanation.  
**Lesson links:** 00-05 §3.5; 00-01 §3.2

### FND-HW-004
**Answer:** B.

**Explanation:** Commands entered under `configure terminal` update the running configuration in RAM. RAM is volatile, so unsaved changes are lost when power is removed. To save them, use:

```text
copy running-config startup-config
```

The startup configuration is stored in non-volatile memory.

**Lesson links:** 00-05 §§3.8 and 7

### FND-HW-005
**Answer:** The hostname was in the unsaved running configuration and was lost. The VLANs remained because the VLAN database is stored separately in the switch's flash storage, typically in `vlan.dat`.

**Explanation:** On Catalyst switches, the startup configuration and VLAN database are separate persistent records. The `hostname` command changes the running configuration; without saving it, the change disappears on reboot. Creating VLANs updates the VLAN database, which remains in flash.

**Scoring:** 0.5 for explaining the lost hostname; 0.5 for explaining the persistent VLAN database.  
**Lesson links:** 00-05 §7; further detail in 02-08

### FND-HW-006
**Answer:** B.

**Explanation:** There are no CRC errors, so the frames are not apparently arriving corrupted over the cable. The `rx_missed_errors` counter indicates that the NIC could not accept incoming frames quickly enough, often because the receive (RX) ring buffer ran out of available descriptors. The driver and CPU may not be processing frames quickly enough.

**Why the other options are wrong:** A and C would commonly be associated with link errors; D is an IP-layer issue and does not explain an RX ring shortage.

**Lesson links:** 00-07 §§3.3, 5, and 9

### FND-HW-007
**Answer:** a) Approximately **148,810 frames per second**. b) **6.72 microseconds per frame**.

**Explanation:** The link is occupied by 64 frame bytes + 8 bytes for preamble and SFD + 12 byte-times for the interframe gap = 84 byte-times = 672 bits. Therefore (100,000,000/672\approx148,810) frames per second, and (672/100,000,000=6.72\ \mu s).

**Scoring:** 0.5 for each part. Omitting the 20 byte-times of preamble/SFD and IFG gives an incorrect frame rate.  
**Lesson links:** 00-07 §4

### FND-HW-008
**Example answer:** Interrupts are generally useful at low traffic rates because the CPU can do other work until a frame arrives. Polling can be more efficient at high traffic rates because processing many frames in a batch can avoid the cost of handling an interrupt for every frame. Linux NAPI starts with an interrupt, temporarily disables further receive interrupts, polls the receive queue up to a budget, and re-enables interrupts when the queue is drained.

**Scoring rubric (1 point total):**

| Criterion | Points |
|---|---:|
| Explains the low-traffic advantage of interrupts | 0.25 |
| Explains interrupt overhead and batching with polling at high traffic | 0.25 |
| Describes NAPI's interrupt → poll → re-enable sequence | 0.50 |

**Lesson links:** 00-07 §3.4

### FND-HW-009
**Answer:** a) The student is probably not correct. The likely explanation is **transmit checksum offload**. b) Verify it by capturing the packet on the receiving computer or elsewhere on the path, and by checking or temporarily disabling checksum offload.

**Explanation:** With checksum offload enabled, the operating system may hand a packet to the NIC before the final checksum is calculated. A capture taken on the sending computer can therefore see an unfinished checksum and mark it as incorrect. The NIC calculates the checksum before transmitting the frame.

Useful checks include:
- Capture the same traffic on the receiving host or at an intermediate observation point.
- Check offload settings. On Linux, use `ethtool -k <interface>`; on Windows, inspect the adapter's advanced properties.
- Check switch-port CRC counters. A cable error would be more likely to produce receive-side frame errors.
- Temporarily disable checksum offload for a controlled test.

**Scoring:** 0.5 for the explanation; 0.5 for two valid verification methods.  
**Lesson links:** 00-07 §§3.6 and 5
