---
summary: Calls a function under a call stack and thread you make up.
---

# trampoline_call

```luau
trampoline_call(
    target: function,
    callstack: { { func: function, currentline: number } },
    options: { thread: thread?, identity: number?, script: LuaSourceContainer?, env: table? },
    ...any
) -> (boolean, ...any)
```

Runs a function so it looks like something else called it. Anything inspecting the stack from inside, like `debug.info` or an anti-cheat's own checks, finds the frames you provide.

It works like `pcall`. It returns `true` and the results, or `false` and the error.

The fake frames are never called. They only exist to be looked at. Frame 1 is the closest caller.

| Option | What it does |
| --- | --- |
| `thread` | The parent thread. `coroutine.running()` returns it, and the function inherits its identity and script. |
| `identity` | The thread identity to run at. |
| `script` | What `getcallingscript` returns. |
| `env` | The environment to run with. |

## Parameters

- `target`: The function to call.
- `callstack`: The frames to show, closest caller first.
- `options`: The options above. Pass `{}` for none.
- `...`: Arguments for the function.

## Example

```luau
local function checkCaller()
    print(debug.info(2, "n"), debug.info(2, "l"))
end

local function fromGameCode() end

trampoline_call(checkCaller, {
    { func = fromGameCode, currentline = 118 },
}, {})
-- fromGameCode 118
```

## Must

- Return `true` and every result, nils included, or `false` and the error, unchanged.
- Call C functions too.
- Show the frames in order, closest caller first, with the right function and line.
- Never call a fake frame's function.
- Accept a stack from `debug.getcallstack`.
- Honor `thread` without running or resuming it, and inherit its identity.
- Honor `script`, `identity` and `env`.
- Leave the caller's identity alone.
- Error when an argument is missing, a frame has no `func` or `currentline`, or `script` isn't a script.

## Should

- Let the function yield.
- Give `thread` priority over `identity` and `script`.
