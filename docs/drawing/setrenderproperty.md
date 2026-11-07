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
local Circle = Drawing.new("Circle")

for Property, Value in { Radius = 50, Visible = true } do
    setrenderproperty(Circle, Property, Value)
end
```

## Must

- Change the property.
- Never accept a property that doesn't exist.
- Error when given something that isn't a drawing.

## Should

- Error on a property that doesn't exist, instead of doing nothing.
