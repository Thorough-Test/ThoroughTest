---
summary: Checks whether a path is a file.
---

# isfile

```luau
isfile(path: string) -> boolean
```

Returns `true` only if the path exists and is a file.

## Parameters

- `path`: The path to check.

## Example

```luau
print(isfile("nothing.txt")) -- false

writefile("nothing.txt", "")
print(isfile("nothing.txt")) -- true
```

## Must

- Return `false` for a missing file.
- Return `true` for a real file, including an empty one.
- Return `false` for a folder.
