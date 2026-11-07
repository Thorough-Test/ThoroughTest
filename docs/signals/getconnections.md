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
| `Function` | The connected function. `nil` for C connections and other Luau states. |
| `Thread` | The thread that made the connection. For `:Wait`, the waiting thread. |
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
for _, connection in getconnections(game.Players.LocalPlayer.Idled) do
    connection:Disable()
end
```

### Reading what's connected

```luau
for _, connection in getconnections(workspace.ChildAdded) do
    if connection.Function then
        print(debug.info(connection.Function, "sl"))
    end
end
```

## Must

- List every connection, including ones from `:Once`, `:Wait`, `GetPropertyChangedSignal` and game scripts.
- Stop listing connections once they're gone.
- Give correct values for every field, and leave `Function` and `Thread` as `nil` for C connections and foreign states.
- Make `Fire` and `Defer` call the function with the arguments, with `Defer` using `task.defer`.
- Make `Disable` and `Enable` work, including on game scripts, and on a `:Wait` connection without resuming its thread.
- Make `Disconnect` disconnect the real connection.
- Let `hookfunction` on `Function` change what runs.
- Error when given something that isn't a signal.

## Should

- Keep the function that called `Fire` off the connection's call stack.
