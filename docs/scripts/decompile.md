---
summary: Turns a script back into readable Luau.
---

# decompile

```luau
decompile(script: LuaSourceContainer) -> string
```

Turns a script's bytecode back into source code. Comments and local names are gone from bytecode, so the output won't match the original, but it should do the same thing.

TT decompiles a real module, runs the output and checks that it behaves like the original. Output that doesn't run the same way fails.

## Parameters

- `script`: The script to decompile.

## Example

```luau
local Module = game.ReplicatedStorage.Config

writefile("Config.lua", decompile(Module))
```

## Must

- Return code for ModuleScripts, LocalScripts and Scripts with `RunContext` set to `Client`.
- Keep strings, numbers and method names in the output.
- Give different output for different scripts.
- Produce a module that compiles, runs and returns its table.
- Keep the module's behavior: math, loops, `break`, conditions, `nil` and `false` handling, closures, varargs, methods and tables.
- Error when given something that isn't a script.

## Should

- Produce output that compiles for every script, not only for modules.
