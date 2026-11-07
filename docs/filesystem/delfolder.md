---
summary: Deletes a folder and everything in it.
---

# delfolder

```luau
delfolder(path: string) -> ()
```

Deletes a folder, along with the files inside it.

> **Note:** This can't be undone, so check the path before you call it.

## Parameters

- `path`: The folder to delete.

## Example

```luau
makefolder("cache")
writefile("cache/data.txt", "temporary")

delfolder("cache")

print(isfolder("cache")) -- false
```

## Must

- Delete the folder, including one with files in it.
- Leave files alone.

## Should

- Do nothing for a folder that doesn't exist, instead of erroring.
- Error on a path outside the workspace, instead of doing nothing.
