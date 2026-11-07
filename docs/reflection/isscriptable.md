---
summary: Checks whether scripts can index a property.
---

# isscriptable

```luau
isscriptable(instance: Instance, property: string) -> boolean
```

Returns `true` if scripts can read the property normally, and `false` if indexing it would error.

## Parameters

- `instance`: The instance.
- `property`: The property's name.

## Example

```luau
local part = Instance.new("Part")

print(isscriptable(part, "Name")) -- true
print(isscriptable(part, "MaterialVariantSerialized")) -- false
```

## Must

- Return `true` for normal properties and `false` for hidden ones.
- Match whether the property can be indexed.
- Never return a value for a property that doesn't exist.
- Error when given something that isn't an instance.

## Should

- Error on a property that doesn't exist, instead of returning nothing.
