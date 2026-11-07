---
summary: Changes one of a function's upvalues.
---

# debug.setupvalue

```luau
debug.setupvalue(target: function | number, index: number, value: any) -> ()
```

Changes an upvalue, which is the actual variable, not a copy. The new value applies to the function and anything else sharing that variable.

## Parameters

- `target`: A Luau function, or a stack level.
- `index`: The position of the upvalue.
- `value`: The new value. It doesn't need to be the same type.

## Example

```luau
local coins = 0

local function addCoin()
    coins += 1
    return coins
end

debug.setupvalue(addCoin, 1, 500)

print(addCoin()) -- 501
print(coins) -- 501
```

## Must

- Change the real variable, in both the function and its scope.
- Allow a value of a different type.
- Change the upvalue in every function that shares it.
- Work with a stack level.
- Write to functions from game scripts.
- Never write past the last upvalue, to a function with none, or to a C function.

## Should

- Error in those cases, instead of doing nothing.
