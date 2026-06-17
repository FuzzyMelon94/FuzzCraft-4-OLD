# FuzzCraft 4 — Batch 7 Testing: QoL & Final Compat

## Summary
**Pack version:** 0.7.1–x.x.x
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

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

## 8. Wave 2 — QoL Mods

These mods are added in the follow-up B7b session. Test them in the same play session as the items above.

### Performance & Visual
- [ ] Dynamic FPS active — minimize the game window, confirm FPS drops significantly (mod is working)
- [ ] Sound Physics Remastered — enter a cave, confirm audio has reverb/echo effect
- [ ] Chunks Fade In — travel to unloaded area, confirm chunks fade in rather than popping
- [ ] Log Begone — open `logs/latest.log` after launch; confirm less spam vs before

### HUD & Tooltips
- [ ] Overflowing Bars — use a health-boosting item (Artifacts trinket or potion); confirm health bar overflows into a second row rather than capping
- [ ] Durability Tooltip — hover a tool with damage; confirm durability shown as number in tooltip
- [ ] Equipment Compare — hold Shift while hovering armour in a chest; confirm stat comparison overlay appears
- [ ] Enhanced Attack Indicator — open its config (or Options → Accessibility); disable food, item cooldown, sleep progress, and fullness indicators; confirm HUD is cleaner
- [ ] Legendary Tooltips — hover an Apotheosis-rarity item; confirm tooltip border reflects the rarity tier
- [ ] Enchantment Descriptions — hover an enchanted book; confirm enchantment effect is described in the tooltip
- [ ] BetterF3 — open F3; confirm debug screen is coloured and readable
- [ ] Better Advancements — open advancements screen; confirm improved UI layout
- [ ] Advancement Plaques — earn any advancement; confirm toast popup is the new styled plaque

### Navigation
- [ ] Nature's Compass — craft and use; confirm can search for a biome by name
- [ ] Explorer's Compass — craft and use; confirm can search for a structure by name
- [ ] Traveler's Titles — walk into a new biome; confirm biome name overlay appears on screen
- [ ] Nether Portal Fix — enter the Nether through a portal, build a second portal at a different location; confirm they link correctly (important for multiplayer)

### Inventory & Crafting
- [ ] Crafting Tweaks — open crafting table; confirm rotate/balance/clear buttons are present
- [ ] TrashSlot — open inventory; confirm trash slot is visible; drop an item in it
- [ ] Stack Refill — use up the last item in a stack of something in your hotbar; confirm it auto-refills from inventory
- [ ] Visual Workbench — leave items in a crafting table and walk away; confirm items are rendered on the table surface
- [ ] Easy Magic — open an enchanting table; confirm option to re-roll available enchantment options
- [ ] Trade Cycling — open a villager trade UI; confirm can cycle/refresh available trades
- [ ] Easy Villagers — interact with a villager; confirm simplified trade interface
- [ ] Carry On — Shift+right-click a chest or mob; confirm you can pick it up and carry it
  - [ ] Specifically confirm a spawner can be picked up and placed elsewhere (intentional design)

### Gameplay QoL
- [ ] Double Doors — place two adjacent doors; open one; confirm both open simultaneously
- [ ] Jump Over Fences — sprint-jump at a fence; confirm you clear it
- [ ] SwingThrough — swing at a mob through tall grass or leaves; confirm the hit registers
- [ ] Monsters in the Closet — attempt to sleep; if it fails, confirm nearby monsters are highlighted
- [ ] Zume — press the zoom key; confirm zoom activates; scroll while zoomed; confirm zoom level changes
- [ ] VeinMiner — hold the VeinMiner hotkey while mining an ore vein; confirm connected ores break together
- [ ] GraveStone Mod — die in any way; confirm a grave spawns at death location containing your items
- [ ] Polymorph — find two recipes with the same ingredient pattern (or check JEI for conflicts); confirm Polymorph output selector appears
- [ ] Better Days — confirm day/night cycle feels longer; days should be ~2× vanilla length; night shorter proportionally
- [ ] Crops Love Rain — start raining; confirm crops visibly grow faster during rain
- [ ] Despawn Tweaks — throw an item on the ground; confirm it stays longer than the vanilla 5-minute despawn

### System / Social
- [ ] No Chat Reports — join the server; confirm no chat signing warnings in console
- [ ] AttributeFix — check that modded attributes (Apotheosis, Artifacts) don't cap out or show integer overflow
- [ ] Yeetus Experimentus — create a new world with experimental features; confirm the warning screen is suppressed
- [ ] Emoji Type — in chat, type `:` and start typing an emoji name; confirm autocomplete appears
- [ ] Scribble — place a sign and edit it; confirm coloured text and formatting options are available
- [ ] KleeSlabs — place a double slab; try to break only the top or bottom half; confirm it works
- [ ] Yung's Menu Tweaks — check main menu layout is improved (singleplayer/server buttons rearranged)
- [ ] Create: Power Loader — craft a Power Loader; confirm it chunk-loads the target chunk while powered

## 9. Deferred — Requires Server / Multiplayer

- Verify Curios slot counts are consistent for all players on a server
- Test Clumps XP behaviour in a multiplayer mob farm context
- BOMD and RFTools questing (deferred to B8)
- Hybrid Aquatic re-add test (if pursuing — requires fresh world creation on server to confirm no crash)

## Tester Notes
<!-- Broken things, surprises, feedback -->
