---
summary: Starts or ends a touch between two parts.
---

# firetouchinterest

```luau
firetouchinterest(part: BasePart, target: BasePart, state: number | boolean) -> ()
```

Makes `part` touch `target` without moving either of them. Use `0` to start a touch and `1` to end it. A full touch needs both calls.

> **Note:** Executors disagree on booleans. Some treat `true` as start, others read `true` as `1` and end the touch. Use `0` and `1` when it matters.

## Parameters

- `part`: The part doing the touching.
- `target`: The part being touched.
- `state`: `0` to start, `1` to end. `true` and `false` also work, but which one starts depends on the executor.

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

## Should

- Fire each event once per call, for the part that was passed.
- Keep the touch going until `1`.
- Accept `true` and `false` as a start and end pair, in either order.
- Error when either part is missing or isn't a part.
