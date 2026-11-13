---
summary: Clicks a ClickDetector from anywhere.
---

# fireclickdetector

```luau
fireclickdetector(detector: ClickDetector, distance: number?, event: string?) -> ()
```

Fires a ClickDetector as if you clicked it, no matter how far away you are. The event can be `MouseClick`, `RightMouseClick`, `MouseHoverEnter` or `MouseHoverLeave`.

## Parameters

- `detector`: The ClickDetector.
- `distance`: Optional. The distance to click from.
- `event`: Optional. The event to fire. `"MouseClick"` by default.

## Example

```luau
for _, Detector in workspace:GetDescendants() do
    if Detector:IsA("ClickDetector") and Detector.Parent.Name == "Button" then
        fireclickdetector(Detector)
    end
end
```

## Must

- Fire `MouseClick` from any distance, passing the local player.
- Fire `RightMouseClick`, `MouseHoverEnter` and `MouseHoverLeave` when asked.
- Fire without changing `MaxActivationDistance` or moving the part.
- Reach the server.

## Should

- Error on an Instance that isn't a ClickDetector, instead of doing nothing.
- Error when given something that isn't an Instance.
