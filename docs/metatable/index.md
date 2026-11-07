---
summary: Bypass metatable locks and change read-only tables.
---

# Metatable

Metatables are how instances work. Reading a property runs `__index`, and calling a method runs `__namecall`. Roblox locks these down so normal scripts can't touch them. The functions here lift that restriction.

To hook a metamethod, use [hookmetamethod](../closures/hookmetamethod.md). It's safer than writing to the metatable yourself.
