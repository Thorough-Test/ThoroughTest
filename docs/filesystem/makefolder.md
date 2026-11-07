---
summary: Creates a folder.
---

# makefolder

```luau
makefolder(path: string) -> ()
```

Creates a folder, along with any parent folders it needs. Calling it on a folder that already exists is safe.

## Parameters

- `path`: The folder to create.

## Example

```luau
makefolder("saves/profiles")
writefile("saves/profiles/main.json", "{}")
```

## Must

- Create the folder.
- Leave an existing folder and its files alone.
- Never destroy a file when given its path.

## Should

- Create parent folders.
