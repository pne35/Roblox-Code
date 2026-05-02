# FormatNumber (GUI Updater)

**Game:** Cookie Selling Sim  
**Type:** LocalScript  
**Location:** StarterPlayerScripts

## What it does

Listens for a `RemoteEvent` fired from the server and updates all currency and upgrade cost labels in the player's GUI. Uses a `FormatNumber` module to display large values in compact form (e.g. `1,200` → `1.2K`).

## GUI elements updated

| Label | Content |
|---|---|
| Cash | Current cash balance |
| Cookies | Current cookies / backpack capacity |
| Cookies/sec | Chef level (passive production rate) |
| Delivering/sec | Driver level (passive delivery rate) |
| Storage upgrade cost | `backpackSize × 3` |
| Delivery upgrade cost | `deliveryCapacity × 30` |
| Sell upgrade cost | `sellMultiplier × 250` |
| Cookie upgrade cost | `cookieMultiplier × 200` |
| Chef upgrade cost | `(chefLevel + 1) × 1000` |
| Driver upgrade cost | `(driverLevel + 1) × 1000` |

## Key implementation details

- All values routed through `FormatNumber.FormatCompact` for consistent large-number display
- Upgrade costs are computed client-side from raw stat values using simple scaling formulas
- GUI visibility (`frame2.Visible = false`) on init prevents a flash of default text before the first server update fires
- Server fires `UpdateGui` RemoteEvent whenever any relevant stat changes, keeping the client purely reactive

## What I learned

Separating the data model (server) from the display layer (client) via RemoteEvents makes the codebase much cleaner — the client doesn't need to know how values change, only how to display them. The compact number formatter also highlighted the value of reusable utility modules.
