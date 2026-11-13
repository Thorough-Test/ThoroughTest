---
summary: Wraps a Luau function so it acts like a C function.
---

# newcclosure

```luau
newcclosure(target: function, debugName: string?) -> function
```

Wraps a Luau function in a C closure. The wrapper looks like a C function to anything that inspects it: no upvalues, no constants, and `[C]` in `debug.info`.

The goal is that you can't tell it from a real C function. That covers the tricky parts too, like yielding and being canceled.

## Parameters

- `target`: The function to wrap.
- `debugName`: Optional. The name shown by `debug.info`.

## Example

```luau
local function Secret()
    return "still works"
end

local Wrapped = newcclosure(Secret)

print(iscclosure(Wrapped)) -- true
print(debug.info(Wrapped, "s")) -- [C]
print(Wrapped()) -- still works
```

## Must

- Return a new function that counts as a C closure and shows `[C]` in `debug.info`.
- Keep every argument and return value, nils included.
- Hide the wrapped function's upvalues.
- Run on the caller's thread.
- Let the function yield, and pass values through `coroutine.yield`.
- Keep error messages and error objects the same, including errors after a yield.
- Stop when `task.cancel` cancels a thread yielding inside it.
- Work as a metamethod and as a signal handler.
- Work when wrapped again, and inside 150 nested `coroutine.wrap` calls.

## Should

- Keep line numbers out of error messages, since real C functions don't have them.
- Wrap C functions too.
- Show the debug name in `debug.info`.
- Error when given something that isn't a function.
