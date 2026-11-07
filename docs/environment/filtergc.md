---
summary: Searches the garbage collector for a function or table that matches your filters.
---

# filtergc

```luau
filtergc(kind: string, filters: { [string]: any }, returnOne: boolean?) -> any
```

Finds things in the garbage collector without writing a loop around [getgc](getgc.md). You describe what you want, and every filter has to match.

Returns a table of matches. With `returnOne`, it returns the first match, or `nil` if there isn't one.

## Function filters

Use these with `filtergc("function", ...)`.

| Filter | Matches |
| --- | --- |
| `Name` | The function's name. |
| `IgnoreExecutor` | `true` by default, which leaves out your own functions. |
| `Hash` | The result of [getfunctionhash](../closures/getfunctionhash.md). |
| `Constants` | A list of constants it must have. |
| `Upvalues` | A list of upvalues it must have. |
| `Source` | The script it came from. |
| `Environment` | The function's environment. |
| `StartLine` | The line it's defined on. |
| `UpvalueCount` | How many upvalues it has. |
| `ConstantCount` | How many constants it has. |

## Table filters

Use these with `filtergc("table", ...)`.

| Filter | Matches |
| --- | --- |
| `Keys` | A list of keys it must have. |
| `Values` | A list of values it must have. |
| `KeyValuePairs` | Keys that must have exactly these values. |
| `Metatable` | The table's metatable. |

## Parameters

- `kind`: `"function"` or `"table"`.
- `filters`: The filters to match.
- `returnOne`: Optional. Return the first match instead of a table.

## Example

```luau
local OnDamage = filtergc("function", { Name = "onDamage" }, true)

local Config = filtergc("table", {
    Keys = { "WalkSpeed", "JumpPower" },
}, true)
```

## Must

- Support every filter above, with every filter having to match.
- Find every match without `returnOne`, and one match with it.
- Leave out the executor's functions unless `IgnoreExecutor` is `false`.
- Return an empty table or `nil` when nothing matches.
- Require all of `Keys`, and require the exact values in `KeyValuePairs`.
- Error on an unknown kind, or when the filters aren't a table.

## Should

- Filter by `UpvalueCount`, leaving out functions with a different count.
