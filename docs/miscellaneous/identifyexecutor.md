---
summary: Gets the executor's name and version.
---

# identifyexecutor

```luau
identifyexecutor() -> (string, string)
```

Returns the executor's name and its version. It's the right way to handle something that behaves differently on one executor. `getexecutorname` returns just the name.

## Example

```luau
local Name, Version = identifyexecutor()

print(`Running on {Name} {Version}`)
```

## Must

- Return a non-empty name.

## Should

- Return a version string as well.
- Have `getexecutorname`, returning the same name.
