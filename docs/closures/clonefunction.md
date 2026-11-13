---
summary: Makes a separate copy of a function that hooks can't reach.
---

# clonefunction

```luau
clonefunction(target: function) -> function
```

Returns a new function that runs the same code and shares the same upvalues. Hooking the original doesn't touch the copy, which makes this the safe way to keep a working version of something you or another script might hook.

## Parameters

- `target`: The function to copy. Can be a Luau or a C function.

## Example

```luau
local function GetName()
    return "real"
end

local SafeGetName = clonefunction(GetName)

hookfunction(GetName, function()
    return "hooked"
end)

print(GetName()) -- hooked
print(SafeGetName()) -- real
```

## Must

- Return a new function, not the one it was given.
- Keep the same environment, and share upvalues with the original.
- Keep the same constants and `debug.info` details.
- Run the same as the original, including yielding.
- Return a new C closure for a C function.
- Work on Roblox methods and on other clones.
- Keep the clone separate: `setfenv` on the clone doesn't change the original, and hooking the original doesn't change the clone.

## Should

- Error when given something that isn't a function.
