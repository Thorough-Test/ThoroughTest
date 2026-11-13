---
summary: Runs a file.
---

# dofile

```luau
dofile(path: string) -> ...any
```

Compiles and runs a file, and returns what the file returns. It's [loadfile](loadfile.md) in one step, for when you don't need to look at the chunk first.

## Parameters

- `path`: The file to run.

## Example

```luau
writefile("add.lua", "return 1 + 1")

print(dofile("add.lua")) -- 2
```

## Must

- Run the whole file before returning, and return its values.
- Error on a file with a syntax error.
- Let errors inside the file reach the caller unchanged.
- Never return a value for a file that doesn't exist.

## Should

- Error on a file that doesn't exist, instead of returning nothing.
