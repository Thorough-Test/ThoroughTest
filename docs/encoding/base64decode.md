---
summary: Turns base64 text back into data.
---

# base64decode

```luau
base64decode(data: string) -> string
```

The opposite of [base64encode](base64encode.md). `base64_decode` is also accepted.

## Parameters

- `data`: The base64 text.

## Example

```luau
print(base64decode("SGVsbG8gV29ybGQh")) -- Hello World!
```

## Must

- Decode standard base64 correctly, padding included.
- Return all 256 byte values unchanged.
- Handle 300KB of data.

## Should

- Error when given `nil`.
