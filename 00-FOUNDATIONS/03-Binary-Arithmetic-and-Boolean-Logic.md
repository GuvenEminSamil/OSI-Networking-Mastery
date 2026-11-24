# 00-03 — Binary Arithmetic and Boolean Logic

> **Prerequisite:** 00-02 — Number Systems and Units  
> **CCNA 200-301 v1.1 connection:** Foundations for IPv4 subnetting, wildcard masks, and access control lists (ACLs).  
> **Suggested study time:** Flexible.

## What You Will Learn

- Add binary numbers.
- Understand what happens when a fixed-size number becomes too large.
- Explain the basic Boolean operations: AND, OR, NOT, and XOR.
- Use bitwise AND and OR to understand network and broadcast addresses.
- Recognize why XOR is useful for error detection.

## 1. What Is Boolean Logic?

**Boolean logic** is a system in which a value is either true or false. In digital systems, we commonly represent these values as:

- True = 1
- False = 0

Think about a secure door that opens only when you have both a valid card **and** the correct PIN. This is an AND condition.

Another door might open when you use either a card **or** a PIN. This is an OR condition.

Routers and computers use these simple operations to make decisions about bits.

## 2. Binary Addition

Binary addition follows rules similar to decimal addition.

| First bit | Second bit | Result | Carry |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

A **carry** is the value moved to the next column when a sum is too large for the current column.

The most important rule is:

[
1+1=10_2
]

This means write 0 in the current column and carry 1 to the next column.

Example:

```
   01101011   (107)
 + 00110110   ( 54)
 -----------
   10100001   (161)
```

Check the decimal result: 107 + 54 = 161.

## 3. Fixed-Size Numbers and Overflow

Computers store values using a fixed number of bits in many places.

An **8-bit unsigned number** can represent values from 0 to 255.

Why 255?

[
2^8=256 possible values
]

The values start at zero, so the largest one is 255.

What happens when we add 1 to 255 using only eight bits?

```
  11111111   (255)
+ 00000001   (  1)
-----------
1 00000000   (256)
```

The result needs nine bits. If the system keeps only eight bits, the extra bit is lost and the stored value becomes zero. This is called **overflow**.

You may see a similar idea with counters that eventually return to zero after reaching their maximum value.

## 4. Boolean Operations

These operations work on one or more bits.

| A | B | AND | OR | XOR |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

**AND:** The result is 1 only when both inputs are 1.

**OR:** The result is 1 when at least one input is 1.

**XOR** (exclusive OR): The result is 1 when the two inputs are different.

**NOT:** Reverses a bit. 0 becomes 1, and 1 becomes 0.

**NAND:** The opposite of AND. It is 0 only when both inputs are 1.

The table below shows NOT and NAND:

| A | NOT A |
|---:|---:|
| 0 | 1 |
| 1 | 0 |

| A | B | NAND |
|---:|---:|---:|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

## 5. Bitwise Operations

A **bitwise operation** applies a logical operation to each bit position separately.

For example:

```
  10110110
AND 11110000
-----------
  10110000
```

The same idea applies to OR and XOR:

| Operation | What it does | Example |
|---|---|---|
| AND | Keeps a bit only where both values have 1 | 1010 AND 1100 = 1000 |
| OR | Sets a bit to 1 when either value has 1 | 1010 OR 1100 = 1110 |
| XOR | Sets a bit to 1 when the values differ | 1010 XOR 1100 = 0110 |
| NOT | Reverses every bit | NOT 1010 = 0101 (for a 4-bit value) |

## 6. How AND Helps Find a Network Address

A **subnet mask** tells a device which part of an IPv4 address identifies the network and which part identifies the host (the individual interface in that network).

When a device performs a bitwise AND between an IP address and its subnet mask, the result is the **network address**.

Example:

- IP address: `192.168.10.77/26`
- Subnet mask: `255.255.255.192`

The prefix `/26` means that the first 26 bits of the mask are 1.

For this example, the first three octets stay the same. We only need to calculate the last octet:

```
IP address:   77  = 01001101
Subnet mask: 192  = 11000000
                    --------
AND result:         01000000 = 64
```

The network address is:

`192.168.10.64`

You will learn the complete subnetting method in the dedicated IPv4 lessons.

## 7. Wildcard Masks and Broadcast Addresses

A **wildcard mask** is used by some Cisco features, including access control lists and OSPF network statements. In a wildcard mask, a 0 means “check this bit” and a 1 means “ignore this bit.”

For a normal subnet mask, the wildcard mask is its bitwise inverse.

Example:

```
Subnet mask:   255.255.255.192
Wildcard mask:   0.  0.  0. 63
```

A **broadcast address** is an IPv4 address used to send traffic to all hosts in a subnet.

For the `192.168.10.64/26` subnet, the broadcast address is `192.168.10.127`. The host bits are all set to 1.

You do not need to master all subnetting calculations here; the important point is that AND and bit values help explain how addresses are divided.

## 8. XOR and Error Detection

XOR can help detect certain data errors.

A simple **parity bit** is an extra bit added to data so that the number of 1s follows an agreed rule, such as being even.

If one bit changes during transmission, the parity may no longer match. However, if two bits change, simple parity may fail to detect the error.

Ethernet uses a stronger method called **CRC** (Cyclic Redundancy Check). CRC is a calculation added to a frame so the receiver can detect many transmission errors. Its mathematics uses XOR operations.

## 9. Common Mistakes

| Mistake | Correct idea |
|---|---|
| XOR and OR are identical. | OR is 1 when either or both bits are 1. XOR is 1 only when the bits differ. |
| AND always produces the same value. | The result depends on both bit patterns. |
| Overflow means the computer is broken. | Overflow can be a normal result of storing a value in a fixed number of bits. |
| The router always decides whether a destination is local. | The sending host first uses its own IP address and subnet mask to decide whether a destination is local. |

## 10. Knowledge Check

1. What is the result of binary `1 + 1`?
   <details><summary>Answer</summary>`10` in binary: write 0 and carry 1.</details>

2. What is the largest unsigned value that can be stored in eight bits?
   <details><summary>Answer</summary>**255**. Eight bits provide 256 possible values, from 0 to 255.</details>

3. What is the result of `1010 AND 1100`?
   <details><summary>Answer</summary>`1000`. Only the third bit from the right is 1 in both values.</details>

4. What is the result of `1010 XOR 1100`?
   <details><summary>Answer</summary>`0110`. XOR produces 1 where the two input bits are different.</details>

5. Find the network address of `192.168.10.77/26`.
   <details><summary>Answer</summary>`192.168.10.64`.</details>

6. What is the wildcard mask for `255.255.255.192`?
   <details><summary>Answer</summary>`0.0.0.63`.</details>

7. What is the broadcast address of the `192.168.10.64/26` subnet?
   <details><summary>Answer</summary>`192.168.10.127`.</details>

## 11. Practice

Use Python to check the last-octet calculations:

```python
ip = 77
mask = 192
wildcard = 255 - mask

network = ip & mask
broadcast = ip | wildcard

print(network)    # 64
print(broadcast)  # 127
print(wildcard)   # 63
```

Then try the same method with the last octet of `10.0.5.130/25`.

## 12. CCNA Takeaways

- AND, OR, NOT, and XOR are basic operations on bits.
- AND helps identify the network portion of an IPv4 address.
- A wildcard mask is commonly the inverse of a subnet mask.
- XOR is used in error-detection calculations.
- Learn the reasoning, not just the table: understand what each bit operation does.

## Self-Check

- [ ] I can add simple binary numbers.
- [ ] I understand overflow in an 8-bit value.
- [ ] I can explain AND, OR, NOT, and XOR.
- [ ] I can use AND to find a simple network address.
- [ ] I understand the purpose of wildcard masks and CRC.

**Next lesson:** 00-04 — Electricity Fundamentals.
