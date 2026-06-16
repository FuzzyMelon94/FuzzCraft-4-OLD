# FuzzCraft 4 — Batch 5b Testing: Aether Cluster

## Summary
**Pack version:** 0.5.5
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
- **Paradise Lost** was scoped for this batch but deferred — NeoForge build requires Sinytra Connector which conflicts with Sodium/Iris. Not in the pack.
- **The Aether Redux** and **Aether: Lost Content** have no 1.21.1 ports yet — watchlisted. The base Aether content is what we have.
- **owo-lib** was auto-pulled as a dependency of The Aether. It's a library mod — expect nothing visible from it.
- The Aether is a sky dimension with its own biomes, mobs, bosses, and structures. It is accessed via a Glowstone portal in the overworld. Hostile mobs require Golden Swords (or better) to damage — be prepared before entering.

---

## 1. Launch & Stability

- [ ] Pack launches without crashes
- [ ] No errors in log related to B5b mods (aether, deep-aether, aether-villages, aethers-delight, farmers-cutting-the-aether, owo-lib)
- [ ] New world creates without errors

---

## 2. Regression — Batch 1–5a

- [ ] JourneyMap opens, chunk overlay visible
- [ ] JEI opens, recipes browse correctly
- [ ] Create contraption (e.g. mechanical arm or belt) functions
- [ ] AE2 network comes up without errors
- [ ] Twilight Forest portal activates and dimension loads

---

## 3. The Aether — Portal & Basic Access

- [ ] Build a Glowstone portal frame (minimum 4×5, like a Nether portal but Glowstone) and light it with a Flint & Steel
- [ ] Portal activates (glowing blue Aether portal block appears)
- [ ] Entering portal transitions to the Aether dimension without crash
- [ ] Aether sky (floating islands, blue sky) renders correctly
- [ ] JourneyMap works inside the Aether
- [ ] Returning through the portal brings you back to the overworld

---

## 4. The Aether — Basic Content

- [ ] Aether-specific biomes generate (e.g. Skyroot Meadows, Skyroot Forest, Crystal Peaks)
- [ ] Aether mobs spawn (Phyg, Blue Swet, Moa, Sheepuff, Aerwhale visible or via `/summon`)
- [ ] Hostile mobs present (Zephyr, Cockatrice, etc.)
- [ ] Skyroot trees generate — Skyroot wood placeable and craftable
- [ ] Aether ores visible on island surfaces (Ambrosium, Zanite, Gravitite)
- [ ] JEI shows Aether item recipes (Skyroot tools, Ambrosium Torches, etc.)

---

## 5. The Aether — Dungeons & Bosses

- [ ] Bronze Dungeon (Slider boss) generates in the world — can be located via exploration or creative
- [ ] Silver Dungeon (Valkyrie Queen) generates
- [ ] Gold Dungeon (Sun Spirit) generates
- [ ] Entering a dungeon doesn't crash

> Note: Full boss fights are optional for SP testing. Verify the structures generate and can be entered. Boss fights can be a group event.

---

## 6. Deep Aether — Extended Biomes

- [ ] Deep Aether biomes generate in the Aether (e.g. Irradiated Forests, Aether Highlands) — may require exploring or using `/locate biome`
- [ ] Deep Aether mobs spawn in their biomes
- [ ] Deep Aether ores and blocks appear (check JEI for what to look for)
- [ ] No conflicts or crashes when both The Aether and Deep Aether are loaded

---

## 7. Aether Villages

- [ ] Aether villages generate in the Aether — use `/locate structure` in creative to find one if exploration is slow
- [ ] Village structures render without visual errors
- [ ] Village NPCs (Aether villagers) present and interactive
- [ ] No crash on approaching/loading a village chunk

---

## 8. Aether's Delight — FD Compat

- [ ] Aether-themed food items appear in JEI
- [ ] At least one Aether food item is craftable via standard FD recipes (Cutting Board or Cooking Pot)
- [ ] No crash when opening Cooking Pot or Cutting Board with Aether's Delight installed

---

## 9. Farmer's Cutting: The Aether — Knife Recipes

- [ ] Skyroot logs can be stripped on the Cutting Board using a knife → produces Skyroot bark / stripped log
- [ ] Golden Oak log can be stripped by an Amber Harvester on the Cutting Board (check JEI — search "Skyroot" or "Golden Oak" in the cutting board filter)
- [ ] No JEI errors or missing recipe entries for Aether wood types

---

## 10. Deferred — Requires Server / Multiplayer

- Aether multiplayer stability (dimension sync, portal linking across players)
- Deep Aether biome generation consistency in a shared world
- Aether Villages villager trading in multiplayer

---

## Tester Notes

<!-- Fill in during testing: broken things, surprises, suggestions. -->
