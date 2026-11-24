# 12-02 — Flashcards by Module

> These are optional review prompts, not a mandatory daily routine. Try to answer in your own words before revealing or checking the answer. Import-ready Anki decks are stored in `12-REVISION/anki/`.

## 00-FOUNDATIONS

### 00-01 — Information and Data

| Question | Answer |
|---|---|
| What is the difference between data and information? | Data is a representation, such as bits or symbols. Information is the meaning we understand when we interpret that representation. |
| What is a bit? | A binary digit that can have a value of 0 or 1. |
| Why do digital systems use two-state signals? | Two clearly separated states are easier to distinguish reliably in the presence of noise. |
| What is noise margin? | The safety difference between a valid signal level and the receiver's decision threshold. |
| What does signal regeneration mean? | A receiver decides which symbol was sent and creates a clean new signal for the next link. |

### 00-02 — Number Systems and Units

| Question | Answer |
|---|---|
| What digits does binary use? | 0 and 1. |
| What is the base of hexadecimal? | 16. It uses 0–9 and A–F. |
| How many bits does one hexadecimal digit represent? | Four bits, also called a nibble. |
| How many bits are in a byte or octet? | Eight bits. |
| What is the maximum decimal value of an 8-bit octet? | 255. |
| What is the theoretical equivalent of 1 Gbps in MB/s? | 125 MB/s, before communication overhead. |
| What is the difference between Mbps and MB/s? | Mbps measures megabits per second; MB/s measures megabytes per second. Eight bits make one byte. |

### 00-03 — Binary Arithmetic and Boolean Logic

| Question | Answer |
|---|---|
| When does AND return 1? | Only when both input bits are 1. |
| When does OR return 1? | When at least one input bit is 1. |
| When does XOR return 1? | When the input bits are different. |
| What is overflow? | A result that needs more bits than the fixed-size field can store. |
| How is an IPv4 network address calculated? | Perform a bitwise AND between the IP address and the subnet mask. |
| What is a wildcard mask? | A mask used by Cisco features such as ACLs and OSPF; 0 means check the bit and 1 means ignore it. |
| What is CRC used for? | Detecting errors in transmitted data. |

### 00-04 — Electricity Fundamentals

| Question | Answer |
|---|---|
| What is voltage? | Electrical potential difference between two points, measured in volts. |
| What is current? | The rate at which electric charge flows, measured in amperes. |
| What is resistance? | How strongly a material opposes current flow, measured in ohms. |
| What is Ohm's law? | V = I × R. |
| How is electrical power calculated? | P = V × I. |
| Why does higher current increase cable loss? | Resistive loss is proportional to I² × R. |
| What is differential signaling? | Sending information using the voltage difference between two wires. |
| What does PoE provide? | Electrical power and network data over a compatible Ethernet cable. |

### 00-05 — Transistors and Digital Logic

| Question | Answer |
|---|---|
| What does a transistor do in a digital circuit? | It can act as an electronic switch and help build logic circuits. |
| What is a logic gate? | A circuit that performs a Boolean operation on input bits. |
| What does volatile memory mean? | Its contents are lost when power is removed. |
| What is RAM used for in a Cisco device? | Working memory, including the active running configuration. |
| What is flash commonly used for? | Storing the IOS image and other files. |
| What is the difference between running-config and startup-config? | Running-config is active in RAM; startup-config is saved and loaded during startup. |
| Which command saves the running configuration? | `copy running-config startup-config`. |

### 00-06 — Data Representation

| Question | Answer |
|---|---|
| Why do bytes need an agreed interpretation? | The same bytes can represent different data; a protocol or file format defines their meaning. |
| How many values can an 8-bit unsigned field represent? | 256 values, from 0 to 255. |
| What does big-endian mean? | The most significant byte comes first. |
| What is network byte order? | Big-endian order used for multi-byte numeric fields in Internet protocols. |
| What is a character encoding? | A rule that maps characters to numbers and bytes, such as ASCII or UTF-8. |
| Why can a file signature be more useful than a file extension? | A signature is a recognizable byte pattern inside the file; an extension is only part of its name. |

### 00-07 — Computer Architecture for Networking

| Question | Answer |
|---|---|
| What is a NIC? | A Network Interface Card or Controller; it connects a computer to a network. |
| What is a network driver? | Software that lets the operating system communicate with a network adapter. |
| What is DMA? | Direct Memory Access; hardware transfers data to or from RAM without the CPU copying every byte. |
| What is a buffer? | A temporary memory area that holds data while it waits to be processed. |
| What can happen when a receive buffer is full? | Incoming frames may be dropped because no free buffer is available. |
| Which Cisco command shows interface counters? | `show interfaces`. |
| Why can a local packet capture show a false outgoing checksum warning? | The NIC may calculate the final checksum after the packet-capture point. |

### 00-08 — Networking Fundamentals

| Question | Answer |
|---|---|
| What is a LAN? | A Local Area Network covering a limited area such as a home or office. |
| What is the main role of a Layer 2 switch? | Forward Ethernet frames within a local network using MAC addresses. |
| What is the main role of a router? | Forward IP packets between different IP networks. |
| What is a WLAN? | A Wireless Local Area Network, usually using Wi-Fi. |
| What is the difference between bandwidth and throughput? | Bandwidth is capacity; throughput is the actual successful data rate. |
| What is jitter? | Variation in packet delay. |
| What is a default gateway? | The router or Layer 3 device a host uses to reach destinations outside its local network. |

### 00-09 — Layered Models: OSI and TCP/IP

| Question | Answer |
|---|---|
| How many layers are in the OSI model? | Seven: Physical, Data Link, Network, Transport, Session, Presentation, Application. |
| How many layers are in the TCP/IP model used here? | Four: Link, Internet, Transport, Application. |
| What does PDU mean? | Protocol Data Unit: the name for data handled at a particular layer. |
| What are the common PDU names from Layer 4 down to Layer 1? | TCP segment (UDP datagram), packet, frame, bits. |
| What is encapsulation? | Adding protocol information, such as headers, as data moves down the layers. |
| Which field identifies IPv4 or IPv6 in an Ethernet frame? | EtherType: 0x0800 for IPv4 and 0x86DD for IPv6. |
| Which command displays a Cisco routing table? | `show ip route`. |
