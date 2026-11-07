---
summary: Gets the script a thread belongs to.
---

# getscriptfromthread

```luau
getscriptfromthread(thread: thread) -> LuaSourceContainer?
```

Returns the script that owns a thread. It pairs well with [getreg](../environment/getreg.md), which lets you go through the running threads.

## Parameters

- `thread`: The thread.

## Example

```luau
for _, value in getreg() do
    if type(value) == "thread" then
        print(getscriptfromthread(value))
    end
end
```

## Must

- Return the script for a game script's thread.
- Return `nil` for executor threads and new coroutines.
- Error when given something that isn't a thread.
