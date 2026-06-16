# FuzzCraft 4 — Batch 5c Testing: Underground & Quirky Dimensions

## Summary
**Pack version:** 0.5.7
**Test date:** 2026-06-16
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Dynamic Trees compat** — Undergarden, Deeper and Darker, and Bumblezone trees are expected to generate as vanilla static trees (not DT dynamic trees). Same pattern as TF (B5a) and The Aether (B5b). Non-blocking — no DT compat addon exists for any of these mods.
- **Farmer's Cutting** — No Farmer's Cutting datapack exists for Undergarden, Deeper and Darker, or Bumblezone (searched; none found). Dimension wood types will not have FC stripping recipes. Non-blocking.
- **B5a server test still outstanding** — B5a, 5b, and 5c server testing is planned as a combined pass after B5c merges to main.

---

## 1. Launch & Stability

- [x] Pack launches without crash or error log flood
- [x] Title screen and world select load correctly
- [x] Create a new world — no worldgen crash on load
- [x] Load an existing B5b world — no crash, no missing block errors

## 2. Regression — Batch 5a/5b

- [x] Twilight Forest portal ignites and dimension loads correctly
- [x] The Aether portal ignites and dimension loads correctly
- [x] Dimensional Pockets II pocket dimension opens and closes
- [x] RFTools Dimensions dimension tab visible in creative / crafting accessible

## 3. The Undergarden

- [x] Undergarden portal crafted and activated (obsidian frame + catalyst item)
- [x] Dimension loads without crash
- [x] Biomes visually distinct — gloomy, cave-world aesthetic
- [x] Undergarden-specific blocks and mobs spawn correctly (Depthrock, Gloomber, Rotwood, etc.)
- [x] Unique ores/resources obtainable (Depthrock Coal, Wigglite, Forgotten items)
- [x] Trees present — note whether static (expected) or DT dynamic
- [x] Return to Overworld works cleanly (portal or respawn)

## 4. Deeper and Darker

- [x] Deep Dark generates in the Overworld (find a deep dark biome ~Y -50 or lower, or use `/locate biome minecraft:deep_dark`)
- [x] Ancient Cities spawn with Deeper and Darker additions (sculk traps, new structures)
- [x] New blocks present in ancient city context (chiseled deepslate variants, echo shards, etc.)
- [x] Warden spawns and functions normally
- [x] New Deeper and Darker mob(s) spawn in deep dark (if any in 1.4.x)
- [x] New equipment/items craftable from dimension drops
- [x] No crash when entering/exiting deep dark areas

## 5. The Bumblezone

- [x] Bumblezone portal entry works (find bee nest/hive, trigger portal — check mod wiki for exact method)
- [x] Dimension loads without crash
- [x] Honey-themed environment visually correct (honeycomb blocks, bee structures)
- [x] Bumblezone bees/mobs present and functional
- [x] Unique Bumblezone resources obtainable
- [x] Return to Overworld works cleanly

## 6. Tropicraft

- [x] Tropicraft portal crafted and activated (bamboo/pineapple + cocktail ritual — check mod wiki)
- [x] Tropics dimension loads without crash
- [x] Beach/jungle biomes visually correct — palm trees, sand, tropical water
- [x] Tropicraft mobs spawn (Tropicreeper, Iguana, etc.)
- [x] Unique Tropicraft resources obtainable (bamboo items, shells, tropical fish variants)
- [x] Return to Overworld works cleanly

## 7. Stellaris

- [x] Stellaris rocket/launch mechanic accessible (check JEI for launch item or pad recipe)
- [x] Space dimension / planet loads without crash
- [x] Planets visually distinct from each other (at least two visited)
- [x] Space mobs and bosses present and functional
- [x] Unique Stellaris resources obtainable
- [x] Return to Overworld works cleanly
- [x] Potentials (auto-dep) — no errors in log; check if it adds any visible progression/skill system

## 8. Cross-mod Spot Checks

- [x] JEI shows recipes for all five B5c mods — no broken recipe pages
- [x] Waystones can be placed in Undergarden, Tropics, and Bumblezone (or confirm dimensions are flagged as non-waystone)
- [x] No obvious Almost Unified conflicts on new material types (Wigglite, Tropicraft metals, Stellaris ores, etc.)

## 9. Deferred — Requires Server / Multiplayer

- Combined B5a + B5b + B5c server test pass (planned post-B5c merge)
  - All five B5c dimensions load on the server
  - Multiplayer portal sync (two players entering/exiting dimensions simultaneously)
  - Bumblezone portal behaviour when multiple players are near bee nests
  - Stellaris multiplayer (two players on different planets simultaneously)

## 10. Tester Notes

**Tropicraft portal recipe — JEI misleading due to Almost Unified**
JEI shows Pam's HarvestCraft Pina Colada as the output for the Tropicraft cocktail recipe (AU tag unification collision). The actual working recipe is: pineapple cubes (pineapple → crafting table) + coconut chunks + bamboo mug — shapeless craft. The resulting item is `tropicraft:cocktail` with the Pina Colada data component, not a Pam's item. `/give @s tropicraft:cocktail` produces a blank non-interactable item (missing drink data component — must be crafted). Portal triggered correctly with the crafted drink. **Needs AU config fix before release** — logged in charter.
1. The following trees are also static (no dynamic tree support):
  - Undergarden
  - Deeper and Darker
  - The Bumblezone
2. Need to add proper quest instructions to get into each of the dimensions - some are quirky or have multiple steps
