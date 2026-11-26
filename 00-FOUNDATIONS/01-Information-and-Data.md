# 00-01 — Information and Data

> **Prerequisite:** None  
> **CCNA connection:** Background for understanding network data, protocols, and communication.

## What You Will Learn

- Explain the difference between data and information.
- Describe how a protocol gives meaning to transmitted data.
- Explain, in practical terms, why digital systems commonly use two logic states.
- Understand how noise can affect signals and why a receiver needs a decision threshold.
- Calculate how many bits are needed to represent a set of possible values.

## 1. Start with a Simple Example

Imagine you and a friend agree on a signal:

- A room light switched **on** means “I am coming.”
- The light switched **off** means “I am not coming.”

The light is the **data**: a physical state that can be observed. The meaning your friend learns is the **information**.

The agreement matters. Someone who does not know your rule sees only a light. They cannot know what it means.

Networks work in the same way. A cable carries electrical signals, fiber carries light, and Wi-Fi uses radio waves. These physical signals represent data. A shared set of rules tells the sender and receiver how to interpret that data. Those rules are called a **protocol**.

## 2. Data, Information, and Bits

**Data** is a representation: symbols, numbers, bytes, or signal states.

**Information** is what a receiver can understand from data by applying an agreed interpretation.

For example, the byte sequence `01000001` may represent the letter “A” under ASCII. Without knowing the encoding rule, it is only a sequence of bits.

A **bit** (binary digit) is a unit that can represent one of two values, commonly written as 0 and 1. One bit can distinguish between two alternatives.

The same data can mean different things in different contexts. A protocol defines what each field means and where it appears. For example, an Ethernet frame uses its first six bytes for the destination MAC address. A receiver must understand the Ethernet format to interpret those bytes correctly.

## 3. Analog and Digital Signals

### 3.1 Analog representation

An **analog** value can vary continuously across a range. A microphone, for example, converts changes in air pressure into a changing electrical voltage.

Noise can alter an analog signal. When an analog signal is copied or amplified, unwanted noise may be amplified too.

### 3.2 Digital representation

A **digital** system interprets a physical signal as one of a limited set of symbols. In a simple two-state system, the receiver decides whether a received voltage represents 0 or 1.

A **decision threshold** is the boundary the receiver uses to make that decision.

For example, imagine:
- A voltage below 0.5 V is interpreted as 0.
- A voltage above 0.5 V is interpreted as 1.

The received voltage does not have to be exactly the value sent. It only needs to remain on the correct side of the threshold.

The safety distance between a valid signal level and the point where the receiver could make the wrong decision is called the **noise margin**. More noise margin generally makes a signal easier to interpret reliably.

### 3.3 Why digital systems are useful

Digital systems have several practical advantages:

1. **Regeneration:** A device can interpret incoming symbols and generate a clean new signal for the next link. Small amounts of noise do not have to accumulate at every stage.
2. **Error detection:** Extra bits can help a receiver detect damaged data. Ethernet uses a Frame Check Sequence (FCS) for this purpose.
3. **Reliable copying and storage:** Digital data can be copied without gradually changing its values, provided the storage and transfer process works correctly.
4. **Logical processing:** Digital values can be processed using operations such as AND, OR, and XOR. These operations are useful in networking, including subnet masks and error detection.

## 4. Why Do Computers Commonly Use Two States?

Two states are relatively easy for electronic circuits to distinguish reliably. Transistors can be used as switches, and digital circuits are designed around defined voltage ranges for 0 and 1.

Using only two states is not necessarily faster than using more states. Its main advantage is practical reliability and simpler circuit design.

However, do not assume that every network signal has only two physical levels. Some communication systems use multiple signal levels to carry more than one bit per symbol. For example, 1000BASE-T uses five-level PAM-5 signalling, while Wi-Fi can use QAM schemes with many possible signal states.

The information is digital, but the physical signal can use a more complex alphabet.

## 5. A Physical Signal Is Not Literally a Stream of 0s and 1s

A cable does not contain tiny 0s and 1s. It carries a physical signal, such as a changing voltage. Fiber carries light, and wireless links carry radio waves.

The receiver measures the physical signal and interprets it according to the agreed encoding rules. “Digital” describes how the signal is interpreted, not a separate kind of physical substance.

For some applications, an analog source such as sound must first be converted into digital data:

1. **Sampling** means measuring a changing signal at regular time intervals.
2. **Quantization** means mapping each measurement to one of a limited number of values.

These steps allow sound, images, and other information to be represented as digital data.

## 6. How Many Bits Are Needed?

With (n) bits, you can represent (2^n) different combinations.

To represent at least (N) different possibilities, choose the smallest whole number (n) for which (2^n geq N).

Examples:

| Number of possibilities | Minimum bits | Why |
|---:|---:|---|
| 2 | 1 | (2^1 = 2) |
| 6 | 3 | (2^2 = 4) is too small; (2^3 = 8) is enough |
| 26 | 5 | (2^4 = 16) is too small; (2^5 = 32) is enough |
| 1,000 | 10 | (2^{10} = 1,024) |
| All IPv4 addresses | 32 | An IPv4 address has 32 bits |
| A common MAC address | 48 | A MAC address has 48 bits |

This relationship is useful throughout networking. IPv4 subnetting, for example, depends on how many combinations a given number of host bits can represent.

## 7. Networking Examples

**A video call:** A microphone converts sound into an electrical signal. The computer converts that signal into digital data, encodes it, and sends it through the network. The receiving device converts the data back into sound.

**An online game:** A button press can become a short message describing an action. The receiver interprets the message according to the game's protocol.

**A home Wi-Fi connection:** Data may travel as radio signals between a laptop and an access point, and as electrical signals over a copper cable after that. The physical form changes, but the data is interpreted according to the same higher-level protocols.

## 8. Troubleshooting Connection

A physical problem can corrupt a signal. If the receiver interprets a symbol incorrectly, a frame may fail its integrity check.

On a Cisco switch, increasing `CRC` or `input errors` counters can point to a physical-link problem, such as a damaged cable, interference, or a duplex mismatch. These counters do not identify the cause by themselves, but they help guide the investigation.

A useful reasoning chain is:

`physical issue → corrupted signal → damaged frame → failed FCS check → frame discarded`

You will study signal problems in the Physical Layer unit and Ethernet error detection in the Data Link Layer unit.

## 9. Common Misunderstandings

| Misunderstanding | Correct idea |
|---|---|
| “Data and information are the same thing.” | Data is the representation; information is what the receiver understands from it. |
| “A cable literally carries 0s and 1s.” | A cable carries a physical signal that the receiver interprets as symbols. |
| “All network signals use only two voltage levels.” | Some technologies use multiple signal levels to carry more information per symbol. |
| “Computers use binary because it is always faster.” | Two-state circuits are practical and reliable to build. |
| “Digital means there is no noise.” | Physical signals can still be affected by noise. Digital receivers are designed to tolerate a range of signal variation. |

## 10. Check Your Understanding

1. What is the difference between data and information? Give a network example.
2. What does a protocol contribute to communication?
3. What is a decision threshold?
4. What does noise margin describe?
5. Why can a network signal use multiple physical levels even though computers process binary data?

<details><summary>Answers</summary>

1. Data is a representation, such as bytes. Information is the meaning obtained by interpreting those bytes. For example, an Ethernet header's destination field is understood as a MAC address because Ethernet defines that field.
2. A protocol defines the rules that let devices interpret messages consistently.
3. It is the boundary a receiver uses to decide which symbol a received signal represents.
4. It is the tolerance between a valid signal level and the point where noise could cause an incorrect decision.
5. The physical encoding can map bit groups to multi-level symbols. The receiver decodes those symbols back into bits.

</details>

## 11. Practical Reflection

Think about a video reaching your phone over Wi-Fi. Identify one place where information starts as an analog physical quantity, how it becomes digital data, and the different physical media the data may travel through.

## Readiness Checklist

- [ ] I can explain data versus information using my own example.
- [ ] I can explain what a protocol does.
- [ ] I can describe a decision threshold and noise margin in simple terms.
- [ ] I can explain why two-state digital circuits are practical.
- [ ] I can calculate the minimum number of bits needed for a given number of possibilities.

## Further Reading

- C. E. Shannon, “A Mathematical Theory of Communication” (1948), for the foundations of information theory.
- Charles Petzold, *Code: The Hidden Language of Computer Hardware and Software*, for an approachable introduction to digital representation.
