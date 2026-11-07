---
summary: Decompresses an LZ4 block.
---

# lz4decompress

```luau
lz4decompress(data: string, size: number) -> string
```

Turns an LZ4 block back into the original data. `size` is the length of the original.

## Parameters

- `data`: The compressed block.
- `size`: The original length.

## Example

```luau
local text = "Hello, world! Hello, world!"
local compressed = lz4compress(text)

print(lz4decompress(compressed, #text)) -- Hello, world! Hello, world!
```

## Must

- Return text, binary data and runs of null bytes exactly.
- Read blocks made by other LZ4 tools, with literals and matches.
- Handle 1MB of data.
- Error when given `nil`.

## Should

- Ignore a `size` larger than the decompressed data.
- Not return data for a `size` smaller than the decompressed data.
