# 02-04 — Error Detection: FCS and CRC

> **Prerequisites:** 00-03 — Binary Arithmetic and Boolean Logic; 02-03 — Ethernet Frame Structure  
> **Purpose:** Understand how a receiver can detect that a frame was corrupted.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain why data-link technologies need error detection.
- Distinguish error detection from error correction.
- Recognize parity and checksum methods.
- Explain how CRC uses binary polynomial division and XOR.
- Understand the purpose of the Ethernet Frame Check Sequence (FCS).
- Explain what happens when an Ethernet frame fails its FCS check.

## 1. Why Is Error Detection Necessary?

Signals can be affected by noise, interference, attenuation, and other physical problems.

A receiver may therefore receive bits that are different from the bits sent.

An **error-detection method** adds or calculates extra information so the receiver can check whether the data may have been changed.

For example, a sender transmits a frame and includes an FCS value. The receiver calculates a new value from the received frame and compares it with the received FCS.

If they do not match, the frame is considered corrupted.

## 2. Error Detection vs. Error Correction

These terms are different:

- **Error detection** identifies that data may have been corrupted.
- **Error correction** attempts to identify and repair the corrupted data.

Ethernet's FCS provides error detection. It does not repair the damaged frame.

Some other systems use codes that can correct certain errors, but you should not assume every error-detection method can correct errors.

## 3. Parity

A **parity bit** is an extra bit added to data so that the total number of 1s follows a chosen rule.

Two common rules are:

- **Even parity:** the total number of 1s should be even.
- **Odd parity:** the total number of 1s should be odd.

Example using even parity:

Data bits:

`1011001`

There are four 1s, so the even-parity bit is 0.

If one bit changes during transmission, the total number of 1s may become odd and the receiver can detect an error.

However, parity has a limitation: if two bits change, the total count may still have the required parity. So a simple parity bit does not detect every possible error.

## 4. Checksums

A **checksum** is a value calculated from a group of data, then sent so the receiver can calculate and compare the result.

A simple checksum may add fixed-size groups of bits or bytes and send a value derived from the sum.

Checksums can detect many common errors, but some combinations of changes may still produce the same checksum.

Different protocols use different checksum algorithms. Do not assume that a checksum and a CRC use the same calculation.

## 5. CRC — Cyclic Redundancy Check

**CRC** means *Cyclic Redundancy Check*. It is an error-detection method that treats a sequence of bits as a mathematical polynomial and calculates a remainder using binary division.

You do not need advanced mathematics to understand the basic process.

The sender:

1. Takes the data bits.
2. Uses an agreed bit pattern called a **generator polynomial**.
3. Performs modulo-2 binary division.
4. Appends the calculated remainder to the data.

The receiver performs the corresponding calculation. If the check does not match the expected result, the data is considered corrupted.

### Why Does CRC Use XOR?

**Modulo-2 arithmetic** is binary arithmetic without carries or borrows.

In modulo-2 addition and subtraction, the operation is XOR:

| A | B | A XOR B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

This is why CRC calculations use XOR operations instead of ordinary decimal subtraction.

CRC is particularly effective at detecting many common transmission errors, including burst errors (multiple changed bits close together).

## 6. Ethernet FCS

Ethernet uses a **Frame Check Sequence (FCS)** field at the end of the frame.

The FCS is four bytes long and carries an Ethernet CRC-32 value.

The sender calculates the CRC from the relevant frame fields and puts the result in the FCS.

The receiver calculates the CRC again and checks it against the received FCS.

Simplified process:

```
Sender:
Frame data → Calculate CRC → Add FCS → Transmit

Receiver:
Receive frame → Calculate CRC → Compare with FCS
                                  |
                         +--------+--------+
                         |                 |
                       Match            Mismatch
                         |                 |
                    Continue          Discard frame
```

A valid FCS does not prove that every part of a network path is perfect. It tells the receiver that this frame passed the CRC check.

## 7. What Happens When an Ethernet FCS Is Invalid?

When a switch or NIC receives a frame with an invalid FCS, it normally discards the frame.

Ethernet itself does not automatically retransmit the frame.

A higher-layer protocol may recover from lost data. For example, TCP can detect missing data and retransmit it.

This distinction is important:

- Ethernet FCS detects frame corruption on a link.
- TCP provides reliable delivery across an IP connection by using acknowledgments, sequence numbers, and retransmission.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Error detection always repairs the data. | Detection identifies possible corruption; correction is a separate capability. |
| A parity bit detects every possible error. | Simple parity can miss errors when an even number of bits changes. |
| CRC uses ordinary decimal subtraction. | CRC uses modulo-2 polynomial division, which relies on XOR. |
| FCS is an IP header field. | Ethernet FCS is a Layer 2 frame field. |
| Ethernet retransmits every frame with a bad FCS. | Ethernet normally discards a bad frame; higher layers may recover. |
| A valid FCS proves the whole network works. | It only means that the received frame passed this error check. |

## 9. Knowledge Check

1. What is the difference between error detection and error correction?
   <details><summary>Answer</summary>Error detection identifies possible corruption; error correction attempts to repair it.</details>

2. What does a parity bit do?
   <details><summary>Answer</summary>It helps detect some errors by making the total number of 1s follow an even or odd rule.</details>

3. Can simple parity detect every error?
   <details><summary>Answer</summary>No. For example, two bit changes can preserve the parity.</details>

4. What does CRC stand for?
   <details><summary>Answer</summary>Cyclic Redundancy Check.</details>

5. Which binary operation is used in modulo-2 addition?
   <details><summary>Answer</summary>XOR.</details>

6. What is the Ethernet FCS?
   <details><summary>Answer</summary>A four-byte field carrying the CRC-32 value used to detect frame corruption.</details>

7. What does a switch normally do with a frame that has an invalid FCS?
   <details><summary>Answer</summary>It discards the frame.</details>

8. Does Ethernet itself retransmit a frame after an FCS failure?
   <details><summary>Answer</summary>No. A higher-layer protocol such as TCP may recover by retransmitting data.</details>

## 10. Practice

Imagine a switch interface's CRC counter increases over time.

1. What does the counter suggest?
2. Name two possible physical causes.
3. Why does an increasing CRC counter not prove exactly which component is faulty?
4. What test could help isolate a damaged cable?

Suggested answer:

- The interface is receiving frames that fail the FCS check.
- Possible causes include damaged cabling, poor termination, interference, or a faulty transceiver.
- The CRC counter reports the error, not the exact root cause.
- Replace the cable temporarily with a known-good cable and compare the counters.

## 11. CCNA Takeaways

- Error detection and error correction are different.
- Parity and checksums are simple error-detection methods.
- CRC uses modulo-2 binary division and XOR.
- Ethernet FCS is a four-byte CRC-32 value.
- A frame with an invalid FCS is normally discarded.
- Ethernet does not itself retransmit a corrupted frame; higher-layer protocols may recover.

## Self-Check

- [ ] I can distinguish error detection from error correction.
- [ ] I can explain even and odd parity.
- [ ] I understand the basic idea of a checksum.
- [ ] I can explain why CRC uses XOR.
- [ ] I know where Ethernet FCS appears and what it does.
- [ ] I understand what happens when a frame fails the FCS check.

**Next lesson:** 02-05 — Media Access, CSMA/CD, and Duplex.

## References

- [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf)
- [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html)
