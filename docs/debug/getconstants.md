---
summary: Lists a function's constants.
---

# debug.getconstants

```luau
debug.getconstants(target: function | number) -> { any }
```

Returns everything fixed in the function's code: strings, numbers and the names of the globals it uses.

This is a handy way to recognize a game function, since a function's constants rarely change even when its name does. You can scan [getgc](../environment/getgc.md) and look for a string you know is in there.

## Parameters

- `target`: A Luau function, or a stack level.

## Example

```luau
local function Target()
    return "text", 2.5, tick
end

for Index, Value in debug.getconstants(Target) do
    print(Index, Value)
end
-- text, 2.5 and tick are all in the list
```

## Must

- Return a table with the function's strings, numbers and global names.
- Work with a stack level.
- Read functions from game scripts.
- Never list constants for a C function.

## Should

- Error on C functions, instead of returning nothing.
