---
summary: The font ids you can use on a Text drawing.
---

# Drawing.Fonts

```luau
Drawing.Fonts: { UI: number, System: number, Plex: number, Monospace: number }
```

A table of font names and ids. Use it instead of raw numbers when setting `Font` on a `Text` drawing.

| Font | Id |
| --- | --- |
| `UI` | `0` |
| `System` | `1` |
| `Plex` | `2` |
| `Monospace` | `3` |

## Example

```luau
local Text = Drawing.new("Text")
Text.Text = "print('hi')"
Text.Font = Drawing.Fonts.Monospace
Text.Size = 18
Text.Visible = true
```

## Must

- Be a table with all four fonts and the ids above.
