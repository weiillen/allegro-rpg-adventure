# Architecture Notes

## 1. Program entry and event loop

`Src/main.c` delegates startup to `startGame()` in `Src/game.c`. The game module initializes Allegro and its image, font, TTF, audio, codec, primitive, keyboard, and mouse subsystems. It creates the display, two timers, and a shared event queue.

The main loop waits for Allegro events, tracks keyboard state in `keyState`, reads the current mouse state, and invokes the active scene's `update()` and `draw()` callbacks when a display frame is due.

## 2. Scene abstraction

`Src/utility.h` defines a `Scene` structure containing a name and four function pointers:

- `init`
- `update`
- `draw`
- `destroy`

`change_scene()` destroys the outgoing scene, replaces it, initializes the incoming scene, and resets the timers. The preserved project contains menu, loading, gameplay, settings, and losing scenes.

## 3. Gameplay composition

`Src/game_scene.c` owns the principal runtime objects:

- one `Player`;
- one `Map`;
- a linked list of enemies;
- a linked list of bullets;
- one `Weapon`;
- health and coin HUD bitmaps.

During each update it checks for player death, updates movement, calculates a player-centered camera, advances enemies, updates the weapon and bullets, and advances the map animation state.

## 4. Map representation

`Src/map.c` reads `Assets/map0.txt` into a dynamically allocated two-dimensional tile array. The symbols used by the preserved level are:

| Symbol | Meaning |
|---|---|
| `#` | Wall |
| `.` | Floor |
| `P` | Player spawn |
| `S` | Slime spawn |
| `C` | Coin |
| `_` | Hole |

The submitted map is 19 rows by 21 columns. A second two-dimensional array stores sprite-atlas offsets. Neighbor-aware helper functions select the appropriate wall, floor, or hole tile from `Assets/map_packets.png`.

## 5. Player movement and collision

`Src/player.c` handles WASD movement, direction, animation ticks, knockback, health, damage tint, and death-state transitions. Collision checks test all four corners of the player's 64 × 64 tile-sized bounding box against the map's walkability rules.

## 6. Enemies and navigation

`Src/enemy.c` manages slime enemies. Each enemy can pursue the player, collide with the map, damage the player, receive projectile damage, enter a dying state, and be removed from the linked list.

Navigation uses breadth-first search on the tile grid. The implementation then performs line-of-sight checks across all four corners of the enemy footprint using a Bresenham-style traversal. When a clear line exists, movement is directed toward the player or a visible point along the recovered path.

## 7. Weapon and projectile systems

`Src/weapon.c` computes the weapon angle from the mouse position relative to the player and camera. A cooldown limits fire rate. Each shot creates a `Bullet` containing a position, angle, speed, damage value, and bitmap.

`Src/bullet.c` advances bullets with trigonometric motion, removes bullets that strike walls or leave the map, and applies damage when a bullet enters an enemy's bounding box. Bullet nodes are dynamically allocated and removed during list traversal.

## 8. UI and multimedia

`Src/UI.c` provides bitmap-backed hoverable buttons. `Src/utility.c` loads fonts, manages shared volume values, switches looping background music, and provides logging helpers. Scene modules load their own visual resources and release them in their `destroy()` callbacks.

## 9. Preserved limitations

The architecture notes intentionally describe the submitted state. They do not imply that placeholder systems such as coin collection, adjustable settings, or a win flow are complete.
