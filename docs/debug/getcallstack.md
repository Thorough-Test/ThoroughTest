---
summary: Lists every function on a thread's call stack.
---

# debug.getcallstack

```luau
debug.getcallstack(thread: thread?) -> { { func: function, currentline: number? } }
```

Returns one entry per frame, starting with the function that called `getcallstack`. Each frame has `func`, and `currentline` when the function is Luau.

Pass a thread to read a paused thread's stack instead of your own.

## Parameters

- `thread`: Optional. The thread to read. Defaults to the current one.

## Example

```luau
local function inner()
    for level, frame in debug.getcallstack() do
        print(level, debug.info(frame.func, "n"), frame.currentline)
    end
end

local function outer()
    inner()
end

outer()
-- 1 inner 3
-- 2 outer 9
-- 3 ...
```

## Must

- Put the calling function in frame 1 and its caller in frame 2.
- Return the right `currentline` for Luau frames.
- Include a `func` in every frame.
- Never return a line number for a C function.
- Include a paused function in its thread's call stack.

## Should

- Include C functions like `pcall` on the stack.
