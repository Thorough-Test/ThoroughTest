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
local Part = Instance.new("Part")

print(gethiddenproperty(Part, "Name")) -- Part false
print(gethiddenproperty(Part, "NetworkOwnerV3")) -- 0 true
```

## Must

- Return the value and `false` for normal properties.
- Return the value and `true` for hidden properties.
- Read `size_xml` on a `Fire`.
- Leave a hidden property hidden after reading it.
- Read `BinaryString` properties.
- Never return a value for a property that doesn't exist.

## Should

- Error on a property that doesn't exist, instead of returning nothing.
- Return `NetworkOwnerV3` as a number.
- Error when given something that isn't an instance.
