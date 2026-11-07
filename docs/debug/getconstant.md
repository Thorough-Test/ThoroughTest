---
summary: Gets one constant from a function.
---

# debug.getconstant

```luau
debug.getconstant(target: function | number, index: number) -> any
```

Returns the constant at `index`. Use [debug.getconstants](getconstants.md) when you don't know the index yet.

## Parameters

- `target`: A Luau function, or a stack level.
- `index`: The position of the constant.

## Example

```luau
local function greet()
    return "hello"
end

for index, value in debug.getconstants(greet) do
    print(index, debug.getconstant(greet, index)) -- 1 hello
end
```

## Must

- Match `debug.getconstants` at every index.
- Work with a stack level.
- Never return a value for an index past the end or for a C function.

## Should

- Error on an index past the end and on C functions, instead of returning nothing.
