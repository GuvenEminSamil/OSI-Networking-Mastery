# 02-03 — Ethernet Frame Structure

> **Prerequisites:** 02-01 — The Purpose of the Data Link Layer; 02-02 — MAC Addresses and NICs  
> **CCNA connection:** Ethernet framing, MAC addresses, payload identification, MTU, and frame-size troubleshooting.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Identify the main fields in an Ethernet frame.
- Explain the purpose of the preamble and Start Frame Delimiter.
- Distinguish destination and source MAC addresses.
- Understand the Length/Type field and EtherType values.
- Explain the minimum and maximum Ethernet frame sizes.
- Understand padding, MTU, jumbo frames, and the Interframe Gap (IFG).

## 1. What Is an Ethernet Frame?

An **Ethernet frame** is the Layer 2 data unit used to carry information over an Ethernet link.

A basic untagged Ethernet II frame has these main fields:

| Field | Size | Purpose |
|---|---:|---|
| Destination MAC | 6 bytes | Identifies the intended receiver |
| Source MAC | 6 bytes | Identifies the sender on this link |
| EtherType | 2 bytes | Identifies the protocol carried in the payload |
| Payload and padding | 46–1500 bytes | Carries the Layer 3 packet or other data |
| FCS | 4 bytes | Helps detect corruption in the received frame |

The destination and source fields are each 48 bits (six bytes), as described in lesson 02-02.

## 2. Preamble and Start Frame Delimiter

Before the Ethernet frame, the sender transmits two important fields.

### Preamble

The **preamble** is a 7-byte pattern that helps the receiving interface synchronize with the incoming signal. It uses a repeating pattern of alternating 1s and 0s.

### SFD — Start Frame Delimiter

The **SFD** is a 1-byte pattern that marks the end of the preamble and the start of the actual Ethernet frame.

Common patterns:

- Preamble: seven bytes of 0x55.
- SFD: one byte of 0xD5.

The preamble and SFD are transmitted before the destination MAC address. They are not included in the usual Ethernet frame-size measurement (64–1518 bytes for an untagged standard frame).

## 3. Destination and Source MAC Addresses

The next two fields are:

- **Destination MAC address:** the interface or group that should receive the frame.
- **Source MAC address:** the interface that sent the frame on this Ethernet link.

The source MAC address is an individual (unicast) address. The destination can be unicast, multicast, or broadcast.

When a router forwards an IP packet to another Ethernet link, it creates a new Ethernet frame with new Layer 2 source and destination addresses for that next link.

## 4. The Length/Type Field

The 2-byte field after the source MAC address has two historical uses:

- It can describe the length of the data field in IEEE 802.3 framing.
- It can identify the upper-layer protocol in Ethernet II framing. This use is called **EtherType**.

Common EtherType values:

| EtherType | Protocol |
|---|---|
| 0x0800 | IPv4 |
| 0x0806 | ARP |
| 0x86DD | IPv6 |

**ARP** means *Address Resolution Protocol*. It helps a device discover the MAC address associated with an IPv4 address on the local network.

How can a receiver distinguish Length from EtherType?

- Values up to 1500 (0x05DC) indicate a length.
- Values from 1536 (0x0600) and above are used as EtherType values.
- Values in between are reserved for this distinction.

For CCNA, remember the practical point: Ethernet II uses EtherType to identify the payload protocol, while IEEE 802.3 uses a length value.

## 5. Payload and Padding

The **payload** is the data carried inside the frame. In a typical Ethernet II frame, it contains an IPv4 packet, IPv6 packet, ARP message, or another protocol data unit.

An Ethernet frame has a minimum size. If the payload is too short, the sender adds extra bytes called **padding**.

Padding makes the frame reach the minimum required size.

For an ordinary untagged Ethernet frame:

- Minimum payload plus padding: 46 bytes.
- Maximum payload: 1500 bytes.
- FCS: 4 bytes.

This ensures that the complete frame is at least 64 bytes long, measured from the destination MAC address through the FCS.

## 6. FCS — Frame Check Sequence

The **FCS** (Frame Check Sequence) is a 4-byte field at the end of the Ethernet frame.

It contains the result of an error-detection calculation called **CRC** (Cyclic Redundancy Check).

The sender calculates the CRC value and places it in the FCS. The receiver performs the corresponding check:

- If the check is valid, the frame can continue to be processed.
- If the check fails, the frame is considered corrupted and is normally discarded.

Ethernet's FCS detects corruption; it does not itself request that the frame be retransmitted. A higher-layer protocol such as TCP may recover from lost data by retransmitting it.

You will study CRC and FCS in more detail in lesson 02-04.

## 7. Ethernet Frame Size: 64 to 1518 Bytes

For a standard untagged Ethernet frame, the size is measured from the destination MAC field to the FCS field. It does not include the preamble, SFD, or Interframe Gap.

Minimum frame:

\[
6+6+2+46+4=64\ bytes
\]

Maximum standard frame:

\[
6+6+2+1500+4=1518\ bytes
\]

A single 802.1Q VLAN tag adds four bytes to the header, so a standard tagged frame can be up to 1522 bytes.

The minimum frame size remains 64 bytes. A tagged frame can use a smaller padding amount because the VLAN tag adds four bytes to the frame header.

## 8. MTU and Jumbo Frames

**MTU** means *Maximum Transmission Unit*. It is the maximum size of the Layer 3 packet that a link can carry without fragmentation at that link.

For standard Ethernet, the common IP MTU is 1500 bytes.

Do not confuse:

- **Ethernet frame size:** includes the Layer 2 header and FCS.
- **MTU:** the maximum Layer 3 packet size carried in the Ethernet payload.

A **jumbo frame** is an Ethernet frame with a payload larger than the standard 1500-byte Ethernet payload limit.

Jumbo frames are used in some data-center and storage networks, but every device along the path must support compatible frame sizes. They are not enabled or supported identically on every network.

## 9. Interframe Gap (IFG)

The **Interframe Gap (IFG)** is the minimum idle time required between successive Ethernet frames.

For classic Ethernet, the minimum IFG is 96 bit times, equivalent to 12 byte times.

The IFG is not part of the Ethernet frame. It provides a short interval between frame transmissions.

## 10. Putting It Together

A simplified Ethernet transmission looks like this:

    Preamble | SFD | Destination MAC | Source MAC | Length/Type
             | VLAN tag (optional)
             | Payload + Padding | FCS
             | IFG (before the next frame)

Remember:

- Preamble and SFD come before the frame.
- The frame starts with the destination MAC address.
- FCS is the final field in the frame.
- IFG separates one frame transmission from the next.

## 11. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Preamble is counted in the 64-byte minimum frame size. | The usual frame-size count starts at destination MAC and ends at FCS. |
| SFD and IFG are the same thing. | SFD marks the start of the frame; IFG is the idle time between frames. |
| EtherType is the same as the payload length. | EtherType identifies the payload protocol; a Length value identifies the data length. |
| MTU and maximum frame size are both 1500 bytes. | Standard Ethernet MTU is commonly 1500 bytes; an untagged frame can be up to 1518 bytes including its Layer 2 header and FCS. |
| FCS repairs a damaged frame. | FCS detects corruption. Ethernet normally discards a frame with an invalid FCS. |
| Every network supports jumbo frames. | All relevant interfaces and devices must support compatible larger frame sizes. |

## 12. Knowledge Check

1. What does the Ethernet preamble help the receiver do?
   <details><summary>Answer</summary>Synchronize with the incoming signal before the frame begins.</details>

2. What does SFD stand for?
   <details><summary>Answer</summary>Start Frame Delimiter. It marks the start of the actual Ethernet frame.</details>

3. Which field identifies the source interface?
   <details><summary>Answer</summary>The source MAC address field.</details>

4. What is the EtherType for IPv4?
   <details><summary>Answer</summary>0x0800.</details>

5. What is the purpose of padding?
   <details><summary>Answer</summary>To make a short Ethernet frame reach the required minimum size.</details>

6. What is the minimum standard Ethernet frame size?
   <details><summary>Answer</summary>64 bytes, counted from destination MAC through FCS.</details>

7. What is the maximum standard untagged Ethernet frame size?
   <details><summary>Answer</summary>1518 bytes.</details>

8. How large can a standard frame be with one 802.1Q VLAN tag?
   <details><summary>Answer</summary>1522 bytes.</details>

9. What does FCS help detect?
   <details><summary>Answer</summary>Corruption in the received frame, using a CRC calculation.</details>

10. Is the IFG part of the Ethernet frame?
    <details><summary>Answer</summary>No. It is the minimum idle time between frame transmissions.</details>

## 13. Practice

A captured untagged Ethernet frame has:

- Destination MAC: 6 bytes
- Source MAC: 6 bytes
- EtherType: 2 bytes
- Payload: 40 bytes
- FCS: 4 bytes

Questions:

1. How many bytes are present before padding?
2. How many padding bytes are needed to reach the minimum frame size?
3. What is the final frame size?

Suggested calculation:

\[
6+6+2+40+4=58\ bytes
\]

The minimum is 64 bytes, so 6 bytes of padding are needed.

\[
58+6=64\ bytes
\]

## 14. CCNA Takeaways

- Know the basic Ethernet frame fields and their purposes.
- Preamble is 7 bytes; SFD is 1 byte.
- Destination and source MAC addresses are 6 bytes each.
- EtherType commonly identifies IPv4 (0x0800), ARP (0x0806), or IPv6 (0x86DD).
- Payload is usually 46–1500 bytes in a standard untagged Ethernet frame.
- FCS is 4 bytes and carries a CRC value.
- Standard frame size is 64–1518 bytes untagged and up to 1522 bytes with one VLAN tag.
- Ethernet MTU is commonly 1500 bytes.
- IFG is 96 bit times and is not part of the frame.

## Self-Check

- [ ] I can identify the fields in an Ethernet frame.
- [ ] I can explain preamble and SFD.
- [ ] I can distinguish EtherType from Length.
- [ ] I can calculate the minimum and maximum standard frame sizes.
- [ ] I understand padding and FCS.
- [ ] I can distinguish MTU, frame size, and IFG.

**Next lesson:** 02-04 — Error Detection: FCS and CRC.

## References

- [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf)
- [Cisco — NetFlow Layer 2 and Ethernet Frame Formats](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_pi/configuration/15-s/nf-15-s-book.pdf)
- [Cisco Press — Ethernet Frames](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4)
