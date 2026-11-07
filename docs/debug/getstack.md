---
summary: Reads the locals of a running function.
---

# debug.getstack

```luau
debug.getstack(level: number, index: number?) -> any
debug.getstack(thread: thread, level: number, index: number?) -> any
```

Returns the values on a function's stack, which is where its locals and temporary values live. Leave out `index` to get them all as a table.

Pass a thread first to read a paused thread instead of your own.

Compilers can move values around, so don't rely on a local being at a fixed index. Look for the value you want instead.

## Parameters

- `thread`: Optional. A paused thread.
- `level`: The stack level.
- `index`: Optional. One position to read.

## Example

```luau
local function Secret()
    local Password = {}
    Password.Value = "swordfish"

    for _, Value in debug.getstack(1) do
        if type(Value) == "table" then
            print(Value.Value) -- swordfish
        end
    end
end

Secret()
```

## Must

- Return the whole frame as a table when there's no index.
- Include the function's own locals.
- Return the same value at an index as the full stack has there.
- Read the caller at level 2.
- Read a paused thread when it's passed first.
- Never return a value for a C function's level or a level that doesn't exist.

## Should

- Error on those levels, instead of returning nothing.
