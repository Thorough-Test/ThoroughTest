---
summary: Reads a property from a drawing.
---

# getrenderproperty

```luau
getrenderproperty(drawing: Drawing, property: string) -> any
```

Does the same thing as `drawing[property]`. It's useful when you have the property name in a variable or want to read one safely with `pcall`.

## Parameters

- `drawing`: The drawing to read.
- `property`: The property's name.

## Example

```luau
local circle = Drawing.new("Circle")
circle.Radius = 50

print(getrenderproperty(circle, "Radius")) -- 50
```

## Must

- Return the property's value.
- Never return a value for a property that doesn't exist.
- Error when given something that isn't a drawing.

## Should

- Error on a property that doesn't exist, instead of returning nothing.
