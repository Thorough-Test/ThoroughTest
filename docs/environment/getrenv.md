---
summary: Gets the game's global table.
---

# getrenv

```luau
getrenv() -> { [any]: any }
```

Returns the globals that game scripts use. Its `_G` and `shared` are the same ones game scripts use, which makes this the way to read what they've stored there.

## Example

```luau
getrenv()._G.playerCoins = 100

for key, value in getrenv()._G do
    print(key, value)
end
```

## Must

- Return the real table, with `print`, `game`, `_G` and `shared`.
- Be a different table from `getgenv`.
- Keep executor globals out of it.
- Keep values written to it.

## Should

- Make values written to it available in the executor's environment.
