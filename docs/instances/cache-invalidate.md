---
summary: Removes an instance's reference from the cache.
---

# cache.invalidate

```luau
cache.invalidate(instance: Instance) -> ()
```

Drops the cached reference for an instance. The next lookup creates a new reference, so it won't equal the one you were holding, even though both point at the same instance.

## Parameters

- `instance`: The instance to remove from the cache.

## Example

```luau
local folder = Instance.new("Folder")
local part = Instance.new("Part", folder)

cache.invalidate(folder.Part)

print(part == folder.Part) -- false
```

## Must

- Make the next lookup return a new reference.
- Error when given something that isn't an instance.
