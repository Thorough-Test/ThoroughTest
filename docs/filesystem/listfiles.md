---
summary: Lists what's in a folder.
---

# listfiles

```luau
listfiles(path: string) -> { string }
```

Returns the path of everything directly in a folder, both files and folders. It doesn't go into subfolders. Pass `""` to list the workspace itself.

The paths are relative to the workspace, so you can pass them straight to `readfile`.

## Parameters

- `path`: The folder.

## Example

```luau
for _, path in listfiles("saves") do
    if isfile(path) then
        print(path, #readfile(path))
    end
end
```

## Must

- List every file and folder directly inside, and nothing deeper.
- Return relative paths that work with other file functions.
- List the workspace when given `""`.
- Keep unicode file names intact, emoji included.
- Never return a value for a folder that doesn't exist, or for a file.

## Should

- Accept a path ending in a slash.
- Error on a folder that doesn't exist or a file, instead of returning nothing.
