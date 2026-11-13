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
local Object = setmetatable({}, { __metatable = "Locked" })

setrawmetatable(Object, {
    __index = function(_, Key)
        return `no value for {Key}`
    end,
})

print(Object.Coins) -- no value for coins
```

## Must

- Replace a locked metatable, or clear it with `nil`.
- Work on userdata and strings.
- Keep the `__metatable` field of the new metatable.

## Should

- Return the object.
- Work on frozen tables.
- Error when the metatable isn't a table or `nil`.
- Error when the object is `nil`.
