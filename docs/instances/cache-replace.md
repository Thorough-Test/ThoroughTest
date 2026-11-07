---
summary: Makes lookups of one instance return another.
---

# cache.replace

```luau
cache.replace(instance: Instance, replacement: Instance) -> ()
```

Changes the cache so that looking up `instance` returns `replacement` instead.

## Parameters

- `instance`: The instance to replace.
- `replacement`: The instance lookups should return.

## Example

```luau
local Folder = Instance.new("Folder")
local Part = Instance.new("Part", Folder)
local Fire = Instance.new("Fire")

cache.replace(Part, Fire)

print(Folder:FindFirstChild("Part")) -- Fire
```

## Must

- Make lookups return the replacement.
- Error when given something that isn't an instance.
