---
summary: Hashes data with MD5, SHA1 or SHA2.
---

# crypt.hash

```luau
crypt.hash(data: string, algorithm: string) -> string
```

Returns the hash of `data` as lowercase or uppercase hex. Supported algorithms are `md5`, `sha1`, `sha256`, `sha384` and `sha512`.

## Parameters

- `data`: The data to hash.
- `algorithm`: The algorithm's name.

## Example

```luau
print(crypt.hash("abc", "sha256"))
-- ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad
```

## Must

- Match the published digests for all five algorithms.
- Hash empty strings and binary data correctly.
- Never return a value for an algorithm that doesn't exist.
- Error when the data is `nil`.

## Should

- Support `sha3-256`.
- Error on an algorithm that doesn't exist, instead of returning nothing.
