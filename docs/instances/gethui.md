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
local Screen = Instance.new("ScreenGui")
Screen.Parent = gethui()
```

## Must

- Return the same container every time, one that can hold UI.
- Accept UI as children.
- Not be `PlayerGui` or `CoreGui`.
- Hide its contents from a game script calling `game:GetDescendants()` or listening to `game.DescendantAdded`.

## Should

- Return a `BasePlayerGui` or a `Folder`, not a `ScreenGui`.
