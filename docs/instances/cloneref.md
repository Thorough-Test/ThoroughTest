---
summary: Makes a second reference to an instance.
---

# cloneref

```luau
cloneref(instance: Instance) -> Instance
```

Returns a new reference to the same instance. The reference isn't equal to the original, but anything you do through it affects the real instance.

Scripts sometimes use this to keep a service reference that weak tables and comparisons don't recognize. To check whether two references point at the same instance, use [compareinstances](compareinstances.md).

## Parameters

- `instance`: The instance.

## Example

```luau
local Part = Instance.new("Part")
local Clone = cloneref(Part)

print(Clone == Part) -- false

Clone.Name = "Renamed"
print(Part.Name) -- Renamed
```

## Must

- Return a new reference that works like the instance.
- Pass reads, writes and method calls through to the real instance.
- Reflect changes made to the real instance.
- Stay separate from the original in weak tables.
- Error when given something that isn't an instance.
