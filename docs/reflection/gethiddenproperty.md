---
summary: Reads a property that scripts normally can't.
---

# gethiddenproperty

```luau
gethiddenproperty(instance: Instance, property: string) -> (any, boolean)
```

Returns a property's value, and whether the property is hidden. It works on normal properties too, in which case the second value is `false`.

Reading a property this way doesn't make it scriptable, and it reads `BinaryString` properties as strings.

## Parameters

- `instance`: The instance.
- `property`: The property's name.

## Example

```luau
local part = Instance.new("Part")

print(gethiddenproperty(part, "Name")) -- Part false
print(gethiddenproperty(part, "NetworkOwnerV3")) -- 0 true
```

## Must

- Return the value and `false` for normal properties.
- Return the value and `true` for hidden properties.
- Leave a hidden property hidden after reading it.
- Read `BinaryString` properties.
- Never return a value for a property that doesn't exist.
- Error when given something that isn't an instance.

## Should

- Error on a property that doesn't exist, instead of returning nothing.
