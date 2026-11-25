---
summary: Reads a file.
---

# readfile

```luau
readfile(path: string) -> string
```

Returns a file's contents.

## Parameters

- `path`: The file.

## Example

```luau
writefile("notes.txt", "jarvis, make me ud")

print(readfile("notes.txt")) -- jarvis, make me ud
```

## Must

- Return exactly what's in the file.
- Return an empty string for an empty file.
- Never return a value for a missing file or a folder.
