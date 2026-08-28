#data-representation #programming #computer-fundamentals

# Data Representation

Computers operate on binary data. At the lowest level, information is represented using bits, where each bit can have a value of `0` or `1`. Groups of bits form larger units such as bytes, and software interprets those bytes according to a defined data representation.

Understanding data representation is fundamental to programming, networking, digital forensics, reverse engineering, and vulnerability research because the same bytes can represent completely different information depending on how they are interpreted.

## Bits and Bytes

A bit is the smallest unit of digital information and can represent two possible states. Eight bits form one byte, allowing 256 distinct values, from `0` through `255`.

Larger integer values are represented using multiple bytes. The number of bytes used and whether the value is signed or unsigned determine the range of values that can be represented.

## Binary, Decimal, and Hexadecimal

Binary uses base 2 and directly corresponds to the two-state nature of digital logic. Decimal uses base 10 and is the conventional representation used by humans. Hexadecimal uses base 16 and is particularly useful when working with bytes because one hexadecimal digit represents four bits.

A byte can therefore be represented using exactly two hexadecimal digits. For example, the decimal value `255` corresponds to binary `11111111` and hexadecimal `FF`.

Hexadecimal is extensively used when inspecting memory, files, network packets, executable formats, and cryptographic material.

## Text Representation

Text is not stored as abstract characters. Characters are represented using numeric values defined by character encodings such as ASCII and Unicode.

For example, the character `A` has a defined numeric representation in ASCII. A program can interpret the corresponding byte as a character when it knows that the bytes should be interpreted using an appropriate character encoding.

See [[Data-Encoding]] for the distinction between character representation and encoding mechanisms.

## Integers and Floating-Point Numbers

Integers represent whole numbers. Depending on their size and whether they are signed, different ranges can be represented. Signed integer representations commonly use two's complement, which allows positive and negative values to be represented efficiently.

Floating-point representations are used for values that require a fractional component or a large dynamic range. They are generally represented using a structure containing a sign, exponent, and significand. Floating-point arithmetic is therefore subject to precision and rounding limitations.

## Endianness

When a value occupies multiple bytes, the order in which those bytes are stored becomes significant.

Big-endian stores the most significant byte first, while little-endian stores the least significant byte first. Many modern desktop systems use little-endian architectures.

Endianness becomes particularly important when analysing binary files, memory dumps, network protocols, executable formats, and low-level data structures.

## Data Structures and Serialization

Programming languages provide higher-level structures such as arrays, strings, objects, dictionaries, and records. These structures ultimately need to be represented as bytes when stored or transmitted.

Serialization converts structured data into a representation suitable for storage or transmission. Common formats include JSON, XML, CSV, and binary serialization formats. Deserialization reconstructs the data structure from its serialized representation.

Unsafe deserialization can become a security vulnerability when an application reconstructs attacker-controlled objects or executes unintended behaviour during the process.

## Security Relevance

Many security problems require understanding the difference between the data itself and the representation used to store or transmit it. Incorrect assumptions about byte order, character encoding, integer size, or serialization can cause vulnerabilities, parsing errors, information disclosure, and forensic misinterpretation.

At a low level, security analysis often reduces to understanding what sequence of bytes actually exists and how a particular application interprets those bytes.

## Related Concepts

- [[Data-Encoding]]
- [[Cryptography]]
- [[Networking-Basics]]
- [[Packets-and-Frames]]
- [[File-Systems]]