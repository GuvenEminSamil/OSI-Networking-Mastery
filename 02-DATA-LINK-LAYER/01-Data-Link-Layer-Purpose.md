# 02-01 — The Purpose of the Data Link Layer

> **Prerequisites:** 00-09 — Layered Models: OSI and TCP/IP; 01-01 — The Purpose of the Physical Layer  
> **CCNA connection:** Foundation for Ethernet frames, MAC addressing, switching, and WAN data-link technologies.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain the role of the Data Link layer.
- Understand how it differs from the Physical and Network layers.
- Recognize the LLC and MAC sublayers.
- Explain framing and media access.
- Distinguish point-to-point and shared media.
- Understand why LAN and WAN links may use different Data Link technologies.
- Recognize Ethernet, PPP, and HDLC at a basic level.

## 1. Why Do We Need the Data Link Layer?

The **Data Link layer** is OSI Layer 2 (L2). It provides communication over one local network link.

The Physical layer carries raw bits as electrical, optical, or radio signals. The Data Link layer organizes those bits into a unit called a **frame** and provides rules for local delivery.

Think about sending a parcel:

- The Physical layer is like the road or physical route the parcel travels on.
- The Data Link layer is like the local label and handling rules used to deliver it across one part of the journey.
- The Network layer decides how the parcel can travel across different networks toward its destination.

A frame is normally delivered across one link. A router receives a frame, processes the enclosed packet, and builds a new frame for the next link.

## 2. What Does the Data Link Layer Do?

Common responsibilities include:

- **Framing:** Organizing a stream of bits into identifiable frames.
- **Local addressing:** Identifying devices or interfaces on the local link, commonly using MAC addresses in Ethernet.
- **Media access:** Defining how devices share or take turns using a communication medium.
- **Error detection:** Detecting some forms of corruption in a received frame.
- **Link management:** Supporting the rules required for communication over a particular link.

The exact services depend on the Data Link technology. Not every Layer 2 protocol performs every function in the same way.

## 3. What Is Framing?

**Framing** is the process of organizing a stream of bits into separate units called frames.

Why is this necessary?

The Physical layer carries a continuous sequence of signal changes. The receiving device needs to know where one data unit begins and ends.

A frame can contain:

- A header with control information.
- A payload containing the data being carried.
- Sometimes a trailer with error-detection information.

A **header** is control information placed before the payload. A **payload** is the data carried by the frame. A **trailer** is information placed after the payload.

Different Data Link technologies define different frame formats. You will study the Ethernet frame in detail in lesson 02-03.

## 4. LLC and MAC: Two Sublayers

The IEEE 802 architecture divides the Data Link layer into two sublayers:

- **LLC** (Logical Link Control), associated with IEEE 802.2.
- **MAC** (Media Access Control), defined by the specific link technology, such as Ethernet.

### LLC — Logical Link Control

The LLC sublayer provides a common interface to the Network layer and helps identify which upper-layer protocol is carried.

For example, a receiving device needs to determine whether the payload should be processed as IPv4, IPv6, or another protocol.

You do not need to memorize the detailed historical LLC header format for this lesson.

### MAC — Media Access Control

The MAC sublayer handles technology-specific local-link tasks.

In Ethernet, this includes:

- Source and destination MAC addresses.
- Ethernet frame handling.
- Rules for sending frames on the Ethernet medium.

A **MAC address** is a link-layer address used to identify a network interface on a local link. You will study its 48-bit structure and special bits in lesson 02-02.

Simplified view:

```
Data Link Layer (Layer 2)
+-------------------------------------+
| LLC — upper-layer protocol interface|
+-------------------------------------+
| MAC — local addressing and access   |
+-------------------------------------+
Physical Layer (Layer 1)
| Signals carry the bits              |
+-------------------------------------+
```

The diagram is conceptual. Ethernet frame details are covered in later lessons.

## 5. Media Access: Who Can Send?

**Media access** means the rules that determine how devices use a communication medium.

There are two useful situations.

### Point-to-Point Link

A **point-to-point link** connects two endpoints directly.

Example: a dedicated connection between two routers.

Because only two endpoints share the link, there is no need to decide which of many local devices can use a shared cable at a given time.

### Shared Medium

A **shared medium** is used by multiple devices.

Example: a traditional hub-based Ethernet segment or a wireless network.

When multiple devices share the same medium, they need rules to avoid or manage simultaneous transmissions.

Ethernet and Wi-Fi use different media-access approaches. You will study these details in the relevant Data Link and Wireless lessons.

## 6. LAN and WAN Data-Link Technologies

A **LAN** (Local Area Network) connects devices in a limited area, such as an office or home.

A **WAN** (Wide Area Network) connects locations over a wider geographic area.

Different link technologies can be used at Layer 2.

### Ethernet

**Ethernet** is the common Data Link technology used in wired LANs. It defines frame structure, MAC addressing, and media-access behavior for Ethernet networks.

You will study Ethernet frames, switches, VLANs, and related features in this module.

### PPP

**PPP** means *Point-to-Point Protocol*. It is a Data Link protocol historically used for direct connections between two network devices.

PPP provides framing and supports configuration of the connection. It can carry different Network-layer protocols.

### HDLC

**HDLC** means *High-Level Data Link Control*. It is a bit-oriented Data Link protocol used on point-to-point links.

Cisco routers support a Cisco version of HDLC encapsulation on certain serial interfaces. Cisco HDLC is not identical to the international standard in all details.

For CCNA, recognize that Ethernet is common in LANs and PPP/HDLC are Data Link technologies historically used on WAN point-to-point links. Modern WAN services may use other technologies as well.

## 7. How Layer 2 and Layer 3 Work Together

Imagine a computer sends data to a server on another IP network.

1. The Network layer creates an IP packet with source and destination IP addresses.
2. The Data Link layer places that packet inside a local Ethernet frame.
3. The Physical layer sends the frame's bits as signals.
4. The router receives the frame and removes its Layer 2 information.
5. The router examines the IP packet and selects the next hop.
6. The router builds a new Layer 2 frame for the next link.

A **next hop** is the next router or network device that should receive a packet on its journey toward the destination.

Key point: the Layer 2 frame is local to a link. The IP packet normally continues across multiple routed networks, although some features such as NAT can change IP information.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| The Data Link layer sends electrical signals. | The Physical layer sends signals; the Data Link layer organizes bits into frames. |
| A frame and a packet are the same thing. | A frame is the Layer 2 data unit; a packet is the Network-layer data unit. |
| MAC and IP addresses do the same job. | MAC addresses support local-link delivery; IP addresses support communication across IP networks. |
| Every Data Link protocol uses Ethernet MAC addressing. | Different Layer 2 technologies use different addressing and framing rules. |
| A router forwards the same Ethernet frame unchanged across every network. | A router removes the incoming Layer 2 frame and builds a new frame for the next link. |
| PPP and HDLC are routing protocols. | They are Data Link protocols used to encapsulate network-layer traffic on links. |

## 9. Knowledge Check

1. Which OSI layer is the Data Link layer?
   <details><summary>Answer</summary>Layer 2.</details>

2. What is the main purpose of framing?
   <details><summary>Answer</summary>To organize a stream of bits into separate data units called frames.</details>

3. What are the two Data Link sublayers in the IEEE 802 architecture?
   <details><summary>Answer</summary>LLC (Logical Link Control) and MAC (Media Access Control).</details>

4. What is the main role of the MAC sublayer in Ethernet?
   <details><summary>Answer</summary>It handles local-link tasks such as MAC addressing and Ethernet frame handling.</details>

5. What is a point-to-point link?
   <details><summary>Answer</summary>A direct communication link between two endpoints.</details>

6. What does PPP stand for?
   <details><summary>Answer</summary>Point-to-Point Protocol.</details>

7. What does HDLC stand for?
   <details><summary>Answer</summary>High-Level Data Link Control.</details>

8. When a router forwards an IP packet to a new link, does it normally keep the original Ethernet frame?
   <details><summary>Answer</summary>No. It removes the incoming Layer 2 frame and creates a new frame for the outgoing link.</details>

## 10. Practice

Draw a simple path:

`PC — Switch — Router — Remote Server`

For each link, identify:

- Which devices are connected.
- What the local Data Link frame is used for.
- What the Physical layer carries.

Then explain why the router needs to create a new Layer 2 frame when it forwards the packet to the next link.

## 11. CCNA Takeaways

- Layer 2 organizes bits into frames and provides local-link delivery.
- The two IEEE 802 sublayers are LLC and MAC.
- Ethernet uses MAC addressing and Ethernet frames.
- Media access defines how devices use a communication medium.
- Point-to-point links connect two endpoints; shared media are used by multiple devices.
- PPP and HDLC are Data Link protocols historically used on point-to-point links.
- Routers remove the incoming Layer 2 frame and create a new one for the next link.

## Self-Check

- [ ] I can explain the purpose of the Data Link layer.
- [ ] I can distinguish a frame from a packet.
- [ ] I can explain LLC and MAC.
- [ ] I understand framing and media access.
- [ ] I can distinguish point-to-point links from shared media.
- [ ] I can recognize Ethernet, PPP, and HDLC as Data Link technologies.
- [ ] I understand why a router creates a new Layer 2 frame for the next link.

**Next lesson:** 02-02 — MAC Addresses and NICs.
