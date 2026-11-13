---
summary: Sets the maximum frame rate.
---

# setfpscap

```luau
setfpscap(fps: number) -> ()
getfpscap() -> number
```

Sets the frame rate cap. Use `0` to remove it. `getfpscap` returns the cap.

## Parameters

- `fps`: The cap. `0` means no cap.

## Example

```luau
setfpscap(30) -- save power while you're idle
task.wait(60)
setfpscap(0)
```

## Must

- Keep the frame rate near the cap.
- Remove the cap with `0`.
- Never accept a negative cap.

## Should

- Have `getfpscap`, and return the value that was set.
- Accept numbers written as strings.
- Error on a negative cap, instead of doing nothing.
- Error with no argument, or with a boolean.
