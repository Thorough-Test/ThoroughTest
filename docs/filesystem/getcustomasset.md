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
local image = Instance.new("ImageLabel")
image.Size = UDim2.fromOffset(128, 128)
image.Image = getcustomasset("logo.png")
image.Parent = Instance.new("ScreenGui", gethui())
```

## Must

- Return an `rbxasset://` url.
- Return a url Roblox can really load.
- Never return a value for a file that doesn't exist.

## Should

- Keep the file's extension in the url.
- Return a new url after the file changes, so Roblox doesn't show the old one.
- Error on a file that doesn't exist, instead of returning nothing.
