# FuzzCraft 4 — Batch 5c Testing: Underground & Quirky Dimensions

## Summary
**Pack version:** 0.5.7
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
- **Dynamic Trees compat** — Undergarden, Deeper and Darker, and Bumblezone trees are expected to generate as vanilla static trees (not DT dynamic trees). Same pattern as TF (B5a) and The Aether (B5b). Non-blocking — no DT compat addon exists for any of these mods.
- **Farmer's Cutting** — No Farmer's Cutting datapack exists for Undergarden, Deeper and Darker, or Bumblezone (searched; none found). Dimension wood types will not have FC stripping recipes. Non-blocking.
- **B5a server test still outstanding** — B5a, 5b, and 5c server testing is planned as a combined pass after B5c merges to main.

---

## 1. Launch & Stability

- [ ] Pack launches without crash or error log flood
- [ ] Title screen and world select load correctly
- [ ] Create a new world — no worldgen crash on load
- [ ] Load an existing B5b world — no crash, no missing block errors

## 2. Regression — Batch 5a/5b

- [ ] Twilight Forest portal ignites and dimension loads correctly
- [ ] The Aether portal ignites and dimension loads correctly
- [ ] Dimensional Pockets II pocket dimension opens and closes
- [ ] RFTools Dimensions dimension tab visible in creative / crafting accessible

## 3. The Undergarden

- [ ] Undergarden portal crafted and activated (obsidian frame + catalyst item)
- [ ] Dimension loads without crash
- [ ] Biomes visually distinct — gloomy, cave-world aesthetic
- [ ] Undergarden-specific blocks and mobs spawn correctly (Depthrock, Gloomber, Rotwood, etc.)
- [ ] Unique ores/resources obtainable (Depthrock Coal, Wigglite, Forgotten items)
- [ ] Trees present — note whether static (expected) or DT dynamic
- [ ] Return to Overworld works cleanly (portal or respawn)

## 4. Deeper and Darker

- [ ] Deep Dark generates in the Overworld (find a deep dark biome ~Y -50 or lower, or use `/locate biome minecraft:deep_dark`)
- [ ] Ancient Cities spawn with Deeper and Darker additions (sculk traps, new structures)
- [ ] New blocks present in ancient city context (chiseled deepslate variants, echo shards, etc.)
- [ ] Warden spawns and functions normally
- [ ] New Deeper and Darker mob(s) spawn in deep dark (if any in 1.4.x)
- [ ] New equipment/items craftable from dimension drops
- [ ] No crash when entering/exiting deep dark areas

## 5. The Bumblezone

- [ ] Bumblezone portal entry works (find bee nest/hive, trigger portal — check mod wiki for exact method)
- [ ] Dimension loads without crash
- [ ] Honey-themed environment visually correct (honeycomb blocks, bee structures)
- [ ] Bumblezone bees/mobs present and functional
- [ ] Unique Bumblezone resources obtainable
- [ ] Return to Overworld works cleanly

## 6. Cross-mod Spot Checks

- [ ] JEI shows recipes for Undergarden, Deeper and Darker, and Bumblezone items (no broken recipe pages)
- [ ] Waystones can be placed in Undergarden and Bumblezone (or confirm dimension is flagged as non-waystone)
- [ ] No obvious Almost Unified conflicts on new material types (Wigglite etc.)

## 7. Deferred — Requires Server / Multiplayer

- Combined B5a + B5b + B5c server test pass (planned post-B5c merge)
  - All three B5c dimensions load on the server
  - Multiplayer portal sync (two players entering/exiting dimensions simultaneously)
  - Bumblezone portal behaviour when multiple players are near bee nests

## 8. Tester Notes

<!-- Freeform — broken things, surprises, anything to feed back -->
