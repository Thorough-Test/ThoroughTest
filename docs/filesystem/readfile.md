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
writefile("hello.txt", "Hello")

print(readfile("hello.txt")) -- Hello
```

## Must

- Return exactly what's in the file.
- Return an empty string for an empty file.
- Never return a value for a missing file or a folder.

## Should

- Error on a missing file or a folder, instead of returning nothing.
