---
summary: Changes a constant in a function's code.
---

# debug.setconstant

```luau
debug.setconstant(target: function | number, index: number, value: any) -> ()
```

Replaces a constant, so the function behaves as if its code had a different value in it. The change applies to everything sharing that function's code.

## Parameters

- `target`: A Luau function, or a stack level.
- `index`: The position of the constant.
- `value`: The new value.

## Example

```luau
local function Greet()
    return "hello"
end

local Index = table.find(debug.getconstants(Greet), "hello")
debug.setconstant(Greet, Index, "goodbye")

print(Greet()) -- goodbye
```

## Must

- Change string and number constants so the function really uses the new value.
- Change a property name constant, so `game.Name` reads a different property.
- Work with a stack level.
- Never write past the last constant or to a C function.

## Should

- Error on an index past the end and on C functions, instead of doing nothing.
