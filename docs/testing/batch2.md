# FuzzCraft 4 — Batch 2 Testing: Tech & Automation

## Summary
**Pack version:** 0.1.2
**Test date:** <fill in>
**Tester:** <fill in>
**Play mode:** Single player

## Known Issues
- **Ender IO** — added at beta (8.2.x). Watch for crashes when placing conduit bundles or opening machines. Report version in notes if crash occurs.
- **Iron Chests** — added at 1.21 (not 1.21.1 specifically). Functional but flag any visual or GUI issues.
- **Create: Dreams & Desires** — beta release. May have rough edges on contraption blocks.
- **Thermal Series** — not available for 1.21.1. Replaced by Ender IO + Powah!. On watchlist.

---

## Launch & Stability

- [ ] Game launches to main menu without crash
- [ ] New world generates without crash — check `logs/latest.log` for ERROR lines
- [ ] F3 screen shows TPS at or near 20 at idle in a fresh world
- [ ] No crash after 10 minutes of normal play

## Regression — Batch 1

- [ ] JEI — recipe panel visible, search works
- [ ] Jade — look at a block, tooltip appears
- [ ] JourneyMap — minimap renders in HUD, full map opens with J
- [ ] FTB Chunks — claim a chunk, protection overlay visible on map
- [ ] Iris — Shader Packs button present in video settings
- [ ] Dynamic Lights — hold a torch, area lights up

## JEI & Recipe Viewer

- [ ] No obvious duplicate recipes (Almost Unified working — search `copper ingot`, one dominant result)
- [ ] Create recipes visible — press R on a Create block
- [ ] IE recipes visible — press R on an IE block
- [ ] AE2 recipes visible
- [ ] Apotheosis gem/affix tooltips rendering on items
- [ ] Mechanical Extruder has at least default recipes listed (water + lava adjacent → check JEI)

## Create — Core

- [ ] Place a shaft and cogwheels, connect a hand crank — rotation works
- [ ] Mechanical Press functions (place above a basin, power it)
- [ ] Contraption assembles and moves
  1. Place a mechanical piston or bearing
  2. Attach blocks to form a contraption
  3. Power it — contraption should move as a unit
- [ ] Blaze Burner accepts a fluid fuel (Create: Liquid Fuel)
  1. Set up a Blaze Burner
  2. Pipe lava or another fluid into it
  3. Confirm it burns

## Create — Trains (Steam 'n' Rails)

- [ ] Place track segments and connect them
- [ ] Assemble a locomotive on the track
- [ ] Drive the train — movement smooth, no crash
- [ ] Steam 'n' Rails bogies/locomotive types appear in creative search

## Create — Renewables

- [ ] **Ore Excavation** — place a drill head, power it with rotational force, confirm it mines blocks below
- [ ] **Molten Vents** — confirm orestone vents generate in world
  1. Use `/tp @s ~ ~ ~` and explore caves or ocean floor
  2. Look for dormant orestone vent blocks (more common underwater)
- [ ] **Mechanical Extruder** — place one with water on one side and lava on the other, confirm output (cobblestone or stone)

## Create — Addons Spot Checks

- [ ] Copycat block — apply any block texture to a copycat panel, confirm it renders correctly
- [ ] CC:C Bridge — place a Create peripheral block next to a CC computer
  1. Open the computer
  2. Run `peripheral.getNames()` — the Create peripheral should appear in the list
- [ ] Trading Floor — place a Trading Depot near a villager, confirm GUI opens

## Immersive Engineering

- [ ] Coke Oven multiblock forms
  1. Place a 3×3×3 of Coke Oven bricks
  2. Right-click the centre with an Engineer's Hammer
  3. GUI should open
- [ ] LV wiring — connect two LV connectors with wire, power transfers
- [ ] IE Crusher processes ores → confirm doubled output in output slot

## Applied Energistics 2

- [ ] ME Controller places and illuminates with power connected
- [ ] ME Drive + storage cell recognised by the network
- [ ] ME Terminal shows inventory and allows item retrieval
- [ ] Applied Create — place a Stress P2P Tunnel, confirm it appears in JEI recipes

## Ender IO ⚠️

- [ ] Energy conduit places and connects between two blocks
- [ ] Item conduit transfers items between two chests
- [ ] Conduit bundle — place two conduit types in the same block, no crash
- [ ] Alloy Smelter — place, power with a conduit, insert ingredients, confirm output

## CC: Tweaked + Advanced Peripherals

- [ ] Computer places, right-click opens terminal, `print("hello")` works
- [ ] Turtle mines a block
  1. Place a Turtle
  2. Open its terminal
  3. Run `turtle.dig()` — block in front should break
- [ ] Advanced Peripherals — ME Bridge peripheral
  1. Place an ME Bridge adjacent to an active ME network
  2. Wrap it in a computer: `peripheral.wrap("top")` (adjust direction)
  3. Confirm the peripheral responds with methods

## Storage

- [ ] Storage Drawer places, accepts items, displays count on front
- [ ] Sophisticated Storage — chest opens, upgrade slot visible in GUI
- [ ] Sophisticated Backpacks — equip a backpack in the correct slot, open it, insert an upgrade
- [ ] Traveller's Backpack — equip, open GUI, confirm tank and tool slots visible
- [ ] Iron Chests — craft and place a gold or diamond chest, confirm it opens and holds more than vanilla ⚠️
- [ ] Iron Furnaces — craft an iron furnace, place it, confirm faster smelting than vanilla

## Power & Energy

- [ ] Powah! — place a Thermo Generator adjacent to a lava source, confirm RF generation in GUI
- [ ] Solar Flux Reborn — place a solar panel outdoors, confirm RF generation in daylight
- [ ] Flux Networks — place a Flux Plug on a power source and a Flux Point near a machine
  1. Create a Flux Network in the Flux Networks GUI
  2. Add both the Plug and Point to the network
  3. Confirm energy transfers wirelessly
- [ ] Iron Jetpacks — craft a basic jetpack
  1. Open Curios inventory (press G or configured key)
  2. Equip jetpack in the back slot
  3. Hold jump to fly — confirm it works
  4. *(Optional)* Confirm a higher-tier jetpack approaches creative flight speed
- [ ] Ender IO conduit transfers power from a Powah! cell to an Ender IO machine

## Tools, Weapons & Combat

- [ ] Silent Gear — craft a tool
  1. Craft a binding, tool rod, and tool head using materials in JEI
  2. Assemble in a gear crafting station
  3. Confirm the tool has material stats in its tooltip
- [ ] Silent's Gems — gem ore generates in the world (check caves), mine one, confirm it's usable as a Silent Gear material
- [ ] Spartan Weaponry — find a halberd or lance in creative, equip it, confirm it deals damage to a mob
- [ ] Better Combat — dual-wield
  1. Hold a sword in each hand
  2. Attack a mob — confirm animation differs from vanilla single-weapon swing
- [ ] Apotheosis — enchanting table
  1. Place an enchanting table with bookshelves
  2. Confirm affix slots or gem socket options appear beyond vanilla enchants
- [ ] Apotheosis — affix item drop
  ```
  /difficulty hard
  /loot give @s loot minecraft:chests/end_city_treasure
  ```
  Confirm at least one item has coloured affix modifier lines in its tooltip

## Performance

- [ ] Enable a shaderpack (Iris) — stable FPS in overworld with Create Better FPS active
- [ ] Run a Create contraption nearby — no significant FPS drop while it operates
- [ ] Open an AE2 terminal with items in storage — no lag spike on open

## Compat Spot Checks

- [ ] Jade — hover over a Create machine, confirm extended info (stress, RPM, etc.) visible
- [ ] Jade — hover over an IE machine, confirm internal state visible
- [ ] Advanced Peripherals — hover over a CC computer in Jade, confirm peripheral info shown

---

## Deferred — Requires Server / Multiplayer
*Full tests in `multiplayer.md` — Batch 2 section.*

- Flux Networks wireless power across loaded chunks with multiple players
- FTB Chunks + Create: forceloaded chunk keeps contraption running when owner offline
- Create trains: two players on the same track network simultaneously
- AE2 shared ME network — simultaneous access by two players
- Sophisticated Backpacks: upgrade behaviour consistent across clients
- Ender IO conduits: cross-chunk item and fluid transfer stability
- General TPS under load with active contraptions and multiple players

---

## Tester Notes
<!-- Fill in: anything broken, surprising, or worth flagging back. -->
