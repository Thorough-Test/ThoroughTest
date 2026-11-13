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
- Fire without changing the prompt's properties, even for a moment, or moving the part.
- Reach the server.

## Should

- Error on an Instance that isn't a ProximityPrompt, instead of doing nothing.
- Error when given something that isn't an Instance.
