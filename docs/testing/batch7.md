# FuzzCraft 4 — Batch 7 Testing: QoL & Final Compat

## Summary
**Pack version:** 0.7.1–0.7.3 (wave 1: 0.7.1; wave 2: 0.7.2–0.7.3)
**Test date:** 17 June 2026
**Tester:** FuzzyMelon94
**Play mode:** Single player / Server

## Known Issues
- **Almost Unified / Tropicraft cocktail** — fix committed (`tropicraft:cocktail` in `ignored_items`). Verify in testing that JEI now shows the correct cocktail output.
- **Curios slots** — config is now in `config/curios-server.toml`. Verify in-game that 2 back / 4 ring / 4 charm slots are showing correctly; if not, the config key format may need adjusting after a game run (Curios sometimes requires a first-run config merge).
- **Hybrid Aquatic** — watchlisted as "re-add candidate" after the Lithostitched fix. Not in the pack yet — test without it first. If you want to test it, add via `packwiz mr add hybrid-aquatic -y` and create a fresh world to confirm no world-create crash.
- **KubeJS work (caramel bridge, extruder recipes, difficulty scaling)** — all deferred to B8. Caramel circular recipe issue still present.
- **Alex's Mobs** — already in the pack via an unofficial 1.21.1 Citadel port. Monitor for any instability; this is not an official release.

---

## 1. Launch & Stability

- [x] Pack launches to main menu without crash
- [x] Create a new world — no crash on world gen
- [x] Load into the world — no errors in chat, F3 screen shows expected mod count
- [x] Check JEI loads and is populated correctly (no missing textures, no crashes on search)
- [x] Check Collapsible Groups is working — item groups in JEI should be collapsible

## 2. Regression — Batches 1–6

- [x] JourneyMap loads, FTB Chunks claim overlay visible
- [x] Create contraptions functional (deployer, mixer, etc.)
- [x] AE2 ME system connectable
- [x] Ars Nouveau spells craftable (check Arcane Core)
- [x] Farmer's Delight cooking grid accessible
- [x] Twilight Forest portal craftable (check JEI for magic map recipe)
- [x] Aether portal ignites correctly
- [x] Waystones can be placed and teleported to
- [x] Tropicraft portal item craftable (cocktail) — JEI fix committed; verify cocktail recipe shows correctly in playthrough

## 3. New QoL Mods

### TorchMaster
- [x] Craft a Mega Torch
- [x] Place it — mob spawning should be suppressed in a radius around it
- [x] Craft a Feral Torch (allows mob spawning in a radius) as a counterpart check

### Particle Effects
- [x] Hit a mob — confirm hit particles are visible and look polished
- [x] No unusual particle spam or performance drop

### Clumps
- [x] Kill a large number of mobs (e.g. spawner farm)
- [x] Verify XP orbs clump into larger single orbs rather than scattering individually
- [x] Confirm XP pickup is normal

### Reese's Sodium Options
- [x] Open Video Settings — should show the Reese's Sodium Options expanded layout rather than the default Sodium screen
- [x] No crash when navigating video settings

### Collapsible Groups (JEI)
- [x] Open JEI item browser — confirm item group headers are collapsible
- [x] Collapse and expand a few groups — confirm UI is functional

## 4. Alex's Mobs (Unofficial Port)

- [x] Alex's Mobs creatures spawn in the world (check in appropriate biomes)
- [x] No crash from Alex's Mobs-specific entities or loot tables
- [x] Monitor for any unusual behaviour — this is an unofficial port

## 5. Memory Check

- [x] GC feels responsive with 8GB heap (75–90% usage observed — GC-driven range, expected)
- [x] Record peak usage: 8192 MB / 8192 MB — heap is full; GC keeps up

## 6. Wave 2 — QoL Mods (Confirmed Working)

### Performance & Visual
- [x] Dynamic FPS active — minimize the game window, confirmed FPS drops
- [x] Sound Physics Remastered — cave reverb/echo confirmed
- [x] Log Begone — reduced log spam confirmed
- [x] BetterF3 — F3 screen coloured and readable
- [x] Better Advancements — improved advancements UI confirmed
- [x] Advancement Plaques — styled plaque toast confirmed

### HUD & Tooltips
- [x] Durability Tooltip — durability shown as number in tooltip confirmed

### Inventory & Crafting
- [x] TrashSlot — trash slot visible and functional
- [x] Visual Workbench — items render on table surface confirmed

### Gameplay QoL
- [x] Jump Over Fences — sprint-jump clears fences confirmed
- [x] Cut Through — hit registers through grass/leaves confirmed
- [x] Monsters in the Closet — nearby monsters highlighted on sleep-fail confirmed
- [x] Zume — zoom activates on Z; scroll changes zoom level confirmed
- [x] Better Days — day/night cycle longer confirmed
- [x] Crops Love Rain — crops grow faster in rain confirmed
- [x] KleeSlabs — break top/bottom half of double slab confirmed

### System / Social
- [x] No Chat Reports — no signing warnings on server join confirmed
- [x] Yeetus Experimentus — experimental features warning suppressed confirmed
- [x] Emoji Type — `:` autocomplete in chat confirmed

---

## Tester Notes — Resolution Log

| # | Note | Resolution |
|---|---|---|
| 0 | Farmland reverts to dirt when jumped on | **Fixed** — added Trample No More |
| 1 | Lag spikes on chunk traversal | Deferred → playthrough1 (likely server CPU bottleneck) |
| 2 | Chunks Fade In lighting mismatch at fade start | Deferred → playthrough1 (cosmetic; needs Chunks Fade In config) |
| 3 | Equipment Compare shows overlay 3× on Shift | **Working as intended** — one comparison per equipped slot; 3 armour pieces = 3 overlays |
| 4 | Double Doors not working | **Fixed** — mod was `side = "server"`; corrected to `both` |
| 5 | Remove "recipes unlocked" popup | Deferred → playthrough1 (no vanilla toggle; needs a mod or config) |
| 6 | Scribble — thought it was books only | **Clarified** — Scribble works on both signs AND books; use § codes or the formatting UI on signs |
| 7 | Create: Power Loader — defer to playthrough | Deferred → playthrough1 |
| 8 | GraveStone obituary item unwanted | Deferred → requires generated `gravestone-common.toml`; disable after first run |
| 9 | Zoom (Z) and Dodge Roll (Z) conflict | **Fixed** — Better Combat dodge rebound to R in `defaultoptions/options.txt` |
| 10 | Need searchable keybinds | **Fixed** — added Controlling mod |
| 11 | VeinMiner no "shapeless" mode | Deferred → playthrough1; needs generated config to extend ore block list |
| 12 | Despawn Tweaks — hard to test | Deferred → playthrough1 |
| 13 | AttributeFix — no obvious issue | Deferred → playthrough1 |
| 14 | Memory at 75–90% of 8GB | Noted above (GC-driven range, expected) |
| 15 | Polymorph — keep an eye on it | Deferred → playthrough1 |
| 16 | RightClickHarvest not working | **Fixed** — mod was `side = "server"`; corrected to `both` |
| 17 | Tropicraft cocktail not in JEI | **Fixed** — `tropicraft:cocktail` in `ignored_items`; verify in playthrough |
| 18 | Naturally Trimmed — hard to test SP | Deferred → playthrough1 |
| 19 | Trimmable Tools — no visual difference | **Expected** — trims on tools are subtle; recipes confirmed working |
| 20 | Traveler's Titles — dimension change only | Deferred → requires generated config; disable biome titles after first run |
