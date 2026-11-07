---
summary: Lists the argument types a signal passes.
---

# getsignalarguments

```luau
getsignalarguments(signal: RBXScriptSignal) -> { string }
```

Returns the type name of each argument the signal passes to its handlers. If you need names as well, use [getsignalargumentsinfo](getsignalargumentsinfo.md).

## Parameters

- `signal`: The signal.

## Example

```luau
print(getsignalarguments(game.Players.PlayerAdded)[1]) -- Instance
```

## Must

- Return one type name per argument.
- Return an empty table for a signal with no arguments.
- Error without a signal.
