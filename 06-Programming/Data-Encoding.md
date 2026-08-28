#data-encoding #programming #data

# Data Encoding

Data encoding is the process of representing information in a format that can be stored, transmitted, or interpreted by another system. An encoding defines how a set of values is mapped to a sequence of bytes, characters, or symbols. Encoding is not the same as encryption: an encoding normally provides no confidentiality and can be reversed without a secret key.

## Character Encoding

Character encoding defines how textual characters are represented as bytes. ASCII is an early character encoding that represents a limited set of characters, while Unicode provides a much larger character set capable of representing writing systems from around the world.

UTF-8 is the dominant Unicode encoding on the modern Internet. It uses one to four bytes per character and preserves compatibility with ASCII for the first 128 characters. When analysing web requests, files, logs, or network traffic, understanding the character encoding is important because the same logical text can have different byte representations.

## Common Encodings

Base64 represents binary data using a restricted set of printable characters. It is commonly used to transport binary or structured data through systems designed primarily for text. Base64 is encoding, not encryption, so its contents can be decoded without a key.

URL encoding represents characters that have special meaning inside URLs or HTTP requests. Characters are commonly represented using percent encoding, such as `%20` for a space. This allows arbitrary data to be safely represented within components of a URL.

Hexadecimal encoding represents each byte using two hexadecimal characters. It is frequently encountered in hashes, packet analysis, memory analysis, file contents, and debugging because hexadecimal provides a convenient human-readable representation of raw bytes.

## Encoding vs Encryption vs Hashing

Encoding changes representation so that data can be transported or interpreted correctly. Encryption transforms data to provide confidentiality and requires a cryptographic key for decryption. Hashing transforms data into a fixed-size digest designed primarily for integrity verification and other cryptographic applications.

Confusing these mechanisms can lead to incorrect security assumptions. Base64-encoded credentials, for example, are still credentials and should not be considered protected merely because they are not immediately readable.

## Security Relevance

Security analysts frequently encounter encoded data in HTTP requests, cookies, authentication mechanisms, malware, configuration files, logs, and forensic artefacts. Correctly identifying the encoding makes it possible to recover the original representation and understand what the data actually contains.

Encoding can also be layered. A value may be URL-encoded and then Base64-encoded, or binary data may be represented as hexadecimal before being embedded in another format. Analysis therefore requires identifying each transformation rather than assuming that every apparently random string is encrypted or hashed.

## Related Concepts

- [[Data-Representation]]
- [[Cryptography]]
- [[HTTP]]
- [[Cookies]]
- [[Sessions]]