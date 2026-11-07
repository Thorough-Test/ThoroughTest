---
summary: Gets the script that's calling your code.
---

# getcallingscript

```luau
getcallingscript() -> LuaSourceContainer?
```

Returns the script that the current thread belongs to. On your own threads it's `nil`, so it's mostly useful inside hooks, where it tells you which game script made the call.

## Example

```luau
local OriginalNamecall
OriginalNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    if getnamecallmethod() == "FireServer" and not checkcaller() then
        print(getcallingscript(), "fired", self.Name)
    end
    return OriginalNamecall(self, ...)
end)
```

## Must

- Return `nil` on an executor thread.
- Return the game script when a game script is the caller, including inside a hook.
