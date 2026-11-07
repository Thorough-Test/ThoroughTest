---
summary: Starts or ends a touch between two parts.
---

# firetouchinterest

```luau
firetouchinterest(part: BasePart, target: BasePart, state: number | boolean) -> ()
```

Makes `part` touch `target` without moving either of them. Use `0` to start a touch and `1` to end it. A full touch needs both calls.

> **Note:** `0` starts and `1` ends, but `true` starts and `false` ends. It's easy to mix those up.

## Parameters

- `part`: The part doing the touching.
- `target`: The part being touched.
- `state`: `0` or `true` to start, `1` or `false` to end.

## Example

```luau
local Root = game.Players.LocalPlayer.Character.HumanoidRootPart
local Coin = workspace.Coin

firetouchinterest(Root, Coin, 0)
task.wait()
firetouchinterest(Root, Coin, 1)
```

## Must

- Fire `Touched` with `0`, including the part that was passed.
- Fire `TouchEnded` with `1`.
- Reach the server for both.
- Fire the touch without moving either part, even for a moment.
- Error when either part is missing or isn't a part.

## Should

- Fire each event once per call, for the part that was passed.
- Keep the touch going until `1`.
- Treat `true` as start and `false` as end.
