---
summary: Checks whether a function is a Luau closure.
---

# islclosure

```luau
islclosure(target: function) -> boolean
```

Returns `true` for functions written in Luau and `false` for C functions. It's the opposite of [iscclosure](iscclosure.md).

This is a useful check before calling something like `debug.getconstants`, which only works on Luau functions.

## Parameters

- `target`: The function to check.

## Example

```luau
print(islclosure(function() end)) -- true
print(islclosure(print)) -- false
print(islclosure(newcclosure(function() end))) -- false
```

## Must

- Return `true` for Luau functions, including game script closures.
- Return `false` for C functions, Roblox methods and `newcclosure` wrappers.

## Should

- Error when given something that isn't a function.
