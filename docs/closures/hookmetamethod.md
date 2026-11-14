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

A game can read a member that doesn't exist and compare the error before and after a hook. A hook that only calls the original has to give exactly the same error. Don't add or remove a script and line at the start of it.

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
- Give a game script the same error through a hooked `__index`, with no Luau code from the hook in its stack.

## Should

- Keep the same function after a hook is restored.
- Make a hooked `__namecall` count as a C function.
- Add no extra frames to a game script's stack, even C ones.
- Error, instead of returning nothing, on a metamethod that doesn't exist or an object with no metatable.
- Error when the hook isn't a function.
