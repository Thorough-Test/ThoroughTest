---
summary: Turns a file into an asset url that Roblox can load.
---

# getcustomasset

```luau
getcustomasset(path: string) -> string
```

Returns an `rbxasset://` url for a file, so you can use your own images, sounds and meshes anywhere Roblox expects a content id.

## Parameters

- `path`: The file.

## Example

```luau
local Image = Instance.new("ImageLabel")
Image.Size = UDim2.fromOffset(128, 128)
Image.Image = getcustomasset("logo.png")
Image.Parent = Instance.new("ScreenGui", gethui())
```

### Fonts

A font takes two files: the `.ttf` and a font family `.json` that points to it.

```luau
writefile("MyFont.json", game:GetService("HttpService"):JSONEncode({
    name = "MyFont",
    faces = { { name = "Regular", weight = 400, style = "normal", assetId = getcustomasset("MyFont.ttf") } },
}))

local Label = Instance.new("TextLabel")
Label.FontFace = Font.new(getcustomasset("MyFont.json"))
```

## Must

- Return an `rbxasset://` url.
- Return a url Roblox can load, for images, sounds (`.mp3`) and fonts (a `.ttf` file listed in a font family `.json`).
- Never return a value for a file that doesn't exist.

## Should

- Keep the file's extension in the url.
- Return a new url after the file changes, so Roblox doesn't show the old one.
