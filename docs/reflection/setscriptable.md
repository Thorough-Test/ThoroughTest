---
summary: Makes a hidden property readable by normal indexing.
---

# setscriptable

```luau
setscriptable(instance: Instance, property: string, state: boolean) -> boolean
```

Turns scripting on or off for a property, so you can read it with `Part.Property` instead of [gethiddenproperty](gethiddenproperty.md). It returns the state the property had before.

> **Note:** Turn it back off when you're done. A game script can check whether a hidden property has become readable.

## Parameters

- `instance`: The instance.
- `property`: The property's name.
- `state`: `true` to allow indexing.

## Example

```luau
local Part = Instance.new("Part")

local Before = setscriptable(Part, "MaterialVariantSerialized", true)
print(Before) -- false
print(Part.MaterialVariantSerialized)

setscriptable(Part, "MaterialVariantSerialized", false)
```

## Must

- Return the previous state.
- Make the property readable, and hidden again when turned off.
- Return `true` for a property that was already scriptable.

## Should

- Error on a property that doesn't exist.
- Error when given something that isn't an instance.
