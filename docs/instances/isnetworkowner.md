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

- Return `true` for every part of your own character, `HumanoidRootPart` included. Ownership belongs to the whole assembly, so the Head and anything welded to you share the root's owner.
- Never return `true` for something that isn't a part.

## Should

- Return `false` for anchored parts the server owns.
