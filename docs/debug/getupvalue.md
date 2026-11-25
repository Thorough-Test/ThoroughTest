---
summary: Gets one upvalue from a function.
---

# debug.getupvalue

```luau
debug.getupvalue(target: function | number, index: number) -> any
```

Returns the upvalue at `index`, starting at 1. Upvalues are numbered by the order the function first uses them.

## Parameters

- `target`: A Luau function, or a stack level.
- `index`: The position of the upvalue.

## Example

```luau
local Coins = 169

local function AddCoin()
    Coins += 1
end

print(debug.getupvalue(AddCoin, 1)) -- 169
```

## Must

- Return the right value, for tables and numbers alike.
- Work with a stack level.
- Never return a value for an index past the end, index 0, a function with no upvalues, or a C function like `print`. A `newcclosure` wrapper may return the function it wraps, since that is its real upvalue.
