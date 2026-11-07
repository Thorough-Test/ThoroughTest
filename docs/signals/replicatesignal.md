---
summary: Fires a replicating signal on the server.
---

# replicatesignal

```luau
replicatesignal(signal: RBXScriptSignal, ...any) -> ()
```

Sends a signal to the server as if the client's engine had sent it. Only signals that replicate work, and the arguments have to match what the signal takes, so check with [getsignalarguments](getsignalarguments.md).

## Parameters

- `signal`: The signal.
- `...`: Exactly the arguments the signal takes.

## Example

```luau
local detector = workspace.Button.ClickDetector

replicatesignal(detector.MouseActionReplicated, game.Players.LocalPlayer, 0)
```

## Must

- Reach the server.
- Work with the right arguments.
- Error on missing arguments or the wrong types.
- Error on a signal that can't replicate.
- Error when given something that isn't a signal.
