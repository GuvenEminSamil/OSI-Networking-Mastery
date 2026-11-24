# 01-08 — Wireless RF Fundamentals

> **Prerequisites:** 01-02 — Signals and Bandwidth; 01-05 — Signal Impairments  
> **CCNA 200-301 v1.1 connection:** Exam objective 1.11 — Describe wireless principles, including non-overlapping channels, SSID, and RF.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain how wireless devices communicate using radio frequency (RF).
- Recognize the 2.4 GHz, 5 GHz, and 6 GHz Wi-Fi bands.
- Understand channels, channel width, and non-overlapping channels.
- Explain SSID and BSSID.
- Understand signal strength (RSSI), dBm, and SNR.
- Recognize interference, attenuation, and multipath.
- Understand the basic idea of MIMO and spatial streams.

## 1. What Is Radio Frequency (RF)?

**Radio frequency (RF)** is a range of electromagnetic frequencies used to transmit information wirelessly.

A Wi-Fi device converts data into a radio signal, sends it through an antenna, and another device receives the signal with its antenna.

An **antenna** is a component that sends or receives radio waves.

Wireless communication does not need a physical cable between the sender and receiver, but the radio signal still travels through a physical environment. Walls, people, furniture, and other radio transmitters can affect it.

## 2. Wi-Fi Frequency Bands

Wi-Fi commonly operates in three frequency bands:

- 2.4 GHz
- 5 GHz
- 6 GHz

A **frequency band** is a range of radio frequencies allocated for a particular use.

| Band | General characteristics |
|---|---|
| 2.4 GHz | Longer reach in many environments, but fewer usable channels and more sources of interference |
| 5 GHz | More channel options and often higher capacity; range through obstacles is generally shorter than 2.4 GHz |
| 6 GHz | Additional spectrum for compatible Wi-Fi 6E and newer devices; clients and access points must support it |

The higher-frequency bands do not automatically provide better coverage. Range also depends on transmit power, antenna design, obstacles, receiver sensitivity, and local regulations.

The 6 GHz band is not available to every Wi-Fi device. A client and access point must support a compatible 6 GHz Wi-Fi mode, and the allowed channels depend on the regulatory region.

## 3. Channels and Channel Width

A **channel** is a specific portion of radio spectrum used for communication.

An access point (AP) selects a channel for its radio. Nearby APs using the same or overlapping channels may compete for airtime or interfere with one another.

**Channel width** is the amount of frequency spectrum used by a channel. Common Wi-Fi channel widths include 20 MHz, 40 MHz, 80 MHz, and 160 MHz, depending on the band and Wi-Fi generation.

A wider channel can carry more data under suitable conditions, but it also uses more spectrum. In a busy environment, narrower channels may allow more APs to operate with less overlap.

### Non-Overlapping Channels

**Non-overlapping channels** are channels whose frequency ranges do not overlap.

In the 2.4 GHz band, many channel numbers overlap because the channels are close together. A common 20 MHz channel plan uses channels 1, 6, and 11 to reduce overlap in many regulatory domains.

Channel availability and exact channel plans vary by country. For this reason, a real wireless deployment must follow the regulatory domain and the access point's supported channels.

In the 5 GHz and 6 GHz bands, there are generally more channel choices, but the number of available channels depends on regional rules and the channel width.

## 4. SSID and BSSID

An **SSID** (Service Set Identifier) is the name displayed for a Wi-Fi network.

For example, a home network might use the SSID:

`Home-WiFi`

A **BSSID** (Basic Service Set Identifier) identifies a particular wireless access point radio. It is commonly represented by a MAC address.

A single SSID can be provided by several access points. Each radio can have its own BSSID while offering the same network name.

| Term | What it identifies |
|---|---|
| SSID | The wireless network name |
| BSSID | A particular wireless access point radio |

A network name is not the same as a unique radio identifier.

## 5. Signal Strength: RSSI and dBm

**RSSI** means *Received Signal Strength Indicator*. It describes how strong the received wireless signal appears to the receiving device.

Wireless signal power is commonly expressed in **dBm**, which measures power relative to 1 milliwatt.

Wi-Fi signal readings are often negative values:

- -40 dBm: very strong signal.
- -60 dBm: generally strong signal.
- -75 dBm: weaker signal.
- -85 dBm: very weak signal in many environments.

These are rough examples, not guaranteed quality boundaries. The usable signal level depends on the device, data rate, noise, interference, and application needs.

Remember: a value closer to zero is a stronger received power. For example, -50 dBm is stronger than -70 dBm.

## 6. Signal-to-Noise Ratio (SNR)

**SNR** (Signal-to-Noise Ratio) compares the strength of the wanted signal with the strength of unwanted noise.

A higher SNR generally makes it easier for the receiver to decode data correctly.

A strong signal does not always mean a good connection. If the noise level is also high, the SNR may still be poor.

Example:

- Wanted signal: -60 dBm.
- Noise level: -90 dBm.
- SNR: approximately 30 dB.

The difference is 30 dB because both readings are expressed in dBm.

If the signal is -60 dBm but the noise is -65 dBm, the SNR is only about 5 dB. The signal is still present, but it is much harder to distinguish from noise.

## 7. Interference and Attenuation

**Interference** is unwanted radio energy that makes it harder for a receiver to interpret the intended signal.

Common sources include:

- Nearby Wi-Fi networks.
- Bluetooth devices and other equipment using the 2.4 GHz band.
- Poorly placed or poorly configured access points.
- Physical obstacles and reflective surfaces.

**Attenuation** means signal strength decreases as the signal travels.

Walls, floors, metal objects, and even people can weaken a Wi-Fi signal. Materials containing metal or water often cause significant signal loss.

Moving an access point closer to users or placing it in a more open location can improve the received signal.

## 8. Multipath

**Multipath** occurs when radio waves reach a receiver by more than one path.

A radio signal may travel directly to the receiver and also reflect from walls, ceilings, furniture, or other objects.

The reflected copies can arrive at slightly different times. Depending on their timing and phase, they can strengthen or weaken the received signal.

Multipath can cause fading and unreliable communication. Modern Wi-Fi technologies use multiple antennas and signal-processing methods to handle multipath more effectively.

## 9. MIMO and Spatial Streams

**MIMO** means *Multiple Input, Multiple Output*. It uses multiple transmitting and receiving antennas to improve wireless communication.

A **spatial stream** is an independent data stream sent using a MIMO system.

Multiple spatial streams can increase the amount of data transferred during the same period, provided that both the access point and client support them and radio conditions are good enough.

MIMO can also improve reliability by using multiple antennas to receive information through different signal paths.

The number of antennas does not always equal the number of usable spatial streams. The capabilities of both devices and the radio environment matter.

## 10. Real-World Example: Slow Wi-Fi in One Room

Imagine that Wi-Fi works well in the living room but becomes slow in a bedroom.

Possible causes include:

- The signal is weakened by walls or floors.
- A nearby network uses an overlapping channel.
- The client has a low SNR.
- The access point is placed too far away.
- The client is connected to a crowded band or channel.

A useful first investigation is to compare signal strength and SNR in both rooms, then inspect which channel and band the client is using.

Do not assume that purchasing a faster Internet plan will fix a weak or congested wireless link.

## 11. Common Mistakes

| Mistake | Correct idea |
|---|---|
| A higher frequency always gives longer range. | Higher Wi-Fi bands often have shorter range through obstacles, although power, antennas, and environment also matter. |
| Every channel number is non-overlapping. | Channels overlap when their frequency ranges overlap. |
| SSID and BSSID are the same thing. | SSID is the network name; BSSID identifies a particular AP radio. |
| A stronger signal always means a better connection. | SNR and interference also matter. |
| -80 dBm is stronger than -50 dBm. | -50 dBm is stronger because it is closer to zero. |
| MIMO simply means having several antennas. | MIMO uses multiple transmit and receive paths; spatial streams can carry separate data streams. |

## 12. Knowledge Check

1. What does RF stand for?
   <details><summary>Answer</summary>Radio Frequency. It refers to electromagnetic frequencies used for wireless communication.</details>

2. Name the three common Wi-Fi frequency bands covered in this lesson.
   <details><summary>Answer</summary>2.4 GHz, 5 GHz, and 6 GHz.</details>

3. What is a Wi-Fi channel?
   <details><summary>Answer</summary>A specific portion of radio spectrum used for wireless communication.</details>

4. Why are channels 1, 6, and 11 commonly used in a 2.4 GHz 20 MHz channel plan?
   <details><summary>Answer</summary>They are commonly used to reduce channel overlap in many regulatory domains.</details>

5. What is the difference between SSID and BSSID?
   <details><summary>Answer</summary>SSID is the wireless network name; BSSID identifies a particular access point radio.</details>

6. Which signal is stronger: -55 dBm or -75 dBm?
   <details><summary>Answer</summary>-55 dBm is stronger because it is closer to zero.</details>

7. What does SNR measure?
   <details><summary>Answer</summary>The ratio between wanted signal power and noise power.</details>

8. What is multipath?
   <details><summary>Answer</summary>When radio waves reach a receiver by multiple paths, often due to reflections.</details>

9. What does MIMO stand for?
   <details><summary>Answer</summary>Multiple Input, Multiple Output.</details>

## 13. Practice

Use a Wi-Fi analyzer on a device you own, if one is available.

Record:

- The SSID of the connected network.
- The channel and frequency band.
- The received signal level in dBm.
- The signal level in a second room.

Compare the two readings. Explain how walls, distance, channel overlap, and noise might affect performance.

Do not change access point settings unless you are authorized to manage the network.

## 14. CCNA Takeaways

- Wi-Fi uses radio frequency (RF) signals.
- Know the 2.4 GHz, 5 GHz, and 6 GHz bands.
- Understand channels, channel width, and non-overlapping channels.
- SSID is the network name; BSSID identifies an AP radio.
- RSSI describes received signal strength; dBm is a power unit.
- SNR compares wanted signal with noise.
- Interference, attenuation, and multipath affect wireless performance.
- MIMO uses multiple transmit and receive paths; spatial streams can increase data capacity.

## Self-Check

- [ ] I can explain the role of RF in Wi-Fi.
- [ ] I can compare the 2.4 GHz, 5 GHz, and 6 GHz bands.
- [ ] I understand channels, channel width, and channel overlap.
- [ ] I can distinguish SSID from BSSID.
- [ ] I can interpret a negative dBm signal reading.
- [ ] I can explain SNR, interference, attenuation, and multipath.
- [ ] I understand the basic purpose of MIMO and spatial streams.

**Next lesson:** 01-09 — Ethernet Physical Standards.

## References

- [Cisco — Wireless RF Reference Guide](https://www.cisco.com/c/en/us/td/docs/wireless/controller/9800/technical-reference/wireless-rf-reference-guide.html)
- [Cisco — Design Guide for Large Public Wireless Networks](https://www.cisco.com/c/en/us/support/docs/wireless/catalyst-9800-series-wireless-controllers/222000-design-guide-cx-wireless-for-large-pub.html)
- [Cisco — CCNA 200-301 v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics)
