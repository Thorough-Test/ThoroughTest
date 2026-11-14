---
summary: Gets a container for UI that game scripts can't find.
---

# gethui

```luau
gethui() -> Instance
```

Returns a place to put your UI where game scripts can't reach it. If an anti-cheat can find your ScreenGui, it isn't hidden. `PlayerGui` never counts, and plain `CoreGui` doesn't either, since a game script can still find what's inside it.

## Example

```luau
local Screen = Instance.new("ScreenGui")
Screen.Parent = gethui()
```

### What a game script sees

Game scripts can't read `CoreGui` directly, but `ContentProvider:PreloadAsync({ game })` walks everything under `game`, including `CoreGui`, and reports each image it finds. That's enough to spot UI in plain `CoreGui`. Put this LocalScript in a place you own:

```luau
local ContentProvider = game:GetService("ContentProvider")
task.wait(10)
ContentProvider:PreloadAsync({ game }, function(Content)
    if Content == "rbxassetid://123456789" then
        print("found it")
    end
end)
```

Then run this from the executor within 10 seconds:

```luau
local Screen = Instance.new("ScreenGui")
local Image = Instance.new("ImageLabel")
Image.Image = "rbxassetid://123456789"
Image.Parent = Screen
Screen.Parent = gethui()
```

Nothing should print.

## Must

- Return the same container every time, one that can hold UI.
- Accept UI as children.
- Not be `PlayerGui`.
- Hide its contents from a game script calling `game:GetDescendants()`, listening to `game.DescendantAdded` or calling `ContentProvider:PreloadAsync({ game })`.

## Should

- Return a `BasePlayerGui` or a `Folder`, not a `ScreenGui`.
