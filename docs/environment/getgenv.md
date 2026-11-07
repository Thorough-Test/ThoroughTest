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
getgenv().Coins = 100

loadstring("print(coins)")() -- 100
```

## Must

- Return the same table every time.
- Make its values readable as globals, in other threads and `loadstring` chunks too.
- Keep each script's own globals out of it.
- Fall back to `getgenv` when a script clears a global of the same name.
- Have every function from the game's environment, checked at run time.
