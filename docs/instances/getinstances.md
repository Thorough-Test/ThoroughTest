---
summary: Lists every instance, even ones parented to nil.
---

# getinstances

```luau
getinstances() -> { Instance }
```

Returns all the instances Luau has a reference to, whether or not they're in the game. Only want the ones outside of it? Use [getnilinstances](getnilinstances.md).

## Example

```luau
for _, Item in getinstances() do
    if Item:IsA("ModuleScript") then
        print(Item:GetFullName())
    end
end
```

## Must

- Return a non-empty list of instances.
- Include instances in the game, like `workspace`.
- Include instances parented to `nil`.
