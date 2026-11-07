---
summary: Creates a channel that carries messages between Luau states.
---

# create_comm_channel

```luau
create_comm_channel() -> (any, BindableEvent)
get_comm_channel(id: any) -> BindableEvent
```

Normal signals can't cross from one Luau state to another. A comm channel can. `create_comm_channel` returns an id and a channel, and any state can get that same channel by passing the id to `get_comm_channel`.

Pass the id into your Actor code, connect to `channel.Event` on one side, and call `Fire` on the other.

## Example

```luau
local id, channel = create_comm_channel()

channel.Event:Connect(function(message)
    print(message) -- hello from the actor
end)

run_on_actor(getactors()[1], [[
    local id = ...
    get_comm_channel(id):Fire("hello from the actor")
]], id)
```

## Must

- Return an id and a channel with an `Event`.
- Send every value through `get_comm_channel` in the same Luau state, nils included.
- Deliver messages from inside an Actor to the outside.
- Let code inside an Actor connect to the channel and receive messages from the outside.

## Should

- Have a `Fire` method on the returned channel, so sending doesn't need `get_comm_channel`.
- Error from `get_comm_channel` when the channel doesn't exist.
