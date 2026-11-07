---
summary: What ThoroughTest is, who it's for and where to start.
---

# ThoroughTest docs

ThoroughTest, or TT, runs a Roblox executor through a set of real tests and tells you which functions work the way scripts expect. These docs are the standard behind those tests. Every function has a page that explains what it does and exactly what TT holds it to.

## Who this is for

**Script developers** can use these pages as a reference. If a function has a page here, the rules on that page are what you should be able to count on. Executors that pass TT behave the same way, so you write less code to work around each one.

**Executor developers** can treat every page as a spec. Nothing is hidden behind a test you can't read about. If TT fails your function, the page says what it wanted and the fail message tells you which rule you broke.

## What makes TT different

- **Rules are public.** Every function page lists what must work and what's only preferred.
- **Tests check behavior.** Checking that a name exists proves nothing, so TT calls functions on real game scripts, real remotes and real Actors.
- **A game server is involved.** TT runs in its own place. When a test says a hook changed what the server received, that result came from the server itself.
- **Fails are saved for real problems.** A function that does a different job fails. Two reasonable ways to do the same job gets a warning at most. [The standard](standard.md) explains where that line is.

## Where to start

- Want to test an executor? Go to [Running the test](running.md).
- Staring at a result page? Go to [Reading results](results.md).
- Debugging one function? Pick its library from the sidebar, or use [Settings](settings.md) to test only that function.
- Want to know how TT decides what's right? Go to [The standard](standard.md).

## Libraries

| Library | What it covers |
| --- | --- |
| [Actors](../actors/index.md) | Running code inside Actors and talking between Luau states |
| [Closures](../closures/index.md) | Hooking, cloning and telling function types apart |
| [Debug](../debug/index.md) | Reading and changing upvalues, constants, stacks and protos |
| [Drawing](../drawing/index.md) | Drawing on the screen outside of the game's UI |
| [Encoding](../encoding/index.md) | base64, lz4, hashing and AES |
| [Environment](../environment/index.md) | The garbage collector, the registry and the global tables |
| [Filesystem](../filesystem/index.md) | Files in the executor's workspace |
| [Instances](../instances/index.md) | The instance cache, hidden UI and firing clicks, prompts and touches |
| [Metatable](../metatable/index.md) | Raw metatables, read-only tables and namecall |
| [Miscellaneous](../miscellaneous/index.md) | Executor identity, HTTP requests and FPS caps |
| [Reflection](../reflection/index.md) | Hidden properties and thread identity |
| [Scripts](../scripts/index.md) | Decompiling, bytecode and finding scripts |
| [Signals](../signals/index.md) | Firing signals and reading their connections |
| [WebSocket](../websocket/index.md) | Talking to WebSocket servers |
