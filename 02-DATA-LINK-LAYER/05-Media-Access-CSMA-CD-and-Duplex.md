# 02-05 — Media Access, CSMA/CD, and Duplex

> **Prerequisites:** 02-01 — The Purpose of the Data Link Layer; 01-09 — Ethernet Physical Standards  
> **CCNA 200-301 v1.1 connection:** Ethernet media access, collision handling, shared media, and duplex operation.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain why devices need media-access rules.
- Understand shared media and collision domains.
- Describe CSMA/CD step by step.
- Understand the purpose of the jam signal and backoff.
- Distinguish half-duplex and full-duplex Ethernet.
- Recognize why modern switched Ethernet does not use CSMA/CD.
- Briefly compare CSMA/CD with Wi-Fi's CSMA/CA.

## 1. Why Do Devices Need Media-Access Rules?

When multiple devices share one communication medium, they need rules that help them transmit without interfering with one another.

A **shared medium** is a communication channel used by more than one device.

Imagine several people trying to speak through one microphone. If everyone speaks at the same time, the message becomes difficult to understand.

Early Ethernet networks used shared coaxial cable or hubs. Multiple devices could try to transmit at the same time, causing a **collision**.

A collision occurs when simultaneous transmissions interfere with each other on a shared half-duplex Ethernet medium.

## 2. What Is CSMA/CD?

**CSMA/CD** stands for *Carrier Sense Multiple Access with Collision Detection*.

It was used by traditional shared, half-duplex Ethernet to control access to the medium.

Each part of the name describes one idea:

- **Carrier Sense:** Listen to the medium before sending.
- **Multiple Access:** Multiple devices share the same medium.
- **Collision Detection:** A transmitting device monitors the medium to detect a collision.

## 3. How CSMA/CD Works

A simplified CSMA/CD process:

1. **Listen:** A device checks whether the medium is idle.
2. **Transmit:** If the medium is idle, the device begins sending.
3. **Monitor:** While sending, it continues monitoring the medium.
4. **Detect:** If it detects a collision, it stops sending.
5. **Jam:** It sends a jam signal so other devices sharing the medium know a collision occurred.
6. **Back off:** It waits for a random period before trying again.

A **jam signal** is a special signal sent after a collision to ensure the collision is recognized by other devices on the shared segment.

## 4. Backoff and Binary Exponential Backoff

After a collision, devices should not all retry immediately. They wait for a random amount of time.

This is called **backoff**.

Ethernet uses a method called **binary exponential backoff**:

- After each collision, the range of possible waiting times increases.
- The device chooses a random waiting time from that range.
- It tries again after the waiting period, when the medium is available.

This reduces the chance that the same devices collide repeatedly.

You do not need to calculate the exact backoff algorithm for this lesson. Remember why it exists: devices wait different random amounts of time before retrying.

## 5. Collision Domain

A **collision domain** is a network segment where simultaneous transmissions can collide when using half-duplex shared Ethernet.

Examples:

- A traditional hub creates one shared collision domain for all connected devices.
- A repeater extends the same collision domain.
- A switch separates collision domains by port.

On a modern switch, each full-duplex Ethernet link is a separate point-to-point link. Collisions do not occur on a normal full-duplex link.

## 6. Half-Duplex vs. Full-Duplex

**Duplex** describes whether a connection can send and receive at the same time.

### Half-Duplex

A half-duplex device can send or receive at a given time, but not both simultaneously.

Traditional shared Ethernet used half-duplex operation and needed CSMA/CD.

### Full-Duplex

A full-duplex device can send and receive at the same time.

Modern switched Ethernet links normally operate in full-duplex mode.

Since the sender and receiver use separate transmit and receive paths, they do not compete for the same shared medium. There are no collisions on a normal full-duplex point-to-point Ethernet link.

Therefore, **CSMA/CD is not used on a normal full-duplex switched Ethernet link**.

## 7. Why Wi-Fi Uses CSMA/CA Instead

Wireless networks face a different challenge.

A Wi-Fi device generally cannot reliably detect a collision while it is transmitting. Its own transmitted radio signal is much stronger at its antenna than a signal arriving from another device.

Wi-Fi uses **CSMA/CA** — *Carrier Sense Multiple Access with Collision Avoidance*.

Instead of detecting a collision while transmitting, it tries to reduce the chance of collisions by listening, waiting, and using acknowledgments.

You will study wireless media access in more detail in the Wireless LAN module.

For now, remember:

- Traditional shared Ethernet half-duplex: CSMA/CD.
- Wi-Fi: CSMA/CA.

## 8. Modern Ethernet and Switches

Modern Ethernet LANs normally use switches and full-duplex point-to-point links.

A switch creates a separate link between itself and each connected device.

This means:

- Devices do not share one collision domain across all switch ports.
- Each full-duplex link can send and receive simultaneously.
- CSMA/CD is not needed on normal full-duplex switched links.

If a modern switch port reports collisions or late collisions, check whether an old device, hub, forced duplex setting, or duplex mismatch is involved.

## 9. Useful Cisco Commands

To check interface state, speed, duplex, and counters:

```
Switch# show interfaces status
Switch# show interfaces gigabitEthernet 1/0/1
```

Look for:

- Speed.
- Duplex.
- Input errors.
- CRC errors.
- Collisions and late collisions, where reported.

If supported by the switch model, the interface configuration may include:

```
Switch(config)# interface gigabitEthernet 1/0/1
Switch(config-if)# duplex auto
Switch(config-if)# speed auto
```

Do not force a speed or duplex mode without checking the capabilities and settings of the device at the other end.

## 10. Common Mistakes

| Mistake | Correct idea |
|---|---|
| CSMA/CD is used by every Ethernet link. | It was used on shared half-duplex Ethernet; modern full-duplex switched links do not use it. |
| A collision means the cable is broken. | A collision can be normal on a shared half-duplex medium. |
| Full-duplex devices must wait for the other side to stop transmitting. | They can send and receive simultaneously. |
| A switch creates one collision domain for all ports. | Each switch port separates collision domains; full-duplex point-to-point links normally have no collisions. |
| CSMA/CA detects collisions while transmitting. | It attempts to avoid collisions because a wireless device cannot reliably detect them while sending. |
| A duplex mismatch always causes the link to go down. | The link may stay up while performance becomes poor and errors appear. |

## 11. Knowledge Check

1. What does CSMA/CD stand for?
   <details><summary>Answer</summary>Carrier Sense Multiple Access with Collision Detection.</details>

2. What does Carrier Sense mean?
   <details><summary>Answer</summary>A device listens to the medium before transmitting.</details>

3. What is a collision?
   <details><summary>Answer</summary>Two or more devices transmit at the same time on a shared half-duplex medium and their signals interfere.</details>

4. What is the purpose of a jam signal?
   <details><summary>Answer</summary>It makes sure other devices on the shared segment recognize that a collision occurred.</details>

5. Why do devices use backoff after a collision?
   <details><summary>Answer</summary>They wait for different random periods so they are less likely to collide again immediately.</details>

6. Can a half-duplex device send and receive at the same time?
   <details><summary>Answer</summary>No. It can send or receive at a given time, but not both simultaneously.</details>

7. Why is CSMA/CD not used on normal full-duplex switched Ethernet?
   <details><summary>Answer</summary>Each point-to-point link can transmit in both directions simultaneously and does not share a collision medium.</details>

8. What does CSMA/CA stand for?
   <details><summary>Answer</summary>Carrier Sense Multiple Access with Collision Avoidance.</details>

## 12. Practice

Consider these three network layouts:

1. Three computers connected to one hub.
2. Three computers connected to separate ports on a full-duplex switch.
3. Two switches connected by a full-duplex point-to-point link.

For each layout, answer:

- Do the devices share one collision domain?
- Can collisions occur during normal operation?
- Is CSMA/CD required?

Suggested answers:

- Hub: one shared collision domain; collisions can occur; CSMA/CD is used for half-duplex shared Ethernet.
- Switch: each port is a separate collision domain; normal full-duplex links do not have collisions; CSMA/CD is not required.
- Switch-to-switch full-duplex link: point-to-point full duplex; no normal collisions; CSMA/CD is not required.

## 13. CCNA Takeaways

- CSMA/CD was used by shared half-duplex Ethernet.
- It listens before transmitting, detects collisions, sends a jam signal, and uses backoff.
- A collision domain is a shared half-duplex segment where collisions can occur.
- Half-duplex cannot send and receive simultaneously.
- Full-duplex can send and receive simultaneously.
- Normal full-duplex switched Ethernet does not use CSMA/CD.
- Wi-Fi uses CSMA/CA to reduce the chance of collisions.

## Self-Check

- [ ] I can explain why shared media need access rules.
- [ ] I can expand and describe CSMA/CD.
- [ ] I can explain jam signals and backoff.
- [ ] I understand collision domains.
- [ ] I can compare half-duplex and full-duplex.
- [ ] I know why modern switched Ethernet does not use CSMA/CD.
- [ ] I can distinguish CSMA/CD from CSMA/CA.

**Next lesson:** 02-06 — Ethernet Switching and MAC Address Learning.

## References

- [Cisco Press — Ethernet Frames and Shared Ethernet](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4)
- [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html)
