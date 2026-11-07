---
summary: Lists the signals the client is allowed to replicate.
---

# getsignalwhitelist

```luau
getsignalwhitelist() -> { { Event: string, Parent: string } }
```

Returns every signal the engine lets [replicatesignal](replicatesignal.md) use, as the signal's name and its class.

## Example

```luau
for _, entry in getsignalwhitelist() do
    print(`{entry.Parent}.{entry.Event}`)
end
```

## Must

- Return a non-empty list, with each entry having a string `Event` and `Parent`.
- Include `ClickDetector.MouseActionReplicated`.
