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
local folder = Instance.new("Folder")
local part = Instance.new("Part", folder)
local fire = Instance.new("Fire")

cache.replace(part, fire)

print(folder:FindFirstChild("Part")) -- Fire
```

## Must

- Make lookups return the replacement.
- Error when given something that isn't an instance.
