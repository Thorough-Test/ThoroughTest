---
summary: Work with instances in ways normal scripts can't.
---

# Instances

Luau scripts never hold an instance directly. They hold a userdata reference, and Roblox keeps one reference per instance in a cache. That's why `part == part` works, and why the `cache` functions and [cloneref](cloneref.md) exist.

The rest of this library covers finding instances that are out of reach, like ones parented to `nil`, hiding your UI, and firing the things players normally trigger by hand: clicks, prompts and touches.
