# FuzzCraft 4 — Config notes

Some notes regarding the configs of various mods as I work through the testing and spot things that might need attention.

## Additions
Some mods I think would be good to add, for optimisation, performance, QoL, and so on.

- [Collapsible Groups](https://www.curseforge.com/minecraft/mc-mods/collapsible-groups) - **Added 0.7.1 (CurseForge).** No Modrinth equivalent exists; CurseForge-only.


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
