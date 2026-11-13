---
summary: Gets a script's compiled bytecode.
---

# getscriptbytecode

```luau
getscriptbytecode(script: LuaSourceContainer) -> string
```

Returns the Luau bytecode the client received for a script. Decompilers read this, and so can you. It contains the script's strings.

## Parameters

- `script`: The script.

## Example

```luau
local Bytecode = getscriptbytecode(game.Players.LocalPlayer.Character.Animate)

print(#Bytecode)
```

## Must

- Return the script's real bytecode, with its strings in it.
- Return the same bytes every time.
- Never return a value for a script with no bytecode.
- Never return a value for an Instance that isn't a script.

## Should

- Error on a script with no bytecode or an Instance that isn't a script, instead of returning nothing or an empty string.
- Error when given something that isn't an Instance.
