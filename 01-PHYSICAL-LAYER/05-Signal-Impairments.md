# 01-05 — Signal Impairments

> **Prerequisites:** 01-02 — Signals and Bandwidth; 01-04 — Bit Synchronization and Reception  
> **CCNA connection:** Helps explain physical-link errors and unstable connections.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain attenuation, noise, and signal-to-noise ratio.
- Understand decibels (dB) and dBm at a basic level.
- Recognize EMI, RFI, and crosstalk.
- Understand reflection, impedance mismatch, dispersion, and jitter.
- Connect physical signal problems to network troubleshooting.

## 1. What Is a Signal Impairment?

A **signal impairment** is any unwanted change that makes a signal harder to receive correctly.

The signal leaving a device may be clear, but the signal arriving at the other end may be weaker, distorted, or mixed with interference.

Common impairments include:

- Attenuation.
- Noise and interference.
- Crosstalk.
- Reflection.
- Dispersion.
- Jitter.

## 2. Attenuation

**Attenuation** is the loss of signal strength as a signal travels through a medium.

For example, a signal traveling through a long copper cable usually becomes weaker as distance increases.

The receiver must still be able to distinguish the wanted signal from noise. If the signal becomes too weak, errors may occur.

### Decibels (dB)

A **decibel (dB)** is a logarithmic way to express a ratio between two power levels. It is commonly used to describe signal gain or loss.

For power:

[
dB=10log_{10}left(rac{P_{out}}{P_{in}}ight)
]

You do not need to calculate complex cable budgets in this lesson. Remember:

- A positive dB value means power increased.
- A negative dB value means power decreased.
- A 10 dB loss means the output power is one tenth of the input power.

### dBm

**dBm** expresses an absolute power level relative to 1 milliwatt (mW).

- 0 dBm = 1 mW.
- 10 dBm = 10 mW.
- -10 dBm = 0.1 mW.

Do not confuse dB and dBm:

- dB compares two values.
- dBm describes one power level relative to 1 mW.

## 3. Noise and Signal-to-Noise Ratio

**Noise** is unwanted energy that becomes mixed with the wanted signal.

A receiver must distinguish the real signal from this unwanted energy.

**SNR** (Signal-to-Noise Ratio) compares the power of the wanted signal with the power of the noise.

A higher SNR generally means the signal is easier to recognize.

A lower SNR makes errors more likely because the wanted signal is harder to separate from noise.

## 4. EMI and RFI

**EMI** (Electromagnetic Interference) is unwanted electromagnetic energy that affects an electrical signal.

**RFI** (Radio-Frequency Interference) is interference caused by radio-frequency energy. It is one form of electromagnetic interference.

Possible sources include:

- Electric motors.
- Power equipment.
- Poorly shielded cables.
- Nearby radio transmitters.
- Poor cable installation.

Twisted-pair Ethernet reduces the effect of external interference, but it cannot make a cable immune to every source of noise.

## 5. Crosstalk

**Crosstalk** happens when a signal on one wire pair affects another nearby pair.

Twisted-pair Ethernet cables contain several pairs of copper wires. Their twisting helps reduce unwanted coupling between pairs.

Two terms describe where crosstalk is measured:

- **NEXT** (Near-End Crosstalk): interference measured at the same end as the signal source.
- **FEXT** (Far-End Crosstalk): interference measured at the far end of the cable.

Poor cable termination and excessive untwisting near the connector can increase crosstalk.

## 6. Reflection and Impedance Mismatch

A signal can be partially reflected when it meets a change in **impedance**.

**Impedance** is the opposition a circuit presents to a changing electrical signal. It is measured in ohms (Ω).

**Impedance mismatch** means the connected parts of a transmission path do not have the expected matching impedance.

This can cause some signal energy to reflect back toward the sender. Reflections can distort the signal and make it harder to decode.

Correct cable types, connectors, and termination help maintain signal integrity.

## 7. Dispersion

**Dispersion** happens when different parts of a signal travel at slightly different speeds or arrive at different times.

As a result, a signal pulse can spread out while traveling through a medium.

If neighboring pulses spread into one another, the receiver may have difficulty telling them apart.

The exact causes and effects depend on the cable or optical medium. You will see this idea again in the fiber-optics lesson.

## 8. Jitter

**Jitter** is unwanted variation in the timing of signal transitions.

A receiver expects transitions at predictable times. If those transitions arrive too early or too late, the receiver may sample at the wrong moment.

Do not confuse physical signal jitter with packet-delay variation:

- Signal jitter concerns the timing of physical signal transitions.
- Packet-delay variation concerns when network packets arrive.

Both can affect communication quality, but they describe different things.

## 9. How Impairments Appear During Troubleshooting

| Symptom or counter | Possible explanation |
|---|---|
| CRC or frame errors increase | Received frames are corrupted; inspect cable quality, termination, and interference. |
| Link repeatedly goes up and down | Physical connection, cable, connector, or negotiation problem may exist. |
| Very weak optical receive power | Attenuation, dirty connector, damaged fiber, or incorrect optics may be involved. |
| High packet loss only under load | Congestion or resource limits may be involved; do not assume it is a physical impairment. |
| Intermittent errors after cable installation | Poor termination, split pairs, excessive untwisting, or an unsuitable cable may be responsible. |

A **CRC** (Cyclic Redundancy Check) is an error-detection calculation used to detect corruption in a received frame.

On Cisco devices, use:

```
Switch# show interfaces
```

Look for CRC and input-error counters. Counters help identify a problem, but they do not always identify its exact cause.

## 10. Knowledge Check

1. What is attenuation?
   <details><summary>Answer</summary>Loss of signal strength as a signal travels through a medium.</details>

2. What does a negative dB value usually indicate when comparing output power with input power?
   <details><summary>Answer</summary>The output power is lower than the input power.</details>

3. What is the difference between dB and dBm?
   <details><summary>Answer</summary>dB expresses a ratio between two power levels; dBm expresses one power level relative to 1 mW.</details>

4. What does SNR compare?
   <details><summary>Answer</summary>The power of the wanted signal with the power of noise.</details>

5. What is crosstalk?
   <details><summary>Answer</summary>Unwanted signal coupling from one wire pair into another nearby pair.</details>

6. What is NEXT?
   <details><summary>Answer</summary>Near-End Crosstalk, measured at the same end as the signal source.</details>

7. What can cause a signal reflection?
   <details><summary>Answer</summary>An impedance mismatch along the transmission path.</details>

8. What is the difference between signal jitter and packet-delay variation?
   <details><summary>Answer</summary>Signal jitter is variation in the timing of physical signal transitions; packet-delay variation is variation in packet arrival times.</details>

## 11. Practice

A switch port is up, but its CRC counter increases over time.

1. What does the CRC counter indicate?
2. Name two possible physical causes.
3. What test can help determine whether the cable is the problem?

Suggested approach: inspect the connectors and cable, replace it temporarily with a known-good cable, and compare the error counters again.

## 12. Takeaways

- Attenuation weakens a signal.
- Noise makes the wanted signal harder to recognize.
- SNR compares wanted signal power with noise power.
- dB is a ratio; dBm is an absolute power level relative to 1 mW.
- Crosstalk is unwanted coupling between wire pairs.
- Impedance mismatch can cause reflection.
- Dispersion spreads signal pulses; jitter changes transition timing.
- Interface counters provide useful evidence during troubleshooting.

## Self-Check

- [ ] I can define attenuation and noise.
- [ ] I understand SNR, dB, and dBm.
- [ ] I can explain EMI, RFI, and crosstalk.
- [ ] I understand why impedance mismatch can cause reflection.
- [ ] I can explain dispersion and signal jitter.
- [ ] I know how to begin investigating CRC errors.

**Next lesson:** 01-06 — Copper Cabling.
