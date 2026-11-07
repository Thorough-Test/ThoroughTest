---
summary: Makes a hidden property readable by normal indexing.
---

# setscriptable

```luau
setscriptable(instance: Instance, property: string, state: boolean) -> boolean
```

Turns scripting on or off for a property, so you can read it with `part.Property` instead of [gethiddenproperty](gethiddenproperty.md). It returns the state the property had before.

> **Note:** Turn it back off when you're done. A game script can check whether a hidden property has become readable.

## Parameters

- `instance`: The instance.
- `property`: The property's name.
- `state`: `true` to allow indexing.

## Example

```luau
local part = Instance.new("Part")

local before = setscriptable(part, "MaterialVariantSerialized", true)
print(before) -- false
print(part.MaterialVariantSerialized)

setscriptable(part, "MaterialVariantSerialized", false)
```

## Must

- Return the previous state.
- Make the property readable, and hidden again when turned off.
- Return `true` for a property that was already scriptable.
- Error when given something that isn't an instance.

## Should

- Error on a property that doesn't exist.
