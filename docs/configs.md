# FuzzCraft 4 — Config notes

Some notes regarding the configs of various mods as I work through the testing and spot things that might need attention.

## Additions
Some mods I think would be good to add, for optimisation, performance, QoL, and so on.

- [Collapsible Groups](https://www.curseforge.com/minecraft/mc-mods/collapsible-groups) - **Added 0.7.1 (CurseForge).** No Modrinth equivalent exists; CurseForge-only.

### To be added to B7 (wave 2 — QoL pass)

All confirmed NeoForge 1.21.1 compatible. Add via `packwiz mr add <slug> -y` unless noted.

**Performance & Client Polish**
- [Dynamic FPS](https://modrinth.com/mod/dynamic-fps)
- [More Culling](https://modrinth.com/mod/moreculling)
- [Sound Physics Remastered](https://modrinth.com/mod/sound-physics-remastered)
- [Model Gap Fix](https://modrinth.com/mod/modelfix)
- [Better Beds](https://modrinth.com/mod/better-beds)
- [Log Begone](https://modrinth.com/mod/log-begone)
- [Chunks Fade In](https://modrinth.com/mod/chunks-fade-in)
- [Remove Reloading Screen](https://modrinth.com/mod/rrls)
- [Chat Animation](https://modrinth.com/mod/chatanimation)

**HUD & Tooltips**
- [BetterF3](https://modrinth.com/mod/betterf3)
- [Overflowing Bars](https://modrinth.com/mod/overflowing-bars)
- [Durability Tooltip](https://modrinth.com/mod/durability-tooltip)
- [Equipment Compare](https://modrinth.com/mod/equipment-compare)
- [Enhanced Attack Indicator](https://modrinth.com/mod/enhanced-attack-indicator) — disable food, item cooldown, sleep progress, and fullness indicators in config
- [Legendary Tooltips](https://modrinth.com/mod/legendary-tooltips)
- [Enchantment Descriptions](https://modrinth.com/mod/enchantment-descriptions)
- [Better Advancements](https://modrinth.com/mod/better-advancements)
- [Advancement Plaques](https://modrinth.com/mod/advancement-plaques)
- [Better ModList](https://modrinth.com/mod/better-modlist) — standalone, does not require Synitra

**Navigation & World**
- [Nature's Compass](https://modrinth.com/mod/natures-compass)
- [Explorer's Compass](https://modrinth.com/mod/explorers-compass)
- [Traveler's Titles](https://modrinth.com/mod/travelers-titles)
- [Nether Portal Fix](https://modrinth.com/mod/netherportalfix)

**Inventory & Crafting**
- [Crafting Tweaks](https://modrinth.com/mod/crafting-tweaks)
- [TrashSlot](https://modrinth.com/mod/trashslot)
- [Stack Refill](https://modrinth.com/mod/stack-refill)
- [Visual Workbench](https://modrinth.com/mod/visual-workbench)
- [Easy Magic](https://modrinth.com/mod/easy-magic)
- [KleeSlabs](https://modrinth.com/mod/kleeslabs)
- [Trade Cycling](https://modrinth.com/mod/trade-cycling)
- [Easy Villagers](https://modrinth.com/mod/easy-villagers)
- [Carry On](https://modrinth.com/mod/carry-on) — **do NOT blacklist spawners** (intentional: players can relocate spawners for mob farms)

**Gameplay QoL**
- [Double Doors](https://modrinth.com/mod/double-doors)
- [Jump Over Fences](https://modrinth.com/mod/jump-over-fences)
- [Bridging Mod](https://modrinth.com/mod/bridging-mod)
- [SwingThrough](https://modrinth.com/mod/swingthrough)
- [Monsters in the Closet](https://modrinth.com/mod/monsters-in-the-closet)
- [Zume](https://modrinth.com/mod/zume) — scroll-wheel zoom multiplier confirmed supported
- [VeinMiner](https://modrinth.com/mod/veinminer) — use the **mod** version (not the datapack); pairs with VeinMiner Hotkey below
- [VeinMiner Hotkey](https://modrinth.com/mod/veinminer-client) — client-side companion to VeinMiner mod
- [Crops Love Rain](https://modrinth.com/mod/crops-love-rain)
- [Despawn Tweaks](https://modrinth.com/mod/despawn-tweaks)
- [GraveStone Mod](https://modrinth.com/mod/gravestone-mod)
- [Polymorph](https://modrinth.com/mod/polymorph) — not redundant with AU; AU unifies item identity, Polymorph resolves recipe conflicts
- [Bow Infinity Fix](https://modrinth.com/mod/bow-infinity-fix)
- [Better Days](https://modrinth.com/mod/betterdays) — configure: `daySpeed=0.5`, `nightSpeed=1.0` (days 2× longer than vanilla, nights vanilla length, ~67% day fraction)

**System / Compat**
- [No Chat Reports](https://modrinth.com/mod/no-chat-reports)
- [AttributeFix](https://modrinth.com/mod/attributefix)
- [Yeetus Experimentus](https://modrinth.com/mod/yeetus-experimentus)
- [Create: Power Loader](https://modrinth.com/mod/create-power-loader) — FTB Chunks covers forceloading; this adds a Create-themed alternative

**Cosmetic / Social**
- [Emoji Type](https://modrinth.com/mod/emoji-type)
- [Scribble](https://modrinth.com/mod/scribble)
- [Yung's Menu Tweaks](https://modrinth.com/mod/yungs-menu-tweaks)

**Skipped (decided against):**
- Mouse Tweaks — already in pack (B1)
- Particle Effects — already added B7 (0.7.1)
- Max Health Fix — redundant; AttributeFix + Overflowing Bars covers this


### To be added to B8
- [FancyMenu](https://modrinth.com/mod/fancymenu)
- [Drippy Loading Screen](https://modrinth.com/mod/drippy-loading-screen)



## Memory — JVM & Pack-level Notes

Pack was running at ~16GB heap usage during B6 testing (16GB max allocation, GC clears 4-5GB before hitting limit). This is a GC pressure issue, not a true leak — the heap grows large before G1GC triggers.

**Recommendation: lower max heap to 8–10GB in Prism.**
- FerriteCore, ModernFix, EntityCulling, and ImmediatelyFast are already in the pack — these cover the main memory-reduction vectors at the pack level.
- 16GB gives G1GC too much room to defer collection. At 8–10GB it collects more aggressively and average RSS stays lower.
- In Prism: Instance → Settings → Java → override memory → 8192 MB (or 10240 MB if 8 feels too tight in established worlds).
- If GC pauses become noticeable, add these JVM args: `-XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1`
- In established worlds with many loaded chunks, 10GB is the safer cap.

No pack-level config changes needed — memory profile is already well-managed by existing performance mods.


## Mods

### Bosses of Mass Destruction
- No in-game guidebook — boss trigger mechanics are not obvious to new players
- B8 quest pass: BOMD needs dedicated quest coverage explaining how to locate and trigger each boss (locator items, structure hunting, etc.)

### RFTools Dimensions
- No return travel device is placed in the created dimension — players entering a new RFTools dimension have no built-in way back
- B8 quest pass: when the player first crafts a Matter Transmitter, reward them with a charged Porter bound to a Matter Receiver in their base so they always have an escape route

### Almost Unified — Tropicraft Cocktail
- AU tag unification causes JEI to show Pam's HarvestCraft Pina Colada as the output for the Tropicraft cocktail recipe
- **Fixed in B7:** `"tropicraft:cocktail"` added to `ignored_items` in `config/almostunified/unification/materials.json`. Full AU config set committed to repo.
- The portal mechanic works correctly with the crafted item; this was a JEI display issue.

### Almost Unified — Full Tag Review
- Run a full JEI audit pass during B7 testing — check for any other AU unifications that produce wrong outputs
- Focus areas: Pam's items (many similar-named items to modded equivalents), Tropicraft (above), Ars Nouveau (mana items), Create (fluid handling)
- Document any additional `ignoredItems` entries needed alongside the cocktail fix above

### Create Mechanical Extruder
- Balance default recipes
- Add recipes for all the resources Create requires
- Consider adding recipes for other modded resources
- **Deferred to B8** — requires KubeJS; adding KubeJS is planned for B8 alongside difficulty scaling

### KubeJS — Deferred to B8
Three items require KubeJS, all deferred:
1. **Caramel recipe bridge** — Pam's `caramel` item → Create Confectionery caramel fluid (resolves circular recipe issue logged in B3)
2. **Create Mechanical Extruder recipe pass** (see above)
3. **Difficulty scaling** — listen for vanilla advancements (Suit Up, Diamonds!, etc.) and ramp Legendary Monsters rarity + Mutant Monsters spawn rates progressively
