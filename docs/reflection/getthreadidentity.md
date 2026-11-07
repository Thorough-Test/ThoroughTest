---
summary: Gets the current thread's identity level.
---

# getthreadidentity

```luau
getthreadidentity() -> number
```

Returns the identity of the current thread.

## Example

```luau
setthreadidentity(2)
print(getthreadidentity()) -- 2
```

## Must

- Return the identity as a number.
- Return each thread's own identity, even when another thread changes its own.
