---
summary: Compresses data into an LZ4 block.
---

# lz4compress

```luau
lz4compress(data: string) -> string
```

Compresses a string with LZ4. Save the original length too, because [lz4decompress](lz4decompress.md) needs it.

## Parameters

- `data`: The data to compress.

## Example

```luau
local Text = string.rep("hello ", 100)
local Compressed = lz4compress(Text)

print(#Text, #Compressed) -- 600 21
```

## Must

- Return a string that's smaller than repetitive input.
- Produce real LZ4 blocks that any decoder can read.
- Handle binary data and empty strings.
- Error when given `nil`.
