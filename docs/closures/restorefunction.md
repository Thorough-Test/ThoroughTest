---
summary: Removes every hook from a function.
---

# restorefunction

```luau
restorefunction(target: function) -> ()
```

Puts a hooked function back the way it was, no matter how many hooks are on it. Nothing else changes. Its upvalues keep their values, other hooked functions stay hooked, and you can hook it again afterward.

## Parameters

- `target`: The hooked function.

## Example

```luau
local function Greet()
    return "hello"
end

hookfunction(Greet, function()
    return "hooked"
end)
print(Greet()) -- hooked

restorefunction(Greet)
print(Greet()) -- hello
```

## Must

- Remove every hook on the function at once.
- Work on C closures.
- Keep the function's upvalues.
- Only affect the function it was given.
- Allow hooking and restoring the same function again.

## Should

- Error on a function that was never hooked.
- Error when given something that isn't a function.
