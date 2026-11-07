---
summary: Checks whether a signal can be replicated to the server.
---

# cansignalreplicate

```luau
cansignalreplicate(signal: RBXScriptSignal) -> boolean
```

Returns `true` if [replicatesignal](replicatesignal.md) can send this signal to the server.

## Parameters

- `signal`: The signal.

## Example

```luau
local detector = Instance.new("ClickDetector")

print(cansignalreplicate(detector.MouseActionReplicated)) -- true
print(cansignalreplicate(Instance.new("Part").Touched)) -- false
```

## Must

- Return `true` for signals that replicate.
- Return `false` for signals that don't, like `Touched` and bindable events.
- Error without a signal.
