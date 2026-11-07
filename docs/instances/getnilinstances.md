---
summary: Lists instances parented to nil.
---

# getnilinstances

```luau
getnilinstances() -> { Instance }
```

Returns instances that exist but aren't in the game. Scripts often hide things this way by setting `Parent` to `nil`.

## Example

```luau
for _, Item in getnilinstances() do
    print(Item.ClassName, Item.Name)
end
```

## Must

- Include instances that were never parented.
- Include instances that were removed from the game.
- Include instances a game script keeps parented to `nil`.
- Only list instances with no parent.
