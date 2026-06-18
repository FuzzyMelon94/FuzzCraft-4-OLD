# FuzzCraft 4 — Playthrough 1 Testing

Deferred items from SP batch testing that are better validated during an actual playthrough, require multiplayer, or need generated configs first.

## Summary
**Pack version:** (fill in on start)
**Start date:** (fill in)
**Tester:** FuzzyMelon94
**Play mode:** Multiplayer server

---

## Configs to Apply Before Starting

These mods generate config files on first launch that need to be tuned before the playthrough begins properly. Collect the generated files after first run and adjust:

- **GraveStone** (`config/gravestone-common.toml`) — disable the obituary item given to player on death; there's already a waypoint marker so it's redundant
- **Traveler's Titles** (`config/TravelersTitles-client.toml` or similar) — disable biome titles, keep dimension titles only
- **VeinMiner** (`config/veinminer-server.toml` or similar) — extend the block/ore list using ore tags so it works on modded ores, not just vanilla

---

## Known Outstanding Issues

- **Zoom (Z) / Dodge Roll** — rebound Dodge Roll to R by default; players can remap in Controls if needed
- **Caramel circular recipe** — still present; deferred to B8 KubeJS fix
- **BOMD and RFTools questing** — deferred to B8
- **RightClickHarvest / Double Doors** — side fix applied in B7b; confirm both work in server play
- **Recipes unlocked popup** — no config toggle found; note if it becomes annoying enough to warrant a mod

---

## 1. Performance & Stability

- [ ] Note any lag spikes during chunk loading/traversal — suspected server CPU bottleneck; track frequency and severity
- [ ] Memory stays manageable over a long session — B7 SP testing showed 75–90% of 8GB; check if it climbs further

---

## 2. Mods to Verify In Play

### Navigation
- [ ] Traveler's Titles — walk into a new biome; confirm biome title shows (or is suppressed if config applied); confirm dimension title shows on Nether/End entry
- [ ] Nature's Compass — craft and use; confirm biome search by name works
- [ ] Explorer's Compass — craft and use; confirm structure search by name works
- [ ] Nether Portal Fix — enter Nether, build a second portal at a different location; confirm they link correctly (critical for multiplayer)

### Inventory & Crafting
- [ ] RightClickHarvest — plant a crop, grow it fully, right-click to harvest and replant; confirm partial crops are NOT harvested
- [ ] Crafting Tweaks — open crafting table; confirm rotate/balance/clear buttons are present
- [ ] Stack Refill — use up the last item in a hotbar stack; confirm auto-refills from inventory
- [ ] Easy Magic — open enchanting table; confirm option to re-roll enchantment choices
- [ ] Trade Cycling — open a villager trade UI; confirm can cycle/refresh trades
- [ ] Easy Villagers — interact with a villager; confirm simplified trade interface
- [ ] Carry On — Shift+right-click a chest or mob to pick it up and carry it
  - [ ] Confirm a spawner can be picked up and placed elsewhere

### Gameplay QoL
- [ ] Double Doors — place two adjacent doors; open one; confirm both open simultaneously (vanilla and modded doors)
- [ ] VeinMiner — hold VeinMiner hotkey while mining an ore vein; confirm connected ores break together; note if modded ores are included
- [ ] GraveStone Mod — die in any way; confirm grave spawns at death location; confirm no obituary item in inventory (if config applied)
- [ ] Despawn Tweaks — note if mobs holding items despawn correctly (vanilla holds them too long due to held item; this fixes that)
- [ ] Chunks Fade In — note if the lighting on chunk fade looks jarring; if so, look for a Chunks Fade In config to adjust
- [ ] Trample No More — jump on farmland; confirm it does NOT revert to dirt

### HUD & Tooltips
- [ ] Overflowing Bars — use a health-boosting item; confirm health bar overflows into a second row
- [ ] Enhanced Attack Indicator — check HUD is clean; configure off any intrusive indicators (food/cooldown/sleep/fullness)
- [ ] Legendary Tooltips — hover an Apotheosis-rarity item; confirm tooltip border matches rarity tier
- [ ] Enchantment Descriptions — hover an enchanted book; confirm enchantment effect is described
- [ ] Equipment Compare — hold Shift while hovering armour in a chest; confirm stat comparison appears (one overlay per equipped slot — intended behaviour)

### System / Social
- [ ] Polymorph — find two recipes with the same ingredient pattern; confirm output selector appears
- [ ] AttributeFix — check Apotheosis / Artifacts attributes don't overflow or cap oddly
- [ ] Yung's Menu Tweaks — check main menu layout is improved
- [ ] Scribble — edit a sign; confirm coloured text and formatting options work; also works in Book & Quill

---

## 3. Content to Monitor Over Time

### Mobs & Combat
- [ ] Naturally Trimmed — kill several armoured mobs (zombies, skeletons); check armour trims spawning on gear and dropping as loot
- [ ] Alex's Mobs — confirm creatures spawn in appropriate biomes; no crashes from entities or loot tables (unofficial port — monitor)

### Progression
- [ ] Tropicraft cocktail — confirm JEI shows `tropicraft:cocktail` recipe correctly (Pam's Pina Colada should no longer appear as the output)
- [ ] Curios slots — confirm 2 back / 4 ring / 4 charm slots showing for all players; equip items in each type

### Infrastructure
- [ ] Create: Power Loader — craft and use; confirm it chunk-loads the target chunk while powered
- [ ] Clumps (multiplayer) — confirm XP orbs clump correctly in a mob farm context with multiple players

---

## 4. Post-Config Verification

Items to check after the generated configs above have been applied and the pack updated:

- [ ] GraveStone — no obituary item on death; waypoint still appears
- [ ] Traveler's Titles — biome titles suppressed; dimension change title still shows
- [ ] VeinMiner — modded ore veins break correctly with the hotkey

---

## 5. Deferred Multiplayer (from B7 batch tests)

- [ ] Curios slot counts consistent for all players on the server
- [ ] Nether Portal Fix — portal linking works correctly in multiplayer
- [ ] Hybrid Aquatic re-add test — if pursuing, requires fresh world; add via `packwiz mr add hybrid-aquatic -y` and confirm no world-create crash
