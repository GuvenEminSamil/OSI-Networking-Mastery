# 01-02 — Signals and Bandwidth

> **Prerequisites:** 00-04 — Electricity Fundamentals; 01-01 — The Purpose of the Physical Layer  
> **CCNA connection:** Foundation for understanding Ethernet media, wireless signals, and physical-link performance.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain what a signal is.
- Define amplitude, frequency, phase, and period.
- Distinguish analog and digital signals.
- Explain the difference between bandwidth measured in hertz and data rate measured in bits per second.
- Understand the basic ideas behind the Nyquist and Shannon limits.

## 1. What Is a Signal?

A **signal** is a physical change that carries information from one place to another.

Examples:

- A changing voltage in a copper cable.
- Light pulses in an optical fiber.
- Radio waves used by Wi-Fi.

The Physical layer uses signals to carry the bits produced by higher layers.

A signal changes over time. To describe that change, we use a few basic properties.

## 2. Four Basic Signal Properties

### Amplitude

**Amplitude** describes the size or strength of a signal.

For a simple electrical signal, it can describe how far the voltage moves from its reference level.

A larger amplitude does not automatically mean a faster data rate. It describes signal size, not how many bits are sent each second.

### Frequency

**Frequency** is the number of complete cycles a repeating signal makes in one second.

It is measured in hertz (Hz).

- 1 Hz = 1 cycle per second.
- 1 kHz = 1,000 cycles per second.
- 1 MHz = 1,000,000 cycles per second.

A **cycle** is one complete repetition of a waveform.

### Period

**Period** is the time required for one complete cycle. It is measured in seconds.

Frequency and period are inverses:

[
T=rac{1}{f}
]

For example, a signal with a frequency of 1,000 Hz has a period of:

[
T=rac{1}{1000}=0.001 s=1 ms
]

### Phase

**Phase** describes the position of a waveform within its cycle, relative to a reference waveform.

Imagine two identical waves. If one starts later than the other, they have a phase difference.

Phase is often measured in degrees:

- 0° means the waves are aligned.
- 180° means one is half a cycle behind the other.

You do not need to calculate phase for this introductory lesson. Just recognize that it is another way to describe how a signal is positioned in time.

## 3. Analog and Digital Signals

An **analog signal** can take a continuous range of values over time.

A **digital signal** represents information using a limited set of distinct symbols or levels.

For example:

- An analog voltage may rise and fall smoothly.
- A simple digital signal may use one voltage range for 0 and another for 1.

Important distinction: digital data is often carried by a physical waveform that changes continuously. “Digital” describes the information symbols being represented; it does not mean the physical signal is perfectly square or free from noise.

## 4. Bandwidth: Two Meanings

The word **bandwidth** is used in two related but different ways.

### Signal bandwidth — measured in hertz (Hz)

In signal theory, bandwidth is the range of frequencies occupied by a signal or allowed by a channel.

Example:

If a channel carries frequencies from 1 MHz to 5 MHz, its bandwidth is:

[
5 MHz-1 MHz=4 MHz
]

### Network bandwidth — often measured in bits per second

In everyday networking, bandwidth usually means the data-carrying capacity of a link. It is measured in bits per second (bps), such as 100 Mbps or 1 Gbps.

Do not confuse the units:

| Term | What it describes | Unit |
|---|---|---|
| Signal bandwidth | Range of frequencies | Hz |
| Network link bandwidth / capacity | Data-carrying rate | bps |

They are related, but they are not the same quantity.

## 5. Why Do Frequencies Matter?

A real signal may contain many frequency components.

A useful idea from **Fourier analysis** is that a complex repeating waveform can be understood as a combination of simpler sine waves with different frequencies.

A **sine wave** is a smooth, repeating waveform. You do not need to calculate Fourier transforms for CCNA. The important intuition is that signals can contain multiple frequencies, and a communication channel may not carry all of them equally well.

If a channel removes or weakens important frequency components, the received signal can become distorted.

## 6. The Nyquist Sampling Idea

Sometimes a receiver or system measures a changing signal at regular time intervals. This is called **sampling**.

The **Nyquist sampling criterion** says that, in an ideal system, the sampling rate must be at least twice the highest frequency present in a band-limited signal to reconstruct it correctly.

Example:

If the highest frequency in a signal is 4 kHz, the ideal minimum sampling rate is 8,000 samples per second.

If the sampling rate is too low, **aliasing** can occur. Aliasing makes a high-frequency component appear to be a different, lower frequency in the sampled result.

For this course, remember the relationship. The detailed mathematics of sampling is optional background.

## 7. The Shannon Capacity Idea

A communication channel has limits. The maximum reliable data rate depends partly on:

- How much frequency bandwidth is available.
- How strong the wanted signal is compared with unwanted noise.

**SNR** means *Signal-to-Noise Ratio*. It compares the power of the wanted signal with the power of noise.

A higher SNR means the wanted signal is easier to distinguish from noise.

The **Shannon capacity** formula gives a theoretical upper limit for data rate in an idealized noisy channel:

[
C=Blog_2(1+SNR)
]

Where:

- C = theoretical channel capacity in bits per second.
- B = signal bandwidth in hertz.
- SNR = signal-to-noise ratio as a linear power ratio, not a decibel value.

You do not need to derive or calculate this formula for this lesson. Remember the practical message:

- More channel bandwidth can allow a higher data rate.
- A cleaner signal (higher SNR) can allow a higher data rate.
- Noise and the available frequency range limit communication.

## 8. Real-World Example: A Noisy Wi-Fi Connection

Imagine your laptop is connected to Wi-Fi in a crowded apartment building.

Many nearby networks use the same radio band. Their transmissions can interfere with one another.

The result may include:

- Lower actual throughput.
- More retransmissions.
- Delays and variation in delay.
- A connection that feels unstable even though the Wi-Fi icon still shows a connection.

The signal may still be present, but the receiver has more difficulty distinguishing the wanted transmission from interference and noise.

## 9. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Frequency and data rate mean the same thing. | Frequency counts cycles per second; data rate counts bits per second. |
| Signal bandwidth and network bandwidth always use the same unit. | Signal bandwidth is measured in Hz; network data rate is measured in bps. |
| Digital signals are perfectly square and cannot be affected by noise. | A digital signal is a physical waveform and can still be distorted or corrupted. |
| A higher amplitude always means a higher data rate. | Amplitude describes signal size, not bits per second. |
| More bandwidth guarantees a particular data rate. | Data rate also depends on signal quality, modulation, coding, and other system limits. |

## 10. Knowledge Check

1. What is a signal?
   <details><summary>Answer</summary>A physical change that carries information from one place to another.</details>

2. What is frequency measured in?
   <details><summary>Answer</summary>Hertz (Hz), or cycles per second.</details>

3. A signal repeats 1,000 times per second. What is its frequency and period?
   <details><summary>Answer</summary>Frequency = 1,000 Hz (1 kHz). Period = 1/1,000 s = 1 ms.</details>

4. What is the difference between amplitude and frequency?
   <details><summary>Answer</summary>Amplitude describes signal size or strength. Frequency describes how many cycles occur each second.</details>

5. What unit is used for signal bandwidth?
   <details><summary>Answer</summary>Hertz (Hz).</details>

6. What does SNR compare?
   <details><summary>Answer</summary>The power of the wanted signal with the power of noise.</details>

7. What can happen when a signal is sampled too slowly?
   <details><summary>Answer</summary>Aliasing: high-frequency components may appear as incorrect lower frequencies.</details>

8. According to the Shannon idea, what two things can increase theoretical channel capacity?
   <details><summary>Answer</summary>More available signal bandwidth and a higher signal-to-noise ratio.</details>

## 11. Practice

1. Calculate the period of a 500 Hz signal.
2. A channel uses frequencies from 2 MHz to 8 MHz. Calculate its signal bandwidth in MHz.
3. Explain, in your own words, why a Wi-Fi connection can become slower in a crowded area even when the signal icon still shows a connection.

Suggested answers:

- 500 Hz has a period of 1/500 s = 0.002 s = 2 ms.
- 8 MHz − 2 MHz = 6 MHz.
- Other transmissions and noise make it harder for the receiver to distinguish the wanted signal, reducing effective performance.

## 12. CCNA Takeaways

- A signal physically carries information across a medium.
- Amplitude is signal size; frequency is cycles per second; period is time per cycle; phase is position within a cycle.
- Signal bandwidth is measured in Hz.
- Network link data rate is measured in bps.
- Sampling too slowly can cause aliasing.
- Bandwidth and SNR both affect theoretical channel capacity.

## Self-Check

- [ ] I can explain amplitude, frequency, period, and phase.
- [ ] I can calculate period from frequency.
- [ ] I can distinguish analog and digital signals.
- [ ] I understand the difference between bandwidth in Hz and data rate in bps.
- [ ] I can explain the basic Nyquist and Shannon ideas without deriving their formulas.

**Next lesson:** 01-03 — Line Coding and Modulation.
