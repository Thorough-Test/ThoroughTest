---
summary: Hooks a metamethod on any object, including game instances.
---

# hookmetamethod

```luau
hookmetamethod(object: any, method: string, hook: function) -> function
```

Hooks one metamethod on an object's metatable, even if the metatable is locked. All instances share a metatable, so hooking `__namecall` on `game` catches method calls on every instance in the game.

Returns the previous metamethod. Passing it back in as the hook undoes your hook.

Use [getnamecallmethod](../metatable/getnamecallmethod.md) inside a `__namecall` hook to see which method was called.

## Parameters

- `object`: Anything with a metatable.
- `method`: The metamethod, like `"__index"`.
- `hook`: The function to run instead.

## Example

```luau
local OriginalNamecall
OriginalNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    if getnamecallmethod() == "FireServer" and not checkcaller() then
        print("Remote fired:", self.Name)
    end
    return OriginalNamecall(self, ...)
end)
```

To remove the hook later:

```luau
hookmetamethod(game, "__namecall", OriginalNamecall)
```

### What a game script sees

A game can read a member that doesn't exist and compare the error before and after a hook. It can do the same with `__namecall` and `__newindex`, and an error handler can check which function raised the error. A hook that only calls the original has to give exactly the same error. Don't add or remove a script and line at the start of it.

```luau
local function Read()
    return game.NotAMember
end
print(pcall(Read))

local Original
Original = hookmetamethod(game, "__index", function(...)
    return Original(...)
end)
print(pcall(Read))
hookmetamethod(game, "__index", Original)
```

Both lines have to print the same error.

Every method call a game script makes goes through a `__namecall` hook, so a game can also time its own calls. A hook that only calls the original shouldn't make them much slower.

A `pcall` inside a `__namecall` hook should catch errors too. If one gets past it, the game script's method call errors.

## Must

- Hook `__index` on tables, whether the metamethod is Luau or C.
- Hook `__index`, `__namecall` and `__newindex` on `game`.
- Return the previous metamethod, and keep it working.
- Hook the function itself, leaving the metatable entry in place.
- Keep the object's `__metatable` field.
- Restore the metamethod when the original is passed back as the hook.
- Allow stacked hooks, with the newest hook running first.
- Keep the method name when a hook yields before calling the original.
- Change what the server receives when a `__namecall` hook changes a `FireServer` call, without the original call also going through.
- Never hook a metamethod that doesn't exist or an object with no metatable.
- Leave the metamethod working when the hook isn't a function.
- Keep the error a game script gets the same after hooking `__index`, `__namecall` or `__newindex`, raised by the same function, with no Luau code from the hook in its stack.
- Add no extra frames to a game script's stack, even C ones.

## Should

- Make a hooked `__namecall` count as a C function.
- Let a `pcall` inside a hook catch errors.
- Keep the same function after a hook is restored.
- Keep method calls fast. Every method call in the game goes through a `__namecall` hook, so one that only calls the original shouldn't make a game script's method calls 6 times slower or more.
- Error, instead of returning nothing, on a metamethod that doesn't exist or an object with no metatable.
- Error when the hook isn't a function.
