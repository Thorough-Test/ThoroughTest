---
summary: Wraps a Luau function so it acts like a C function.
---

# newcclosure

```luau
newcclosure(target: function, debugName: string?) -> function
```

Wraps a Luau function in a C closure. The wrapper looks like a C function to game scripts: `[C]` in `debug.info`, 0 parameters, and nothing of the wrapped function in their stack.

The goal is that a game script can't tell it from a real C function. Executor debug functions may still show the wrapped function as the wrapper's upvalue. Game scripts can't read upvalues, so that is allowed. That covers the tricky parts too, like yielding and being canceled.

## Parameters

- `target`: The function to wrap.
- `debugName`: Optional. The name shown by `debug.info`.

## Example

```luau
local function Secret()
    return "ok"
end

local Wrapped = newcclosure(Secret)

print(iscclosure(Wrapped)) -- true
print(debug.info(Wrapped, "s")) -- [C]
print(Wrapped()) -- ok
```

### What a game script sees

A game script can run `debug.info` on any function it's handed. For the wrapper it has to get what a real C function gives: source `[C]`, line `-1`, 0 parameters and a vararg. When the wrapper calls something that errors, the game's error handler can also walk the call stack, and it must find no frame from your Luau function.

A `pcall` inside your function should still catch its own errors. If one gets past it, the error reaches the game script that called the wrapper.

## Must

- Return a new function that counts as a C closure and shows `[C]` in `debug.info`, for game scripts too.
- Show 0 parameters and a vararg in a game script's `debug.info`, like a real C function.
- Keep the wrapped Luau function out of a game script's stack.
- Keep every argument and return value, nils included.
- Run on the caller's thread.
- Let the function yield, and pass values through `coroutine.yield`.
- Keep error messages and error objects the same, including errors after a yield.
- Stop when `task.cancel` cancels a thread yielding inside it.
- Work as a metamethod and as a signal handler.
- Work when wrapped again, and inside 150 nested `coroutine.wrap` calls.

## Should

- Let a `pcall` inside the function catch errors, the same as in a normal call.
- Keep line numbers out of error messages, since real C functions don't have them.
- Wrap C functions too.
- Show the debug name in `debug.info`.
- Error when given something that isn't a function.
