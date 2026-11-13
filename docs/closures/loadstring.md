---
summary: Compiles a string of Luau and returns a function to run it.
---

# loadstring

```luau
loadstring(source: string, chunkName: string?) -> (function?, string?)
```

Compiles Luau source into a function. It doesn't run the code, you call the result to do that. Bad code doesn't error. It returns `nil` and the compile error instead, so you can decide what to do with it.

The chunk has the same environment as the code that compiled it, and it runs at the caller's thread identity.

Only source is compiled. Luau doesn't verify bytecode, so crafted bytecode could break out of the sandbox and has to be rejected.

## Parameters

- `source`: The code to compile.
- `chunkName`: Optional. The name shown in error messages and `debug.info`.

## Example

```luau
local Add = loadstring("return ... + 1")
print(Add(1)) -- 2

local Chunk, Problem = loadstring("Example =", "MyChunk")
print(Chunk) -- nil
print(Problem) -- MyChunk:1: Expected identifier when parsing expression, got <eof>
```

## Must

- Compile valid code and run it with the right result, return values and arguments.
- Return `nil` and a message for bad code, without erroring.
- Use the chunk name in compile errors and in `debug.info`.
- Share globals with the caller, and give the chunk access to `game`.
- Work with `setfenv`.
- Compile current Luau: type annotations, aliases, generics, if expressions, string interpolation, compound assignment, `continue`, floor division, function attributes and compiler directives.
- Compile a 2MB script.
- Run the chunk at the caller's thread identity.
- Never load compiled bytecode.

## Should

- Error when the source isn't a string.
