---
summary: Reach the garbage collector, the registry and the global tables.
---

# Environment

These functions let you see what else is running. `getgc` and `filtergc` find functions and tables that are still alive. `getreg` reads the Luau registry. `getgenv` and `getrenv` return the two global tables: your own and the game's.

Scripts in an executor have their own globals, separate from the game's. Writing to one doesn't change the other unless you do it on purpose.
