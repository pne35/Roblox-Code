# Flashlight

**Game:** Horror Islands  
**Type:** LocalScript  
**Location:** StarterPlayerScripts

## What it does

Implements a mouse-tracking flashlight that the player can toggle on and off with right-click. Also handles a scripted scare sequence where the flashlight flickers automatically and a scripted enemy character moves into position.

## Features

- **Right-click toggle** — flashlight clones a part from ReplicatedStorage and parents it to the camera rig on press; destroys it on release
- **Real-time mouse tracking** — uses `RunService.RenderStepped` and `TweenService` to smoothly orient the flashlight toward `Mouse.Hit.Position` every frame
- **Debounce system** — prevents rapid toggling by enforcing a minimum time between state changes (default 0.35s)
- **Scripted scare sequence** — on campfire detection, repositions the `ScaryGuy` NPC, triggers a flickering sequence, then moves the NPC to its end position and temporarily disables player control of the flashlight

## Key implementation details

- `TweenInfo` with `Enum.EasingStyle.Sine` for smooth directional interpolation rather than snapping
- `canToggle` flag used during the scripted sequence to prevent player interference
- Guards against missing `PrimaryPart` on the NPC with a fallback `FindFirstChildWhichIsA("BasePart")`
- Supports both mouse (MouseButton2) and gamepad (ButtonR2) input via `UserInputService`

## What I learned

Real-time input handling at render speed requires care around performance — attaching logic to `RenderStepped` runs every frame, so keeping the per-frame work minimal matters. The debounce pattern here is also something I've reused in other projects.
