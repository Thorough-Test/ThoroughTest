---
summary: Gets the global table of a running script.
---

# getsenv

```luau
getsenv(script: LuaSourceContainer) -> { [any]: any }
```

Returns a running script's environment, with the globals it declared. Writing to it reaches the running script, so you can change its values and swap its functions.

> **Note:** Only globals are here. Anything declared with `local` isn't in this table. [debug.getupvalues](../debug/getupvalues.md) can reach those.

## Parameters

- `script`: A running script, even one parented to `nil`.

## Example

```luau
local Environment = getsenv(game.Players.LocalPlayer.Character.Animate)

print(Environment.script) -- Animate
print(Environment.onSwimming) -- function: 0x...
```

## Must

- Return the script's real environment, with `script` and its globals.
- Still find a running script after it parents itself to `nil`, the way anti-cheats hide, and pass writes through to it.
- Pass writes through to the running script.
- Never return a value for a script that isn't running.
- Never return a value for an Instance that isn't a script.

## Should

- Return the same table for the same script.
- Error on a script that isn't running or an Instance that isn't a script, instead of returning nothing.
- Error when given something that isn't an Instance.
