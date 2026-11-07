---
summary: Gets a metatable, ignoring the __metatable lock.
---

# getrawmetatable

```luau
getrawmetatable(object: any) -> table?
```

`getmetatable` stops at the `__metatable` field. This one doesn't, so it returns the real table.

## Parameters

- `object`: Anything.

## Example

```luau
local metatable = getrawmetatable(game)

print(metatable.__index(game, "Workspace")) -- Workspace
```

## Must

- Bypass the `__metatable` field without changing what `getmetatable` returns.
- Return a working metatable for `game`.
- Return the metatable of proxies, strings and Vector3s.
- Return `nil` for values with no metatable, like plain tables and numbers.
- Error with no arguments.
