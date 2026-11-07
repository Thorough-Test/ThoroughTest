---
summary: Encode, compress, hash and encrypt data.
---

# Encoding

Everything here works on Luau strings, and Luau strings can hold any bytes, so binary data is fine. None of these functions should lose a null byte or quietly change your data.

TT checks these against published test vectors and a real decoder, because a function that only understands its own output is no use when you need to talk to anything else.
