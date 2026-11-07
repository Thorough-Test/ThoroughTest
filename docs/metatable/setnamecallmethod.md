---
summary: Sets the method name for the next __namecall.
---

# setnamecallmethod

```luau
setnamecallmethod(method: string) -> ()
```

Changes the method name of the current `__namecall`. Any method you call from inside a hook replaces the current name, so this is how you put it back afterward.

## Parameters

- `method`: The method name.

## Example

```luau
local OriginalNamecall
OriginalNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    local Method = getnamecallmethod()
    if self == workspace and not checkcaller() then
        print(self:GetFullName())
        setnamecallmethod(Method)
    end
    return OriginalNamecall(self, ...)
end)
```

## Must

- Change what `getnamecallmethod` returns.
- Make `game`'s `__namecall` run the method that was set.
- Let a hook call another method and restore the name.
- Error when the name isn't a string.
