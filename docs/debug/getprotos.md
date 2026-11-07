---
summary: Lists every function nested directly inside a function.
---

# debug.getprotos

```luau
debug.getprotos(target: function | number) -> { function }
```

Returns the protos in the order they're written in the code. Like [debug.getproto](getproto.md), these are blueprints, and calling one won't run its code.

## Parameters

- `target`: A Luau function, or a stack level.

## Example

```luau
local function Outer()
    local function First()
        return "first"
    end
    local function Second()
        return "second"
    end
    return First, Second
end

for Index, Proto in debug.getprotos(Outer) do
    print(Index, debug.getconstants(Proto)[1])
end
-- 1 first
-- 2 second
```

## Must

- List protos in the order they're written.
- Return an empty table for a function with none.
- Never run a proto's code when it's called.
- Read game scripts.
- Never list protos for a C function.

## Should

- Error on C functions, instead of returning nothing.
