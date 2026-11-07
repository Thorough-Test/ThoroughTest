---
summary: Deletes a file.
---

# delfile

```luau
delfile(path: string) -> ()
```

Deletes a file from the workspace.

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

- Do nothing for a file that doesn't exist, instead of erroring.
