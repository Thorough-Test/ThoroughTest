---
summary: Lists the scripts running right now.
---

# getrunningscripts

```luau
getrunningscripts() -> { LuaSourceContainer }
```

Returns the scripts running on your client, including `Script`s with `RunContext` set to `Client`.

## Example

```luau
for _, Script in getrunningscripts() do
    print(Script:GetFullName())
end
```

## Must

- Include running LocalScripts and Scripts with `RunContext` set to `Client`.
- Include a running script that parented itself to `nil`.
- Leave out disabled scripts, server scripts and scripts with no bytecode.
- List each script once.
- Only list scripts.
