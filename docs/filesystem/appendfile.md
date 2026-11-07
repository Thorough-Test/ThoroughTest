---
summary: Adds data to the end of a file.
---

# appendfile

```luau
appendfile(path: string, data: string) -> ()
```

Adds to the end of a file without touching what's already there. The file is created if it doesn't exist.

## Parameters

- `path`: The file.
- `data`: The data to add.

## Example

```luau
writefile("log.txt", "first line\n")
appendfile("log.txt", "second line\n")

print(readfile("log.txt"))
-- first line
-- second line
```

## Must

- Add to the file without overwriting it.
- Change nothing when the data is an empty string.
- Create the file if it's missing.
- Keep binary data intact.
- Error when the path is a folder, and leave the folder alone.

## Should

- Create missing parent folders, like `writefile`.
