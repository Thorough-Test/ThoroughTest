---
summary: Compresses data into a zstd frame.
---

# zstdcompress

```luau
zstdcompress(data: string, level: number?) -> string
```

Compresses a string with [zstd](https://facebook.github.io/zstd/). It usually makes binary data smaller than [lz4compress](lz4compress.md) does, and the output is a standard zstd frame, so [zstddecompress](zstddecompress.md), Roblox's `EncodingService` and any outside zstd tool can read it.

`level` works like it does in `EncodingService:CompressBuffer`. It goes from -7 to 22, and defaults to 1. Higher levels take longer and make smaller output.

Roblox's `EncodingService` can also compress with zstd, but calling `GetService` on it creates the service, and any game can find it with `FindService`. This function has to do the work itself.

## Parameters

- `data`: The data to compress.
- `level`: Optional. The compression level, from -7 to 22. `1` by default.

## Example

```luau
local SaveData = { Coins = 250, Level = 8 }
local Data = game:GetService("HttpService"):JSONEncode(SaveData)

writefile("Save.zst", zstdcompress(Data, 19))
```

## Must

- Return a standard zstd frame that Roblox's `EncodingService` can decompress.
- Handle text, binary data, null bytes, empty strings and 1MB of data.
- Make smaller output at level 22 than at level 1.
- Work without creating `EncodingService`.

## Should

- Error when given `nil`.
