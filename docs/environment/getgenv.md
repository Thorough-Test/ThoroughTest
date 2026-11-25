---
summary: Gets the executor's global table, shared by all your scripts.
---

# getgenv

```luau
getgenv() -> { [any]: any }
```

Returns the table behind your executor's globals. Anything you put here can be read as a global by every script you run, so it's the normal way to share data between scripts.

## Example

```luau
getgenv().Coins = 1038

loadstring("print(Coins)")() -- 1038
```

### What a game script sees

Game scripts read their globals from [getrenv](getrenv.md), never from `getgenv`. A value you store here, and executor functions like `hookfunction`, read as `nil` in a game script.

## Must

- Return the same table every time.
- Make its values readable as globals, in other threads and `loadstring` chunks too.
- Keep each script's own globals out of it.
- Stay out of game scripts' environments, so they can't read its values or executor functions as globals.
- Fall back to `getgenv` when a script clears a global of the same name.
- Have every function from the game's environment, checked at run time.
