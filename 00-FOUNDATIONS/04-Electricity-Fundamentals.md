# 00-04 — Electricity Fundamentals

> **Prerequisite:** 00-03 — Binary Arithmetic and Boolean Logic  
> **CCNA connection:** Understanding copper cabling, Ethernet signals, noise, and Power over Ethernet (PoE).  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain voltage, current, and resistance.
- Use Ohm's law for simple calculations.
- Understand electrical power and why cable resistance matters.
- Explain how Ethernet sends signals over copper cables.
- Understand the basic idea of differential signaling and Power over Ethernet.

This is a practical introduction, not an advanced electronics course.

## 1. Why Does Networking Need Electricity?

A copper Ethernet cable carries electrical signals between devices. A sender changes the electrical signal in a controlled pattern. The receiver detects those changes and interprets them as data.

Some Ethernet devices can also receive electrical power through the same cable. This is called **Power over Ethernet (PoE)**.

To understand these ideas, we need a few basic terms.

## 2. Three Important Electrical Terms

### Voltage (V)

**Voltage** is the electrical potential difference between two points. It is measured in volts (V).

A useful analogy is water pressure in a pipe: voltage is similar to the pressure that can drive current. The analogy is helpful, but voltage is not literally water pressure.

Voltage is always measured between two points.

### Current (I)

**Current** is the rate at which electric charge flows. It is measured in amperes (A).

Using the water analogy, current is similar to the amount of water flowing through a pipe each second.

### Resistance (R)

**Resistance** is how strongly a material opposes current flow. It is measured in ohms (Ω).

A longer or thinner copper wire generally has more resistance than a shorter or thicker wire of the same material.

## 3. Ohm's Law

**Ohm's law** describes the relationship between voltage, current, and resistance:

[
V=I	imes R
]

Where:

- V = voltage in volts
- I = current in amperes
- R = resistance in ohms

Example:

A cable section has a resistance of 2 Ω and carries 0.5 A.

[
V=0.5	imes2=1 V
]

The voltage drop across that resistance is 1 volt.

You can rearrange the formula:

[
I=rac{V}{R}qquad R=rac{V}{I}
]

## 4. Electrical Power

**Power** is the rate at which energy is transferred or used. It is measured in watts (W).

The basic formula is:

[
P=V	imes I
]

Combining this with Ohm's law gives another useful formula for power lost as heat in a resistance:

[
P_{loss}=I^2	imes R
]

This helps explain why cable resistance matters: more current creates more heat loss.

## 5. Why Does PoE Use a Higher Voltage?

PoE allows a network cable to carry both data and electrical power. It can power devices such as wireless access points, IP phones, and some cameras.

For the same amount of power, using a higher voltage means using less current:

[
I=rac{P}{V}
]

Imagine a device needs 15 watts:

- At 48 V: 15 ÷ 48 ≈ 0.31 A
- At 24 V: 15 ÷ 24 ≈ 0.63 A

The lower-voltage example needs about twice the current. Since cable loss increases with the square of current, the higher-current case can waste much more energy as heat.

This is one reason PoE uses a voltage around 48 V. Actual PoE voltage and power levels depend on the IEEE PoE type and the connected equipment.

## 6. Noise and Differential Signaling

**Noise** is unwanted electrical energy that can interfere with the signal.

It can come from nearby electrical equipment, radio sources, poor connections, or damaged cables.

Ethernet twisted-pair cables use pairs of wires. In **differential signaling**, the sender uses the voltage difference between the two wires to represent the signal. The receiver compares the two wires rather than relying on only one wire.

Why is this useful?

If similar unwanted noise affects both wires, the receiver can largely cancel it when it measures the difference. Twisting the wires helps them pick up similar noise.

A cable with damaged pairs, poor termination, or excessive interference may cause errors or reduce the speed of the connection.

## 7. Does Electricity Move Slowly Through the Cable?

Do not confuse the movement of individual electrons with the speed of a signal.

The signal is an electromagnetic wave that propagates through the cable. It travels very quickly, often at a substantial fraction of the speed of light.

This is why data can travel across a long cable without waiting for individual electrons to move from one end to the other.

## 8. Real-World Troubleshooting

Imagine a user reports that an Ethernet link is unstable.

Possible physical causes include:

- A damaged or sharply bent cable.
- A connector that is not properly terminated.
- Strong electrical interference.
- A cable that exceeds the supported length for the Ethernet standard.

A practical first step is to replace the cable with a known-good cable and check whether the link becomes stable.

## 9. Common Mistakes

| Mistake | Correct idea |
|---|---|
| Voltage and current are the same. | Voltage is potential difference; current is the flow of charge. |
| Resistance creates useful network data. | Resistance opposes current and can cause voltage drop and heat. |
| Electrons travel from one device to another at signal speed. | The electrical signal propagates quickly; individual electron drift is much slower. |
| Twisting the pairs is only for appearance. | Twisting helps reduce the effect of external noise. |
| PoE sends power instead of data. | PoE can carry both power and data on the same cable. |

## 10. Knowledge Check

1. What unit is used to measure voltage?
   <details><summary>Answer</summary>Volts (V).</details>

2. A resistance is 4 Ω and the current is 2 A. What is the voltage?
   <details><summary>Answer</summary>V = I × R = 2 × 4 = **8 V**.</details>

3. What is electrical power measured in?
   <details><summary>Answer</summary>Watts (W).</details>

4. A device needs 24 W at 48 V. Approximately how much current does it need?
   <details><summary>Answer</summary>I = P ÷ V = 24 ÷ 48 = **0.5 A**.</details>

5. Why can differential signaling resist some external noise?
   <details><summary>Answer</summary>The receiver measures the difference between two wires. Similar noise added to both wires can cancel out in that comparison.</details>

6. What does PoE allow an Ethernet cable to carry?
   <details><summary>Answer</summary>Both network data and electrical power.</details>

## 11. Practice

Look at the Ethernet cables and connectors around you. Check for:

- Damaged or crushed cable sections.
- Loose connectors.
- Pairs that have been untwisted too far near a connector.
- Ethernet cables placed directly alongside sources of strong electrical interference.

For each issue, explain how it could affect the signal.

## 12. CCNA Takeaways

- Voltage, current, and resistance are different electrical quantities.
- Ohm's law is V = I × R.
- Power is P = V × I.
- High current increases resistive cable loss.
- Differential signaling helps Ethernet resist external noise.
- PoE carries electrical power and data over Ethernet cabling.

## Self-Check

- [ ] I can define voltage, current, and resistance.
- [ ] I can solve a simple Ohm's law problem.
- [ ] I can calculate electrical power.
- [ ] I can explain why higher voltage can reduce current for the same power.
- [ ] I can describe differential signaling and the purpose of twisted pairs.

**Next lesson:** 00-05 — Transistors and Digital Logic.
