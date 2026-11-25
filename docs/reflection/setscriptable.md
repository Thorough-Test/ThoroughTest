---
summary: Makes a hidden property readable like a normal one.
---

# setscriptable

```luau
setscriptable(object: Object, property: string, state: boolean) -> boolean
```

Turns scripting on or off for a property, so you can read it with `Part.Property` instead of [gethiddenproperty](gethiddenproperty.md). It returns the state the property had before.

## Parameters

- `object`: The instance, or another Object like an `EditableImage`.
- `property`: The property's name.
- `state`: `true` to make it readable, `false` to hide it again.

## Example

```luau
local Part = Instance.new("Part")

local Before = setscriptable(Part, "MaterialVariantSerialized", true)
print(Before) -- false
print(Part.MaterialVariantSerialized)

setscriptable(Part, "MaterialVariantSerialized", false)
```

### What a game script sees

`setscriptable` changes what your scripts can read, not what game scripts can. A game script reading the property on the same instance still gets an error, so it can't tell you made it readable.

## Must

- Return the previous state.
- Make the property readable, and hidden again when turned off.
- Only change the instance it was given, so other instances and game scripts can't read the property.
- Return `true` for a property that was already scriptable.
- Never make a property from another class readable.

## Should

- Work on Objects that aren't Instances, like `EditableImage`.
- Error on a property that doesn't exist or belongs to another class.
- Error when given something that isn't an Object.
