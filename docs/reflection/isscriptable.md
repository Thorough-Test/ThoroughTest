---
summary: Checks whether scripts can read a property.
---

# isscriptable

```luau
isscriptable(object: Object, property: string) -> boolean
```

Returns `true` if scripts can read the property normally, and `false` if reading it would error.

## Parameters

- `object`: The instance, or another Object like an `EditableImage`.
- `property`: The property's name.

## Example

```luau
local Part = Instance.new("Part")

print(isscriptable(Part, "Name")) -- true
print(isscriptable(Part, "MaterialVariantSerialized")) -- false
```

## Must

- Return `true` for normal properties and `false` for hidden ones.
- Match whether the property can be read.
- Never return `true` for a property that doesn't exist, or exists only on another class.
- Never return `true` for something that isn't an Object.

## Should

- Work on Objects that aren't Instances, like `EditableImage`.
- Return `nil` or error on a property that doesn't exist or belongs to another class, instead of `false`, which means the property is hidden.
