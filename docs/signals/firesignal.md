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

### What a game script sees

When `firesignal` runs a connection a game script made, the handler is game code and can check where it's running. It has to run at the game's identity, so privileged calls like `game:GetService("CoreGui"):GetChildren()` still error, and its call stack can't hold any of your Luau code. That's how a real fire looks.

## Must

- Run every connection, game scripts' included.
- Run a game script's connection at the game's identity, with no Luau code from the caller in its stack.
- Add no extra frames to a game script's connection stack, even C ones.
- Pass all arguments, including `nil`, and nothing when none are given.
- Work on `GetPropertyChangedSignal` signals.
- Return without waiting for a handler that yields, and let it finish.
- Do nothing on a signal with no connections, without erroring.

## Should

- Start handlers right away when the game's own signals do. In games with deferred signals, waiting is fine.
- Error when given something that isn't a signal.
