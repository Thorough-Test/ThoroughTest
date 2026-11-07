---
summary: Destroys every drawing.
---

# cleardrawcache

```luau
cleardrawcache() -> ()
```

Removes every drawing at once. Use it to clean up after a script without keeping track of everything it made.

## Example

```luau
local Circle = Drawing.new("Circle")

cleardrawcache()

print(Circle.__OBJECT_EXISTS) -- false
```

## Must

- Destroy every drawing, of any type, right away.
- Work when deferred, and leave drawings in place until the call runs.
