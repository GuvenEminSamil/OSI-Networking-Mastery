# FND-OSI — Layered Models (OSI and TCP/IP)

> **Coverage:** 00-09 | **Questions:** 10 | **Suggested time:** 30 minutes  
> Answers: `answers/A-FND-OSI.md`. See `10-QUESTION-BANK/README.md` for scoring rules. No calculator.

---

### FND-OSI-001
**Category:** MC · **Difficulty:** 1 · **Lesson:** 00-09

Which layer–PDU pairing is correct?

- A) Data Link layer — packet
- B) Network layer — frame
- C) Transport layer (UDP) — datagram
- D) Physical layer — segment

### FND-OSI-002
**Category:** MC · **Difficulty:** 2 · **Lesson:** 00-09

Which **two** protocols operate at the application layer (Layer 7)? (Select two.)

- A) DNS
- B) ICMP
- C) ARP
- D) DHCP
- E) OSPF

### FND-OSI-003
**Category:** B · **Difficulty:** 1 · **Lesson:** 00-09

In the OSI model, which layer is responsible for data encryption and compression? Where are these functions usually implemented in the TCP/IP world today? Give one example of each.

### FND-OSI-004
**Category:** O · **Difficulty:** 2 · **Lessons:** 00-09, 00-06

A computer receives two Ethernet frames.

a) The first frame has EtherType `0x0806`. Which protocol is in the payload? Is there an IP header in that payload?  
b) The second frame has EtherType `0x0800`, IPv4 Protocol field `17`, and destination port `53`. Through which layers and protocols does the payload pass on its way to the receiving application?

### FND-OSI-005
**Category:** I · **Difficulty:** 3 · **Lessons:** 00-09, 00-08

A Layer 2 switch and an NGFW inspect the same frame.

a) What is the highest OSI layer each device normally examines when making its forwarding or security decision?  
b) Explain one security consequence of this difference with an example.

### FND-OSI-006
**Category:** S · **Difficulty:** 2 · **Lesson:** 00-09

Consider this output:

```text
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     192.168.20.1    YES manual down                  down
GigabitEthernet0/2     192.168.30.1    YES manual administratively down down
```

a) Which layer does the status of G0/1 and G0/2 point to?  
b) What would you check or do first for each interface?

### FND-OSI-007
**Category:** O · **Difficulty:** 2 · **Lesson:** 00-09

An application sends 1,472 bytes of data in each UDP datagram (IPv4 without options, Ethernet).

a) What is the Ethernet frame size, and how many byte-times does it occupy on the link when preamble, SFD, and IFG are included?  
b) What is the approximate payload efficiency?  
c) What is the approximate maximum application data rate on a 100 Mbps link?

### FND-OSI-008
**Category:** K · **Difficulty:** 2 · **Lesson:** 00-09

Explain encapsulation and decapsulation in your own words. Include: what each layer adds, what is special about the Data Link layer, what the receiver checks before passing a payload upward, and what a router does during forwarding. Write 5–8 sentences.

### FND-OSI-009
**Category:** KK · **Difficulty:** 2 · **Lesson:** 00-09

Compare the OSI and TCP/IP models. Give two differences and explain why the industry still uses OSI layer numbers even though real-world protocols belong to the TCP/IP suite.

### FND-OSI-010
**Category:** A · **Difficulty:** 2 · **Lesson:** 00-09

A user reports that a website will not open. You check the following:

1. The link light is on.
2. `ipconfig` shows a valid IP address, mask, and default gateway.
3. `ping 192.168.1.1` (the gateway) succeeds.
4. `ping 8.8.8.8` succeeds.
5. `ping www.example.com` returns: “Ping request could not find host www.example.com.”

a) Which layer and service are most likely responsible?  
b) What two checks would you perform next?
