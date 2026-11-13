---
summary: Checks whether your client controls a part's physics.
---

# isnetworkowner

```luau
isnetworkowner(part: BasePart) -> boolean
```

Returns `true` when your client owns the part's physics. Changes you make to a part you own replicate to the server, so this tells you what you can move.

## Parameters

- `part`: The part to check.

## Example

```luau
local Root = game.Players.LocalPlayer.Character.HumanoidRootPart

print(isnetworkowner(Root)) -- true
```

## Must

- Return `true` for your own character.

## Should

- Return `false` for anchored parts the server owns.
- Error when given something that isn't a part.
