---
summary: Lists every script, running or not.
---

# getscripts

```luau
getscripts() -> { LuaSourceContainer }
```

Returns every script on the client, including disabled scripts and scripts parented to `nil`. If you only want the ones that are running, use [getrunningscripts](getrunningscripts.md).

## Example

```luau
for _, Script in getscripts() do
    if not Script.Parent then
        print("Hidden script:", Script.Name)
    end
end
```

## Must

- Include running scripts, disabled scripts and scripts parented to `nil`.
- Only list scripts.
