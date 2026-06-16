# FuzzCraft 4 — Batch 7 Testing: QoL & Final Compat

## Summary
**Pack version:** 0.7.1–x.x.x
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
- **Almost Unified / Tropicraft cocktail** — JEI still shows Pam's Pina Colada as the Tropicraft cocktail recipe output. Fix is in configs.md: run the game once to generate `config/almostunified/unify.json`, add `"tropicraft:cocktail"` to `ignoredItems`, commit the file. The Tropicraft portal works correctly regardless.
- **Curios slots** — config is now in `config/curios-server.toml`. Verify in-game that 2 back / 4 ring / 4 charm slots are showing correctly; if not, the config key format may need adjusting after a game run (Curios sometimes requires a first-run config merge).
- **Hybrid Aquatic** — watchlisted as "re-add candidate" after the Lithostitched fix. Not in the pack yet — test without it first. If you want to test it, add via `packwiz mr add hybrid-aquatic -y` and create a fresh world to confirm no world-create crash.
- **KubeJS work (caramel bridge, extruder recipes, difficulty scaling)** — all deferred to B8. Caramel circular recipe issue still present.
- **Alex's Mobs** — already in the pack via an unofficial 1.21.1 Citadel port. Monitor for any instability; this is not an official release.

---

## 1. Launch & Stability

- [ ] Pack launches to main menu without crash
- [ ] Create a new world — no crash on world gen
- [ ] Load into the world — no errors in chat, F3 screen shows expected mod count
- [ ] Check JEI loads and is populated correctly (no missing textures, no crashes on search)
- [ ] Check Collapsible Groups is working — item groups in JEI should be collapsible

## 2. Regression — Batches 1–6

- [ ] JourneyMap loads, FTB Chunks claim overlay visible
- [ ] Create contraptions functional (deployer, mixer, etc.)
- [ ] AE2 ME system connectable
- [ ] Ars Nouveau spells craftable (check Arcane Core)
- [ ] Farmer's Delight cooking grid accessible
- [ ] Twilight Forest portal craftable (check JEI for magic map recipe)
- [ ] Aether portal ignites correctly
- [ ] Waystones can be placed and teleported to
- [ ] Tropicraft portal item craftable (cocktail) — confirm JEI shows correct recipe (tropicraft:cocktail, not Pam's Pina Colada)

## 3. New QoL Mods

### RightClickHarvest
- [ ] Plant a crop (e.g. wheat), wait for it to be fully grown
- [ ] Right-click the fully-grown crop — it should harvest and immediately replant
- [ ] Verify partially-grown crops are NOT harvested on right-click

### TorchMaster
- [ ] Craft a Mega Torch
- [ ] Place it — mob spawning should be suppressed in a radius around it
- [ ] Craft a Feral Torch (allows mob spawning in a radius) as a counterpart check

### Particle Effects
- [ ] Hit a mob — confirm hit particles are visible and look polished
- [ ] No unusual particle spam or performance drop

### Naturally Trimmed
- [ ] Kill several mobs (zombies, skeletons) in armour — check they spawn with armour trims on their gear
- [ ] Check loot — trimmed armour pieces should be dropping

### Trimmable Tools
- [ ] Open a smithing table — confirm tool trim recipes are available in JEI
- [ ] Apply a trim to a pickaxe or sword — confirm it works

### Clumps
- [ ] Kill a large number of mobs (e.g. spawner farm)
- [ ] Verify XP orbs clump into larger single orbs rather than scattering individually
- [ ] Confirm XP pickup is normal

### Reese's Sodium Options
- [ ] Open Video Settings — should show the Reese's Sodium Options expanded layout rather than the default Sodium screen
- [ ] No crash when navigating video settings

### Collapsible Groups (JEI)
- [ ] Open JEI item browser — confirm item group headers are collapsible
- [ ] Collapse and expand a few groups — confirm UI is functional

## 4. Curios Slots

- [ ] Open Curios inventory (`H` key or via button) — confirm slot counts:
  - Back: 2 slots
  - Ring: 4 slots
  - Charm: 4 slots
- [ ] Equip items in each slot type to confirm they function correctly
- [ ] If slot counts are wrong, check `config/curios-server.toml` and whether Curios loaded it (it may need a `curios-common.toml` instead — adjust and retest)

## 5. Alex's Mobs (Unofficial Port)

- [ ] Alex's Mobs creatures spawn in the world (check in appropriate biomes)
- [ ] No crash from Alex's Mobs-specific entities or loot tables
- [ ] Monitor for any unusual behaviour — this is an unofficial port

## 6. Almost Unified — Tag Audit

Do this after applying the Tropicraft cocktail fix from configs.md.

- [ ] Check JEI for Tropicraft cocktail recipe — should now show `tropicraft:cocktail` output, not Pam's Pina Colada
- [ ] Browse JEI for Pam's HarvestCraft items — spot-check a few (caramel, juices, etc.) to confirm AU unifications look correct
- [ ] Browse JEI for Create fluid recipes — check caramel fluid shows correctly (circular recipe still present until B8 KubeJS fix)
- [ ] Check Ars Nouveau mana items in JEI — no unexpected unifications
- [ ] Note any additional items that look unified incorrectly → add to `ignoredItems` in `unify.json` and re-test

## 7. Memory Check

- [ ] After 20–30 minutes of play, open F3 and note memory usage
- [ ] If you've lowered max heap to 8–10GB (recommended in configs.md), note whether GC feels responsive or if there are noticeable pauses
- [ ] Record peak usage here: ________ MB

## 8. Deferred — Requires Server / Multiplayer

- Verify Curios slot counts are consistent for all players on a server
- Test Clumps XP behaviour in a multiplayer mob farm context
- BOMD and RFTools questing (deferred to B8)
- Hybrid Aquatic re-add test (if pursuing — requires fresh world creation on server to confirm no crash)

## Tester Notes
<!-- Broken things, surprises, feedback -->
