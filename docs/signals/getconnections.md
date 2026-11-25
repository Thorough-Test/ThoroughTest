---
summary: Lists a signal's connections, with control over each one.
---

# getconnections

```luau
getconnections(signal: RBXScriptSignal) -> { Connection }
```

Returns an object for each connection on a signal.

| Field | What it holds |
| --- | --- |
| `Enabled` | Whether the connection runs when the signal fires. |
| `Function` | The connected function. `nil` for C connections and `ForeignState` connections. |
| `Thread` | The thread that made the connection. For `:Wait`, the waiting thread. `nil` for C connections and `ForeignState` connections. |
| `LuaConnection` | `true` if the connection was made from Luau. |
| `ForeignState` | `true` if it belongs to another Luau state, like an Actor. |

| Method | What it does |
| --- | --- |
| `Fire(...)` | Calls the connection. |
| `Defer(...)` | Calls it with `task.defer`. |
| `Disable()` | Stops it from running. |
| `Enable()` | Lets it run again. |
| `Disconnect()` | Removes it for good. |

## Parameters

- `signal`: The signal.

## Example

### Blocking anti-idle kicks

```luau
for _, Connection in getconnections(game.Players.LocalPlayer.Idled) do
    Connection:Disable()
end
```

### Reading what's connected

```luau
for _, Connection in getconnections(workspace.ChildAdded) do
    if Connection.Function then
        print(debug.info(Connection.Function, "sl"))
    end
end
```

### What a game script sees

A game script keeps its own reference to each connection it makes. `Disable` and `Enable` can't change what it reads from `Connected`, which stays `true`. When `Fire` runs one of its connections, the handler runs at the game's identity with none of your Luau code in its call stack, the same as when the signal fires for real.

## Must

- List every connection, including ones from `:Once`, `:Wait`, `GetPropertyChangedSignal` and game scripts.
- Stop listing connections once they're gone.
- Give correct values for every field, and leave `Function` and `Thread` as `nil` for C connections and foreign states.
- Make `Fire` and `Defer` call the function with the arguments, with `Defer` using `task.defer`.
- Make `Disable` and `Enable` work, including on game scripts, and on a `:Wait` connection without resuming its thread.
- List connections made in another Luau state, like inside an Actor, and make `Disable` and `Enable` work on them.
- Leave the real connection's `Connected` as `true` through `Disable` and `Enable`, including when the game script that made it reads it.
- Make `Fire` run a game script's connection at the game's identity, with no Luau code from the caller in its stack.
- Add no extra frames to a game script's connection stack when `Fire` runs it, even C ones.
- Make `Disconnect` disconnect the real connection.
- Let `hookfunction` on `Function` change what runs.

## Should

- Error when given something that isn't a signal.
