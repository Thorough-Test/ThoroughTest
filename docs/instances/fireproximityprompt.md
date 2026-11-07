---
summary: Triggers a ProximityPrompt instantly from anywhere.
---

# fireproximityprompt

```luau
fireproximityprompt(prompt: ProximityPrompt) -> ()
```

Triggers a prompt without walking to it, looking at it or holding the key. The prompt's properties are restored afterward.

## Parameters

- `prompt`: The ProximityPrompt.

## Example

```luau
local Prompt = workspace.Door:FindFirstChildOfClass("ProximityPrompt")

fireproximityprompt(Prompt)
```

## Must

- Trigger from any distance, passing the local player.
- Skip `HoldDuration`.
- Leave `HoldDuration` and `MaxActivationDistance` unchanged.
- Reach the server.
- Error when given something that isn't a ProximityPrompt.
