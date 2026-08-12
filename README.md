# Thornwake

A small top-down action RPG built entirely from scratch in vanilla JavaScript and the HTML5 Canvas API - no game engine, no libraries, no frameworks.

> *For as long as anyone living can remember, Thornwake has slept. Three nights ago the ground split beneath the old grove, and the thorns began to move on their own.*

You are the only witness to the awakening. Explore the village and the corrupted wilds beyond it, help the people of Thornwake, gear up, and descend into the grove to face whatever has been sleeping beneath it.

---

## Controls

| Action | Key |
|---|---|
| Move | `WASD` or Arrow Keys |
| Attack | `Space` |
| Talk / Interact | `E` |
| Inventory | `Tab` |
| Journal | `J` |
| Crafting | `C` |
| Mute Audio | `M` |
| Toggle Debug Info | `I` |
| Close Menus | `Esc` |

## Features

- **Living world** - a hand-built tilemap with grass, water, paths, walls, and trees, procedurally shaded per-tile for texture and life (swaying grass, rippling water, drifting leaves).
- **Four zones** to explore, each with its own visual identity and rising corruption: the Village, the Grove's Edge, the Hollow, and the Heart's Chamber - gated by quest progress and character level.
- **NPCs and dialogue** - talk to Mirela the herbalist, Bram the peddler, Dorn the blacksmith, and Aldric the warden, each with branching, state-aware lines.
- **Quest journal** - a multi-stage quest line with collection and kill objectives, plus a growing lore log discovered as you explore.
- **Combat** - real-time melee combat with knockback, damage popups, hit-stop, and screen shake, against a roster of enemies that wander, chase, and give up pursuit realistically (with A\* pathfinding).
- **A boss fight** - "The Heart of Thornwake," a multi-phase encounter with telegraphed melee, ranged, and summon attacks that escalate as its health drops.
- **Inventory & equipment** - a drag-and-drop inventory with stackable items, four equipment slots, and live stat recalculation.
- **Crafting & blacksmithing** - combine materials into stronger gear, then upgrade that gear further at the forge.
- **Shop economy** - buy and sell goods with Bram using gold looted from enemies.
- **Leveling & perks** - gain XP, level up, and unlock permanent perks like Thickened Hide and Quick Hands.
- **Three difficulty settings** (Easy / Normal / Hard) affecting enemy damage, enemy health, and your own damage output.
- **Full save system** - autosaves every 15 seconds and on exit, storing player stats, inventory, equipment, quest state, zone state, and settings in `localStorage`.
- **Procedural ambient audio** - every sound effect and music layer is synthesized live with the Web Audio API (oscillators, noise bursts, and filters) rather than played from audio files.
- **Title screen & difficulty select**, plus dedicated victory and game-over states with their own narration.

## Project Structure

| File | Responsibility |
|---|---|
| `index.html` | Page structure, canvas, and all UI overlays |
| `styles.css` | All visual styling |
| `game.js` | Core loop, tilemap, rendering, camera, input, collision |
| `inventory.js` | Items, equipment, inventory UI, player stats, world pickups, HUD |
| `combat.js` | Enemy definitions, damage math, player attacks, loot |
| `enemyAI.js` | Enemy wander / chase / return state machine |
| `pathfinding.js` | A\* pathfinding over the tile grid |
| `npc.js` | NPCs, dialogue system, dialogue UI |
| `journal.js` | Lore and quest journal UI |
| `quests.js` | Quest definitions and progress tracking |
| `zones.js` | Zone/map definitions, portals, gating, zone transitions |
| `boss.js` | Boss encounter logic, patterns, and rendering |
| `crafting.js` | Crafting recipes and UI |
| `shop.js` | Buy/sell shop logic and UI |
| `blacksmith.js` | Gear upgrade system and UI |
| `progression.js` | XP, leveling, and perks |
| `fx.js` | Screen shake, hit-stop, ambient leaves, thorn-creep overlay |
| `audio.js` | Procedurally synthesized music and sound effects (Web Audio API) |
| `endstates.js` | Game-over and victory screens |
| `titlescreen.js` | Title screen, difficulty selection, new game / continue |
| `save.js` | Save/load and autosave via `localStorage` |

## Technical Notes

- Everything is rendered with the 2D Canvas API at a fixed 800×600 resolution.
- The game loop uses `requestAnimationFrame` with delta-time updates and a frame-error guard so a single bad frame can't crash the whole game.
- Most cross-file calls are defensively wrapped in `typeof fn === "function"` checks, so the game degrades gracefully if a script is missing rather than hard-crashing.
- No external assets, libraries, or network requests are used - the entire game (including audio) is generated in code.
