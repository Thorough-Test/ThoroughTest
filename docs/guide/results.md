---
summary: What the verdict, the score, warnings and missing functions actually mean.
---

# Reading results

Every finished run gets a page with its own link. Share it however you like. It holds the executor's name and version, the results and the console output, and nothing about you.

## Verdicts

The tag next to the executor's name tells you how much to trust the page.

| Verdict | What happened |
| --- | --- |
| **Verified** | The server ran its own checks during the run and every one passed. |
| **Sub-optimal** | The server checks passed, but something else was running. A few results could be off, so try a fresh server. |
| **Tampered** | The game or the script was changed during the run. The test still finishes, but the results may not be correct. |
| **Spoofed** | The results were faked or don't match the server's own results. Don't trust the score. |

## Test results

Every test ends up as one of these.

| Result | Meaning | Counts against the score |
| --- | --- | --- |
| **Passed** | The function does its job. | No |
| **Failed** | The function exists but doesn't do its job. | Yes |
| **Missing** | The function doesn't exist. | Yes |
| **Skipped** | The test couldn't run because of something outside of the function. | No |

A test can pass and still have **warnings**. A warning means the function works, but not the way the standard prefers. Warnings never change the score.

Sometimes one test needs a second function, like `restorefunction` needing `hookfunction`. If that second function is missing, the test is skipped or marked missing with a message saying why, so one gap doesn't turn into a pile of confusing fails.

## The score

```
score = passed / (passed + failed + missing)
```

The console also prints a second number that leaves missing functions out. That one tells you how well the functions an executor has actually work. A high second number and a low first number means it's correct but incomplete.

## The console view

The terminal button on a result page shows the run exactly as it printed, timestamps included. This is the best thing to send a developer when something looks wrong.

## What gets stored

TT doesn't store your IP, username or user ID. If a test prints something that contains your name or user ID, the game server removes it before anything leaves the place.
