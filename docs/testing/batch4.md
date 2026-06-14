# FuzzCraft 4 — Batch 4 Testing: World Gen & Combat

## Summary
**Pack version:** 0.4.2–
**Test date:** 2026-06-14
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Dynamic Trees removed** — DT + DT-Terralith + DT-BWG + DT-Plus caused a feature order cycle crash (Terralith + BWG biome conflict). All four mods removed at v0.4.2. Vanilla tree gen in effect.
- **BetterNether NeoForge** is an unofficial port. Generally stable but worth flagging any Nether-specific crashes or world gen errors in logs.

---

## 1. Launch & Stability

- [x] Game launches without crashes
- [ ] No errors in the log on a fresh world load
- [ ] All mod GUIs open without crashes (spot-check: JEI, Jade, FTB Chunks, AE2 terminal)
- [ ] No obvious TPS issues in a fresh world with default world gen

---

## 2. World Gen

### Terrain & Biomes

- [ ] New world generates without errors in the log
- [ ] Terralith biomes visible — check F3 biome name while exploring (look for e.g. Starfall Caverns, Yosemite Cliffs, Scarlet Mountains)
- [ ] BYG biomes visible (e.g. Maple Forest, Cika Mountains, Howling Peaks)
- [ ] Terrain shape feels varied — large mountains, deep valleys, interesting coastlines (Tectonic)
- [ ] Biome transitions look natural — no jarring seams between Terralith and BYG biomes

### Nether

- [ ] Nether generates with BetterNether biomes (new plants, terrain variety)
- [ ] No world gen errors in log after entering the Nether
- [ ] BetterNether structures visible (Nether fortresses are handled by YUNG's later — just check general Nether content for now)

---

## 3. Deferred — Requires Server / Multiplayer

- Chunk gen performance under concurrent player load (multiple players exploring new biomes simultaneously)
- BetterNether stability under server-side world gen (unofficial port — worth a specific check)

---

## 4. Tester Notes

<!-- Broken things, surprises, biomes that look great, anything worth feeding back -->
