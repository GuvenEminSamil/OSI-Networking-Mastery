# 00-09 — Layered Models: OSI and TCP/IP

> **Prerequisite:** 00-08 — Networking Fundamentals  
> **CCNA 200-301 v1.1 connection:** Understanding how network protocols work together and how to troubleshoot by layer.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain why networks use layers.
- Identify the seven layers of the OSI model.
- Understand the four layers of the TCP/IP model.
- Recognize common protocols and devices at different layers.
- Explain encapsulation and decapsulation.
- Use the layered approach to organize troubleshooting.

## 1. Why Do We Use Layers?

Imagine sending a package to another city.

You pack the item, write the address, hand it to a delivery company, and the company transports it through several facilities. Each participant has a particular responsibility.

Network communication works in a similar way. It is divided into layers so that each part has a clear job.

A **layered model** is a way to organize a complex system into smaller parts. Each layer uses services from the layer below and provides services to the layer above.

This makes networks easier to design, understand, and troubleshoot.

## 2. The OSI Model

The **OSI model** (Open Systems Interconnection model) is a seven-layer reference model. It helps us describe the different tasks involved in network communication.

Learn the layers from bottom to top:

| Layer | Name | Main responsibility | Example |
|---:|---|---|---|
| 7 | Application | Network services used by applications | HTTP, DNS |
| 6 | Presentation | Data format, encoding, and encryption concepts | Data representation, encryption |
| 5 | Session | Establishes and manages communication sessions | Session control |
| 4 | Transport | End-to-end communication between applications | TCP, UDP |
| 3 | Network | Logical addressing and routing between networks | IP, routers |
| 2 | Data Link | Delivery across a local link using frames and MAC addresses | Ethernet, switches |
| 1 | Physical | Sends raw bits as electrical, optical, or radio signals | Cables, connectors, radio |

A **frame** is the data unit used at the Data Link layer. A **packet** is the data unit commonly used at the Network layer. A **segment** is the data unit commonly used for TCP at the Transport layer; UDP data is often called a datagram.

You may see different PDU terms in books. **PDU** means Protocol Data Unit: the name given to the data handled at a particular layer.

Memory aid, from Layer 7 down to Layer 1:

**Application – Presentation – Session – Transport – Network – Data Link – Physical**

## 3. The TCP/IP Model

The **TCP/IP model** describes the protocol architecture used by the Internet. A common version has four layers:

| TCP/IP layer | Main role | Rough OSI mapping |
|---|---|---|
| Application | Services used by applications | OSI 5–7 |
| Transport | End-to-end delivery between applications | OSI 4 |
| Internet | IP addressing and routing | OSI 3 |
| Link | Communication over the local medium | OSI 1–2 |

The two models are not identical. The OSI model is a seven-layer reference model; the TCP/IP model groups some of those responsibilities together.

## 4. Encapsulation and Decapsulation

**Encapsulation** is the process of adding control information as data moves down the layers before transmission.

**Decapsulation** is the process of reading and removing that information as data moves up the layers at the receiving side.

Imagine that your browser sends a web request:

1. The application creates the data.
2. The transport layer adds information such as TCP source and destination ports.
3. The Internet layer adds source and destination IP addresses.
4. The link layer adds local delivery information, such as source and destination MAC addresses.
5. The physical layer sends the bits through the medium.

At the destination, the process happens in reverse. Each layer reads the information it needs and passes the remaining data upward.

A **header** is control information added before a data payload. A **payload** is the data being carried.

Simplified view:

```
Application data
       ↓
[TCP header | Data]                         Segment
       ↓
[IP header | TCP header | Data]             Packet
       ↓
[Ethernet header | IP packet | Trailer]     Frame
       ↓
Bits sent over the medium
```

The exact structure varies by protocol. The diagram shows the basic idea.

## 5. How Does a Device Know What Comes Next?

A receiver examines fields in protocol headers to decide how to process the payload.

For example:

- The Ethernet **EtherType** field identifies the type of payload, such as IPv4 (`0x0800`) or IPv6 (`0x86DD`).
- The IPv4 **Protocol** field identifies the next protocol, such as TCP (6) or UDP (17).
- TCP and UDP port numbers help deliver data to the correct application or service.

A **port number** is a 16-bit number used by TCP or UDP to identify a communication endpoint on a host.

You do not need to memorize every header field yet. Understand that each layer uses its own information to decide where the data should go.

## 6. Do All Protocols Fit Perfectly into One Layer?

No. The models are useful guides, but real protocols do not always fit neatly into one box.

Examples:

- **ARP** helps discover the MAC address associated with an IPv4 address on a local network. It is carried directly in an Ethernet frame.
- **ICMP** supports network-layer messages such as error reporting and diagnostics. It is carried inside IP.
- **DHCP** provides network configuration to clients and uses UDP.
- **TLS** provides encryption and security for application communication, typically above TCP or another transport.

For troubleshooting, focus on what a protocol does and what carries it rather than arguing about a perfect layer label.

## 7. Troubleshooting by Layer

The layered model gives you a structured way to investigate problems.

| Layer | Example question | Possible check |
|---|---|---|
| Physical | Is the cable connected? | Check cable, link lights, interface status |
| Data Link | Is the correct VLAN or MAC learning working? | Check switch ports and MAC table |
| Network | Is the IP address and route correct? | Check IP configuration and routing table |
| Transport | Is the service reachable on the required port? | Check TCP/UDP connectivity and firewall rules |
| Application | Is DNS or the application service working? | Test name resolution and the service itself |

A good troubleshooter starts with evidence. Do not assume that every connection problem is an IP problem.

## 8. Useful Cisco Commands

These commands help inspect different parts of a network device:

```
Switch# show interfaces status
Switch# show mac address-table
Switch# show vlan brief
Router# show ip interface brief
Router# show ip route
```

- `show interfaces status` displays interface status on supported switches.
- `show mac address-table` displays learned MAC addresses.
- `show vlan brief` displays VLAN information.
- `show ip interface brief` summarizes IP interface addresses and status.
- `show ip route` displays the router's routing table.

A **VLAN** (Virtual Local Area Network) logically separates devices into different Layer 2 networks. You will study VLANs later in the course.

## 9. Common Mistakes

| Mistake | Correct idea |
|---|---|
| The OSI model is a physical device or protocol. | It is a reference model used to describe communication tasks. |
| Each protocol maps perfectly to one OSI layer. | The model is a guide; real protocol responsibilities can cross layer boundaries. |
| Encapsulation removes headers. | Encapsulation adds control information; decapsulation reads and removes it at the receiver. |
| MAC addresses and IP addresses do the same job. | MAC addresses are used for local-link delivery; IP addresses support delivery across networks. |
| A physical link being up proves the whole application works. | Higher layers can still have addressing, routing, transport, or application problems. |

## 10. Knowledge Check

1. How many layers are in the OSI model?
   <details><summary>Answer</summary>Seven.</details>

2. Which OSI layer is responsible for routing between IP networks?
   <details><summary>Answer</summary>Layer 3 — Network.</details>

3. Which OSI layer commonly uses MAC addresses and Ethernet frames?
   <details><summary>Answer</summary>Layer 2 — Data Link.</details>

4. Which TCP/IP layer roughly combines OSI Layers 5, 6, and 7?
   <details><summary>Answer</summary>The Application layer.</details>

5. What is encapsulation?
   <details><summary>Answer</summary>Adding control information, such as headers, as data moves down the layers before transmission.</details>

6. Which field in an Ethernet frame identifies whether its payload is IPv4 or IPv6?
   <details><summary>Answer</summary>The EtherType field.</details>

7. Which command displays a Cisco router's routing table?
   <details><summary>Answer</summary>`show ip route`.</details>

## 11. Practice

Draw the seven OSI layers from memory. Next to each layer, write:

- Its main responsibility.
- One example protocol, device, or technology.
- The PDU name where applicable.

Then consider this problem:

*A laptop is connected to a switch, but it cannot open a web page.*

Write one possible check for the Physical, Data Link, Network, Transport, and Application layers.

## 12. CCNA Takeaways

- Know the seven OSI layers and their main responsibilities.
- Understand the four TCP/IP layers and how they map approximately to OSI.
- Know the basic names of segment, packet, frame, and bits.
- Understand encapsulation and decapsulation.
- Use the layered model to troubleshoot systematically.

## Self-Check

- [ ] I can list the seven OSI layers in order.
- [ ] I can match the four TCP/IP layers to the OSI model.
- [ ] I can explain encapsulation and decapsulation.
- [ ] I can describe the roles of Ethernet, IP, TCP, and UDP headers.
- [ ] I can suggest a troubleshooting check at several network layers.

**You have reached the end of the Foundations module.** The next module will build on these concepts and apply them to Ethernet and network communication.
