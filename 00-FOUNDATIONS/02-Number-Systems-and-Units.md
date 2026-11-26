# 00-02 — Number Systems and Units

> **Prerequisite:** 00-01 — Information and Data  
> **CCNA 200-301 v1.1 connection:** Foundations for IPv4 subnetting and IPv6 address representation.  
> **Suggested study time:** Flexible. Take breaks whenever you need them.

## What You Will Learn

By the end of this lesson, you should be able to:

- Explain decimal, binary, and hexadecimal numbers.
- Convert an 8-bit binary value to decimal and hexadecimal.
- Explain bits, bytes, and octets.
- Understand why network addresses often use hexadecimal.
- Convert between Mbps and MB/s.

## 1. Why Do We Need Different Number Systems?

A **number system** is a way to write and represent numbers.

The number system you use every day is called **decimal**. Computers use two-state electronic circuits, so digital information is commonly represented using **binary**. Network engineers also use **hexadecimal** because it makes long binary values shorter and easier to read.

The important idea is simple: the value does not change when we write it in a different number system. Only its representation changes.

## 2. Decimal, Binary, and Hexadecimal

### Decimal — Base 10

**Base** tells us how many different digits a number system uses.

Decimal has base 10 and uses these ten digits:

`0, 1, 2, 3, 4, 5, 6, 7, 8, 9`

For example, the number `352` means:

- 3 hundreds
- 5 tens
- 2 ones

Each digit's value depends on its position. This is called **place value**.

### Binary — Base 2

Binary uses only two digits: `0` and `1`.

A **bit** (short for *binary digit*) is one binary value. A bit can be either 0 or 1.

In binary, place values grow by powers of two from right to left:

| Place | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|

Let's convert `1011` to decimal:

| Binary digit | 1 | 0 | 1 | 1 |
|---|---:|---:|---:|---:|
| Place value | 8 | 4 | 2 | 1 |
| Contribution | 8 | 0 | 2 | 1 |

Add the contributions:

[
8+0+2+1=11
]

Therefore:

[
1011_2=11_{10}
]

The small number after a value tells us its base: 2 means binary and 10 means decimal.

### Hexadecimal — Base 16

**Hexadecimal** (often shortened to *hex*) uses sixteen symbols:

`0–9` and `A–F`

The letters represent values that decimal writes using two digits:

| Hex digit | Decimal value |
|---|---:|
| A | 10 |
| B | 11 |
| C | 12 |
| D | 13 |
| E | 14 |
| F | 15 |

One hexadecimal digit represents exactly four bits. A group of four bits is called a **nibble**.

Examples:

- Binary `1010` = hexadecimal `A`
- Binary `1100` = hexadecimal `C`
- Binary `1010 1100` = hexadecimal `AC`

So:

[
10101100_2=AC_{16}
]

Hexadecimal is useful because it makes long binary values easier to read. For example, a **MAC address** (Media Access Control address) identifies a network interface on a local network link. It is normally written in hexadecimal.

## 3. Bits, Bytes, and Octets

A **byte** is a group of eight bits:

[
1 byte=8 bits
]

An **octet** is a group of exactly eight bits. Networking standards often use the word *octet* when they need to be precise about the size.

An **IPv4 address** (Internet Protocol version 4 address) identifies an interface on an IP network. It is written as four decimal numbers separated by dots.

Example:

`192.168.1.10`

It contains four octets:

`192` · `168` · `1` · `10`

Each octet contains eight bits, so its decimal value can range from 0 to 255.

## 4. Network Speeds: Mbps and MB/s

These two units look similar, but they measure different things:

- **Mbps** means *megabits per second*. The lowercase `b` means bits.
- **MB/s** means *megabytes per second*. The uppercase `B` means bytes.

Because one byte contains eight bits, divide Mbps by eight to find its theoretical equivalent in MB/s.

Example:

[
100 Mbpsdiv 8=12.5 MB/s
]

A 100 Mbps connection can therefore carry at most about 12.5 MB of data per second before accounting for communication overhead.

**Overhead** is extra data used to manage communication, such as packet headers. Because of overhead and other real-world limits, an actual download is usually slower than the theoretical value.

## 5. Decimal and Binary Size Prefixes

You may see two ways to describe storage sizes:

| Decimal prefix | Meaning | Binary prefix | Meaning |
|---|---:|---|---:|
| 1 kB | 1,000 bytes | 1 KiB | 1,024 bytes |
| 1 MB | 1,000,000 bytes | 1 MiB | 1,048,576 bytes |
| 1 GB | 1,000,000,000 bytes | 1 GiB | 1,073,741,824 bytes |

**SI prefixes** (kilo, mega, giga) use powers of 1,000. **IEC prefixes** (kibi, mebi, gibi) use powers of 1,024.

For network link speeds, decimal units are standard. A 1 Gbps link means one billion bits per second.

## 6. A Practical Example

Your internet plan is 100 Mbps. A file is downloading at 11.8 MB/s.

Is the connection necessarily faulty?

No. First convert the advertised connection speed:

[
100div 8=12.5 MB/s
]

The theoretical limit is about 12.5 MB/s. An observed speed of 11.8 MB/s can be reasonable after overhead and other limits.

## 7. Common Mistakes

| Mistake | Correct idea |
|---|---|
| `b` and `B` mean the same thing. | `b` is bit; `B` is byte. |
| Hexadecimal changes the actual value. | It changes only how the value is written. |
| One IPv4 octet can be larger than 255. | An octet has 8 bits, so its maximum value is 255. |
| 100 Mbps means 100 MB/s. | 100 Mbps is theoretically 12.5 MB/s before overhead. |

## 8. Knowledge Check

Try each question before opening its answer.

1. Which digits does binary use?
   <details><summary>Answer</summary>Only `0` and `1`.</details>

2. What is the decimal value of binary `1011`?
   <details><summary>Answer</summary>8 + 2 + 1 = **11**.</details>

3. What is the decimal value of hexadecimal `A`?
   <details><summary>Answer</summary>**10**.</details>

4. How many bits are in one byte?
   <details><summary>Answer</summary>**8 bits**.</details>

5. What is the maximum decimal value of one octet?
   <details><summary>Answer</summary>**255**, because 11111111 in binary equals 255.</details>

6. Convert binary `11001000` to decimal.
   <details><summary>Answer</summary>128 + 64 + 8 = **200**.</details>

7. What is 128 + 32 + 8?
   <details><summary>Answer</summary>**168**. (This question's answer key has been checked.)</details>

8. A connection is 100 Mbps. What is its theoretical equivalent in MB/s?
   <details><summary>Answer</summary>100 ÷ 8 = **12.5 MB/s**.</details>

## 9. Practice

Write down five decimal values between 0 and 255. Convert each value to 8-bit binary. Then group the binary digits into two nibbles and convert them to hexadecimal.

You can check your work with Python:

```python
bin(200)            # '0b11001000'
hex(200)            # '0xc8'
int('11001000', 2)  # 200
```

## 10. CCNA Takeaways

- Binary uses 0 and 1; hexadecimal uses 0–9 and A–F.
- One hexadecimal digit represents four bits.
- One byte and one octet contain eight bits.
- One IPv4 address contains four 8-bit octets.
- Remember the difference between Mbps and MB/s.

## Self-Check

- [ X ] I can explain decimal, binary, and hexadecimal in simple words.
- [ X ] I can convert an 8-bit binary number to decimal.
- [ X ] I can convert four-bit groups to hexadecimal.
- [ X ] I understand bits, bytes, and octets.
- [ X ] I can convert Mbps to MB/s.

**Next lesson:** 00-03 — Binary Arithmetic and Boolean Logic.
