---
summary: Reads a callback property, like OnInvoke.
---

# getcallbackvalue

```luau
getcallbackvalue(instance: Instance, property: string) -> function?
```

Normally you can set a callback like `OnInvoke`, but you can't read it back. This reads it, including callbacks set by game scripts, and returns `nil` if nothing is set.

## Parameters

- `instance`: The instance.
- `property`: The callback's name.

## Example

```luau
local bindable = Instance.new("BindableFunction")
bindable.OnInvoke = function()
    return "hello"
end

print(getcallbackvalue(bindable, "OnInvoke")()) -- hello
```

## Must

- Return a working callback, for your own and for game scripts' callbacks.
- Return `nil` for an unset or cleared callback.
- Error when given something that isn't an instance.
