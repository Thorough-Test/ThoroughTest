---
summary: Connects to a WebSocket server.
---

# WebSocket.connect

```luau
WebSocket.connect(url: string) -> WebSocket
```

Connects to a `ws://` or `wss://` server and yields until it's ready. If it can't connect, it errors.

| Member | What it does |
| --- | --- |
| `Send(message)` | Sends a message. |
| `Close()` | Closes the connection. |
| `OnMessage` | Fires with the message, and with `true` as a second value if it's binary. |
| `OnClose` | Fires once when the connection closes. |
| `IsClosed` | `true` once the connection has closed. |

## Parameters

- `url`: The server's address.

## Example

```luau
local Socket = WebSocket.connect("wss://ws.postman-echo.com/raw")

Socket.OnMessage:Connect(function(Message)
    print("Got:", Message) -- Got: hello
    Socket:Close()
end)

Socket.OnClose:Connect(function()
    print("Closed")
end)

Socket:Send("hello")
```

## Must

- Connect to `wss://` servers.
- Have `Send`, `Close`, `OnMessage` and `OnClose`.
- Deliver messages without marking text as binary.
- Keep messages in order, even when they're sent one right after another.
- Keep unicode intact.
- Fire `OnClose` exactly once.
- Have `IsClosed`, starting as `false` and set to `true` after closing.
- Handle a 60KB message.
- Never return a socket for an invalid url, or when nothing is listening.

## Should

- Error on an invalid url, or when nothing is listening, instead of returning nothing.
- Let a second `Close` do nothing.
