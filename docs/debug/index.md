---
summary: Look inside running functions and change their upvalues, constants and locals.
---

# Debug

Roblox's own `debug` library can tell you a function's name and line, and that's about it. These functions go further. You can read and change a function's upvalues and constants, walk its nested functions and edit the locals of a running thread.

A few words come up on every page here:

- **Upvalue**: a local from outside the function that the function uses.
- **Constant**: a fixed value inside the function's code, like a string, a number or a global's name.
- **Proto**: the compiled blueprint of a function nested inside another function.
- **Stack level**: a position on the call stack. Level 1 is the function calling `debug.something`, level 2 is the function that called it, and so on.

Most functions take either a function or a stack level. All of them work on game scripts, not only on your own code. C functions have no upvalues, constants or protos you're allowed to touch, so these functions shouldn't work on them.
