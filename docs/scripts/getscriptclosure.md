---
summary: Builds a function from a script's bytecode.
---

# getscriptclosure

```luau
getscriptclosure(script: LuaSourceContainer) -> function
```

Builds a new Luau function from a script's bytecode. It's a fresh closure of the script's main function, separate from the one that's running, and you can inspect it with the debug library without waiting for the script to do anything.

## Parameters

- `script`: The script.

## Example

```luau
local Closure = getscriptclosure(game.Players.LocalPlayer.Character.Animate)

for _, Constant in debug.getconstants(Closure) do
    print(Constant)
end
```

## Must

- Return a Luau closure with the script's constants in it.
- Work on LocalScripts and ModuleScripts.
- Never return a value for a script with no bytecode.
- Error when given something that isn't a script.

## Should

- Return a new closure on each call.
- Set `script` in the closure's environment to the script it came from.
- Error on a script with no bytecode, instead of returning nothing.
