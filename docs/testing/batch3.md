# FuzzCraft 4 — Batch 3 Testing: Magic & Farming

## Summary
**Pack version:** 0.3.1–0.3.3
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

- [x] Game launches without crashes
- [x] No errors in the log on a fresh world load
- [x] All mod GUIs open without crashes (spot-check: JEI, Jade, FTB Chunks, AE2 terminal)
- [x] No obvious TPS issues in a fresh world with default world gen

---

## 2. Regression — Batches 1 & 2

- [x] JourneyMap loads, chunk claims visible on map
- [x] JEI recipe viewer functional
- [x] Create contraption assembles and runs (windmill + millstone)
- [x] AE2 ME Terminal accessible and shows stored items
- [x] Immersive Engineering multiblock (e.g. Crusher) assembles correctly
- [x] CC: Tweaked — open a computer, run a basic program

---

## 3. Ars Nouveau

- [x] Arcane Compendium (guidebook) opens and is readable
- [x] Craft a spell book and inscribe a basic spell (e.g. Launch or Ignite)
- [x] Cast spell successfully
- [x] Source Jar fills from a Source Berry bush or Mana Bloom
  1. Craft a Source Jar (check JEI — needs Source Gems)
  2. Place it on the ground
  3. Find a Source Berry bush nearby (blue berries, generates in most biomes) — or plant a Mana Bloom flower within ~10 blocks
  4. Watch the jar — it should fill passively over time; hover with Jade to confirm
- [x] Summon a familiar
  1. Open the Arcane Compendium, navigate to Familiars for the full list
  2. Craft a **Starbuncle Charm** (check JEI)
  3. Right-click the ground with it to summon a Starbuncle (small orange lizard)
  4. It should idle near you and respond to items
- [x] **Ars Additions** — Starbuncle can be summoned and pathfinds to items
  1. If not already summoned above, summon a Starbuncle via Starbuncle Charm
  2. Drop a few items on the ground nearby
  3. Starbuncle should pathfind to the items and pick them up
- [x] **Ars Énergistique** — Source Cable connects to AE2 network (basic connection test)
  1. Craft a Source Cable (check JEI — part of Ars Énergistique)
  2. Place it adjacent to an ME Controller or AE2 cable
  3. It should visually connect; open the ME Terminal to confirm the network is still alive
- [x] **Ars Elemental** — new spell glyphs appear in JEI
  1. Open JEI and search `ars_elemental` or browse the Ars Elemental creative tab
  2. Confirm new glyphs (e.g. extra damage/projectile types) are present
- [x] **Create Ars Nouveau** — Sorcerer Blaze Burner crafts and accepts Source as fuel
  1. Craft a Sorcerer's Blaze Burner (check JEI)
  2. Place it and connect a Source Jar or Source Cable to it
  3. Confirm it accepts Source as a fuel source (flame should appear)
- [x] **Create: Ars Nouveau Compat** — Ars Nouveau items appear in Create machine recipes in JEI
  1. In JEI, search for an Ars Nouveau item (e.g. Source Gem)
  2. Check its uses — there should be Create machine recipes (milling, pressing, etc.) listed

---

## 4. Theurgy

- [x] Theurgy guidebook (Modonomicon) opens and is readable
  1. Press `E` to open inventory, find the Theurgy book in the Theurgy tab, or search JEI for `Theurgy Book` / `Hermetica`
  2. The Modonomicon should open — confirm pages render and are navigable
  3. **Follow the book for all steps below** — Theurgy is a guided progression mod and the book is the primary reference
- [x] Craft a Sal Ammoniac Crystal and a Mercury Catalyst
  1. Check JEI for `Sal Ammoniac Crystal` — it involves calcination (heating) of salt or related materials in a Calcination Oven
  2. Check JEI for `Mercury Catalyst` — involves a similar alchemical process
  3. The Hermetica book has a Spagyrics chapter that walks through both step by step
- [x] Run a basic Spagyrics operation (any purification or separation process)
  1. Set up a Calcination Oven (JEI for recipe and structure)
  2. Process any material listed in the Spagyrics chapter of the Hermetica
  3. Confirm output is produced without error
- [x] Reformation Array — set up and transmute a resource
  1. Check the Hermetica for the Reformation Array chapter
  2. Build the multiblock structure as shown
  3. Attempt any listed transmutation recipe
- [x] No crashes or visual errors in the Theurgy GUIs

---

## 5. Neo Vitae ⚠️

- [x] Craft a basic Blood Altar (tier 1)
  1. Search JEI for `Blood Altar` — the block recipe uses standard materials
  2. Place it on the ground (it's a standalone block at tier 1, no multiblock needed yet)
- [x] Fill the altar with LP (take self-damage near the altar)
  1. Stand next to the altar
  2. Take damage — punch a cactus, jump off a small ledge, or hit yourself with a tool
  3. LP (Life Points) should transfer from you to the altar; watch the altar's blood pool fill
  4. Keep health above 2–3 hearts — the altar won't drain you to death at tier 1 but be cautious
- [x] Craft a basic Blood Orb
  1. Fill the altar with enough LP (check the altar GUI or Jade tooltip for current level)
  2. Place a crafting ingredient in the altar's slot (check JEI for Weak Blood Orb recipe)
  3. Right-click the altar to begin — the orb should materialise when enough LP is consumed
- [x] Craft and use a basic Sigil
  1. Check JEI for a tier-1 Sigil (e.g. Sigil of the Green Grove or Water Sigil)
  2. Craft it using the altar + LP as above
  3. Right-click with the Sigil to activate its effect
- [x] No crashes when interacting with the altar
- [x] No runaway damage loops or instant-death bugs

---

## 6. Farmer's Delight & Food Ecosystem

- [x] Farmer's Delight cooking pot crafts and produces a food item
- [x] Cutting Board + knife works to prep ingredients
- [x] **Pam's HarvestCraft** — garden bushes spawn in the world; harvest a crop seed from one
- [x] Pam's crop grows to maturity and drops food
- [x] Pam's Trees — fruit tree spawns in a biome; fruit drops from leaves
- [x] **Cooking for Blockheads** — place a kitchen block, open it, confirm recipe filtering works with available ingredients
- [x] **Brewin' And Chewin'** — craft a fermenting barrel and begin a fermentation recipe
- [x] **More Delight** — spot-check a recipe in JEI (search `moredelight`)
- [x] **Farmer's Delight: Extended** — at least one Create+FD crossover recipe visible in JEI (e.g. milling a FD crop)
- [x] **Create Slice & Dice** — Deployer or Mechanical Saw processes a FD cutting recipe

---

## 7. Let's Do Series

- [x] **Vinery** — grape sapling plants and grows; craft a bottle of wine
- [x] **Farm & Charm** — place a butter churn or similar functional block; process an item
- [x] **Bakery** — bake a bread or cake variant
- [x] **Brewery** — set up a barrel; begin a brew recipe
- [x] **Meadow** — meadow sub-biome generates (may need to explore); craft a cheese
- [x] **HerbalBrews** — dry a leaf, brew a tea or coffee
- [x] **[Let's Do] Compat** — no recipe conflicts between the Let's Do mods (spot-check in JEI)

---

## 8. Botany Pots

- [x] Place a Botany Pot and plant a vanilla crop; confirm it grows and auto-harvests
- [x] **Botany Trees** — plant a sapling in a Botany Tree Pot; confirm it produces logs/saplings
- [x] **Botany Pots Tiers** — craft a higher-tier pot; confirm improved growth speed
- [x] **Mystical Agriculture compat** — plant a Mystical Agriculture seed in a Botany Pot; confirm it works

---

## 9. Mystical Agriculture

- [x] Crafting seed and growth accelerator visible in JEI
- [x] Plant a basic resource crop (e.g. iron seeds); grows to maturity
- [x] Harvest produces a resource essence; craft it into the resource
- [x] Inferium crop grows and produces essence

---

## 10. Productive Bees ⚠️

- [x] Advanced Beehive places and accepts bees
- [x] At least one resource bee (e.g. Honey Bee or Iron Bee) produces output over time
- [x] Output rate feels roughly comparable to Modern Chickens at default — note anything extreme
- [x] No crashes or infinite loop behaviour in the bee GUIs

---

## 11. Modern Chickens

- [x] Chicken coop (or vanilla breeding) produces a resource chicken (e.g. Iron Chicken)
- [x] Resource chicken lays an appropriate item over time
- [x] Breeding two resource chickens produces offspring
- [x] No item duplication or egg loop issues

---

## 12. Fishing

- [x] **Aquaculture 2** — craft an Aquaculture rod; fish up at least one new fish species
- [x] New fish visible in JEI with cooking/food recipes
- [x] **Lava Fishing** — fish in lava in the Nether; catch at least one lava-specific item
- [x] **Create Fishing Bobber Detector** — place detector; confirm it outputs a redstone/Create signal when a fish bites

---

## 13. Create Food Integrations

- [x] **Create Confectionery** — crush cocoa beans in a Millstone to get Crushed Cocoa; craft a chocolate item - NOTE: use mechanical press, millstone makes dye
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

1. Not sure there's a Create caramel recipe. I can only see the "Caramel", "Caramel Bucket", and "Bar of Caramel" from "Create Confectionary" but there's no recipe for any of those. The bar and liquid are made from the bucket, the bucket is made from the liquid, it's cyclical with no "entry" to the actual caramel resource. There is, howevere, also a "Caramel" from "Pam's HarvestCraft" I'm wondering if "melting" that can transition into the Create recipes, or if there's a recipe conflict in there. Marshmallow's have a recipe.