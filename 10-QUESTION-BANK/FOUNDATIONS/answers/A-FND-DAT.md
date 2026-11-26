# FND-DAT — Answer Key

> Questions: `../Q-FND-DAT.md`. Complete the questions before opening this file. Scoring rules: `10-QUESTION-BANK/README.md`.

---

### FND-DAT-001
**Answer:** B

**Explanation:** Binary is useful because two clearly separated states provide a relatively wide noise margin, and transistors can operate reliably as switches. Speed is not the main reason.

**Why the other options are wrong:**
- A) Binary arithmetic is not inherently faster in every context.
- C) Cables can carry more than two signal levels. 1000BASE-T, for example, uses five-level PAM-5 signalling.
- D) Binary usually requires more digits than decimal for the same value.

**Lesson links:** 00-01 §4; 00-05 §3.3

### FND-DAT-002
**Answer:** a) **12 bits**. b) **1,096 unused values**.

**Explanation:** (2^{11}=2,048), which is not enough. (2^{12}=4,096), so 12 bits are required. The number of unused values is (4,096-3,000=1,096).

**Scoring:** 0.5 for each part.  
**Lesson links:** 00-01 §6; 00-02 §4.5

### FND-DAT-003
**Answer:** a) `1100 0000 1010 1000`. b) **49,320**. c) **192.168.**

**Explanation:** Each hexadecimal digit represents four bits: C = 1100, 0 = 0000, A = 1010, and 8 = 1000. As an unsigned 16-bit value, (0xC0A8 = 192\times256+168=49,320). Interpreted as two IPv4 octets, the bytes are 192 and 168.

**Scoring:** One third per part.  
**Lesson links:** 00-02 §§4.2, 4.4; 00-06 §1

### FND-DAT-004
**Answer:** No. A measured rate of 60 MB/s is close to what a 500 Mbps connection can deliver.

**Explanation:**
- (500\text{ Mbps} = 500\text{ million bits/s}).
- Divide by eight to convert bits to bytes: (500/8=62.5\text{ MB/s}) before protocol overhead.
- Ethernet, IP, and TCP headers consume some of the link capacity, so the useful application rate is lower. The earlier estimate of about 59.3 MB/s is consistent with a 60 MB/s display, depending on how the application reports units and measures throughput.

The mistake is comparing megabits per second (Mbps) with megabytes per second (MB/s) as though they were the same unit.

**Scoring:** 0.5 for dividing by eight; 0.5 for accounting for overhead or correctly discussing MB versus MiB.  
**Lesson links:** 00-02 §§4.8–4.9; 00-09 §4.1

### FND-DAT-005
**Answer:** A and C.

**Explanation:** A /26 mask is 255.255.255.192. The block size in the final octet is (256-192=64). Address 77 belongs to the range 64–127. Therefore, the network address is 10.20.30.64, and the wildcard mask is 0.0.0.63. The broadcast address is 10.20.30.127.

**Why the other options are wrong:**
- B) 10.20.30.255 would be the broadcast address for a /24 network.
- D) 10.20.30.0 is not the /26 network containing .77.
- E) 0.0.0.192 confuses the subnet mask with the wildcard mask.

**Lesson links:** 00-03 §§4.1–4.3

### FND-DAT-006
**Answer:** a) A considers B **remote**. b) B considers A **local**. c) **No**, a ping initiated by A will fail without a default gateway.

**Explanation:** Each host makes the local-versus-remote decision using its own IP address and its own subnet mask.

a) Host A uses /25 (255.255.255.128). A's network is 192.168.1.130 AND 255.255.255.128 = 192.168.1.128. B's address using that same mask gives 192.168.1.0. The results differ, so A considers B remote and tries to send the packet to its default gateway.

b) Host B uses /24 (255.255.255.0). Both addresses produce network address 192.168.1.0 with that mask, so B considers A local and sends directly.

c) A has no gateway to which it can send a packet it considers remote. A ping initiated by A therefore fails. A request from B may reach A, but A cannot route the reply back.

**Scoring:** One third per part. For (a), the subnet calculation must be shown.  
**Lesson links:** 00-03 §§4.1 and 5; details in 03-06

### FND-DAT-007
**Answer:** a) `01100110`. b) `11001010`. c) XOR is its own inverse: ((x\ XOR\ k)\ XOR\ k=x).

**Explanation:** XOR outputs 1 when the input bits differ. XORing with the same value twice reverses the first operation, returning the original value. This property is useful in parity and CRC operations and appears in some cryptographic constructions.

**Scoring:** One third per part.  
**Lesson links:** 00-03 §§3.4 and 4.4

### FND-DAT-008
**Answer:** B — destination port 53, DNS.

**Explanation:** Multi-byte network protocol fields use big-endian (network byte order). Bytes `00 35` represent hexadecimal `0x0035`, which is decimal 53.

**Why the other options are wrong:** A reverses the byte order; C treats hexadecimal 35 as decimal 35; D reverses the bytes and then misreads the result.

**Lesson links:** 00-06 §§3.2 and 4; 07-02

### FND-DAT-009
**Answer:** a) **500**. b) `0xF4010000`.

**Explanation:** In big-endian order, `00 00 01 F4` is `0x000001F4`, or 500. In little-endian order the byte sequence is interpreted with the least significant byte first, giving `0xF4010000` (4,093,706,240 in decimal).

**Scoring:** 0.5 for each part; hexadecimal is sufficient for (b).  
**Lesson links:** 00-06 §3.2

### FND-DAT-010
**Answer:** a) **22 calls**. b) The 64 kbps figure excludes packet and link overhead.

**Explanation:** (2,000/87.2\approx22.9), so only 22 complete calls fit. The 64 kbps rate describes the encoded voice payload, not the full Ethernet traffic. Packet headers and the Ethernet frame add overhead to every 20 ms packet. Twenty-three calls would exceed the 2 Mbps link.

**Scoring:** 0.5 for each part.  
**Lesson links:** 00-06 §§3.5 and 5

### FND-DAT-011
**Answer:** The client likely copied the port number into the packet without converting it to network byte order, for example by omitting `htons()`.

**Explanation:** Decimal 5000 is hexadecimal `0x1388`. The correct byte sequence is `13 88`. On a little-endian computer, the value may be stored in memory as `88 13`. If those bytes are copied into a network packet without conversion, the receiver interprets them as `0x8813`, which is decimal 34,835 — the value seen in Wireshark.

**Scoring:** 0.5 for identifying byte order / missing `htons()`; 0.5 for showing the hexadecimal conversion.  
**Lesson links:** 00-06 §3.2

### FND-DAT-012
**Example answer:** The bits sent over a link do not explain their own meaning. A protocol defines how the receiver should interpret each field. For example, the Ethernet EtherType value `0x0800` tells the receiver that the frame payload contains an IPv4 packet. The same two bytes in a TCP port field would represent a port number, not an IPv4 packet. The field's location and the protocol definition determine the interpretation.

**Scoring rubric (1 point total):**

| Criterion | Points |
|---|---:|
| Explains that data consists of bits or bytes and has no built-in meaning | 0.25 |
| Gives a different, correct example showing the same bytes can have different meanings | 0.50 |
| Explains that a protocol or field position defines the interpretation | 0.25 |

**Lesson links:** 00-01 §2; 00-06 §§1 and 3.7
