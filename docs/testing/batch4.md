# FuzzCraft 4 — Batch 4 Testing: World Gen & Combat

## Summary
**Pack version:** 0.4.5–0.4.27
**Test date:** 2026-06-14–2026-06-15
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Dynamic Trees — BWG compat** upgraded from BETA02 to 1.1.0. Should be more stable but watch for odd tree generation in BYG biomes.
- **Terralith pinned to 2.5.8** — 2.6.2 caused a feature order cycle with BWG 2.6.0. Do not update Terralith until this is resolved upstream.
- **BetterNether NeoForge** is an unofficial port. Generally stable but worth flagging any Nether-specific crashes or world gen errors in logs.
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
- [x] BYG biome trees render correctly (DT–BWG compat)
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

- [x] The End void feels denser/more atmospheric (Nullscape adds void particles, ambient fog, and island detail — the outer islands should feel less empty)
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

- [x] Game launches without crashes with all structure mods active
- [x] No world gen errors in log on a fresh world load
- [x] No `Feature order cycle` or `BiomeModifier` errors in log (structure mods are a common trigger)

### YUNG's Suite

- [x] YUNG's Better Dungeons — find a dungeon (`/locate structure minecraft:monster_room`); should look more detailed with multiple room types, traps, and loot variety
- [x] YUNG's Better Mineshafts — find a mineshaft (`/locate structure minecraft:mineshaft`); should feel more natural and cave-like, less grid-y
- [x] YUNG's Better Strongholds — locate a stronghold (`/locate structure minecraft:stronghold`); should be significantly larger and more complex
- [x] YUNG's Better Desert Temples — locate one (`/locate structure minecraft:desert_pyramid`); should have new traps and internal rooms
- [x] YUNG's Better Jungle Temples — locate one (`/locate structure minecraft:jungle_pyramid`); should have more puzzle rooms
- [x] YUNG's Better Ocean Monuments — locate one (`/locate structure minecraft:ocean_monument`); should feel more labyrinthine
- [x] YUNG's Better Nether Fortresses — enter the Nether and locate a fortress (`/locate structure minecraft:fortress`); should be considerably larger
- [x] YUNG's Better Witch Huts — locate one (`/locate structure minecraft:swamp_hut`); spot-check appearance
- [x] YUNG's Bridges — explore overworld rivers and paths; natural-looking bridges should appear connecting terrain

### Villages & Settlements

- [x] CTOV — villages look more varied and biome-appropriate (CTOV adds biome-specific village styles); check a plains village, a taiga village, and a desert village if possible
- [x] Towns and Towers — watchtowers and outposts visible in the world; distinct from vanilla pillager outposts
- [x] Tidal Towns — locate an ocean/coastal area and look for underwater or coastal settlements

### Dungeons & Structures

- [x] When Dungeons Arise — locate a large structure (`/locate structure whendungeonsarise:*` — tab-complete for options); should be a substantial standalone dungeon
- [x] Dungeons and Taverns — find a tavern or inn in the world; check for loot and interior detail
- [x] Blossom Blade — find a cherry/blossom-themed structure (explore cherry groves or general surface); spot-check appearance
- [x] Better Archeology — find a trail ruins or suspicious sand site; BetterArcheology should add new structure variants and loot to dig sites

### Sparse Structures

- [x] Structures don't feel completely overwhelming in density — Sparse Structures should be reducing frequency of vanilla structures; explore a reasonable area and check it doesn't feel like structures on every chunk

### Nether Structures

- [x] YUNG's Better Nether Fortresses generates without errors in the Nether (logged separately above — just confirm no new errors after structures batch)

---

## 5. Mobs & Combat

### Launch & Stability

- [x] Game launches without crashes with all mob mods active
- [x] No errors in log on a fresh world load
- [x] No missing texture errors or entity registration errors in log

### Mob Variety

- [x] Alex's Mobs ⚠️ (unofficial port) — spot wildlife in the overworld; grizzly bears, raccoons, etc. should appear naturally. Check for any Citadel-related errors in log
- [x] Born in Chaos — encounter enhanced vanilla mob variants in the overworld (darker skeletons, larger zombies, etc.); check they don't crash on spawn
- [x] Galosphere — find Allay-adjacent content in the overworld; spot-check new mobs in appropriate biomes
- [x] Ribbits — find a swamp or jungle; new frog/toad variants should appear
- [x] Critters & Companions — small ambient creatures (ferrets, koi, etc.) should appear in appropriate biomes
- [x] Creeper Overhaul — find creepers in different biomes; should have biome-specific appearances (jungle creeper, desert creeper, etc.)
- [x] Golem Overhaul — create or find an iron golem; should have a visually distinct variant based on biome
- [x] Enderman Overhaul — enter the End or find an Enderman; should have visual variants depending on dimension/biome
- [x] Nyf's Spiders — find a cave spider or spider; should exhibit new climbing and web behaviours
- [x] Guard Villagers — find a village; armed guard villagers should be patrolling

### Aquatic

- [x] Upgrade Aquatic — check for improved vanilla aquatic mobs (salmon, cod, dolphins) with new behaviours or variants

### Farming & Animals

- [x] Animal Feeding Trough — craft a feeding trough and place near animals; animals in range should feed and breed passively
- [x] Just Enough Breeding — open JEI and look up an animal (e.g. cow); breeding items should now show in JEI

### Combat & Equipment

- [x] Epic Knights — find or craft Epic Knights armour/shield; equip and check it renders correctly with Better Combat animations
- [x] Epic Knights Addon — additional weapons visible in JEI; craft one and check it functions
- [x] Artifacts — find a dungeon chest or trade for an Artifact trinket; equip in a Curios slot and verify the effect works
- [x] Better Combat — equip any two-handed or dual-wield weapon; attack animations should be distinct from vanilla swipe

### Utility

- [x] Waystones — find a waystone in a village or structure; right-click to activate, then teleport to it from elsewhere
- [x] Bountiful — find a bounty board in a village; collect a bounty, fulfil it, and claim the reward
- [x] Lootr ⚠️ — open a dungeon/structure chest; it should be instanced (each player gets their own loot, chest doesn't deplete for others). Verify in creative with two accounts or check the chest tooltip says "Looted"
- [x] In Control! — no active rules yet, but confirm no errors in log on load (it should silently do nothing until rules are configured)

### Visuals

- [x] EMF + ETF — mob models should look enhanced where Fresh Animations applies (limb movement, idle animations on passive mobs like cows and sheep)
- [x] Fresh Animations — passive mobs should have smoother, more lifelike idle and movement animations compared to vanilla
- [x] Entity Culling — no visual impact to verify, but confirm no rendering errors or invisible entity issues

### CTOV Compat Datapacks ⚠️

> These datapacks are tagged for 1.20.1 but should be forward-compatible. Watch for any structure generation errors.

- [x] Find a village — check for Farmer's Delight-themed additions (small crop gardens, cooking stations integrated into village buildings)
- [x] Check a village near a plains/taiga biome — Friends & Foes content (bees, copper golems) should appear in village contexts
- [x] No datapack errors in log on world load

---

## 6. Deferred — Requires Server / Multiplayer

- Chunk gen performance under concurrent player load (multiple players exploring new biomes simultaneously)
- BetterNether stability under server-side world gen (unofficial port — worth a specific check)

---

## 7. Tester Notes

1. BYG and BetterNether saplings don't work with Dynamic Trees. BetterNether has no DT compat addon (none exists); dtbwg may not cover all BWG tree types — this is a known compat gap, not fixable without a dedicated addon. Deferred.