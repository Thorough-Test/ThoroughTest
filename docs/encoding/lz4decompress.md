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
local Text = "Hello, world! Hello, world!"
local Compressed = lz4compress(Text)

print(lz4decompress(Compressed, #Text)) -- Hello, world! Hello, world!
```

## Must

- Return text, binary data and runs of null bytes exactly.
- Read blocks made by other LZ4 tools, with literals and matches.
- Handle 1MB of data.

## Should

- Ignore a `size` larger than the decompressed data.
- Not return data for a `size` smaller than the decompressed data.
- Error when given `nil`.
