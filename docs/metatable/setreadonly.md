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
local frozen = table.freeze({ value = 1 })

setreadonly(frozen, false)
frozen.value = 2
setreadonly(frozen, true)

print(frozen.value) -- 2
```

## Must

- Unlock frozen tables so they can be written to.
- Lock tables so a write errors.
- Unlock and lock `game`'s metatable.
- Error when given something that isn't a table.
