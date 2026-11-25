---
summary: Downloads a url and returns the body as a string.
---

# HttpGet

```luau
game:HttpGet(url: string, noCache: boolean?) -> string
```

Downloads a url and returns the body as a string. Almost every script loads this way, with `loadstring(game:HttpGet(url))()`. It yields until the response arrives, and the game keeps running while it waits.

The executor adds it to `game` for your scripts only. To a game script, `HttpGet` is a member that doesn't exist.

`noCache` works like it does in `HttpService:GetAsync`. Pass `true` to always download a new copy, so a script picks up an update as soon as it's pushed. Without it, the executor may return a cached response.

For headers, other methods or the status code, use [request](request.md).

## Parameters

- `url`: The url to download.
- `noCache`: `true` to skip any cached response. Defaults to `false`.

## Example

### Loading a script

```luau
loadstring(game:HttpGet("https://example.com/hub.lua", true))()
```

### Saving an image

```luau
writefile("Logo.png", game:HttpGet("https://example.com/logo.png"))
```

## Must

- Return the body as a string, without changing binary data.
- Work when called with a dot, as `game.HttpGet(game, url)`.
- Follow redirects.
- Return large responses in full.
- Send a `User-Agent` header.
- Decompress a response when the request asked for gzip.
- Keep the game running while the request is in flight.
- Download a new copy every time `noCache` is `true`.
- Error for a game script the same way a missing member does, through both `game.HttpGet` and `game:HttpGet`, raised by the same function and with no Luau code in its stack.
- Never return a value for an invalid url or a url that isn't a string.

## Should

- Error on an invalid url, instead of returning nothing.
