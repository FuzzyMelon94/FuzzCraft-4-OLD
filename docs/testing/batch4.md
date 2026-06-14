# FuzzCraft 4 — Batch 4 Testing: World Gen & Combat

## Summary
**Pack version:** 0.4.5–0.4.9–
**Test date:** 2026-06-14
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Dynamic Trees — BWG compat** upgraded from BETA02 to 1.1.0. Should be more stable but watch for odd tree generation in BYG biomes.
- **Terralith pinned to 2.5.8** — 2.6.2 caused a feature order cycle with BWG 2.6.0. Do not update Terralith until this is resolved upstream.
- **BetterNether NeoForge** is an unofficial port. Required deps (WunderLib, BCLib, WorldWeaver/WOver) were manually added — not auto-detected by packwiz. Worth flagging any Nether-specific crashes or world gen errors in logs.
---

## 1. Launch & Stability

- [x] Game launches without crashes
- [x] No errors in the log on a fresh world load
- [x] All mod GUIs open without crashes (spot-check: JEI, Jade, FTB Chunks, AE2 terminal)
- [x] No obvious TPS issues in a fresh world with default world gen

---

## 2. World Gen

### Terrain & Biomes

- [x] New world generates without errors in the log
- [x] Terralith biomes visible — check F3 biome name while exploring (look for e.g. Starfall Caverns, Yosemite Cliffs, Scarlet Mountains)
- [x] BYG biomes visible (e.g. Maple Forest, Cika Mountains, Howling Peaks)
- [x] Terrain shape feels varied — large mountains, deep valleys, interesting coastlines (Tectonic)
- [x] Biome transitions look natural — no jarring seams between Terralith and BYG biomes

### Dynamic Trees

- [x] Trees in the overworld use Dynamic Trees models (no standard flat-top vanilla trees)
- [x] Chopping the base of a tree causes the whole tree to fall
- [x] Replanting works — sapling grows dynamically over time
- [ ] BYG biome trees render correctly (DT–BWG compat)
- [x] Terralith biome trees render correctly (DT–Terralith compat)
- [x] No runaway chunk update spam in F3 debug (watch `C:` chunk updates while near trees)

### Nether

- [x] Nether generates with BetterNether biomes (new plants, terrain variety)
- [x] No world gen errors in log after entering the Nether
- [x] BetterNether structures visible (Nether fortresses are handled by YUNG's later — just check general Nether content for now)

---

## 3. End Gen

### Launch & Entry

- [x] Game launches without crashes with End gen mods active
- [x] No errors in log on a fresh world load
- [x] Entering the End dimension does not crash or produce world gen errors in log

### Nullscape

- [ ] The End void feels denser/more atmospheric (Nullscape adds void particles, ambient fog, and island detail — the outer islands should feel less empty)
- [x] No world gen errors in log after generating End chunks

### YUNG's Better End Island ⚠️

- [x] The main End island (where the Ender Dragon spawns) is visually improved — should look more natural and detailed rather than flat obsidian pillars on a barren island
- [x] End portal and fountain still present and functional
- [x] Ender Dragon fight initiates normally on entering the End
- [x] No world gen errors in log during main island generation

---

## 4. Structures

> Use `/locate` commands to find structures quickly — e.g. `/locate structure minecraft:stronghold`. For modded structures, use tab-complete after `/locate structure` to find the relevant namespace.

### Launch & Stability

- [ ] Game launches without crashes with all structure mods active
- [ ] No world gen errors in log on a fresh world load
- [ ] No `Feature order cycle` or `BiomeModifier` errors in log (structure mods are a common trigger)

### YUNG's Suite

- [ ] YUNG's Better Dungeons — find a dungeon (`/locate structure minecraft:monster_room`); should look more detailed with multiple room types, traps, and loot variety
- [ ] YUNG's Better Mineshafts — find a mineshaft (`/locate structure minecraft:mineshaft`); should feel more natural and cave-like, less grid-y
- [ ] YUNG's Better Strongholds — locate a stronghold (`/locate structure minecraft:stronghold`); should be significantly larger and more complex
- [ ] YUNG's Better Desert Temples — locate one (`/locate structure minecraft:desert_pyramid`); should have new traps and internal rooms
- [ ] YUNG's Better Jungle Temples — locate one (`/locate structure minecraft:jungle_pyramid`); should have more puzzle rooms
- [ ] YUNG's Better Ocean Monuments — locate one (`/locate structure minecraft:ocean_monument`); should feel more labyrinthine
- [ ] YUNG's Better Nether Fortresses — enter the Nether and locate a fortress (`/locate structure minecraft:fortress`); should be considerably larger
- [ ] YUNG's Better Witch Huts — locate one (`/locate structure minecraft:swamp_hut`); spot-check appearance
- [ ] YUNG's Bridges — explore overworld rivers and paths; natural-looking bridges should appear connecting terrain

### Villages & Settlements

- [ ] CTOV — villages look more varied and biome-appropriate (CTOV adds biome-specific village styles); check a plains village, a taiga village, and a desert village if possible
- [ ] Towns and Towers — watchtowers and outposts visible in the world; distinct from vanilla pillager outposts
- [ ] Tidal Towns — locate an ocean/coastal area and look for underwater or coastal settlements

### Dungeons & Structures

- [ ] When Dungeons Arise — locate a large structure (`/locate structure whendungeonsarise:*` — tab-complete for options); should be a substantial standalone dungeon
- [ ] Dungeons and Taverns — find a tavern or inn in the world; check for loot and interior detail
- [ ] Blossom Blade — find a cherry/blossom-themed structure (explore cherry groves or general surface); spot-check appearance
- [ ] Better Archeology — find a trail ruins or suspicious sand site; BetterArcheology should add new structure variants and loot to dig sites

### Sparse Structures

- [ ] Structures don't feel completely overwhelming in density — Sparse Structures should be reducing frequency of vanilla structures; explore a reasonable area and check it doesn't feel like structures on every chunk

### Nether Structures

- [ ] YUNG's Better Nether Fortresses generates without errors in the Nether (logged separately above — just confirm no new errors after structures batch)

---

## 6. Deferred — Requires Server / Multiplayer

- Chunk gen performance under concurrent player load (multiple players exploring new biomes simultaneously)
- BetterNether stability under server-side world gen (unofficial port — worth a specific check)

---

## 7. Tester Notes

1. BYG and BetterNether saplings don't work with Dynamic Trees. BetterNether has no DT compat addon (none exists); dtbwg may not cover all BWG tree types — this is a known compat gap, not fixable without a dedicated addon. Deferred.
2. Falling trees disabled via config (`enableFallingTrees = false`, `enableFallingTreeDamage = false` in `dynamictrees-server.toml`). Trees still use DT models and branch-chopping — just no felling animation.

