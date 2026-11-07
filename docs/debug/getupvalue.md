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
local coins = 100

local function addCoin()
    coins += 1
end

print(debug.getupvalue(addCoin, 1)) -- 100
```

## Must

- Return the right value, for tables and numbers alike.
- Work with a stack level.
- Never return a value for an index past the end, index 0, a function with no upvalues, or a C function.

## Should

- Error in those cases, instead of returning nothing.
