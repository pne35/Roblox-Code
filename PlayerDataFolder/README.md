# PlayerData

**Game:** Cookie Selling Sim  
**Type:** Server Script  
**Location:** ServerScriptService

## What it does

Handles all persistent player data for Cookie Selling Sim using Roblox's `DataStoreService`. When a player joins, it initialises their stats and loads any previously saved data. When they leave — or the server shuts down — their data is saved back to the DataStore.

## Stats tracked

| Stat | Default | Description |
|---|---|---|
| `cash` | 100 | In-game currency |
| `cookies` | 10 | Current cookie count |
| `backpackSize` | 25 | Storage capacity |
| `sellMultiplier` | 2 | Cash earned per cookie sold |
| `cookieMultiplier` | 1 | Cookie production rate |
| `deliveryCapacity` | 5 | Cookies deliverable per trip |
| `chefLevel` | 1 | Passive cookie production rate |
| `driverLevel` | 1 | Passive delivery rate |

## Key implementation details

- Uses `pcall` to safely wrap all DataStore operations — errors are caught and warned without crashing the server
- Binds to `game:BindToClose` to ensure data is saved on server shutdown, not just on player disconnect
- Stats are split across `leaderstats` (visible on leaderboard: cash, cookies) and direct player children (upgrade stats)

## What I learned

Handling persistent data correctly in a multiplayer game requires careful error handling — a failed DataStore read should never leave a player with broken state, and a failed write should never silently lose progress. This script was my first real use of `pcall` in production code.
