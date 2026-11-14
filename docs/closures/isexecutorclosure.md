---
summary: Checks whether a function came from the executor instead of the game.
---

# isexecutorclosure

```luau
isexecutorclosure(target: function) -> boolean
```

Returns `true` for functions made by the executor or by your scripts, and `false` for functions from Roblox or the game. It's the quick way to tell your functions apart from everything else, such as when you're scanning [getgc](../environment/getgc.md).

## Parameters

- `target`: The function to check.

## Example

```luau
print(isexecutorclosure(getgenv)) -- true
print(isexecutorclosure(function() end)) -- true
print(isexecutorclosure(newcclosure(function() end))) -- true
print(isexecutorclosure(loadstring("return 1"))) -- true

print(isexecutorclosure(print)) -- false
print(isexecutorclosure(game.IsA)) -- false
```

### Game script functions

A function defined inside a game script is the game's, even when you reach it from the executor. It has to stay `false` after you've hooked and restored it.

```luau
local Animate = game:GetService("Players").LocalPlayer.Character.Animate
local OnClimbing = getsenv(Animate).onClimbing
print(isexecutorclosure(OnClimbing)) -- false
```

## Must

- Return `true` for functions you write, `newcclosure` wrappers, `loadstring` chunks and executor functions.
- Return `false` for Roblox globals, Roblox methods and functions from game scripts.

## Should

- Return `true` for the result of `getscriptclosure`, since the executor created that closure.
- Error when given something that isn't a function.
