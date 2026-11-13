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
local function Inner()
    for Level, Frame in debug.getcallstack() do
        print(Level, debug.info(Frame.func, "n"), Frame.currentline)
    end
end

local function Outer()
    Inner()
end

Outer()
-- 1 Inner 3
-- 2 Outer 9
-- 3 ...
```

## Must

- Put the calling function in frame 1 and its caller in frame 2.
- Return the right `currentline` for Luau frames.
- Include a `func` in every frame.
- Never return a line number for a C function.
- Read a paused thread's stack when one is passed, with the paused function in it.

## Should

- Include C functions like `pcall` on the stack.
