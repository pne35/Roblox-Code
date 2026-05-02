# Roblox Game Systems — Harry Smalley

A collection of Luau scripts written for two original Roblox games: **Horror Islands** (a horror exploration game) and **Cookie Selling Sim** (an idle/tycoon game). These were built independently from around age 13-14, covering everything from persistent data storage to real-time physics and UI systems.

## Scripts

| File | Game | Description |
|---|---|---|
| [`PlayerData`](./PlayerData) | Cookie Selling Sim | Persistent player data — saves and loads all stats via DataStoreService |
| [`Dialogues`](./Dialogues) | Horror Islands | Event-driven dialogue system with typewriter animation |
| [`Flashlight`](./Flashlight) | Horror Islands | Mouse-tracking flashlight with debounce, tweening, and scripted scare sequence |
| [`FormatNumber`](./FormatNumber) | Cookie Selling Sim | Live GUI updater using a compact number formatter for all currency and upgrade displays |
| [`Lightning`](./Lightning) | Horror Islands | Procedural lightning strike system with spatial restrictions and randomised timing |
| [`Use of module scripts`](./Use%20of%20module%20scripts) | Cookie Selling Sim | Module script demonstrating a reusable sell transaction system |

## Technical highlights

- **DataStoreService** with `pcall` error handling for safe persistent storage across sessions
- **Event-driven architecture** using `RemoteEvent` and `BindableEvent` for client-server communication
- **TweenService** for smooth real-time animations on flashlight movement
- **Procedural generation** for randomised lightning positioning with restricted zone avoidance
- **Module scripts** for reusable, decoupled game logic
- Written entirely in **Luau** (Roblox's typed superset of Lua 5.1)

## Languages & Tools

- Luau (Lua 5.1+)
- Roblox Studio
- Roblox DataStoreService API
