---
summary: Runs a signal's connections.
---

# firesignal

```luau
firesignal(signal: RBXScriptSignal, ...any) -> ()
```

Runs every connection on a signal with the arguments you pass, on your client only. Nothing goes to the server, and the real event doesn't happen.

It doesn't wait for handlers to finish, so a handler that yields won't block the call.

## Parameters

- `signal`: The signal to fire.
- `...`: Arguments for the handlers.

## Example

```luau
local Button = game.Players.LocalPlayer.PlayerGui.Shop.BuyButton

firesignal(Button.MouseButton1Click)
```

## Must

- Run every connection, game scripts' included.
- Pass all arguments, including `nil`, and nothing when none are given.
- Work on `GetPropertyChangedSignal` signals.
- Return without waiting for a handler that yields, and let it finish.
- Do nothing on a signal with no connections, without erroring.

## Should

- Start handlers right away. Waiting for deferred signals is fine, so this is only a warning.
- Error when given something that isn't a signal.
