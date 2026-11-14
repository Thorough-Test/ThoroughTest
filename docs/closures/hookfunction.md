---
summary: Replaces what a function does and returns the original.
---

# hookfunction

```luau
hookfunction(target: function, hook: function) -> function
```

After this call, everything that calls `target` runs `hook` instead, including code that saved a reference to it earlier. It returns a function that still runs the original code, so your hook can call it.

Any mix of function types works. You can hook a C function with a Luau function, and the other way around.

## Parameters

- `target`: The function to replace.
- `hook`: The function to run instead.

## Example

### Logging calls

```luau
local OriginalFireServer
OriginalFireServer = hookfunction(Instance.new("RemoteEvent").FireServer, function(self, ...)
    print(self.Name, ...)
    return OriginalFireServer(self, ...)
end)
```

### Changing a result

```luau
local function GetPrice()
    return 100
end

local OriginalGetPrice
OriginalGetPrice = hookfunction(GetPrice, function()
    return OriginalGetPrice() / 2
end)

print(GetPrice()) -- 50
```

### Stacking hooks

Each hook's returned function is the layer below it, so a second hook calls the first, and the first calls the real function.

```luau
local function Greet()
    return "hello"
end

local FirstOriginal, SecondOriginal
FirstOriginal = hookfunction(Greet, function()
    return "1 " .. FirstOriginal()
end)
SecondOriginal = hookfunction(Greet, function()
    return "2 " .. SecondOriginal()
end)

print(Greet()) -- 2 1 hello
```

### What a game script sees

A game can look for hooks by calling a function with a bad argument and comparing the error, the `debug.info` result and the call stack with what the unhooked function gives. Once the hook is in, all three have to stay the same.

The error is the easy one to miss. When a C function errors, Luau starts the message with the script and line that called it:

```
Players.Player1.PlayerScripts.Check:4: invalid argument #1 to 'nfcnormalize' (string expected, got nil)
```

A hooked function has to keep that start, pointing at the same game script line. Dropping it, or pointing it at the hook, makes the hook visible.

The executor shows this too, as long as a Luau function makes the call. `pcall(Target, nil)` has no calling line, so it can't show a difference:

```luau
local Target = clonefunction(utf8.nfcnormalize)
local function Call()
    return Target(nil)
end
print(pcall(Call))

local Original
Original = hookfunction(Target, function(...)
    return Original(...)
end)
print(pcall(Call))
restorefunction(Target)
```

Both lines have to print the same error, line number included. If your executor's chunks have no line info, test from a game script instead. Put this LocalScript in a place you own:

```luau
local Inspector = Instance.new("BindableFunction")
Inspector.Name = "Inspector"
Inspector.OnInvoke = function(Target)
    local _, Problem = pcall(function()
        return Target(nil)
    end)
    return tostring(Problem), debug.info(Target, "sn")
end
Inspector.Parent = game:GetService("ReplicatedStorage")
```

Then run this from the executor:

```luau
local Inspector = game:GetService("ReplicatedStorage"):WaitForChild("Inspector")
local Target = clonefunction(utf8.nfcnormalize)
print(Inspector:Invoke(Target))

local Original
Original = hookfunction(Target, function(...)
    return Original(...)
end)
print(Inspector:Invoke(Target))
restorefunction(Target)
```

Both lines have to match. Hooks made with `newcclosure` have to pass this too.

## Must

- Work on every mix of Luau, `newcclosure` and C functions, as the target and as the hook.
- Keep the target's closure type. A hooked C function still shows `[C]` in `debug.info`.
- Hook the function itself, so existing references are hooked too.
- Return a function that still runs the original code, and only that code.
- Let a hook with more upvalues than the target run.
- Pass errors from the hook to the caller unchanged, including error objects.
- Let a hook yield, and let it yield through the original.
- Pass every argument through a hook, trailing nils included.
- Allow stacked hooks, with each returned function calling exactly one layer down.
- Keep the error messages of the original and the hooked function, for Roblox methods too.
- Hook functions inside running game scripts.
- Look the same to a game script as the unhooked function: the same `debug.info`, the same error including the calling line at its start, and no Luau code from the hook in the game script's stack.
- Change what the server receives when `FireServer` is hooked, without the original call also going through.

## Should

- Return a function of the same closure type as the target.
- Return an original that doesn't add its own line number to error messages.
- Keep a hooked Luau function's line and name in `debug.info`, so it doesn't show the hook's.
- Add no extra frames to a game script's stack, even C ones.
- Error when the hook is missing or either argument isn't a function.
