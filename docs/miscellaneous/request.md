---
summary: Sends an HTTP request without Roblox's restrictions.
---

# request

```luau
request(options: {
    Url: string,
    Method: string?,
    Headers: { [string]: string }?,
    Cookies: { [string]: string }?,
    Body: string?,
}) -> {
    Success: boolean,
    StatusCode: number,
    StatusMessage: string,
    Headers: { [string]: string },
    Body: string,
}
```

Sends a request to any url and yields until the response arrives. Unlike `HttpService`, it can reach any site and send any header. The game keeps running while it waits.

A response like `404` isn't an error. It returns a normal response with `Success` set to `false`.

`http_request` and `http.request` are the same function under other names.

## Parameters

- `options`: The request. Only `Url` is required, and `Method` defaults to `GET`.

## Example

### Reading JSON

```luau
local HttpService = game:GetService("HttpService")

local Response = request({ Url = "https://httpbin.org/get" })

print(Response.StatusCode) -- 200
print(HttpService:JSONDecode(Response.Body).url) -- https://httpbin.org/get
```

### Sending JSON

```luau
local Response = request({
    Url = "https://httpbin.org/post",
    Method = "POST",
    Headers = { ["Content-Type"] = "application/json" },
    Body = game:GetService("HttpService"):JSONEncode({ Score = 100 }),
})
```

## Must

- Return every response field with the right type.
- Support `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD` and `OPTIONS`, with `GET` as the default.
- Send custom headers and a `User-Agent`.
- Return error statuses as responses, with `Success` set to `false`.
- Return response headers.
- Keep the game running while it waits.
- Keep binary data intact in both directions.
- Follow redirects and decompress gzip.
- Error with no arguments, and never report success for an invalid url.

## Should

- Send `Roblox-Game-Id` as the current `game.JobId`.
- Include the executor name in the `User-Agent`.
- Support the `Cookies` option.
- Have `http_request` and `http.request` as aliases.
