---
summary: Run code inside Actors and send messages between Luau states.
---

# Actors

Every Actor in a game runs in its own Luau state, with its own globals and its own copy of everything. Plenty of games and anti-cheats now live inside Actors, which means an executor that can't reach them can't reach much of the game.

These functions let you find Actors, run your code inside them and talk to that code from the outside.

> **Note:** Code you send to an Actor can't access your variables. It's a separate state, so use a comm channel to pass data back and forth.
