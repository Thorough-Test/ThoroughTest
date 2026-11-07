---
summary: Lists the ModuleScripts that have been required.
---

# getloadedmodules

```luau
getloadedmodules() -> { ModuleScript }
```

Returns every ModuleScript that's been required. A module that was never required isn't loaded, so it isn't listed.

## Example

```luau
for _, module in getloadedmodules() do
    print(module:GetFullName())
end
```

## Must

- Include modules game scripts have required.
- Leave out modules that were never required.
- Only list ModuleScripts.
