---
summary: Replaces a metatable, ignoring the __metatable lock.
---

# setrawmetatable

```luau
setrawmetatable(object: any, metatable: table?) -> any
```

Sets an object's metatable even if it's locked. It works on userdata and strings too. Pass `nil` to remove the metatable.

> **Note:** All strings share one metatable. If you swap it, put the old one back.

## Parameters

- `object`: The object to change.
- `metatable`: The new metatable, or `nil`.

## Example

```luau
local object = setmetatable({}, { __metatable = "Locked" })

setrawmetatable(object, {
    __index = function(_, key)
        return `no value for {key}`
    end,
})

print(object.coins) -- no value for coins
```

## Must

- Replace a locked metatable, or clear it with `nil`.
- Work on userdata and strings.
- Keep the `__metatable` field of the new metatable.
- Error when the metatable isn't a table or `nil`.

## Should

- Return the object.
- Work on frozen tables.
- Error when the object is `nil`.
