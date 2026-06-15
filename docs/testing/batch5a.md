# FuzzCraft 4 — Batch 5a Testing: Flagship + Bosses + Utility

## Summary
**Pack version:** 0.5.1
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
- Twilight Forest has an optional progression gate system (defeating bosses in order to unlock areas). This is **enabled by default** and can feel punishing. Config: `config/twilightforest-common.toml` → `progression = false` to disable if the group prefers open exploration.
- Dimensional Dungeons enforces adventure-mode-style block protection inside the dungeon dimension by default — this is intentional and expected.
- Bosses of Mass Destruction (BOMD) is marked as WIP by the author. Some boss arenas may be rough around the edges.
- Deeper and Darker is NOT in this batch — it's in B5c. Don't go looking for the Otherside yet.

---

## 1. Launch & Stability

- [ ] Pack launches without crashes
- [ ] No errors in log related to B5a mods (TF, BOMD, Bosses Rise, Dim Pockets II, Supernova Mining, Dim Dungeons)
- [ ] New world creates without errors

---

## 2. Regression — Batch 1–4

- [ ] JourneyMap opens, chunk overlay visible
- [ ] JEI opens, recipes browse correctly
- [ ] Create contraption (e.g. mechanical arm or belt) functions
- [ ] AE2 network comes up without errors
- [ ] Ars Nouveau spellbook craftable
- [ ] Terralith/BYG biomes generating (check F3 biome name in a new world)

---

## 3. Twilight Forest

- [ ] Twilight Forest portal crafts and activates (place a 2×2 pool of water, surround with flowers/natural blocks, throw diamond in)
- [ ] Portal teleports to Twilight Forest dimension
- [ ] TF dimension generates correctly — trees, biomes, structures visible
- [ ] Naga boss spawns (Naga Courtyard structure) — engage if found
- [ ] Lich Tower visible at a distance or found
- [ ] JEI shows TF recipes
- [ ] Farmer's Cutting: TF — TF plants/crops can be harvested with FD tools (right-click harvest a TF plant if one is found)
- [ ] Return portal works (or craft a new overworld portal)
- [ ] No world-gen crashes when exploring TF chunks

Note on progression: if `progression = true` (default), some structures will be locked until their prerequisite boss is defeated. This is working as intended unless you decide to disable it.

---

## 4. Bosses of Mass Destruction ⚠️

- [ ] BOMD guidebook/manual accessible in JEI or crafted
- [ ] At least one BOMD boss structure locatable (use the mod's locator items or explore)
- [ ] Boss spawns and fight initiates without crash
- [ ] Boss drops loot
- [ ] No conflicts with existing mob/spawner mods (Born in Chaos, Legendary Monsters, In Control!)

---

## 5. Bosses Rise ⚠️

- [ ] Bosses Rise structures generate in the world (check ocean for Kraken ship if accessible)
- [ ] At least one Bosses Rise boss engageable without crash
- [ ] Boss fight completes without server crash
- [ ] Loot drops correctly

---

## 6. Dimensional Dungeons

- [ ] Dungeon portal crafted/found and activated
- [ ] Enter dungeon dimension without crash
- [ ] Dungeon generates rooms correctly
- [ ] Enemies spawn inside dungeon
- [ ] Lootr chest loot rolls correctly (check a dungeon chest — loot should be per-player, Lootr style)
- [ ] Block protection active inside dungeon (can't break walls — expected)
- [ ] Exit dungeon dimension and return to overworld without issue

---

## 7. Dimensional Pockets II

- [ ] Pocket dimension block/item craftable (check JEI)
- [ ] Enter personal pocket dimension without crash
- [ ] Pocket dimension is empty/blank as expected
- [ ] Place blocks and items inside — persists on re-entry
- [ ] Exit pocket dimension and re-enter — content preserved
- [ ] Modular upgrades (crafting station, etc.) craftable and placeable inside

---

## 8. Supernova's Mining Dimension

- [ ] Mining dimension portal/entry item craftable (check JEI)
- [ ] Enter mining dimension without crash
- [ ] Dimension generates with standard ores visible
- [ ] Mine ores — drops correct (no tag/loot issues)
- [ ] Return to overworld without issue
- [ ] Mob spawns in mining dimension (default config — InControl! may affect this)

---

## 9. Deferred — Requires Server / Multiplayer

- Boss night with full group (BOMD + Bosses Rise) — test aggro, multi-player arena behaviour
- Dimensional Dungeons with multiple players — verify per-player Lootr chests work correctly in the dungeon dimension
- Dimensional Pockets II — verify pocket dims are player-isolated (Player A can't enter Player B's pocket)
- Supernova's Mining Dimension — verify mob spawn rates under server load

---

## Tester Notes
<!-- Broken things, surprises, feedback -->
