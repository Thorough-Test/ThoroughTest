---
summary: Deletes a file.
---

# delfile

```luau
delfile(path: string) -> ()
```

Deletes a file from the workspace. A file that doesn't exist can error or do nothing, depending on the executor, so check [isfile](isfile.md) first if that matters.

## Parameters

- `path`: The file to delete.

## Example

```luau
writefile("temp.txt", "bye")
delfile("temp.txt")

print(isfile("temp.txt")) -- false
```

## Must

- Delete the file.
- Leave folders alone.

## Should

- Error when given a folder, instead of doing nothing.
