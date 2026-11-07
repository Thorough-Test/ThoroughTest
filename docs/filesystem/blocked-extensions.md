---
summary: Scripts can't create files that Windows would run.
test: "Filesystem: blocked extensions"
---

# Blocked extensions

A script from the internet should never be able to drop a program on your computer. That makes this one of the most important rules in the standard, and it covers `writefile` and `appendfile`.

These extensions have to be refused:

```
.exe .com .scr .pif .cpl .msc .bat .cmd .ps1 .psd1 .vbs .vbe
.js .jse .wsf .wsh .hta .scf .lnk .msi .msp .reg .inf .url
```

Normal data files have to keep working: `.txt`, `.lua`, `.luau`, `.json`, `.png` and `.mp3`.

Windows is forgiving about file names, so checking the last four letters isn't enough. Windows drops a trailing dot or space, so both of these end up as `run.exe` on disk:

```
run.exe.
run.exe  <- special character
```

## Example

```luau
local Blocked = pcall(writefile, "virus.exe", "payload")
print(Blocked) -- false

print(isfile("virus.exe")) -- false
```

## Must

- Refuse every extension above, in any case, through both `writefile` and `appendfile`.
- Refuse double extensions like `report.txt.exe`.
- Refuse tricks that end up as a blocked file on disk: trailing dots, trailing spaces, `::$DATA` and null bytes.
- Keep allowing `.txt`, `.lua`, `.luau`, `.json`, `.png` and `.mp3`.

## Should

- Refuse containers that can carry programs: `.zip`, `.rar`, `.7z`, `.cab`, `.iso`, `.img` and `.xml`.
- Return `false` from `isfile` for a blocked path, instead of erroring.
