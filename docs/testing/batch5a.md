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

- [x] Pack launches without crashes
- [x] No errors in log related to B5a mods (TF, BOMD, Bosses Rise, Dim Pockets II, Supernova Mining, Dim Dungeons)
- [x] New world creates without errors

---

## 2. Regression — Batch 1–4

- [x] JourneyMap opens, chunk overlay visible
- [x] JEI opens, recipes browse correctly
- [x] Create contraption (e.g. mechanical arm or belt) functions
- [x] AE2 network comes up without errors
- [x] Ars Nouveau spellbook craftable
- [x] Terralith/BYG biomes generating (check F3 biome name in a new world)

---

## 3. Twilight Forest

- [x] Twilight Forest portal crafts and activates (place a 2×2 pool of water, surround with flowers/natural blocks, throw diamond in)
- [x] Portal teleports to Twilight Forest dimension
- [x]] TF dimension generates correctly — trees, biomes, structures visible
- [x] Naga boss spawns (Naga Courtyard structure) — engage if found
- [x] Lich Tower visible at a distance or found
- [x] JEI shows TF recipes
- [x] Farmer's Cutting: TF — TF plants/crops can be harvested with FD tools (right-click harvest a TF plant if one is found)
- [x] Return portal works (or craft a new overworld portal)
- [x] No world-gen crashes when exploring TF chunks

Note on progression: if `progression = true` (default), some structures will be locked until their prerequisite boss is defeated. This is working as intended unless you decide to disable it.

---

## 4. Bosses of Mass Destruction ⚠️

- [x] BOMD guidebook/manual accessible in JEI or crafted
- [x] At least one BOMD boss structure locatable (use the mod's locator items or explore)
- [x] Boss spawns and fight initiates without crash
- [x] Boss drops loot
- [x] No conflicts with existing mob/spawner mods (Born in Chaos, Legendary Monsters, In Control!)

---

## 5. Bosses Rise ⚠️

- [x] Bosses Rise structures generate in the world (check ocean for Kraken ship if accessible)
- [x] At least one Bosses Rise boss engageable without crash
- [x] Boss fight completes without server crash
- [x] Loot drops correctly

---

## 6. Dimensional Dungeons

- [x] Dungeon portal crafted/found and activated
- [x] Enter dungeon dimension without crash
- [x] Dungeon generates rooms correctly
- [x] Enemies spawn inside dungeon
- [x] Lootr chest loot rolls correctly (check a dungeon chest — loot should be per-player, Lootr style)
- [x] Block protection active inside dungeon (can't break walls — expected)
- [x] Exit dungeon dimension and return to overworld without issue

---

## 7. Dimensional Pockets II

- [x] Pocket dimension block/item craftable (check JEI)
- [x] Enter personal pocket dimension without crash
- [x] Pocket dimension is empty/blank as expected
- [x] Place blocks and items inside — persists on re-entry
- [x] Exit pocket dimension and re-enter — content preserved
- [x] Modular upgrades (crafting station, etc.) craftable and placeable inside

---

## 8. RFTools Dimensions ⚠️

Beta for 1.21.1. Requires RF power infrastructure to create and maintain dimensions. Travel via Matter Transmitter/Receiver (RFTools Utility). Deps: McJtyLib, RFTools Base, RFTools Utility.

- [x] RFTools Dimensions guidebook/manual accessible in JEI
- [x] Dimension Builder and Dimension Tab craftable (check JEI)
- [ ] Craft at least one ore module and one terrain module
- [ ] Build and power a Dimension Builder, insert modules, create a dimension tab
- [ ] Activate Dimension Builder and enter the created dimension without crash
- [ ] Dimension generates with configured ores visible
- [ ] Mine ores — drops correct
- [ ] Return to overworld without issue
- [ ] Dimension persists after re-entry (power maintained)

---

## 9. Deferred — Requires Server / Multiplayer

- Boss night with full group (BOMD + Bosses Rise) — test aggro, multi-player arena behaviour
- Dimensional Dungeons with multiple players — verify per-player Lootr chests work correctly in the dungeon dimension
- Dimensional Pockets II — verify pocket dims are player-isolated (Player A can't enter Player B's pocket)
- Supernova's Mining Dimension — verify mob spawn rates under server load

---

## Tester Notes
<!-- Broken things, surprises, feedback -->

1. Note, the Twilight Forest doesn't appear to work with Dynamic Trees (fine, just a note)
2. Bosses Rise: Do we know if the loot would drop enough for each player in the boss fight?
3. BoMD: No guidebook - not sure if there actually is one... Not an issue, note in the config file (or wherever makes sense) that we'll need to set up quests to detail how to trigger the bosses.