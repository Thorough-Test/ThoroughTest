---
summary: Hook, clone and identify functions.
---

# Closures

A closure is a function and the variables it carries. Luau has two kinds: **Luau closures**, written in Luau, and **C closures**, written in C++, like `print` or `game.IsA`.

The difference matters because scripts and anti-cheats can tell them apart. An executor has to hook either kind without leaving a trace, and the functions in this library are how it's done.

Hooking has two main rules. A hooked function should look exactly like it did before, and the function `hookfunction` returns should behave exactly like the original.
