---
summary: Hashes a script's bytecode.
---

# getscripthash

```luau
getscripthash(script: LuaSourceContainer) -> string
```

Returns a SHA384 hash of a script's bytecode, as 96 hex characters. Save it and compare it later to find out whether a game update changed the script.

## Parameters

- `script`: The script.

## Example

```luau
local Animate = game.Players.LocalPlayer.Character.Animate
local Hash = getscripthash(Animate)

if isfile("animate.hash") and readfile("animate.hash") ~= Hash then
    print("Animate changed")
end
writefile("animate.hash", Hash)
```

## Must

- Return a SHA384 hash as a 96 character hex string.
- Return the same hash for the same script and for a clone of it.
- Return different hashes for different scripts.
- Work on Scripts with `RunContext` set to `Client`.
- Never return a value for a script with no bytecode.
- Error when given something that isn't a script.

## Should

- Return the SHA384 of the bytes `getscriptbytecode` returns.
- Error on a script with no bytecode, instead of returning nothing.
