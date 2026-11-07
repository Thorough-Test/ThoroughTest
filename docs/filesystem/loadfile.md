---
summary: Compiles a file into a function.
---

# loadfile

```luau
loadfile(path: string) -> (function?, string?)
```

Works like [loadstring](../closures/loadstring.md), reading the code from a file. Bad code returns `nil` and the compile error.

## Parameters

- `path`: The file.

## Example

```luau
writefile("add.lua", "return 10 + ...")

local Add = loadfile("add.lua")
print(Add(1)) -- 11
```

## Must

- Return a working function for a valid file.
- Give the chunk access to the global environment.
- Return `nil` and a message for a syntax error.
- Never return a value for a file that doesn't exist.

## Should

- Include the file name in the chunk name.
- Error on a file that doesn't exist, instead of returning nothing.
