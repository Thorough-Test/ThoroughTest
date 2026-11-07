---
summary: Decrypts text made by crypt.encrypt or anything else using AES.
---

# crypt.decrypt

```luau
crypt.decrypt(data: string, key: string, iv: string, mode: string?) -> string
```

Decrypts AES data. The data, key and iv are all base64, the same way [crypt.encrypt](crypt-encrypt.md) returns them, and the plain data is returned.

## Parameters

- `data`: The encrypted data, as base64.
- `key`: The key, as base64.
- `iv`: The iv from when it was encrypted, as base64.
- `mode`: Optional. The same mode it was encrypted with. `"CBC"` by default.

## Example

```luau
local Key = base64encode(string.rep("k", 32))

local Encrypted, Iv = crypt.encrypt("secret text", Key)
print(crypt.decrypt(Encrypted, Key, Iv)) -- secret text
```

## Must

- Return the original bytes in `CBC` and `CTR`, and with the default mode.
- Match the published AES-256 test vector.
- Never return the original text with the wrong key.
- Never return a value for a key that isn't valid.
- Error when given `nil`.

## Should

- Support `CFB`, `OFB`, `ECB` and `GCM`.
- Error on a key that isn't valid, instead of returning nothing.
