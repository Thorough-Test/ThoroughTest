---
summary: Checks whether an instance has a cached reference.
---

# cache.iscached

```luau
cache.iscached(instance: Instance) -> boolean
```

Returns `true` if the instance has a reference in the cache.

## Parameters

- `instance`: The instance to check.

## Example

```luau
local part = Instance.new("Part")
print(cache.iscached(part)) -- true

cache.invalidate(part)
print(cache.iscached(part)) -- false
```

## Must

- Return `true` for a new instance.
- Return `false` after `cache.invalidate`.
- Return `true` again once a lookup caches it.
- Error when given something that isn't an instance.
