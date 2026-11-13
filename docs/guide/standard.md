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

Bad input is anything a function can't use: the wrong type, like a number where a function belongs, the wrong kind, like a Part where a script belongs, or something that doesn't exist, like a missing file.

Erroring is the best answer, because it points straight at the problem. Returning `nil`, `false` or an empty table is fair, since a script that passes good input never sees the difference, so that's a warning. Making up a result or doing something with the bad input is a fail, because the function is lying about what happened.

| Bad input | Errors | Returns nothing | Makes up a result or acts on it |
| --- | --- | --- | --- |
| Any kind | Pass | Warning | Fail |

## Options and features

If a feature has a real use and it not working causes a problem where it's used, it's a fail, even if most scripts never touch it. The `Cookies` option on `request` and reading a paused thread with `debug.getstack` both count, because a script using them gets the wrong result.

Bad input is the exception. Erroring on it only matters to a script that's already broken, so a script using the function correctly never hits a problem.

Being common in other test suites doesn't make something a fail. What matters is whether it causes a problem where it's used.

## What every function is held to

- **It has to work.** A stub that does nothing or errors on every call is a fail. A function that isn't there is reported as missing.
- **Its results have to be real.** A hardcoded value that only looks right for the test's input is a fail.
- **It has to look native.** Anything marked `[C]` stays `[C]`, even after it's hooked. Hooks, `newcclosure`, `gethui` and drawings are also checked from a real game script in TT's place, since that's who they're meant to fool.
- **It has to work on game code.** A debug function should handle game scripts as well as the executor's own closures.
- **It can't freeze the game.** A slow request or a big file can yield, but the client keeps running.
- **Its errors should read cleanly.** Real Roblox functions don't add line numbers to their errors, so a wrapper that adds one gets a warning.

## What's left out

TT doesn't test anything that could do damage. It won't crash your client on purpose or touch a file outside of your workspace.

It also doesn't care how something is built. There are plenty of ways to write a hook, and the standard only looks at how the result behaves in a script.

## How it changes

Luau, Roblox and executors all keep changing, so the standard does too. A new rule usually starts as a warning to give developers time to catch up, then becomes a fail later on. Changes start as an issue on GitHub, and [the contributing page](contributing.md#changing-the-standard) explains how that works.
