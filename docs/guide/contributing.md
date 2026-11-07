---
summary: How to fix a page, what a good one looks like and how the standard changes.
---

# Contributing

Spot a mistake, a confusing sentence or an example that could be better? Please fix it. Most changes take five minutes and need nothing installed. The page you're reading is one Markdown file, and the edit link at the bottom of every page takes you right to it.

## Two kinds of changes

**Fixing the docs.** Typos, clearer wording, better examples, a parameter that's described wrong. Open a pull request. No need to ask first.

**Changing the standard.** Adding or removing a rule, or moving one between Must and Should, changes how every executor gets scored. These start as an issue. See [Changing the standard](#changing-the-standard).

Not sure which yours is? If the change would make an executor pass or fail differently, it's the second kind.

## Where things live

Each library is a folder, and each function is a file.

```
docs/
  guide/              pages like this one
  closures/
    index.md          the library's intro
    hookfunction.md   one function
  debug/
    getinfo.md        debug.getinfo
```

GitHub shows these files the same way the site does, so the Preview tab on GitHub is all you need to check your work. Links are normal relative links to other `.md` files, like `[newcclosure](newcclosure.md)`.

## What a function page looks like

Copy this and fill it in. Every function page has the same shape so people can find what they need without reading it all.

````markdown
---
summary: One sentence. This also shows up when you hover the function on the tests page.
---

# functionname

```luau
functionname(first: string, second: number?) -> boolean
```

A paragraph or two on what it does and why someone would use it.

## Parameters

- `first`: What this is.
- `second`: Optional. What this is, and what happens if you leave it out.

## Example

```luau
print(functionname("hello")) -- true
```

## Must

- A rule TT fails the function for.

## Should

- A rule TT warns about.
````

- The `#` title has to be the function's exact name.
- Leave out **Parameters** if there aren't any, and **Should** if there's nothing to prefer.
- The `summary` has to make sense on its own, because the hover shows nothing else.

## Writing like a person

Pretend you're explaining this to a friend who writes scripts. They're smart, they're busy, and they've never seen this function.

- **Start with what it does.** Then say why you'd want it.
- **Write short sentences.** If one needs a semicolon, it wants to be two.
- **Use contractions and American spelling.** "Doesn't" and "behavior," not "does not" and "behaviour."
- **Keep it direct.** "Returns a table" beats "a table is returned to the caller."
- **Skip the filler.** "Simply," "just," "please note that," "it is worth mentioning" can all go.
- **Don't sell it.** "Powerful," "seamless" and "robust" don't tell anyone anything.

| Instead of | Write |
| --- | --- |
| This function can be utilized to retrieve the upvalues of a closure. | Gets a function's upvalues. |
| Please note that an error will be thrown in the event of an invalid index. | A bad index errors. |
| Provides seamless hooking capabilities. | Replaces what a function does. |
| You get back a table of matches. | Returns a table of matches. |

## Examples that earn their spot

An example should show something someone would really do. A list of random calls with no point teaches nothing.

- **Solve a small, real problem.** "Log every remote call" beats `hookfunction(a, b)`.
- **Make it runnable.** Paste it into an executor and it should work as written.
- **Show the output.** There are no videos here, so put what prints in a comment, like `print(1 + 1) -- 2`.
- **Keep it short.** Under 15 lines is great. If it's longer, it's probably two examples.
- **Use real names.** `OriginalIndex` tells you more than `Old`, and `Old` tells you more than `X`.
- **Use PascalCase for names you make up.** `PlayerCoins`, not `playerCoins`. Real API names and fields stay exactly as they are.

Before and after beats a wall of comments:

```luau
local function Greet()
    return "hello"
end
print(Greet()) -- hello

hookfunction(Greet, function()
    return "goodbye"
end)
print(Greet()) -- goodbye
```

## Changing the standard

Open an issue and answer these three things:

1. **What should change?** The function and the rule, in plain words.
2. **Who does it help?** A real script that breaks or gets harder without it.
3. **Can executors do it?** If it's only possible on one, it probably doesn't belong.

The project owner makes the final call on the standard, since one voice keeps the rules consistent. A good argument with a real example goes a long way, and "that's what another test does" doesn't go anywhere.

The test code and anti-tamper checks stay private, so don't worry about those. Describing the rule is enough. If it gets accepted, the test gets written and the page gets updated together.

## Credit

There's no contributors page to keep up. Your name stays on your work in the GitHub history, which is the honest record of who did what.
