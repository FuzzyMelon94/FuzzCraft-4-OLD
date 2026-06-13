# FuzzCraft 4 — Batch 3 Testing: Magic & Farming

## Summary
**Pack version:** 0.3.1
**Test date:** 2026-06-13
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Productive Bees** is config-heavy out of the box — bee resource output rates may feel unbalanced compared to Modern Chickens. Note anything that feels wildly off; a config pass to bring them in line is expected before this batch closes.
- **End's Delight** is in the pack but End content is not accessible until Batch 4 (no End dimension mods yet). Skip End's Delight testing this batch.
- **Botania** is absent — no 1.21.1 NeoForge port exists yet. It is watchlisted.
- **Neo Vitae** is experimental (⚠️). Watch for crashes, odd altar behaviour, or progression blockers.

---

## 1. Launch & Stability

- [ ] Game launches without crashes
- [ ] No errors in the log on a fresh world load
- [ ] All mod GUIs open without crashes (spot-check: JEI, Jade, FTB Chunks, AE2 terminal)
- [ ] No obvious TPS issues in a fresh world with default world gen

---

## 2. Regression — Batches 1 & 2

- [ ] JourneyMap loads, chunk claims visible on map
- [ ] JEI recipe viewer functional
- [ ] Create contraption assembles and runs (windmill + millstone)
- [ ] AE2 ME Terminal accessible and shows stored items
- [ ] Immersive Engineering multiblock (e.g. Crusher) assembles correctly
- [ ] CC: Tweaked — open a computer, run a basic program

---

## 3. Ars Nouveau

- [ ] Arcane Compendium (guidebook) opens and is readable
- [ ] Craft a spell book and inscribe a basic spell (e.g. Launch or Ignite)
- [ ] Cast spell successfully
- [ ] Source Jar fills from a Source Berry bush or Mana Bloom
- [ ] Summon a familiar
- [ ] **Ars Additions** — Starbuncle can be summoned and pathfinds to items
- [ ] **Ars Énergistique** — Source Cable connects to AE2 network (basic connection test)
- [ ] **Ars Elemental** — new spell glyphs appear in JEI
- [ ] **Create Ars Nouveau** — Sorcerer Blaze Burner crafts and accepts Source as fuel
- [ ] **Create: Ars Nouveau Compat** — Ars Nouveau items appear in Create machine recipes in JEI

---

## 4. Theurgy

- [ ] Theurgy guidebook (Modonomicon) opens and is readable
- [ ] Craft a Sal Ammoniac Crystal and a Mercury Catalyst
- [ ] Run a basic Spagyrics operation (any purification or separation process)
- [ ] Reformation Array — set up and transmute a resource
- [ ] No crashes or visual errors in the Theurgy GUIs

---

## 5. Neo Vitae ⚠️

- [ ] Craft a basic Blood Altar (tier 1)
- [ ] Fill the altar with LP (take self-damage near the altar)
- [ ] Craft a basic Blood Orb
- [ ] Craft and use a basic Sigil
- [ ] No crashes when interacting with the altar
- [ ] No runaway damage loops or instant-death bugs

---

## 6. Farmer's Delight & Food Ecosystem

- [ ] Farmer's Delight cooking pot crafts and produces a food item
- [ ] Cutting Board + knife works to prep ingredients
- [ ] **Pam's HarvestCraft** — garden bushes spawn in the world; harvest a crop seed from one
- [ ] Pam's crop grows to maturity and drops food
- [ ] Pam's Trees — fruit tree spawns in a biome; fruit drops from leaves
- [ ] **Cooking for Blockheads** — place a kitchen block, open it, confirm recipe filtering works with available ingredients
- [ ] **Brewin' And Chewin'** — craft a fermenting barrel and begin a fermentation recipe
- [ ] **More Delight / Compat Delight** — spot-check a recipe from each in JEI
- [ ] **Farmer's Delight: Extended** — at least one Create+FD crossover recipe visible in JEI (e.g. milling a FD crop)
- [ ] **Create Slice & Dice** — Deployer or Mechanical Saw processes a FD cutting recipe

---

## 7. Let's Do Series

- [ ] **Vinery** — grape sapling plants and grows; craft a bottle of wine
- [ ] **Farm & Charm** — place a butter churn or similar functional block; process an item
- [ ] **Bakery** — bake a bread or cake variant
- [ ] **Brewery** — set up a barrel; begin a brew recipe
- [ ] **Meadow** — meadow sub-biome generates (may need to explore); craft a cheese
- [ ] **HerbalBrews** — dry a leaf, brew a tea or coffee
- [ ] **[Let's Do] Compat** — no recipe conflicts between the Let's Do mods (spot-check in JEI)

---

## 8. Botany Pots

- [ ] Place a Botany Pot and plant a vanilla crop; confirm it grows and auto-harvests
- [ ] **Botany Trees** — plant a sapling in a Botany Tree Pot; confirm it produces logs/saplings
- [ ] **Botany Pots Tiers** — craft a higher-tier pot; confirm improved growth speed
- [ ] **Mystical Agriculture compat** — plant a Mystical Agriculture seed in a Botany Pot; confirm it works

---

## 9. Mystical Agriculture

- [ ] Crafting seed and growth accelerator visible in JEI
- [ ] Plant a basic resource crop (e.g. iron seeds); grows to maturity
- [ ] Harvest produces a resource essence; craft it into the resource
- [ ] Inferium crop grows and produces essence

---

## 10. Productive Bees ⚠️

- [ ] Advanced Beehive places and accepts bees
- [ ] At least one resource bee (e.g. Honey Bee or Iron Bee) produces output over time
- [ ] Output rate feels roughly comparable to Modern Chickens at default — note anything extreme
- [ ] No crashes or infinite loop behaviour in the bee GUIs

---

## 11. Modern Chickens

- [ ] Chicken coop (or vanilla breeding) produces a resource chicken (e.g. Iron Chicken)
- [ ] Resource chicken lays an appropriate item over time
- [ ] Breeding two resource chickens produces offspring
- [ ] No item duplication or egg loop issues

---

## 12. Fishing

- [ ] **Aquaculture 2** — craft an Aquaculture rod; fish up at least one new fish species
- [ ] New fish visible in JEI with cooking/food recipes
- [ ] **Lava Fishing** — fish in lava in the Nether; catch at least one lava-specific item
- [ ] **Create Fishing Bobber Detector** — place detector; confirm it outputs a redstone/Create signal when a fish bites

---

## 13. Create Food Integrations

- [ ] **Create Confectionery** — crush cocoa beans in a Millstone to get Crushed Cocoa; craft a chocolate item
- [ ] Caramel or marshmallow recipe visible and craftable in JEI

---

## Deferred — Requires Server / Multiplayer

- Productive Bees: confirm resource output is consistent across multiple players' hives on the same server
- Modern Chickens: confirm no cross-player inventory desyncs when multiple players handle the same resource chicken
- Ars Énergistique: two players accessing the same AE2 network with Source automation — no desyncs
- Vinery / Brewery barrels: confirm fermentation ticks correctly when chunk owner is offline (forceload test)
- General TPS check with Botany Pots, Mystical Agriculture crops, and Productive Bees all running simultaneously

---

## Tester Notes

<!-- Anything broken, surprising, or worth feeding back. Config issues, recipe gaps, balance observations. -->
