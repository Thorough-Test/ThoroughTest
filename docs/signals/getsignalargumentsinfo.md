---
summary: Lists the names and types of a signal's arguments.
---

# getsignalargumentsinfo

```luau
getsignalargumentsinfo(signal: RBXScriptSignal) -> { { Name: string, Type: string } }
```

Like [getsignalarguments](getsignalarguments.md), with the argument names too.

## Parameters

- `signal`: The signal.

## Example

```luau
local Argument = getsignalargumentsinfo(game.Players.PlayerAdded)[1]

print(Argument.Name, Argument.Type) -- player Instance
```

## Must

- Return the right `Name` and `Type` for each argument.
- Return an empty table for a signal with no arguments.
- Match `getsignalarguments`.

## Should

- Error without a signal.
