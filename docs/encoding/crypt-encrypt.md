---
summary: Encrypts data with AES.
---

# crypt.encrypt

```luau
crypt.encrypt(data: string, key: string, iv: string?, mode: string?) -> (string, string)
```

Encrypts data and returns the result and the iv, both as base64. The key has to be base64 too. A 32 byte key means AES-256.

An iv makes the same text encrypt differently each time. Leave it out and a random one is used, so keep the one that's returned.

## Parameters

- `data`: The data to encrypt.
- `key`: The key, as base64.
- `iv`: Optional. The iv, as base64. Random by default.
- `mode`: Optional. `"CBC"` by default, or `"CTR"`.

## Example

```luau
local Key = base64encode(string.rep("k", 32))

local Encrypted, Iv = crypt.encrypt("secret text", Key)
print(Encrypted, Iv)
```

## Must

- Work with no `iv` or `mode`, and return the encrypted data and the iv as base64 strings.
- Return an iv of at least 12 bytes, a new one on each call.
- Match the published AES-256 test vectors for `CBC` and `CTR`.
- Never return a value for a key that isn't valid.
- Error when given `nil`.

## Should

- Error on a key that isn't valid, instead of returning nothing.
