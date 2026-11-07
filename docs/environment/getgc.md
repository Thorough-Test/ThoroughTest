---
summary: Lists everything the garbage collector is tracking.
---

# getgc

```luau
getgc(includeTables: boolean?) -> { any }
```

Returns the functions that are alive right now, including ones inside game scripts that nothing else can reach. Pass `true` to get tables too.

It's a big list, so if you know what you're looking for, [filtergc](filtergc.md) is faster and easier.

## Parameters

- `includeTables`: Optional. Include tables as well. `false` by default.

## Example

```luau
for _, value in getgc() do
    if type(value) == "function" and debug.info(value, "n") == "onDamage" then
        print("Found it:", value)
    end
end
```

## Must

- Return a non-empty table with live functions in it.
- Leave tables out by default and with `false`.
- Include live tables and functions with `true`.

## Should

- Only return functions by default.
