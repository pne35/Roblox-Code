# Lightning

**Game:** Horror Islands  
**Type:** Script  
**Location:** Workspace (attached to storm part)

## What it does

Generates procedural lightning strikes across the map on randomised intervals. Strikes are visually animated using beam width variation and incremental position updates, and a sound plays on each strike. A restricted area is defined to prevent strikes from hitting certain zones (e.g. the player spawn or key gameplay areas).

## Key implementation details

- **Randomised positioning** — each strike picks a random `(x, z)` offset within a 250-unit radius using `Random.new(tick())` for a unique seed per server
- **Restricted zone filtering** — a `repeat/until` loop resamples positions until one outside the restricted bounding box is found, preventing strikes in protected areas
- **Animated strike** — the beam's endpoint (`Att1`) moves incrementally from the cloud height to ground level over 5 steps, simulating a strike travelling downward
- **Randomised beam width** — `Width0` and `Width1` are varied per strike for visual diversity
- **Auto-cleanup** — `Debris:AddItem` removes strike parts after the sound finishes, preventing workspace accumulation
- **Randomised delay** — each cycle waits a random interval between 2 and 10 seconds before the next strike

## What I learned

Procedural systems need careful constraints — unlimited randomness breaks gameplay. The restricted zone check was added after playtesting showed strikes landing on spawn, which was frustrating. This was my first use of spatial bounding box logic in a game context.
