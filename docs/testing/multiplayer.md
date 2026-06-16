# FuzzCraft 4 — Multiplayer Testing

Tests that require two or more connected players. Run each batch's section after that batch passes single-player testing and the server has been updated.

**Most recent session:**
**Pack version tested:**
**Test date:**
**Testers:**

---

## Batch 1 — Foundation

### Connection & Basics

- [ ] Second player connects without mod mismatch kick
- [ ] Both players see each other in-game
- [ ] No console errors after both players connect

### FTB Teams

- [ ] Each player has a personal team auto-created on first join
- [ ] Players can see each other's teams in the FTB Teams screen

### FTB Chunks

- [ ] FORCED_ALL ally mode — other players listed as allies without manual setup
- [ ] Chunk claim protection — second player cannot break blocks in another player's claimed chunk
- [ ] Claimed chunk visible on other players' FTB Chunks map
- [ ] Forceload — claim and forceload a chunk, owner logs off, chunk stays loaded (check server console)

### Shared Play

- [ ] Both players can trade items
- [ ] JourneyMap — player dots visible on each other's map
- [ ] JEI — recipe viewer works for both players simultaneously
- [ ] No desync or rubber-banding under normal movement

### Server Stability

- [ ] Server stays up for 30+ minutes with both players active
- [ ] No WARN/ERROR in server console during session
- [ ] World saves cleanly on `/stop`

---

## Batch 2 — Tech & Automation

### Flux Networks

- [ ] Flux Plug on a power source and Flux Point near a second player's machine — energy transfers without both players in the same chunk
- [ ] Wireless transfer works across dimension boundary (if applicable)

### Create — Contraptions & Trains

- [ ] Forceloaded chunk with a running contraption (e.g. windmill + millstone) — owner logs off, contraption keeps running, second player confirms output continues
- [ ] Two players on the same train network simultaneously — no desync, signals behave correctly
- [ ] Two players assemble separate contraptions in the same area — no conflict or crash

### Applied Energistics 2

- [ ] Two players access the same ME Terminal simultaneously — no inventory desyncs
- [ ] Both players can insert and retrieve items from shared storage without conflict

### Ender IO

- [ ] Item conduit transferring across a chunk boundary — items continue flowing when only one player is nearby
- [ ] Fluid conduit — same cross-chunk stability check

### Storage

- [ ] Sophisticated Backpacks — both players have backpacks with upgrades; confirm upgrades function correctly for each player independently (no cross-client bleed)

### General Server Health

- [ ] TPS stays at or near 20 with both players active and at least one Create contraption running
- [ ] No WARN/ERROR in server console during a 20-minute session with active play
- [ ] Chunk loading from FTB Chunks forceloads behaves as expected — no runaway chunk loading

---

*Add a new `## Batch N — <Name>` section here after each batch's single-player test passes.*

---

## Batch 5a — Flagship + Bosses + Utility

### Bosses Rise
- [ ] Bosses Rise boss killed with multiple players present — confirm loot drops for each player (Lootr covers chests, but entity kill drops may not scale; verify no one gets left out)

### Bosses of Mass Destruction
- [ ] Boss fight with full group — confirm aggro behaviour and arena doesn't crash under multi-player load

### Dimensional Dungeons
- [ ] Two players enter the dungeon dimension — confirm Lootr chests give independent loot per player
- [ ] Block protection holds for both players (neither can break dungeon walls)

### Dimensional Pockets II
- [ ] Player A enters their pocket dimension — Player B cannot follow (pocket dims should be player-isolated)

### RFTools Dimensions
- [ ] Both players can travel to the same RFTools dimension via the Matter Transmitter/Receiver setup
- [ ] Mining in the dimension with two players simultaneously — no desync or TPS drop

---

## Batch 3 — Magic & Farming

### Productive Bees

- [ ] Two players each have a hive running — confirm output rates are consistent and neither hive interferes with the other
- [ ] No crashes or desyncs when both players open Productive Bees GUIs simultaneously

### Modern Chickens

- [ ] Two players each have resource chickens — no cross-player item desyncs when chickens lay items
- [ ] Breeding a resource chicken while a second player is nearby — no dupe or loss

### Ars Énergistique

- [ ] Two players accessing the same AE2 network with Source automation active — confirm no inventory desyncs
- [ ] Source Cable throughput is consistent under simultaneous access from both players

### Botany Pots & Mystical Agriculture

- [ ] Forceloaded chunk with Botany Pots and Mystical Agriculture crops running — owner logs off, second player confirms crops continue ticking and items are deposited
- [ ] TPS stable with both running alongside at least one Create contraption

### Fermentation (Vinery / Brewery)

- [ ] Fermentation barrel in a forceloaded chunk — owner logs off, second player confirms fermentation progresses
- [ ] Both players can retrieve finished products from the same barrel without conflict

### General Server Health

- [ ] TPS stable at or near 20 with Productive Bees, Botany Pots, Mystical Agriculture crops, and a Create contraption all running simultaneously
- [ ] No WARN/ERROR in server console during a 20-minute session

---

## Batch 5 — Dimensions (combined 5a + 5b + 5c server pass)

*Run after B5c merges to main. Covers Twilight Forest, Aether cluster, and Underground/Quirky dimensions together.*

### Connection & Pack Sync

- [ ] Server updated to post-B5c main; all clients sync without mod mismatch kick
- [ ] No error flood in server console on startup

### Twilight Forest (B5a)

- [ ] Two players enter TF simultaneously — dimension loads for both, no desync
- [ ] Boss fight with two players — Naga, Lich, or Hydra; confirm no crash or entity desync

### The Aether (B5b)

- [ ] Two players enter the Aether simultaneously — dimension loads for both
- [ ] Aether mobs and structures visible and consistent across both clients

### The Undergarden (B5c)

- [ ] Two players enter the Undergarden simultaneously — no crash, both see correct biomes
- [ ] Undergarden mobs behave correctly in multiplayer (no entity spam or desync)

### Deeper and Darker (B5c)

- [ ] Two players in the same deep dark biome — no server crash, Warden aggro works correctly for both
- [ ] Ancient City loot chests openable by both players (Lootr integration if applicable)

### The Bumblezone (B5c)

- [ ] Two players trigger and enter the Bumblezone portal — dimension loads for both
- [ ] Bumblezone resources obtainable by both players without conflict

### General Dimension Server Health

- [ ] TPS stable with at least two dimension threads active (players in different dimensions simultaneously)
- [ ] No WARN/ERROR in server console during multi-dimension session
