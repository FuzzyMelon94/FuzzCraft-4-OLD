# FuzzCraft 4 — Batch 4 Testing: World Gen & Combat

## Summary
**Pack version:** 0.4.5–0.4.7–
**Test date:** 2026-06-14
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Dynamic Trees — BWG compat** upgraded from BETA02 to 1.1.0. Should be more stable but watch for odd tree generation in BYG biomes.
- **Terralith pinned to 2.5.8** — 2.6.2 caused a feature order cycle with BWG 2.6.0. Do not update Terralith until this is resolved upstream.
- **BetterNether NeoForge** is an unofficial port. Generally stable but worth flagging any Nether-specific crashes or world gen errors in logs.
- **BetterEnd NeoForge** is also an unofficial port (CurseForge source). BCLib is a required dependency. Watch for End-specific world gen errors or crashes on Enter.

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

- [ ] Game launches without crashes with End gen mods active
- [ ] No errors in log on a fresh world load
- [ ] Entering the End dimension does not crash or produce world gen errors in log

### Nullscape

- [ ] The End void feels denser/more atmospheric (Nullscape adds void particles, ambient fog, and island detail — the outer islands should feel less empty)
- [ ] No world gen errors in log after generating End chunks

### BetterEnd ⚠️

- [ ] BetterEnd biomes generate in the End (e.g. Crystal Mountains, Foggy Mushroomland, Shadow Forest — check F3 biome name while exploring)
- [ ] Structures from BetterEnd visible (End cities are vanilla — look for BetterEnd-specific ruins or lanterns)
- [ ] New BetterEnd plants and blocks visible in biomes
- [ ] No BCLib-related errors or warnings in log (BCLib is a required dep — conflicts with other BCLib-dependent mods can surface here)
- [ ] No crashes on entering or exploring the End

### YUNG's Better End Island ⚠️

- [ ] The main End island (where the Ender Dragon spawns) is visually improved — should look more natural and detailed rather than flat obsidian pillars on a barren island
- [ ] End portal and fountain still present and functional
- [ ] Ender Dragon fight initiates normally on entering the End
- [ ] No world gen errors in log during main island generation

---

## 4. Deferred — Requires Server / Multiplayer

- Chunk gen performance under concurrent player load (multiple players exploring new biomes simultaneously)
- BetterNether stability under server-side world gen (unofficial port — worth a specific check)

---

## 5. Tester Notes

1. BYG and BetterNether saplings don't work with Dynamic Trees. BetterNether has no DT compat addon (none exists); dtbwg may not cover all BWG tree types — this is a known compat gap, not fixable without a dedicated addon. Deferred.
2. Falling trees disabled via config (`enableFallingTrees = false`, `enableFallingTreeDamage = false` in `dynamictrees-server.toml`). Trees still use DT models and branch-chopping — just no felling animation.

