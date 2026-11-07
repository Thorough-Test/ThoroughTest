---
summary: Checks whether a value is a drawing.
---

# isrenderobj

```luau
isrenderobj(value: any) -> boolean
```

Returns `true` for drawings and `false` for everything else. It takes anything, so you can call it without checking the type first.

## Parameters

- `value`: The value to check.

## Example

```luau
print(isrenderobj(Drawing.new("Square"))) -- true
print(isrenderobj(workspace)) -- false
print(isrenderobj("text")) -- false
```

## Must

- Return `true` for a real drawing.
- Return `false` for instances, strings and tables.
