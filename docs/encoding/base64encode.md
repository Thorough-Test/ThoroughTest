---
summary: Turns data into base64 text.
---

# base64encode

```luau
base64encode(data: string) -> string
```

Encodes a string as base64, which is a safe way to send binary data through something that only handles text. `base64_encode` is also accepted.

## Parameters

- `data`: The data to encode.

## Example

```luau
print(base64encode("Hello World!")) -- SGVsbG8gV29ybGQh
```

## Must

- Match the standard output, padding included, for text and for strings with null bytes.
- Match the standard output for all 256 byte values.
- Encode an empty string as an empty string.
- Never add line breaks to long output.

## Should

- Error when given `nil`.
