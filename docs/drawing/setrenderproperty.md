---
summary: Sets a property on a drawing.
---

# setrenderproperty

```luau
setrenderproperty(drawing: Drawing, property: string, value: any) -> ()
```

Does the same thing as `drawing[property] = value`. It pairs with [getrenderproperty](getrenderproperty.md).

## Parameters

- `drawing`: The drawing to change.
- `property`: The property's name.
- `value`: The new value.

## Example

```luau
local circle = Drawing.new("Circle")

for property, value in { Radius = 50, Visible = true } do
    setrenderproperty(circle, property, value)
end
```

## Must

- Change the property.
- Never accept a property that doesn't exist.
- Error when given something that isn't a drawing.

## Should

- Error on a property that doesn't exist, instead of doing nothing.
