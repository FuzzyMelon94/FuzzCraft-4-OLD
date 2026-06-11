# FuzzCraft 4 — Multiplayer Testing

Tests that require two or more players. Run these when the pack reaches a "ready" milestone (after Batch 5 or at a suitable stable point), not per-batch.

**Pack version tested:**  
**Test date:**  
**Testers:**  

---

## Connection

- [ ] Second player connects without being kicked for mod mismatch
- [ ] Both players see each other in-game
- [ ] No console errors after both players connected

## FTB Teams

- [ ] Each player has a personal team auto-created on first join
- [ ] Players can see each other's teams in the FTB Teams screen

## FTB Chunks

- [ ] FORCED_ALL ally mode: other players listed as allies without any manual setup
- [ ] Chunk claim protection: second player cannot place/break blocks in another player's claimed chunk
- [ ] Claimed chunk is visible on other players' FTB Chunks map
- [ ] Forceload: claim and forceload a chunk, first player logs off, chunk stays loaded (check server console)

## Shared Play

- [ ] Both players can trade items
- [ ] JourneyMap: player waypoints visible to owner, death waypoints work
- [ ] JEI: recipe viewer works for both players simultaneously
- [ ] No desync or rubber-banding under normal play

## Server Stability

- [ ] Server stays up for 30+ minutes with both players active
- [ ] No WARN/ERROR in server console during session
- [ ] World saves cleanly on `/stop`

---

*Add batch-specific multiplayer tests below as needed when content mods are included.*
