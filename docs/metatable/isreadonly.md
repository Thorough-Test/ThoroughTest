---
summary: Checks whether a table is read only.
---

# isreadonly

```luau
isreadonly(target: table) -> boolean
```

Returns `true` for tables you can't write to, like frozen tables and `game`'s metatable.

## Parameters

- `target`: The table to check.

## Example

```luau
print(isreadonly({})) -- false
print(isreadonly(table.freeze({}))) -- true
print(isreadonly(getrawmetatable(game))) -- true
```

## Must

- Return `false` for normal tables.
- Return `true` for frozen tables and `game`'s metatable.
- Error when given something that isn't a table.
