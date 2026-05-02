# Dialogues

**Game:** Horror Islands  
**Type:** LocalScript  
**Location:** StarterPlayerScripts

## What it does

Drives all in-game dialogue sequences for Horror Islands. Three separate narrative moments are triggered by server-fired `RemoteEvent`s — the game intro, a campfire encounter, and discovering a ruin. Each sequence displays text with a typewriter animation effect.

## Dialogue sequences

| Trigger Event | Scene | Dialogue |
|---|---|---|
| `IntroStart` | Game start | Two lines setting up the island premise |
| `CampfireEnterDetection` | Campfire area | Reaction to seeing something strange |
| `RuinFound` | Ruin location | Discovery of a magical ruin |

## Key implementation details

- **Typewriter effect** — text is rendered character by character using `string.sub` with a `wait(0.05)` delay, giving a natural typing feel
- **Event-driven triggers** — each dialogue fires from the server via `RemoteEvent.OnClientEvent`, keeping the client and server loosely coupled
- **Per-sequence index tracking** — separate index variables for each dialogue sequence prevent state bleed between scenes
- **Colour-coded text** — each sequence uses a distinct `TextColor3` to visually differentiate narrative moments (red for intro, black for campfire, white for ruin)

## What I learned

Managing multiple independent dialogue states simultaneously without them interfering with each other required careful variable scoping. The typewriter effect also introduced the importance of frame-rate considerations — `wait()` in a tight loop can cause jitter on lower-end machines.
