# Use of Module Scripts — Sell System

**Game:** Cookie Selling Sim  
**Type:** ModuleScript  
**Location:** ServerScriptService/Modules

## What it does

A reusable module that handles the cookie selling transaction. When called, it checks the player's current cookie count against their delivery capacity, calculates the correct cash reward, modifies the player's cash via a separate `ModifyCash` module, and fires a GUI update event back to the client.

## Logic

```
if cookies >= deliveryCapacity:
    cash += deliveryCapacity × sellMultiplier
    cookies -= deliveryCapacity
else:
    cash += cookies × sellMultiplier
    cookies = 0
```

The player always sells whatever is smaller — their delivery capacity or their actual stock — preventing exploits where a player could sell more than they have.

## Key implementation details

- **Module pattern** — exposes a single `module.sell(player)` function, keeping the sell logic reusable and testable independently of whatever triggers it (a button press, proximity prompt, etc.)
- **Dependency injection via require** — pulls in `ModifyCash` and the `UpdateGui` RemoteEvent rather than duplicating that logic
- **Defensive checks** — verifies all required player values exist before proceeding, preventing nil errors if a stat is missing

## What I learned

Module scripts enforce a clean separation of concerns — the sell logic doesn't need to know what triggered the sale, and the trigger doesn't need to know how selling works. This was my introduction to writing genuinely reusable code rather than copying logic between scripts.
