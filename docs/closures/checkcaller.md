---
summary: Tells you whether the code that's running came from the executor.
---

# checkcaller

```luau
checkcaller() -> boolean
```

Returns `true` when the current thread belongs to the executor, and `false` when it belongs to the game.

You'll mostly use this inside hooks. Your hook runs for everyone, so this is how you leave your own calls alone while changing what game scripts receive.

## Example

```luau
local originalIndex
originalIndex = hookmetamethod(game, "__index", function(self, key)
    if key == "WalkSpeed" and not checkcaller() then
        return 16 -- only game scripts receive this
    end
    return originalIndex(self, key)
end)
```

## Must

- Return `true` on the executor's own thread.
- Return `true` inside `task.spawn`, `task.delay`, `task.defer` and the executor's own signal connections.
- Return `true` in a metamethod hook when the executor made the call.
- Return `false` in a metamethod hook when a game script made the call.
