---
summary: Creates a drawing object.
---

# Drawing.new

```luau
Drawing.new(className: string) -> Drawing
```

Creates a drawing of the given type. Every type has the shared properties, plus its own.

| Type | Properties |
| --- | --- |
| Every type | `Visible`, `ZIndex`, `Transparency`, `Color` |
| `Line` | `From`, `To`, `Thickness` |
| `Text` | `Text`, `TextBounds` (read only), `Size`, `Position`, `Center`, `Outline`, `OutlineColor`, `Font` |
| `Image` | `Data`, `Size`, `Position`, `Rounding`, `Loaded` (read only) |
| `Circle` | `NumSides`, `Radius`, `Position`, `Thickness`, `Filled` |
| `Square` | `Size`, `Position`, `Thickness`, `Filled` |
| `Quad` | `PointA`, `PointB`, `PointC`, `PointD`, `Thickness`, `Filled` |
| `Triangle` | `PointA`, `PointB`, `PointC`, `Thickness`, `Filled` |

Call `Destroy` to remove a drawing. `__OBJECT_EXISTS` tells you if it's still alive.

## Parameters

- `className`: One of the types above.

## Example

### A centered label

```luau
local camera = workspace.CurrentCamera

local label = Drawing.new("Text")
label.Text = "Hello"
label.Size = 24
label.Color = Color3.new(1, 1, 1)
label.Position = camera.ViewportSize / 2 - label.TextBounds / 2
label.Visible = true
```

### Showing an image

```luau
local image = Drawing.new("Image")
image.Data = readfile("logo.png")
image.Size = Vector2.new(128, 128)
image.Visible = true

repeat task.wait() until image.Loaded
print("ready")
```

## Must

- Create every type, with `Visible` starting as `false`.
- Return every property with the right type, and keep the value that was set, decimals included.
- Keep `__OBJECT_EXISTS` correct and read only.
- Keep `TextBounds` accurate and read only. It changes with the text, `Size` and line count.
- Keep `Outline` and `Center` as separate properties.
- Destroy objects with `Destroy`.
- Create and destroy 1000 drawings in under 3 seconds.
- Draw on its own layer. Building shapes out of Frames in hidden UI doesn't count.
- Never return a value for a type or a property that doesn't exist.

## Should

- Have `Remove` as well as `Destroy`, and let a second `Destroy` do nothing.
- Return `Font` as the id it was set to.
- Accept `Centered` and `Outlined` as aliases.
- Have an `OutlineOpacity` on `Text`.
- Have `Loaded` on `Image`, and set it to `true` for a valid PNG.
- Error when a property is set to the wrong type.
- Error on a type or a property that doesn't exist, instead of returning nothing.
