---
summary: Lists a function's upvalues.
---

# debug.getupvalues

```luau
debug.getupvalues(target: function | number) -> { any }
```

Returns every upvalue the function uses, in the same order as [debug.getupvalue](getupvalue.md).

## Parameters

- `target`: A Luau function, or a stack level.

## Example

```luau
local coins, inventory = 100, {}

local function buy(item)
    coins -= 1
    table.insert(inventory, item)
end

for index, value in debug.getupvalues(buy) do
    print(index, value)
end
-- 1 100
-- 2 table: 0x...
```

## Must

- List every upvalue with its real value.
- Return an empty table for a function with none.
- Read functions from game scripts.
- Never show what's inside a C function, including `coroutine.wrap` functions and `newcclosure` wrappers.

## Should

- Error on C functions, instead of returning an empty table.
