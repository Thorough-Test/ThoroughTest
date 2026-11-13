---
summary: Changes what the current thread is allowed to do.
---

# setthreadidentity

```luau
setthreadidentity(identity: number) -> ()
```

Sets the current thread's identity, which changes what the thread can do. At identity 2 you can't reach `CoreGui`, and at 8 you can.

Each thread has its own identity, and threads you start inherit it.

## Parameters

- `identity`: The identity level.

## Example

```luau
setthreadidentity(2)
print(pcall(game.GetService, game, "CoreGui")) -- runs as a game script would

setthreadidentity(8)
print(game:GetService("CoreGui").Name) -- CoreGui
```

## Must

- Change what the thread can reach. Identity 2 can't reach `CoreGui`, and identity 8 can.
- Only change the current thread.
- Pass the identity on to new threads.
- Keep the identity through a yield.
- Allow setting a higher identity again.

## Should

- Error when the identity isn't a number.
