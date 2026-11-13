---
summary: Locks or unlocks a table.
---

# setreadonly

```luau
setreadonly(target: table, state: boolean) -> ()
```

Sets whether a table can be written to. It's most useful on frozen tables and metatables you'd otherwise be locked out of.

> **Note:** Lock game tables back up when you're done. An anti-cheat can check for tables left open.

## Parameters

- `target`: The table.
- `state`: `true` to lock it, `false` to unlock it.

## Example

```luau
local Frozen = table.freeze({ Value = 1 })

setreadonly(Frozen, false)
Frozen.Value = 2
setreadonly(Frozen, true)

print(Frozen.Value) -- 2
```

## Must

- Unlock frozen tables so they can be written to.
- Lock tables so a write errors.
- Unlock and lock `game`'s metatable.

## Should

- Error when given something that isn't a table.
