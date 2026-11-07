---
summary: Read hidden properties and change what a thread is allowed to do.
---

# Reflection

Instances have more properties than the API shows. Some are hidden from scripts entirely, and some are only there for saving and loading. These functions reach them.

The other half of this library is **thread identity**. Every thread has an identity level that decides which APIs it can use. Game scripts run at 2, and executors run at a higher level so they can reach things like `CoreGui`.
