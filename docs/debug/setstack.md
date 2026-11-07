---
summary: Changes a local in a running function.
---

# debug.setstack

```luau
debug.setstack(level: number, index: number, value: any) -> ()
debug.setstack(thread: thread, level: number, index: number, value: any) -> ()
```

Writes one slot on a function's stack. Use [debug.getstack](getstack.md) to find the slot. The function keeps running with the new value.

## Parameters

- `thread`: Optional. A paused thread.
- `level`: The stack level.
- `index`: The position to write.
- `value`: The new value.

## Example

```luau
local function greet()
    local player = { name = "me" }
    local stranger = { name = "someone else" }

    debug.setstack(1, table.find(debug.getstack(1), player), stranger)

    print(player.name) -- someone else
end

greet()
```

## Must

- Change a local at level 1 and leave the ones next to it alone.
- Change a caller's local at level 2.
- Replace a function on the stack so calling it runs the new one.
- Change a local on a paused thread, and keep that change when it resumes.
- Never write to a C function's level, a level that doesn't exist or an index past the end.

## Should

- Error in those cases, instead of doing nothing.
