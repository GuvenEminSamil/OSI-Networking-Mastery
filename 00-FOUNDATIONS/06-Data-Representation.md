# 00-06 — Data Representation

> **Prerequisite:** 00-02 — Number Systems and Units  
> **CCNA connection:** Understanding protocol fields, byte order, and how data is represented inside packets.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Explain why the same bytes can represent different kinds of information.
- Calculate the value range of a field from its bit length.
- Distinguish big-endian and little-endian byte order.
- Understand network byte order.
- Recognize how text and files are represented as bytes.

## 1. Bytes Need a Meaning

A **byte** is a group of eight bits. By itself, a byte does not tell us what kind of information it represents.

Look at these four bytes:

`C0 A8 01 01`

They could be interpreted as:

- An IPv4 address: `192.168.1.1`
- Part of a 32-bit number.
- Four values in a data file.

The bytes do not explain their meaning. A protocol or file format defines how they must be interpreted.

A **protocol field** is a specific part of a message that carries a particular value, such as a source address, destination address, or length.

## 2. Bit Length and Value Range

The number of bits in a field determines how many values it can represent.

An unsigned field uses only non-negative values.

For an unsigned field with n bits:

[
Number of values=2^n
]

The range begins at zero, so:

[
Maximum value=2^n-1
]

Examples:

| Field size | Number of possible values | Range |
|---:|---:|---:|
| 8 bits | 256 | 0–255 |
| 12 bits | 4,096 | 0–4,095 |
| 16 bits | 65,536 | 0–65,535 |
| 32 bits | 4,294,967,296 | 0–4,294,967,295 |

This is useful when reading protocol fields. For example, a TCP or UDP port number is 16 bits long, so its numeric range is 0–65,535.

## 3. Byte Order: Big-Endian and Little-Endian

When a value uses more than one byte, systems need an agreed order for those bytes.

**Big-endian** stores or sends the most significant byte first.

**Little-endian** stores the least significant byte first.

Consider the 32-bit value:

`0x0A0B0C0D`

| Byte order | Byte sequence |
|---|---|
| Big-endian | `0A 0B 0C 0D` |
| Little-endian | `0D 0C 0B 0A` |

The numeric value is the same. Only the order of the bytes is different.

### Network Byte Order

**Network byte order** is the standard byte order used for multi-byte numeric fields in Internet protocols. It is big-endian.

For example, decimal port 80 is hexadecimal `0x0050`. It is represented in network byte order as:

`00 50`

This agreement allows different types of computers to communicate reliably.

## 4. How Text Becomes Bytes

Computers store text using character encodings.

A **character encoding** is a rule that maps characters to numeric values and bytes.

Two common examples are:

- **ASCII:** an older encoding for basic English letters, digits, and symbols.
- **UTF-8:** a widely used encoding that can represent characters from many writing systems.

For example, the letter `A` has the value 65 in ASCII and is represented by the same single byte in UTF-8.

The important lesson: text is also stored as bytes. The encoding tells the computer how to interpret those bytes.

## 5. Images, Audio, and Video

Digital media is also represented by numbers and bytes.

- An **image** is made of pixels. A pixel is one small picture element that stores color information.
- **Audio** can be represented by taking measurements of a sound signal at regular intervals. Each measurement is called a sample.
- **Video** is commonly made of a sequence of images, often combined with audio.

The details of image compression, audio sampling, and video codecs are outside the core goal of this lesson. For now, remember that digital media is represented using bits and bytes according to an agreed format.

## 6. File Types and File Signatures

A file extension is the text at the end of a file name, such as `.pdf` or `.png`.

A **file signature** is a recognizable sequence of bytes near the beginning of some file types. It can help identify the real file format.

For example:

- A PDF file commonly begins with the bytes for `%PDF-`.
- A PNG image begins with the byte sequence `89 50 4E 47 0D 0A 1A 0A`.

The extension is only a name. The internal data format is more reliable evidence of what the file contains.

## 7. Why This Matters in Networking

Network messages contain fields with defined sizes and meanings.

For example:

- A TCP or UDP port field is 16 bits.
- An IPv4 address is 32 bits, normally shown as four octets.
- Ethernet uses an EtherType field to identify the type of payload carried in a frame.

A receiver reads the fields according to the protocol specification. If the sender and receiver disagree about field size or byte order, the value can be interpreted incorrectly.

## 8. Common Mistakes

| Mistake | Correct idea |
|---|---|
| A byte always means text. | A byte can represent text, part of an address, a number, or many other kinds of data. |
| Big-endian and little-endian change the value. | They change the order of bytes used to represent the value. |
| A file extension proves what the file contains. | A file signature or its internal format is stronger evidence. |
| Network byte order is little-endian. | Internet protocols use big-endian network byte order for multi-byte numeric fields. |

## 9. Knowledge Check

1. How many values can an 8-bit unsigned field represent?
   <details><summary>Answer</summary>2⁸ = **256 values**, from 0 to 255.</details>

2. What is the maximum value of a 16-bit unsigned field?
   <details><summary>Answer</summary>2¹⁶ − 1 = **65,535**.</details>

3. Write `0x0A0B0C0D` in big-endian byte order.
   <details><summary>Answer</summary>`0A 0B 0C 0D`.</details>

4. Which byte order is used by Internet protocols as network byte order?
   <details><summary>Answer</summary>Big-endian.</details>

5. What is a character encoding?
   <details><summary>Answer</summary>A rule that maps characters to numeric values and bytes.</details>

6. Why is a file extension not always enough to identify a file?
   <details><summary>Answer</summary>Because the extension is only part of the file name and may not match the file's actual internal format.</details>

## 10. Practice

Use Python to explore the byte order of a number:

```python
value = 0x0A0B0C0D

value.to_bytes(4, byteorder="big")  
value.to_bytes(4, byteorder="little")
```

Compare the two results. The number is unchanged; only the byte sequence differs.

## 11. CCNA Takeaways

- Protocols define how fields and bytes must be interpreted.
- Field size determines its possible value range.
- Big-endian places the most significant byte first.
- Network byte order is big-endian.
- Text, images, audio, and video are all represented using bits and bytes.

## Self-Check

- [ ] I can calculate the range of an unsigned field.
- [ ] I can explain big-endian and little-endian.
- [ ] I know that Internet protocols use network byte order.
- [ ] I can explain why a byte sequence needs a format or protocol to give it meaning.

**Next lesson:** 00-07 — Computer Architecture for Networking.
