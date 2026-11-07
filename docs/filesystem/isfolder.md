---
summary: Checks whether a path is a folder.
---

# isfolder

```luau
isfolder(path: string) -> boolean
```

Returns `true` only if the path exists and is a folder.

## Parameters

- `path`: The path to check.

## Example

```luau
print(isfolder("saves")) -- false

makefolder("saves")
print(isfolder("saves")) -- true
```

## Must

- Return `true` for a real folder.
- Return `false` for a file and for a missing folder.

## Should

- Accept a path ending in a slash.
