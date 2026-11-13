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
local Coins, Inventory = 100, {}

local function Buy(Item)
    Coins -= 1
    table.insert(Inventory, Item)
end

for Index, Value in debug.getupvalues(Buy) do
    print(Index, Value)
end
-- 1 100
-- 2 table: 0x...
```

## Must

- List every upvalue with its real value.
- Return an empty table for a function with none.
- Read functions from game scripts.
- Never show what's inside a C function like `print` or a `newcclosure` wrapper.

## Should

- Error on C functions, instead of returning an empty table.
- Error on a `coroutine.wrap` function, instead of returning the thread inside it.
