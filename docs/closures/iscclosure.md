---
summary: Checks whether a function is a C closure.
---

# iscclosure

```luau
iscclosure(target: function) -> boolean
```

Returns `true` for C functions and `false` for Luau functions. A function wrapped with [newcclosure](newcclosure.md) counts as C. The opposite check is [islclosure](islclosure.md).

## Parameters

- `target`: The function to check.

## Example

```luau
print(iscclosure(print)) -- true
print(iscclosure(function() end)) -- false
print(iscclosure(newcclosure(function() end))) -- true
```

## Must

- Return `true` for global C functions, Roblox methods and itself.
- Return `true` for `newcclosure` and `coroutine.wrap` functions.
- Return `false` for Luau functions.
- Error when given something that isn't a function.
