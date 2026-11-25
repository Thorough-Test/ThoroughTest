---
summary: Decompresses a zstd frame.
---

# zstddecompress

```luau
zstddecompress(data: string) -> string
```

Turns a zstd frame back into the original data. The frame can come from [zstdcompress](zstdcompress.md), Roblox's `EncodingService` or any outside zstd tool. Unlike [lz4decompress](lz4decompress.md), it doesn't need the original size, because the frame records it.

Like zstdcompress, it has to work without creating `EncodingService`, since any game can find that service once it exists.

## Parameters

- `data`: The zstd frame.

## Example

```luau
local Data = zstddecompress(readfile("Save.zst"))
local SaveData = game:GetService("HttpService"):JSONDecode(Data)
```

## Must

- Return text, binary data, null bytes and 1MB of data exactly.
- Return an empty string for an empty frame.
- Read frames made by Roblox's `EncodingService`, including ones with uncompressed blocks or a checksum.
- Never return data for a frame with a wrong checksum, a frame that's cut off, or data that isn't zstd.
- Work without creating `EncodingService`.

## Should

- Error on a bad frame instead of returning nothing.
- Error when given `nil`.
