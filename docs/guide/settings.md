---
summary: Test one function, cut down the output and track down crashes with TTConfig.
---

# Settings

Set `getgenv().TTConfig` before you run TT. Every setting is optional, so only set the ones you need.

```luau
getgenv().TTConfig = {
    only = { "hookfunction", "Filesystem" },
    output = "problems",
}
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

| Setting | Type | Default | What it does |
| --- | --- | --- | --- |
| `only` | list | everything | Runs only these tests or areas. |
| `skip` | list | nothing | Leaves these tests or areas out. |
| `output` | string | `"all"` | `"problems"` hides passing tests in the console. |
| `delay` | number | `0` | Seconds to wait between tests, up to 5. |
| `stopOnFail` | boolean | `false` | Stops at the first failed test. |
| `crashLog` | boolean | `false` | Saves the current test and check to a file while it runs. |
| `copyLink` | boolean | `true` | Copies the results link to your clipboard. |

TT warns about a setting or a test name it doesn't recognize, so typos show up in the console:

```
⚠️ TTConfig has no setting called crashlog
⚠️ TTConfig.only: hookfuntion isn't a test or an area
```

> **Note:** A run with `only` or `skip`, or one cut short by `stopOnFail`, is a partial run. It runs the same way, but nothing is uploaded, because a score from part of the tests wouldn't mean anything.

## only

Runs only the tests you list. A name can be a test or a whole area from the [tests page](https://thoroughtest.lol/tests), and capitals don't matter.

```luau
getgenv().TTConfig = {
    only = { "debug.getinfo", "Closures" },
}
```

## skip

Leaves tests out. It takes the same names as `only`, and if a test is on both lists, it's skipped. Use it when one test crashes your client and you want results for the rest.

```luau
getgenv().TTConfig = {
    only = { "Signals" },
    skip = { "replicatesignal" },
}
```

## output

`"problems"` hides passing tests in the console. Fails, warnings, missing functions and section titles still print. The results page always has the full output.

```luau
getgenv().TTConfig = {
    output = "problems",
}
```

## delay

Waits between tests, in seconds. Anything over 5 is treated as 5. Use it to match each test to what your debugger or logs show.

```luau
getgenv().TTConfig = {
    delay = 1.5,
}
```

## stopOnFail

Stops at the first failed test, so you can fix one problem at a time. A missing function doesn't count as a fail here.

```luau
getgenv().TTConfig = {
    stopOnFail = true,
}
```

## copyLink

Set it to `false` to print the results link in the console instead of copying it.

```luau
getgenv().TTConfig = {
    copyLink = false,
}
```

## crashLog

Shows which test and check your executor crashed or froze on.

With `crashLog` on, TT writes what it's about to do to `ThoroughTest_last_test.txt` in your workspace: the name of each test before it starts, and each check inside it before it runs. It does the same for the steps outside the tests, from startup to the results. When the run finishes, TT deletes the file. If your client crashes or freezes, the file stays, and the next run with `crashLog` on reads it and tells you where it stopped.

It's off by default because it writes a file before every test and every check.

### Example

If your executor crashes during a run, turn on `crashLog` and run TT:

```luau
getgenv().TTConfig = {
    crashLog = true,
}
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

When the client crashes, `ThoroughTest_last_test.txt` stays in your workspace with the last test and check TT started:

```
test
getsenv
a script that isn't running
```

Rejoin and run it again with `crashLog` on. TT prints where the last run stopped:

```
⚠️ ThoroughTest thinks your executor crashed while testing getsenv. It seems to have stopped on this check: a script that isn't running
```

That check calls `getsenv` on a `LocalScript` that has never run, so the crash is in that call. To see the rest of your results while you fix it, skip that test:

```luau
getgenv().TTConfig = {
    crashLog = true,
    skip = { "getsenv" },
}
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

If the crash happens outside a test, the message names the step instead, like `ThoroughTest thinks your executor crashed during the connection to TT's server.`
