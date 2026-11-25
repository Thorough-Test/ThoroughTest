---
summary: Writes a property that scripts normally can't.
---

# sethiddenproperty

```luau
sethiddenproperty(object: Object, property: string, value: any) -> boolean
```

Sets a property's value. It returns `true` if the property was hidden and `false` if it was a normal one. Both are written.

## Parameters

- `object`: The instance, or another Object like an `EditableImage`.
- `property`: The property's name.
- `value`: The new value.

## Example

```luau
local Fire = Instance.new("Fire")

sethiddenproperty(Fire, "size_xml", 6)

print(Fire.Size) -- 6
```

## Must

- Change hidden properties.
- Change normal properties too.
- Never accept a property that doesn't exist, or exists only on another class.

## Should

- Work on Objects that aren't Instances, like `EditableImage`.
- Return `true` for hidden properties and `false` for normal ones.
- Error on a property that doesn't exist or belongs to another class, instead of doing nothing.
- Error when given something that isn't an Object.
