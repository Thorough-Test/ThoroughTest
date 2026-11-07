---
summary: Checks whether two references point at the same instance.
---

# compareinstances

```luau
compareinstances(first: Instance, second: Instance) -> boolean
```

`==` compares references, so it treats a [cloneref](cloneref.md) as a different object. This compares the real instances.

## Parameters

- `first`: An instance.
- `second`: Another instance.

## Example

```luau
local Part = Instance.new("Part")
local Clone = cloneref(Part)

print(Part == Clone) -- false
print(compareinstances(Part, Clone)) -- true
```

## Must

- Return `true` for the same instance and for a cloneref of it.
- Return `false` for different instances.
- Error unless given two instances.
