---
summary: What ThoroughTest's rules are based on and how a result gets decided.
---

# The standard

The standard is ThoroughTest's answer to one question: what should a Roblox script be able to count on from an executor? It gives script developers behavior they can rely on and gives executor developers a clear target.

## What it's based on

Three things shape every rule.

**Real scripts.** The rules come from what scripts do every day, like hooking functions, reading files, searching the garbage collector and talking to the server. A difference that wouldn't affect a real script doesn't become a rule.

**What developers expect.** Most of these functions are named after something in Luau or Roblox, or have been around long enough that people know how they act. A function should behave the way an experienced developer would guess before reading its page.

**What executors can build.** A rule only helps if it can be met, so each one has to be within reach of a team working on a normal Roblox client. Features only one executor offers aren't part of the standard, since scripts can't depend on them.

Older test suites and documentation taught us a lot, but the standard is its own thing. Where an old convention is bad for scripts, we went with the better behavior.

## Pass, warning or fail

A **fail** means the function doesn't do its job. Wrong answers, made up results, functions that quietly do nothing and swapped arguments all land here, because a script relying on them would break.

A **warning** means the function works, but differently from what we recommend. Scripts will almost always run fine, and warnings don't lower the score.

Function pages use the same split. **Must** rules are the ones that fail, and **Should** rules are the ones that warn.

## Bad input

What a function does with bad input says a lot about how safe it is to build on. There are two kinds.

The **wrong type** is a bug in the calling script, like passing a number where a function belongs. The function should error right away, because staying quiet only hides the bug.

A **value that doesn't exist** is different. A missing file, an upvalue index past the end or a property that isn't real are all things a script might ask about. Erroring is still the clearest answer, but returning `nil` or an empty table is fair, so that's a warning. Making something up is a fail.

| Input | Errors | Returns nothing | Makes up a result |
| --- | --- | --- | --- |
| Wrong type | Pass | Fail | Fail |
| Doesn't exist | Pass | Warning | Fail |

## What every function is held to

- **It has to work.** A stub that does nothing or errors on every call is a fail. A function that isn't there is reported as missing.
- **Its results have to be real.** A hardcoded value that only looks right for the test's input is a fail.
- **It has to look native.** Anything marked `[C]` stays `[C]`, even after it's hooked.
- **It has to work on game code.** A debug function should handle game scripts as well as the executor's own closures.
- **It can't freeze the game.** A slow request or a big file can yield, but the client keeps running.
- **Its errors should read cleanly.** Real Roblox functions don't add line numbers to their errors, so a wrapper that adds one gets a warning.

## What's left out

TT doesn't test anything that could do damage. It won't crash your client on purpose or touch a file outside of your workspace.

It also doesn't care how something is built. There are plenty of ways to write a hook, and the standard only looks at how the result behaves in a script.

## How it changes

Luau, Roblox and executors all keep changing, so the standard does too. A new rule usually starts as a warning to give developers time to catch up, then becomes a fail later on. Changes start as an issue on GitHub, and [the contributing page](contributing.md#changing-the-standard) explains how that works.
