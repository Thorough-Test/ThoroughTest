---
summary: Gets a function nested inside another function.
---

# debug.getproto

```luau
debug.getproto(target: function | number, index: number, activated: boolean?) -> function | { function }
```

By default, this returns a read-only copy of the nested function. You can inspect it with the other debug functions, but it's a blueprint, not a live function, and calling it won't run its code.

With `activated` set to `true`, it returns a table of the real closures that exist right now, which you can call or hook.

## Parameters

- `target`: A Luau function, or a stack level.
- `index`: Which nested function, in the order they're written.
- `activated`: Optional. Get the live closures instead of the proto.

## Example

```luau
local function Outer()
    local function Inner()
        return "inner ran"
    end
    return Inner
end

local Proto = debug.getproto(Outer, 1)
print(debug.getconstants(Proto)[1]) -- inner ran

local Live = Outer()
print(debug.getproto(Outer, 1, true)[1] == Live) -- true
```

## Must

- Return a proto you can use with `debug.getconstants` and `debug.getinfo`.
- Never run the proto's code when it's called.
- Return live closures with `activated`, and none before any exist.
- Work with a stack level.
- Work on protos, so nested protos can be read.
- Never return a value for an index past the end or for a C function.

## Should

- Error on an index past the end and on C functions, instead of returning nothing.
