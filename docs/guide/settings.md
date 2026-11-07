---
summary: Test one function, cut down the output and track down crashes with TTConfig.
---

# Settings

Set `getgenv().TTConfig` before you run TT. Everything is optional, so you only need the ones you care about.

```luau
getgenv().TTConfig = {
    only = { "hookfunction", "Filesystem" },
    output = "problems",
}
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

| Setting | Type | Default | What it does |
| --- | --- | --- | --- |
| `only` | list | everything | Runs just these tests or areas. |
| `skip` | list | nothing | Leaves these tests or areas out. |
| `output` | string | `"all"` | `"problems"` hides passing tests in the console. |
| `delay` | number | `0` | Seconds to wait between tests, up to 5. |
| `stopOnFail` | boolean | `false` | Stops at the first failed test. |
| `crashLog` | boolean | `false` | Saves the current step to a file while it runs. |
| `copyLink` | boolean | `true` | Copies the results link to your clipboard. |

TT warns you about a setting or a name it doesn't recognize, so a typo won't quietly run the wrong thing.

> **Note:** A run with `only`, `skip`, or one cut short by `stopOnFail` is a partial run. It works the same way but nothing is uploaded, because a score from half the tests wouldn't mean anything.

## only

Names can be tests or whole areas from the [tests page](https://thoroughtest.lol/tests). Capitals don't matter.

```luau
getgenv().TTConfig = {
    only = { "debug.getinfo", "Closures" },
}
```

## skip

Works just like `only`, and wins if a test is on both lists. Use this when one test crashes your client and you still want to see the others.

```luau
getgenv().TTConfig = {
    only = { "Signals" },
    skip = { "replicatesignal" },
}
```

## output

`"problems"` keeps fails, warnings and missing functions in the console and hides passing tests. Section titles stay so you can see the run moving. Your result page still has the complete output.

## delay

Slows the run down. It's handy when you're watching a debugger or your own logs and want time to see which test did what.

## stopOnFail

Stops at the first failed test. It's made for fixing things one at a time: fix it, run it again, see what's next. Missing functions don't count as a fail here.

## crashLog

Before each test, TT writes its name to `ThoroughTest_last_test.txt` in your workspace. It does the same for the steps around the tests, from startup to the results. If the run finishes, the file is deleted. If your client dies or freezes, the file stays, and the next run with `crashLog` on tells you where it stopped:

```
⚠️ the last run stopped during getgc
```

It's off by default because it writes a file before every test.

## copyLink

Set this to `false` to keep TT off your clipboard. The results link is printed in the console instead.
