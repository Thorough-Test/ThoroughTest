---
summary: Lists the Actors running in the game.
---

# getactors

```luau
getactors() -> { Actor }
```

Returns every running Actor, wherever it is in the game. This is usually your first step before calling [run_on_actor](run_on_actor.md).

## Example

```luau
for _, actor in getactors() do
    print(actor:GetFullName())
end
```

## Must

- Return a table.
- Include Actors that are running in the game.
- Only list Actors.
