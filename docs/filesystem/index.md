---
summary: Read and write files in the executor's workspace.
---

# Filesystem

Executors give scripts a folder called the workspace. Every path is relative to it, and nothing a script does should be able to leave it. A few rules apply to every function here:

- Paths can use `/` or `\`, and they stay inside the workspace. [Workspace sandbox](sandbox.md) covers this.
- Files that can run on their own can't be created. [Blocked extensions](blocked-extensions.md) has the list.
- A write is visible to the next read, with no waiting.
- A nil path always errors.

Here's a common pattern for saving settings:

```luau
local path = "settings.json"
local HttpService = game:GetService("HttpService")

local settings = isfile(path) and HttpService:JSONDecode(readfile(path)) or { volume = 1 }

settings.volume = 0.5
writefile(path, HttpService:JSONEncode(settings))
```
