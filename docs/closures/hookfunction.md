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
local originalFireServer
originalFireServer = hookfunction(Instance.new("RemoteEvent").FireServer, function(self, ...)
    print(self.Name, ...)
    return originalFireServer(self, ...)
end)
```

### Changing a result

```luau
local function getPrice()
    return 100
end

local originalGetPrice
originalGetPrice = hookfunction(getPrice, function()
    return originalGetPrice() / 2
end)

print(getPrice()) -- 50
```

### Stacking hooks

Each hook's returned function is the layer below it, so a second hook calls the first, and the first calls the real function.

```luau
local function greet()
    return "hello"
end

local firstOriginal, secondOriginal
firstOriginal = hookfunction(greet, function()
    return "1 " .. firstOriginal()
end)
secondOriginal = hookfunction(greet, function()
    return "2 " .. secondOriginal()
end)

print(greet()) -- 2 1 hello
```

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
- Change what the server receives when `FireServer` is hooked, without the original call also going through.
- Error when the hook is missing or either argument isn't a function.

## Should

- Return a function of the same closure type as the target.
- Keep line numbers out of the original's error messages, since the real function has none.
