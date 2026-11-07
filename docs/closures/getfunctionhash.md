---
summary: Hashes a function's code, so you can recognize it without comparing references.
---

# getfunctionhash

```luau
getfunctionhash(target: function) -> string
```

Returns a SHA384 hash of a Luau function's code, as 96 hex characters. Two functions built from the same code match, even if they're different closures, which is how you recognize a game function after an update reloads it.

The hash covers instructions and constants. C functions don't have either, so there's nothing to hash.

## Parameters

- `target`: A Luau function.

## Example

```luau
local function makeCounter()
    local count = 0
    return function()
        count += 1
        return count
    end
end

print(getfunctionhash(makeCounter()) == getfunctionhash(makeCounter())) -- true
```

## Must

- Return a SHA384 hash as a 96 character hex string.
- Return different hashes for functions with different instructions or constants.
- Return the same hash for identical functions, closures of one function, clones, and the same source compiled twice.
- Never return a made up hash for a C function.
- Error when given something that isn't a function.

## Should

- Error on C functions instead of returning nothing.
