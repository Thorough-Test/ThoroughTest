---
summary: Creates a file, or replaces what's in one.
---

# writefile

```luau
writefile(path: string, data: string) -> ()
```

Writes data to a file and replaces whatever was there. The data is available to read as soon as this returns.

## Parameters

- `path`: The file.
- `data`: The data to write.

## Example

```luau
local HttpService = game:GetService("HttpService")

writefile("settings.json", HttpService:JSONEncode({ Volume = 0.5 }))
```

## Must

- Write exactly the data given, and replace old data completely.
- Keep binary data intact.
- Write a 5MB file in full.
- Make every write readable right away, 200 times in a row.
- Create all 200 files when they're written in a row.
- Never report success for a file that wasn't created.
- Error when the path is a folder, and leave the folder alone.
- Error when the data is `nil`.

## Should

- Create missing parent folders.
