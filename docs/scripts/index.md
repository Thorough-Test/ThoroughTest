---
summary: Find the game's scripts and look inside them.
---

# Scripts

A game sends your client its LocalScripts and ModuleScripts as compiled bytecode. The source isn't there, but everything you need to study it is. These functions find scripts, read their bytecode, decompile them and reach into the ones that are running.

Two kinds of lists come up here, and they're easy to mix up. [getrunningscripts](getrunningscripts.md) returns scripts that are running now, and [getscripts](getscripts.md) returns every script that exists, running or not.
