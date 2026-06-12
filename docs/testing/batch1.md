# FuzzCraft 4 — Batch 1 Testing: Foundation

## Summary
**Pack version:** 0.1.2
**Test date:** 2026-06-11
**Tester:** Tom
**Play mode:** Single player + Server

## Known Issues
- **Reese's Sodium Options + SodiumOptionsAPI** — removed; incompatible with Sodium 0.6.x (built for 0.8.x Ruby rewrite). Re-add when ported. Watchlisted.
- **Configured** — no NeoForge 1.21.1 build available. Deferred. Watchlisted.
- **No FTB Chunks + JourneyMap integration** — resolved mid-batch by adding JourneyMap Integration (modrinth: M1ZKbfkJ).

---

## Launch & Stability

- [x] Game launches to main menu without crash
- [x] Video settings open without crash
- [x] New world generates without crash
- [x] World renders correctly (terrain, sky, lighting)
- [x] No errors or crashes after 10+ minutes of play

## Regression
*N/A — Batch 1 is the foundation. No prior content to regress against.*

## Performance & Display

- [x] Iris — open video settings, Shader Packs button present
- [x] Dynamic Lights — hold a torch, surrounding area lights up without lag spike

## HUD & Overlays

- [x] JourneyMap — minimap renders in HUD
- [x] JourneyMap — press J, full map opens
- [x] JourneyMap — set a waypoint
- [x] AppleSkin — hunger/saturation tooltip visible on food item in JEI or inventory

## JEI

- [x] Recipe panel visible on right side of inventory
- [x] Search filters results correctly

## Jade

- [x] Look at a block — tooltip appears with block info

## Inventory

- [x] Inventory Sorter — middle-click a container, items sort
- [x] Mouse Tweaks — drag items across slots to distribute

## FTB Chunks & Teams

- [x] FTB Teams — personal team auto-created on first join
- [x] FTB Chunks — open chunk map, overlay visible
- [x] FTB Chunks — claim a chunk
- [x] FTB Chunks — claimed chunk shows protection overlay on map

## Server Tests

- [x] Server starts cleanly via `start.sh`
- [x] packwiz bootstrap runs and syncs on server start
- [x] All mods load — check mod count in server log
- [x] FTB configs loaded (`ftbchunks-world.snbt`, `ftbteams-server.snbt`)
- [x] Server listening on port 25552
- [x] `Done (Xs)!` in server log with no errors
- [x] Chunky — `/chunky` in server console responds
- [x] JEI and JourneyMap functional while connected to server

## Deferred — Requires Multiplayer
*See `multiplayer.md` — Batch 1 section.*

---

## Tester Notes
All single-player and server tests passed. Sodium 0.8.x incompatibility resolved by pinning Sodium 0.6.13 to match Iris 1.8.12 requirements. Oculus dropped in favour of Iris (multiloader, NeoForge 1.21.1 support). jmi-client.toml chunk overlay colours to be tuned in a later config pass.

**Result: PASS**
