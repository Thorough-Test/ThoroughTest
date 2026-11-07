---
summary: Draw shapes, text and images on top of the game.
---

# Drawing

The Drawing library draws straight on the screen, above the game and its UI. Nothing it makes is an Instance, so game scripts can't find it in the DataModel. That makes it the usual choice for ESP and overlays.

`Drawing.new` creates an object, and you change it by setting properties. New drawings start hidden, so set `Visible` to `true` once they're ready.

> **Note:** Drawings stay on screen until you destroy them, even after your script ends. Clean up with `Destroy` or [cleardrawcache](cleardrawcache.md).
