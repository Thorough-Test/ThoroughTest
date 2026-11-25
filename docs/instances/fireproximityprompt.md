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

### What a game script sees

A game script can listen to `Triggered` and to property changes on its own prompt. It should see the prompt trigger for the local player, with no change to the prompt's `Enabled`, `HoldDuration`, `MaxActivationDistance` or `RequiresLineOfSight` and no movement of its part, even for a frame.

## Must

- Trigger from any distance, passing the local player.
- Work on a prompt inside an Attachment as well as one directly in a part.
- Skip `HoldDuration`.
- Fire without changing the prompt's properties, even for a moment, or moving the part.
- Reach the server.

## Should

- Error on an Instance that isn't a ProximityPrompt, instead of doing nothing.
- Error when given something that isn't an Instance.
