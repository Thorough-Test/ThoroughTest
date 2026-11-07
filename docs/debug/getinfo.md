---
summary: Gets details about a function or a stack level.
---

# debug.getinfo

```luau
debug.getinfo(target: function | number) -> {
    source: string,
    short_src: string,
    func: function,
    what: string,
    currentline: number,
    name: string,
    nups: number,
    numparams: number,
    is_vararg: number,
}
```

Returns details about a function in one table.

| Field | What it holds |
| --- | --- |
| `source` | Where the function came from, starting with `@` or `=`. |
| `short_src` | A shorter version of `source`. |
| `func` | The function itself. |
| `what` | `"Lua"` for Luau functions, `"C"` for C functions. |
| `currentline` | The line it's running, or where it's defined. |
| `name` | The function's name. |
| `nups` | How many upvalues it has. |
| `numparams` | How many named parameters it has. |
| `is_vararg` | `1` if it takes `...`, otherwise `0`. |

## Parameters

- `target`: A function, or a stack level.

## Example

```luau
local count = 0
local function add(left, right)
    count += 1
    return left + right
end

local info = debug.getinfo(add)
print(info.name, info.numparams, info.nups, info.what)
-- add 2 1 Lua
```

## Must

- Return every field with the right type.
- Return correct values for `func`, `name`, `numparams`, `is_vararg`, `nups` and `what`.
- Return `what` as `"C"` for C functions.
- Include the chunk name in `source` and `short_src`.
- Work with stack levels, with level 1 as the caller and the right `currentline`.
- Never return a value for a stack level that doesn't exist.
- Error when given something that isn't a function or a number.

## Should

- Error on a stack level that doesn't exist, instead of returning nothing.
