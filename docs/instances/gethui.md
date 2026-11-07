---
summary: Gets a container for UI that game scripts can't find.
---

# gethui

```luau
gethui() -> Instance
```

Returns a place to put your UI where game scripts can't reach it. If an anti-cheat can find your ScreenGui with `game:GetDescendants()`, it isn't hidden, so returning `CoreGui` or `PlayerGui` doesn't count.

## Example

```luau
local screen = Instance.new("ScreenGui")
screen.Parent = gethui()
```

## Must

- Return the same container every time, a `BasePlayerGui` or a `Folder`.
- Accept UI as children.
- Not be `PlayerGui` or `CoreGui`.
- Hide its contents from a game script calling `game:GetDescendants()`.
