# FramZ 🌾

A 2D top-down farming game built with **Godot 4.4**, inspired by games like Stardew Valley. Chop trees, mine rocks, till soil, water crops, and interact with NPCs — all in a pixel-art world.

> ⚠️ **Work in Progress** — The game is still under active development. There is no main scene yet; individual scenes can be run and tested separately in the Godot editor.

## Gameplay Features (Implemented So Far)

- **4-directional player movement** with WASD / Arrow keys
- **Tool system** — equip an axe, hoe, or watering can and use them with left click
- **Choppable trees** — hit trees with an axe; they shake, take damage, and drop a log on destruction
- **Mineable rocks** — same damage system; rocks drop stone when destroyed
- **Tillable dirt** — use the hoe to till ground tiles
- **Watering** — water tilled crops with the watering can
- **Interactive doors** — walk up to a house door and it opens automatically; walk away and it closes
- **NPC chickens** — wander the map using NavigationAgent2D, alternating between idle and walk states on random cycles
- **Collectables** — pick up items (logs, stones, eggs) by walking over them

## Controls

| Action | Key / Button |
|--------|-------------|
| Move | WASD or Arrow Keys |
| Use Tool | Left Mouse Button |

## Getting Started

### Requirements

- [Godot Engine 4.4](https://godotengine.org/download) (Forward Plus renderer)

### Running the Project

1. Clone or download this repository
2. Open Godot and choose **Import Project**
3. Navigate to the `framz/` folder and select `project.godot`
4. Since the game is still in development, open a test scene manually from `scenes/test/` and press **F6** to run it

### Available Test Scenes

| Scene | What it tests |
|-------|--------------|
| `test_scene_tile_default.tscn` | Basic tilemap |
| `test_scene_tile_map.tscn` | Tilemap with terrain |
| `test_scene_tile_house.tscn` | House with interactive door |
| `test_scene_tile_Npc_chicken.tscn` | NPC chicken wandering |
| `test_scene_tile_object_rocks.tscn` | Rock objects with damage system |

## Project Structure

```
framz/
├── assets/
│   └── game/
│       ├── Characters/     # Player, chicken, cow spritesheets
│       ├── Objects/        # Furniture, plants, tools, items
│       └── Tilesets/       # Grass, dirt, hills, fences, doors
├── scenes/
│   ├── character/
│   │   ├── player/         # Player states: idle, walk, chopping, tilling, watering
│   │   └── chicken/        # Chicken NPC states: idle, walk
│   ├── components/         # Reusable components: damage, hurt, hit, interactable, collectable
│   ├── houses/             # Door scene with open/close interaction
│   ├── object/
│   │   ├── trees/          # Large & small trees with shake shader + log drop
│   │   └── rocks/          # Rocks with shake shader + stone drop
│   └── test/               # Test scenes (run these during development)
└── project.godot
```

## Architecture

The project uses a **state machine** pattern for both the player and NPCs. Each state (idle, walk, chopping, etc.) is a separate `NodeState` script that handles its own animation, physics, and transition logic.

**Reusable components** are scene-instanced nodes that handle cross-cutting concerns:

| Component | Role |
|-----------|------|
| `DamageComponent` | Tracks hit points and emits a signal when max damage is reached |
| `HurtComponent` | Detects when a matching tool's `HitComponent` overlaps it |
| `HitComponent` | Attached to the player's active tool swing area |
| `InteractableComponents` | Emits signals when the player enters/exits an interaction zone |
| `CollectableComponents` | Removes the item from the scene when the player walks over it |

## Tech

- **Engine:** Godot 4.4 (GDScript)
- **Renderer:** Forward Plus
- **Resolution:** 640×360 (scaled to 1280×720 with integer scaling)
- **Physics layers:** ground, player, interactable, tool, object, collectable
- **Navigation:** NavigationServer2D for NPC pathfinding

## License

MIT License — free to use and modify.
