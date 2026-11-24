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


## 01-PHYSICAL-LAYER

### 01-01 — The Purpose of the Physical Layer

| Question | Answer |
|---|---|
| What is the main responsibility of the Physical layer? | It carries bits as physical signals through copper, fiber, or air. |
| Which layer creates Ethernet frames? | Layer 2, the Data Link layer. |
| What is the difference between MAC and PHY? | MAC handles frame and link-access functions; PHY sends and receives physical signals carrying bits. |
| Does a link light prove that DNS and the Internet are working? | No. It provides evidence about the local physical link only. |

### 01-02 — Signals and Bandwidth

| Question | Answer |
|---|---|
| What is amplitude? | The size or strength of a signal. |
| What is frequency? | The number of complete cycles per second, measured in hertz. |
| What is period? | The time required for one complete cycle; T = 1/f. |
| What is the difference between signal bandwidth and data rate? | Signal bandwidth is measured in Hz; data rate is measured in bits per second. |
| What does SNR compare? | Wanted signal power with noise power. |

### 01-03 — Line Coding and Modulation

| Question | Answer |
|---|---|
| What is line coding? | Representing a sequence of bits using signal levels or transitions on a communication medium. |
| What does baud measure? | The number of symbols transmitted per second. |
| What is the purpose of Manchester encoding? | A transition in every bit period helps the receiver recover timing. |
| Which methods are used by 100BASE-TX? | 4B/5B coding and MLT-3 signaling. |
| What does PAM vary? | Signal amplitude. |
| What does QAM change? | Both amplitude and phase. |
| What is OFDM? | A method that sends data across many closely spaced subcarriers within one channel. |

### 01-04 — Bit Synchronization and Reception

| Question | Answer |
|---|---|
| Why does a receiver need bit synchronization? | It must know when to sample the incoming signal. |
| What is a decision threshold? | A boundary used to decide which symbol a measured signal value represents. |
| What does a PLL help recover? | Timing that is synchronized with the incoming signal. |
| What does the Ethernet preamble do? | It gives the receiver a known pattern to prepare and synchronize before the frame. |
| What does SFD stand for? | Start Frame Delimiter; it marks the beginning of the Ethernet frame after the preamble. |
| What does BER measure? | The ratio of incorrect bits to total bits. |

### 01-05 — Signal Impairments

| Question | Answer |
|---|---|
| What is attenuation? | Loss of signal strength as a signal travels through a medium. |
| What is the difference between dB and dBm? | dB compares two values; dBm expresses power relative to 1 mW. |
| What does SNR compare? | Wanted signal power with noise power. |
| What is crosstalk? | Unwanted signal coupling from one wire pair to another. |
| What does NEXT mean? | Near-End Crosstalk, measured at the same end as the signal source. |
| What can impedance mismatch cause? | Signal reflection. |
| What does BER measure? | Incorrect bits divided by total bits. |

### 01-06 — Copper Cabling

| Question | Answer |
|---|---|
| Why are wires twisted in Ethernet copper cable? | To reduce noise and crosstalk. |
| What does UTP mean? | Unshielded Twisted Pair. |
| Which category supports 10GBASE-T up to 100 m? | Cat6A. |
| What does 8P8C mean? | Eight positions and eight electrical contacts. |
| What cable uses T568A at one end and T568B at the other? | A traditional crossover cable. |
| What does Auto-MDIX do? | Detects and adapts to the required transmit and receive pair arrangement. |
| What is the difference between PSE and PD? | PSE supplies PoE power; PD receives it. |
| What is the maximum power at the PD under IEEE 802.3bt Type 4? | Up to 71.3 W. |

### 01-07 — Fiber Optics

| Question | Answer |
|---|---|
| What travels through optical fiber? | Light signals. |
| What is the role of the core? | It guides light through the fiber. |
| What is total internal reflection? | Light reflects back into the higher-index core instead of passing into the lower-index cladding. |
| What is the main difference between SMF and MMF? | SMF has a smaller core and is commonly used for longer links; MMF has a larger core and is common for shorter links. |
| Which wavelength is commonly used with 1000BASE-SX? | 850 nm. |
| What is modal dispersion? | Different light paths in MMF arrive at different times and spread the pulse. |
| What are LC and SC? | Common fiber-optic connector types. |
| What are SFP and SFP+? | Pluggable transceiver form factors; SFP is commonly Gigabit and SFP+ commonly 10 Gigabit. |

### 01-08 — Wireless RF Fundamentals

| Question | Answer |
|---|---|
| What does RF stand for? | Radio Frequency; electromagnetic frequencies used for wireless communication. |
| What are the three common Wi-Fi bands? | 2.4 GHz, 5 GHz, and 6 GHz. |
| What is a Wi-Fi channel? | A specific portion of radio spectrum used for wireless communication. |
| What is the difference between SSID and BSSID? | SSID is the wireless network name; BSSID identifies a particular AP radio. |
| Which is stronger: -55 dBm or -75 dBm? | -55 dBm, because it is closer to zero. |
| What does SNR compare? | Wanted signal power with noise power. |
| What is multipath? | Radio waves reaching a receiver by more than one path, often because of reflections. |
| What does MIMO stand for? | Multiple Input, Multiple Output. |

### 01-09 — Ethernet Physical Standards

| Question | Answer |
|---|---|
| What does 1000BASE-T mean? | 1 Gbps Ethernet over twisted-pair copper. |
| What is auto-negotiation? | A process in which Ethernet interfaces exchange capabilities and select a compatible mode. |
| What is half-duplex? | A mode in which a device can send or receive at a given time, but not both simultaneously. |
| What is full-duplex? | A mode that allows both ends to send and receive at the same time. |
| What is a duplex mismatch? | The two ends of a link use different duplex settings. |
| Which command displays switch-port speed and duplex? | `show interfaces status`. |

### 01-10 — Topologies, Devices, and Interface Issues

| Question | Answer |
|---|---|
| What is physical topology? | The actual arrangement of devices, cables, and physical connections. |
| What is logical topology? | The way data flows through a network. |
| What does a repeater do? | Regenerates a signal so it can travel farther. |
| How does a hub differ from a switch? | A hub repeats bits; a switch forwards frames using MAC-address information. |
| What does a media converter do? | Converts between compatible physical media, such as copper Ethernet and fiber. |
| What does an increasing CRC counter suggest? | Received frames are corrupted; investigate cabling, connectors, interference, and transceivers. |
| What is a late collision? | A collision detected after the normal collision window; it can indicate duplex mismatch or physical cabling problems. |

### 01-08 — Wireless RF Fundamentals

| Question | Answer |
|---|---|
| What does RF stand for? | Radio Frequency; electromagnetic frequencies used for wireless communication. |
| What are the three common Wi-Fi bands? | 2.4 GHz, 5 GHz, and 6 GHz. |
| What is a Wi-Fi channel? | A specific portion of radio spectrum used for wireless communication. |
| What is the difference between SSID and BSSID? | SSID is the wireless network name; BSSID identifies a particular AP radio. |
| Which is stronger: -55 dBm or -75 dBm? | -55 dBm, because it is closer to zero. |
| What does SNR compare? | Wanted signal power with noise power. |
| What is multipath? | Radio waves reaching a receiver by more than one path, often because of reflections. |
| What does MIMO stand for? | Multiple Input, Multiple Output. |

### 01-09 — Ethernet Physical Standards

| Question | Answer |
|---|---|
| What does 1000BASE-T mean? | 1 Gbps Ethernet over twisted-pair copper. |
| What is auto-negotiation? | A process in which Ethernet interfaces exchange capabilities and select a compatible mode. |
| What is half-duplex? | A mode in which a device can send or receive at a given time, but not both simultaneously. |
| What is full-duplex? | A mode that allows both ends to send and receive at the same time. |
| What is a duplex mismatch? | The two ends of a link use different duplex settings. |
| Which command displays switch-port speed and duplex? | `show interfaces status`. |

### 01-10 — Topologies, Devices, and Interface Issues

| Question | Answer |
|---|---|
| What is physical topology? | The actual arrangement of devices, cables, and physical connections. |
| What is logical topology? | The way data flows through a network. |
| What does a repeater do? | Regenerates a signal so it can travel farther. |
| How does a hub differ from a switch? | A hub repeats bits; a switch forwards frames using MAC-address information. |
| What does a media converter do? | Converts between compatible physical media, such as copper Ethernet and fiber. |
| What does an increasing CRC counter suggest? | Received frames are corrupted; investigate cabling, connectors, interference, and transceivers. |
| What is a late collision? | A collision detected after the normal collision window; it can indicate duplex mismatch or physical cabling problems. |

### 02-01 — The Purpose of the Data Link Layer

| Question | Answer |
|---|---|
| Which OSI layer is the Data Link layer? | Layer 2. |
| What is framing? | Organizing a stream of bits into identifiable frames. |
| What are the two IEEE 802 Data Link sublayers? | LLC (Logical Link Control) and MAC (Media Access Control). |
| What is media access? | Rules that determine how devices use a communication medium. |
| What is a point-to-point link? | A direct link between two endpoints. |
| What do PPP and HDLC have in common? | Both are Data Link protocols used on point-to-point links. |
| What happens to the Ethernet frame when a router forwards a packet to a new link? | The incoming Layer 2 frame is removed and a new frame is built for the outgoing link. |

### 02-02 — MAC Addresses and NICs

| Question | Answer |
|---|---|
| How long is a common Ethernet MAC address? | 48 bits, or six bytes. |
| What does OUI stand for? | Organizationally Unique Identifier. |
| What does I/G = 0 mean? | Individual (unicast) address. |
| What does U/L = 1 mean? | Locally administered address. |
| What is the Ethernet broadcast MAC address? | FF:FF:FF:FF:FF:FF. |
| What is promiscuous mode? | A NIC mode that passes received frames to the OS even when the destination MAC is not the NIC's own address. |
| Does promiscuous mode guarantee visibility of all switch unicast traffic? | No. The switch must deliver or mirror the traffic to the monitoring port. |
| What is hardware offloading? | The NIC performs selected processing tasks instead of the CPU performing them all. |

### 02-03 — Ethernet Frame Structure

| Question | Answer |
|---|---|
| What is the purpose of the preamble? | It helps the receiving interface synchronize with the incoming signal. |
| What does SFD stand for? | Start Frame Delimiter; it marks the start of the Ethernet frame. |
| What is the EtherType for IPv4? | 0x0800. |
| What is the EtherType for IPv6? | 0x86DD. |
| What is the EtherType for ARP? | 0x0806. |
| What is the minimum standard Ethernet frame size? | 64 bytes, from destination MAC through FCS. |
| What is the maximum standard untagged Ethernet frame size? | 1518 bytes. |
| What is the maximum standard frame size with one 802.1Q VLAN tag? | 1522 bytes. |
| What does FCS do? | Carries a CRC value used to detect frame corruption. |
| What is the standard Ethernet MTU? | Commonly 1500 bytes. |
| Is IFG part of the frame? | No. It is the minimum idle time between transmissions. |
