---
summary: Gets the method name of the current __namecall.
---

# getnamecallmethod

```luau
getnamecallmethod() -> string?
```

Inside a `__namecall` hook, every method call looks the same. This tells you which method it was. Outside of a `__namecall`, it returns `nil`.

## Example

```luau
local OriginalNamecall
OriginalNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    if getnamecallmethod() == "Kick" and self == game.Players.LocalPlayer then
        return
    end
    return OriginalNamecall(self, ...)
end)
```

## Must

- Return the right name inside `__namecall`, for proxies and for `game`.
- Return `nil` outside of a `__namecall`.
