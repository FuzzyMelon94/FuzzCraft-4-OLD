
# FuzzCraft 4 — Batch 2 Testing: Tech & Automation
## Summary
**Pack version:** 0.2.1–0.2.4
**Test date:** 2026-06-12
**Tester:** Tom
**Play mode:** Single player

## Known Issues
- **Ender IO** — added at beta (8.2.x). Watch for crashes when placing conduit bundles or opening machines. Report version in notes if crash occurs.
- **Iron Chests** — added at 1.21 (not 1.21.1 specifically). Functional but flag any visual or GUI issues.
- **Create: Dreams & Desires** — beta release. May have rough edges on contraption blocks.
- **Thermal Series** — not available for 1.21.1. Replaced by Ender IO + Powah!. On watchlist.

---

## Launch & Stability

- [x] Game launches to main menu without crash
- [x] New world generates without crash — check `logs/latest.log` for ERROR lines
- [x] F3 screen shows TPS at or near 20 at idle in a fresh world
- [x] No crash after 10 minutes of normal play

## Regression — Batch 1

- [x] JEI — recipe panel visible, search works
- [x] Jade — look at a block, tooltip appears
- [x] JourneyMap — minimap renders in HUD, full map opens with J
- [x] FTB Chunks — claim a chunk, protection overlay visible on map
- [x] Iris — Shader Packs button present in video settings
- [x] Dynamic Lights — hold a torch, area lights up

## JEI & Recipe Viewer

- [x] No obvious duplicate recipes (Almost Unified working — search `copper ingot`, one dominant result)
- [x] Create recipes visible — press R on a Create block
- [x] IE recipes visible — press R on an IE block
- [x] AE2 recipes visible
- [x] Apotheosis gem/affix tooltips rendering on items
- [x] Mechanical Extruder has at least default recipes listed (water + lava adjacent → check JEI)

## Create — Core

- [x] Place a shaft and cogwheels, connect a hand crank — rotation works
- [x] Mechanical Press functions (place above a basin, power it)
- [x] Contraption assembles and moves
  1. Place a mechanical piston or bearing
  2. Attach blocks to form a contraption
  3. Power it — contraption should move as a unit
- [x] Blaze Burner accepts a fluid fuel via C&A Straw
  1. Craft a Straw (Create: Crafts & Additions)
  2. Apply it to a Blaze Burner
  3. Connect a fluid pipe with lava or another liquid fuel — confirm it burns

## Create — Trains (Steam 'n' Rails)

- [x] Place track segments and connect them
- [x] Assemble a locomotive on the track
- [x] Drive the train — movement smooth, no crash
- [x] Steam 'n' Rails bogies/locomotive types appear in creative search

## Create — Renewables

- [x] **Ore Excavation** — place a drill head, power it with rotational force, confirm it mines blocks below
- [x] **Molten Vents** — confirm orestone vents generate in world
  1. Use `/tp @s ~ ~ ~` and explore caves or ocean floor
  2. Look for dormant orestone vent blocks (more common underwater)
- [x] **Mechanical Extruder** — place one with water on one side and lava on the other, confirm output (cobblestone or stone)

## Create — Addons Spot Checks

- [x] Copycat block — apply any block texture to a copycat panel, confirm it renders correctly
- [x] CC:C Bridge — place a Create peripheral block next to a CC computer
  1. Open the computer
  2. Run `peripheral.getNames()` — the Create peripheral should appear in the list
- [x] Trading Floor — place a Trading Depot near a villager, confirm GUI opens

## Immersive Engineering

- [x] Coke Oven multiblock forms
  1. Place a 3×3×3 of Coke Oven bricks
  2. Right-click the centre with an Engineer's Hammer
  3. GUI should open
- [x] LV wiring — connect two LV connectors with wire, power transfers
- [x] IE Crusher processes ores → confirm doubled output in output slot

## Applied Energistics 2

- [x] ME Controller places and illuminates with power connected
- [x] ME Drive + storage cell recognised by the network
- [x] ME Terminal shows inventory and allows item retrieval
- [x] Applied Create — place a Stress P2P Tunnel, confirm it appears in JEI recipes

## Ender IO ⚠️

- [x] Energy conduit places and connects between two blocks
- [x] Item conduit transfers items between two chests
- [x] Conduit bundle — place two conduit types in the same block, no crash
- [x] Alloy Smelter — place, power with a conduit, insert ingredients, confirm output

## CC: Tweaked + Advanced Peripherals

- [x] Computer places, right-click opens terminal, `print("hello")` works
- [x] Turtle mines a block
  1. Place a Turtle
  2. Open its terminal
  3. Run `turtle.dig()` — block in front should break
- [x] Advanced Peripherals — ME Bridge peripheral
  1. Place an ME Bridge adjacent to an active ME network
  2. Wrap it in a computer: `peripheral.wrap("top")` (adjust direction)
  3. Confirm the peripheral responds with methods

## Storage

- [x] Storage Drawer places, accepts items, displays count on front
- [x] Sophisticated Storage — chest opens, upgrade slot visible in GUI
- [x] Sophisticated Backpacks — equip a backpack in the correct slot, open it, insert an upgrade
- [x] Traveller's Backpack — equip, open GUI, confirm tank and tool slots visible
- [x] Iron Chests — craft and place a gold or diamond chest, confirm it opens and holds more than vanilla ⚠️
- [x] Iron Furnaces — craft an iron furnace, place it, confirm faster smelting than vanilla

## Power & Energy

- [x] Powah! — place a Thermo Generator adjacent to a lava source, confirm RF generation in GUI
- [x] Solar Flux Reborn — place a solar panel outdoors, confirm RF generation in daylight
- [x] Flux Networks — place a Flux Plug on a power source and a Flux Point near a machine
  1. Create a Flux Network in the Flux Networks GUI
  2. Add both the Plug and Point to the network
  3. Confirm energy transfers wirelessly
- [x] Iron Jetpacks — craft a basic jetpack
  1. Open Curios inventory (press G or configured key)
  2. Equip jetpack in the back slot
  3. Hold jump to fly — confirm it works
  4. *(Optional)* Confirm a higher-tier jetpack approaches creative flight speed
- [x] Ender IO conduit transfers power from a Powah! cell to an Ender IO machine

## Tools, Weapons & Combat

- [x] Silent Gear — craft a tool
  1. Craft a binding, tool rod, and tool head using materials in JEI
  2. Assemble in a gear crafting station
  3. Confirm the tool has material stats in its tooltip
- [x] Silent's Gems — gem ore generates in the world (check caves), mine one, confirm it's usable as a Silent Gear material
- [x] Spartan Weaponry — find a halberd or lance in creative, equip it, confirm it deals damage to a mob
- [x] Better Combat — dual-wield
  1. Hold a sword in each hand
  2. Attack a mob — confirm animation differs from vanilla single-weapon swing
- [x] Apotheosis — enchanting table
  1. Place an enchanting table with bookshelves
  2. Confirm affix slots or gem socket options appear beyond vanilla enchants
- [x] Apotheosis — affix item drop
  ```
  /difficulty hard
  /loot give @s loot minecraft:chests/end_city_treasure
  ```
  Confirm at least one item has coloured affix modifier lines in its tooltip

## Performance

- [x] Enable a shaderpack (Iris) — stable FPS in overworld with Create Better FPS active
- [x] Run a Create contraption nearby — no significant FPS drop while it operates
- [x] Open an AE2 terminal with items in storage — no lag spike on open

## Compat Spot Checks

- [x] Jade — hover over a Create machine, confirm extended info (stress, RPM, etc.) visible
- [x] Jade — hover over an IE machine, confirm internal state visible
- [x] Advanced Peripherals — ME Bridge detects AE2 network (tested in CC: Tweaked section above)

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
1. shadows are weird with shaders on for moving Create contraptions
2. `Create: Liquid Fluids` I'm not sure if this mod is working, but `Create Crafts & Additions` provides a straw that let's you pipe into blaze burners - think we can remove the `Liquid Fluids` mod
3. ~115 FPS / ~90 FPS with Complementary Unbound
4. Contraptions drop FPS by 1 or 2 - small contraption but likely a non-issue