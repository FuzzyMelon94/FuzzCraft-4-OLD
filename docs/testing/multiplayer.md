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
