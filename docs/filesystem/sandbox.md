---
summary: Nothing a script does can leave the workspace folder.
test: "Filesystem: workspace sandbox"
---

# Workspace sandbox

Scripts should only ever touch the workspace. If a path tries to leave, the function has to refuse it or keep it inside the workspace, and that goes for every function that takes a path, reads included. A script reading your files is as bad as a script writing them.

## Paths that can't leave

| Path | Why it's dangerous |
| --- | --- |
| `../file.txt` | Climbs out of the workspace. |
| `folder/../../../file.txt` | Climbs out from deeper inside. |
| `C:/file.txt` | Absolute path. |
| `C:file.txt` | Drive relative path. |
| `\\127.0.0.1\C$\file.txt` | Network path. |
| `\\?\C:\file.txt` | Extended path. |

## Paths that should work

A path that stays inside the workspace is fine, even if it looks unusual. `folder/unused/../file.txt` is simply `folder/file.txt`.

## Example

```luau
local Escaped = pcall(readfile, "../../secret.txt")
print(Escaped) -- false

print(isfile("../../secret.txt")) -- false
```

## Must

- Refuse paths that leave the workspace, or keep them inside it, in `writefile`, `appendfile`, `makefolder`, `readfile`, `listfiles`, `loadfile`, `dofile`, and `getcustomasset`.
- Return `false` or error from `isfile` and `isfolder` for those paths, never `true`.
- Keep a path starting with `/` inside the workspace.

## Should

- Error from `delfile` on those paths, instead of doing nothing.
- Handle `..` and `./` that stay inside the workspace.
- Treat `\` and `/` as the same thing.
- Error on a nil path in all of them.
