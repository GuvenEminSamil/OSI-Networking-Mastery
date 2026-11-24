# 01-03 — Line Coding and Modulation

> **Prerequisites:** 01-02 — Signals and Bandwidth; 00-05 — Transistors and Digital Logic  
> **Purpose:** Understand how bit values are represented by physical signal patterns.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain the difference between bits and symbols.
- Understand line coding and modulation.
- Recognize NRZ, Manchester, 4B/5B, MLT-3, and PAM.
- Distinguish bit rate from symbol rate (baud).
- Recognize ASK, FSK, PSK, QAM, and OFDM.

## 1. From Bits to Signal Patterns

A network device needs a way to turn bits into physical signal changes.

**Line coding** is a method of representing a sequence of bits using signal levels or transitions on a communication medium.

For example, a simple system could use:

- One low voltage level to represent 0.
- One high voltage level to represent 1.

Real Ethernet systems use more sophisticated patterns so receivers can recover timing and distinguish data reliably.

## 2. Bits, Symbols, and Baud

A **bit** is one binary digit: 0 or 1.

A **symbol** is one distinct signal event or state used to represent information. One symbol may represent one bit or several bits.

**Baud** is the number of symbols transmitted per second. It is measured in symbols per second.

Do not confuse these terms:

- Bit rate = number of bits per second.
- Symbol rate = number of symbols per second (baud).

Example:

If a signaling system uses four distinct symbols, it can represent four different combinations:

`00`, `01`, `10`, `11`

That means each symbol can represent two bits. At 1,000 symbols per second, the theoretical bit rate is 2,000 bits per second.

The real relationship depends on the coding method and any extra error-control information.

## 3. Common Line-Coding Methods

### NRZ — Non-Return-to-Zero

**NRZ** uses signal levels to represent bits. The signal does not have to return to a neutral level between consecutive bits.

A problem can occur when many identical bits appear in a row. There may be too few signal transitions for the receiver to keep its timing synchronized.

### Manchester Encoding

**Manchester encoding** uses a transition in the middle of every bit period. The direction of the transition represents the bit value.

This makes timing recovery easier because every bit contains a transition. The trade-off is that it requires more signal transitions than simpler coding.

Manchester encoding is used by 10BASE-T Ethernet.

### 4B/5B and MLT-3

**4B/5B** maps every group of four data bits to a five-bit code group. The selected code groups help ensure enough transitions for reliable timing recovery.

**MLT-3** (Multi-Level Transmit, three levels) uses three non-zero signal levels plus a zero level in a repeating pattern. It reduces how quickly the signal changes compared with a simple two-level pattern.

100BASE-TX combines 4B/5B coding with MLT-3 signaling.

You do not need to memorize every code group. Remember the purpose: coding helps the receiver recover timing and interpret the data.

## 4. Pulse Amplitude Modulation (PAM)

**PAM** (Pulse Amplitude Modulation) represents symbols using different signal amplitudes.

Instead of only two possible levels, the system can use several levels.

Examples:

- 1000BASE-T uses five-level PAM signaling (PAM-5) over four twisted pairs.
- 10GBASE-T uses more complex multi-level signaling based on PAM-16.
- PAM4 uses four amplitude levels and is used in various higher-speed Ethernet and optical technologies.

More levels can carry more information per symbol, but the receiver must distinguish between levels that are closer together. This makes signal quality and noise control important.

## 5. Block Coding

A **block code** maps a group of data bits into a different group of transmitted bits. This can add redundancy or help maintain useful signal properties.

Two examples:

- **8b/10b** maps 8 data bits to 10 transmitted bits. The extra bits help maintain transitions and limit long-term imbalance.
- **64b/66b** adds a 2-bit synchronization header to each 64-bit data block. It has less coding overhead than 8b/10b.

The key idea is that transmitted bits are not always identical to the original data bits. Some encoding methods add extra bits to make transmission more reliable.

## 6. Modulation Methods

**Modulation** changes a signal in a controlled way to represent information. In many systems, information is placed onto a carrier signal.

A **carrier** is a repeating signal that can be changed to carry data.

Common modulation families:

| Method | What changes? | Meaning |
|---|---|---|
| ASK (Amplitude Shift Keying) | Amplitude | Different amplitudes represent symbols |
| FSK (Frequency Shift Keying) | Frequency | Different frequencies represent symbols |
| PSK (Phase Shift Keying) | Phase | Different phase positions represent symbols |
| QAM (Quadrature Amplitude Modulation) | Amplitude and phase | Different combinations represent symbols |

Wi-Fi uses QAM in many of its data rates.

## 7. OFDM

**OFDM** (Orthogonal Frequency-Division Multiplexing) divides a channel into many smaller subcarriers and sends data across them.

A **subcarrier** is one of the smaller frequency components used inside a wider channel.

The subcarriers are arranged so they can overlap in frequency while remaining mathematically separable. This helps use the available channel efficiently.

OFDM is used in Wi-Fi and several other communication technologies.

You do not need to understand the mathematical details here. Remember the idea: one wide channel is divided into many closely spaced subcarriers.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Baud and bits per second are always the same. | One symbol can represent more than one bit. |
| Every Ethernet technology uses the same line code. | Different Ethernet speeds use different encoding and signaling methods. |
| More signal levels always make communication easier. | More levels can carry more information per symbol, but they are harder to distinguish in noise. |
| Line coding and modulation are exactly the same. | Both map information to signals, but they describe different stages or methods of doing so. |
| A 4B/5B code transmits only four bits. | It maps four data bits to a five-bit code group. |

## 9. Knowledge Check

1. What is a symbol?
   <details><summary>Answer</summary>A distinct signal event or state used to represent information. A symbol can represent one or more bits.</details>

2. What does baud measure?
   <details><summary>Answer</summary>Symbols transmitted per second.</details>

3. What is the main advantage of Manchester encoding?
   <details><summary>Answer</summary>Every bit period contains a transition, which helps the receiver recover timing.</details>

4. Which coding combination is used by 100BASE-TX?
   <details><summary>Answer</summary>4B/5B coding with MLT-3 signaling.</details>

5. What does PAM vary to represent symbols?
   <details><summary>Answer</summary>Signal amplitude.</details>

6. Which two signal properties are varied in QAM?
   <details><summary>Answer</summary>Amplitude and phase.</details>

7. What is the basic idea of OFDM?
   <details><summary>Answer</summary>It divides a channel into many smaller, closely spaced subcarriers and sends data across them.</details>

## 10. Practice

A signaling system transmits 2,000 symbols per second. Each symbol represents two bits.

[
2,000	imes2=4,000 bits/s
]

Explain why the bit rate is twice the symbol rate.

Then explain, in your own words, why Manchester encoding can help synchronization but may require more bandwidth than a simpler two-level code.

## 11. Takeaways

- Line coding maps bit patterns to physical signal patterns.
- Modulation changes properties of a signal to carry information.
- Baud measures symbols per second; bps measures bits per second.
- 10BASE-T uses Manchester encoding.
- 100BASE-TX uses 4B/5B and MLT-3.
- Modern Ethernet and wireless technologies use multi-level signaling and modulation.
- QAM changes amplitude and phase; OFDM uses multiple subcarriers.

## Self-Check

- [ ] I can explain the difference between a bit and a symbol.
- [ ] I can distinguish baud from bit rate.
- [ ] I understand the purpose of Manchester and 4B/5B coding.
- [ ] I recognize PAM, QAM, and OFDM.
- [ ] I can describe why line coding and modulation are needed.

**Next lesson:** 01-04 — Bit Synchronization and Reception.
