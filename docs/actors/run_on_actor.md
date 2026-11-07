---
summary: Runs your code inside an Actor's own Luau state.
---

# run_on_actor

```luau
run_on_actor(actor: Actor, code: string, ...any) -> ()
```

Runs code in the Actor's Luau state, with the full executor API. It's the same as if you had executed a script from inside that Actor, so hooks you make there affect that state's functions.

Anything after `code` is passed to the code as `...`. Since states can't share functions or tables, stick to simple values.

## Parameters

- `actor`: The Actor to run in.
- `code`: The source to run.
- `...`: Values for the code to read with `...`.

## Example

```luau
local actor = getactors()[1]

run_on_actor(actor, [[
    local name = ...
    print("Hello from inside the actor,", name)
]], game.Players.LocalPlayer.Name)
```

## Must

- Run the code in the Actor's own Luau state.
- Make `checkcaller` return `true` there.
- Give the code access to the executor API, including `getgc`, `getgenv`, `getrawmetatable`, `getrenv`, `hookfunction`, `hookmetamethod`, `loadstring`, `newcclosure` and `restorefunction`.
- Make hooking and restoring work inside the Actor.
- Keep working after earlier code errored or failed to compile.
- Error when given anything other than an Actor.

## Should

- Pass extra arguments to the code.
