# FuzzCraft 4 — Batch 1 Testing

**Pack version:** 0.0.1  
**Test date:** 2026-06-11  
**Tester:** Tom

---

## Single Player

- [x] Launches to main menu without crash
- [x] Video settings open without crash
- [x] Create new world — world generation completes without crash
- [x] World renders (terrain, sky, lighting all visible)
- [x] Jade — look at a block, tooltip appears
- [x] JEI — open inventory, recipe panel visible on right side
- [x] JEI — search for an item, results filter correctly
- [x] JourneyMap — minimap renders in HUD
- [x] JourneyMap — press J, full map opens
- [x] JourneyMap — set a waypoint
- [x] FTB Teams — personal team auto-created on first join
- [x] FTB Chunks — open chunk map, visible overlay
- [x] FTB Chunks — claim a chunk
- [x] FTB Chunks — claimed chunk shows protection overlay on map
- [x] Inventory Sorter — middle-click a container, items sort
- [x] Mouse Tweaks — drag items across slots to distribute
- [x] AppleSkin — hunger/saturation tooltip visible on food item in JEI or inventory
- [x] Iris — open video settings, Shader Packs button present
- [x] Dynamic Lights — hold a torch, surrounding area lights up
- [x] No errors or crashes after 10+ minutes of play

## Server

- [x] Server starts cleanly via `start.sh`
- [x] packwiz bootstrap runs and syncs on server start
- [x] All mods load (check mod count in server log)
- [x] FTB configs loaded (`ftbchunks-world.snbt`, `ftbteams-server.snbt`)
- [x] Server listening on port 25552
- [x] `Done (Xs)!` in server log — no errors at startup
- [x] Chunky — run `/chunky` in server console, command responds
- [x] JEI — recipe viewer works while connected to server
- [x] JourneyMap — minimap renders on server

## Known Issues

- **Reese's Sodium Options + SodiumOptionsAPI** — removed; incompatible with Sodium 0.6.x (built for 0.8.x Ruby rewrite). Re-add when ported.
- **No FTB Chunks + JourneyMap integration** — no addon available for 1.21.1. FTB Chunks built-in map is the workaround. Monitor for addon release.
- **Configured** — no NeoForge 1.21.1 build available. Deferred.

## Result

**PASS** — all single-player and server tests green. Multiplayer tests deferred to `multiplayer.md`.
