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
getrenv()._G.PlayerCoins = 460

for Key, Value in getrenv()._G do
    print(Key, Value)
end
```

### What a game script sees

Everything here is shared with game scripts. A global you write is readable by any game script right away, which is how you hand one a value, and why executor functions must never end up in this table.

## Must

- Return the real table, with `print`, `game`, `_G` and `shared`.
- Have the same `_G` and `shared` tables that game scripts use.
- Be a different table from `getgenv`.
- Keep executor globals out of it.
- Keep values written to it, and make them readable as globals in game scripts.
