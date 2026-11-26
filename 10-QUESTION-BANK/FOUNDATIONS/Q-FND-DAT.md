# FND-DAT — Information, Number Systems, Logic, and Data Representation

> **Coverage:** 00-01, 00-02, 00-03, 00-06 | **Questions:** 12 | **Suggested time:** 35 minutes  
> Answers: `answers/A-FND-DAT.md`. See `10-QUESTION-BANK/README.md` for scoring rules. No calculator.

---

### FND-DAT-001
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-01

Why do digital computers commonly use binary internally?

- A) Binary addition is always faster than decimal addition.
- B) Two states provide a wide noise margin, and transistors operate reliably as switches.
- C) Cables can physically carry only two voltage levels.
- D) Binary uses fewer digits than decimal for the same number.

### FND-DAT-002
**Category:** O · **Difficulty:** 1 · **Lessons:** 00-01, 00-02

A campus has 3,000 devices. Each device needs a unique identification number.

a) What is the minimum number of bits required?  
b) With that number of bits, how many additional values remain after assigning 3,000 devices?

### FND-DAT-003
**Category:** O · **Difficulty:** 2 · **Lesson:** 00-02

Convert `0xC0A8`.

a) Write it in binary.  
b) What is its decimal value as an unsigned 16-bit integer?  
c) If these two bytes were the first two octets of an IPv4 address, what would the address begin with?

### FND-DAT-004
**Category:** S · **Difficulty:** 2 · **Lessons:** 00-02, 00-09

A friend says: “My Internet plan is 500 Mbps, but my download application shows a maximum of 60 MB/s. My provider is not giving me the full speed.”

Is the friend correct? Show the calculation and explain the units.

### FND-DAT-005
**Category:** MC · **Difficulty:** 2 · **Lesson:** 00-03

Which **two** statements about address `10.20.30.77/26` are correct? (Select two.)

- A) The network address is 10.20.30.64.
- B) The broadcast address is 10.20.30.255.
- C) The wildcard mask is 0.0.0.63.
- D) The network address is 10.20.30.0.
- E) The wildcard mask is 0.0.0.192.

### FND-DAT-006
**Category:** I · **Difficulty:** 3 · **Lesson:** 00-03

Two hosts are connected to the same switch and belong to the same VLAN. An administrator has mistakenly configured different subnet masks:

| Host | Address |
|---|---|
| A | 192.168.1.130/25 |
| B | 192.168.1.100/24 |

a) When A sends a packet to B, does A consider B local or remote? Show the calculation.  
b) When B sends a packet to A, does B consider A local or remote?  
c) If Host A has no default gateway configured, will a ping initiated by A to B succeed?

### FND-DAT-007
**Category:** O · **Difficulty:** 1 · **Lesson:** 00-03

a) Calculate `11001010 XOR 10101100`.  
b) XOR the result from (a) with `10101100` again. What do you get?  
c) Which XOR property does this demonstrate?

### FND-DAT-008
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-06

In Wireshark, a TCP destination-port field appears on the wire as bytes `00 35`. What is the destination port, and which service is most likely intended?

- A) 13,568; an unknown service
- B) 53; DNS
- C) 35; an unknown service
- D) 3,500; an unknown service

### FND-DAT-009
**Category:** O · **Difficulty:** 2 · **Lesson:** 00-06

A header contains a 32-bit unsigned field transmitted as four bytes: `00 00 01 F4`.

a) What is the value when interpreted in network byte order?  
b) What value would a program see if it interpreted these bytes as a little-endian integer? (Hexadecimal is sufficient; decimal is optional.)

### FND-DAT-010
**Category:** S · **Difficulty:** 2 · **Lesson:** 00-06

Two company offices are connected by a 2 Mbps link. Assume the entire link is reserved for G.711 voice calls, and each call uses 87.2 kbps over Ethernet (20 ms packetization).

a) What is the maximum number of simultaneous calls?  
b) An employee says that 31 calls fit if we calculate using 64 kbps per call. What did the employee overlook?

### FND-DAT-011
**Category:** A · **Difficulty:** 2 · **Lesson:** 00-06

A student has written a UDP server that listens on port 5000. The student's client cannot reach it. Wireshark shows that outgoing packets have destination port **34835**.

What is the most likely cause? Support your answer with a calculation.

### FND-DAT-012
**Category:** K · **Difficulty:** 2 · **Lessons:** 00-01, 00-06

Explain this statement in your own words: “Data does not carry its meaning by itself; meaning comes from the interpretation rules agreed by both sides.”

Use a networking example different from the `C0 A8 01 01` example in lesson 00-06. Write 4–6 sentences.
