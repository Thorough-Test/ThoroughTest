---
summary: How to run ThoroughTest and get a result you can trust.
---

# Running the test

TT only runs in its own place, so a result always comes from the same clean setup.

## Steps

1. Join the [test place](https://www.roblox.com/games/136884250234141).
2. Run this in your executor:

```luau
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

3. Leave the game alone until the console says it finished. Most runs take under 30 seconds.
4. Open your result. The link is copied to your clipboard and shown on a small card in the game.

## Getting a clean result

- Run it first. Other scripts can change the same functions TT is testing, and an auto-executed script counts.
- Use a fresh server if you already ran something else. TT marks a result as [sub-optimal](results.md#verdicts) when it finds something in the way.
- Don't touch your character during the run. A few tests click, touch and fire things in the world.

## If it doesn't start

| What you see | What to do |
| --- | --- |
| `TT only runs in its own place` | You're in another game. The place link is copied for you. |
| `couldn't reach TT's server` | Wait a few seconds and run it again. A new run can't start right after the last one. |
| `couldn't upload the results` | The run still counted, and the full output is in your console. Try again later for a link. |
| `Xeno does not support Luraph` | TT is protected with Luraph, and Xeno can't run Luraph scripts, so TT doesn't run on Xeno. |

## If your client crashes

Turn on `crashLog` and run it again. TT writes down each test and each step around them before it starts, and tells you where the last run stopped. This works for freezes too.

```luau
getgenv().TTConfig = { crashLog = true }
loadstring(game:HttpGet("https://thoroughtest.lol/script"))()
```

Then leave that test out with `skip` to see the rest of your result. [Settings](settings.md) has the details.
