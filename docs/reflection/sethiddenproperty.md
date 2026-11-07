---
summary: Writes a property that scripts normally can't.
---

# sethiddenproperty

```luau
sethiddenproperty(instance: Instance, property: string, value: any) -> boolean
```

Sets a property's value. It returns `true` if the property was hidden and `false` if it was a normal one. Both are written.

## Parameters

- `instance`: The instance.
- `property`: The property's name.
- `value`: The new value.

## Example

```luau
local Fire = Instance.new("Fire")

sethiddenproperty(Fire, "size_xml", 6)

print(gethiddenproperty(Fire, "size_xml")) -- 6 true
```

## Must

- Change hidden properties.
- Change normal properties too.
- Never accept a property that doesn't exist.
- Error when given something that isn't an instance.

## Should

- Return `true` for hidden properties and `false` for normal ones.
- Error on a property that doesn't exist, instead of doing nothing.
