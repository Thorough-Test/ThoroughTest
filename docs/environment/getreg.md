---
summary: Gets the Luau registry.
---

# getreg

```luau
getreg() -> { [any]: any }
```

Returns the Luau registry, a hidden table where the engine keeps references to threads, functions and more. Going through it is one way to find threads that scripts are running.

## Example

```luau
for _, Value in getreg() do
    if type(Value) == "thread" then
        print(coroutine.status(Value))
    end
end
```

## Must

- Return a non-empty table.
- Include running threads.
