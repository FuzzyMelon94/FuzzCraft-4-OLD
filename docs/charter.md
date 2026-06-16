# FuzzCraft — Project Charter
**Author:** FuzzyMelon94  
**Working Title:** FuzzCraft  
**Status:** Active — Pre-Production  
**Last Updated:** 2026-06-14  
---
## 1. Vision
FuzzCraft is a personal, long-term modpack for a casual friend group of ~7 players. It is designed to be a "forever pack" — something that grows and evolves over time rather than a fixed, versioned release. The north star is **FTB Ultimate**: everyone can do their own thing, pursue their own progression, and then rally together for group adventures and boss nights.
The pack leans toward **tech and automation** as its primary pillar, with magic, exploration, and adventure as strong secondary pillars. It is not a competitive or balance-focused pack — if something is overpowered and fun, it's in. Tweaks happen in config, not by exclusion.
---
## 2. Technical Foundation
| Property | Decision | Notes |
|---|---|---|
| **Loader** | NeoForge (preferred) | Fabric acceptable where NeoForge coverage is weak |
| **Minecraft Version** | 1.21.1 (target) | Not locked — version bumps permitted as ecosystem matures |
| **Java Version** | 21+ | Hard minimum |
| **Server Hardware** | HP Mini PC (home network) | Runs via Pterodactyl + Wings on Ubuntu Server |
| **Server Overhead** | Low-stakes background operation | Should run alongside other servers; shut down when resources needed |
| **Distribution** | Modrinth (primary target) | CurseForge as fallback; packwiz supports both |
| **Pack Toolchain** | [packwiz](https://packwiz.infra.link) | Used in FuzzCraft-3, carries forward — handles mod versioning, Modrinth/CF sourcing, bootstrap workflow |
| **Player Updates** | packwiz bootstrap (pre-launch command) | Tested on ATLauncher and Prism Launcher; bootstrap jar + GitHub Pages to serve `pack.toml` |
| **Version Control** | Git repository | Configs, manifests, datapacks, docs all tracked |
| **Prior Reference** | FuzzCraft-3 repo | NeoForge `21.1.209` on 1.21.1 — useful reference, not a constraint |
### Repo Structure
```
fuzzcraft/
├── docs/               # Charter, batch logs, issue log
├── mods/               # packwiz mod manifests (auto-managed)
├── config/             # Server & client configs
├── kubejs/             # Compat/scripting mod, added when needed
├── datapacks/          # Custom datapacks
├── resourcepacks/      # Bundled resource packs
├── shaderpacks/        # Bundled shader packs
├── pack.toml           # packwiz pack definition
├── index.toml          # packwiz index (auto-managed)
└── README.md
```
### Player Setup (packwiz bootstrap)
Players download `packwiz-installer-bootstrap.jar` once and add a pre-launch command to their instance. The launcher fetches and syncs the latest pack on every launch automatically.
**Pre-launch command (ATLauncher & Prism):**
```
"$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://fuzzymelon94.github.io/FuzzCraft-4/pack.toml
```
### Development Workflow
```bash
packwiz serve                        # Local dev server for testing
packwiz mr add [URL|name]            # Add mod from Modrinth
packwiz cf add [URL|name]            # Add mod from CurseForge
packwiz update --all                 # Update all mods
```
---
## 3. Design Principles
- **No progression gates.** Quests guide and reward — they never lock content.
- **Casual-first balance.** Overpowered mods are fine. If the group doesn't like something, it gets disabled or ignored — not excluded upfront.
- **Config over removal.** Problems are solved by tweaking configs before reaching for mod removal. Deferred config and recipe work is tracked in `docs/configs.md` for the final QoL pass.
- **Compat mod available.** A core compat/scripting mod (e.g. KubeJS) will be added when cross-mod work is needed. Custom recipes, loot tweaks, and datapack work are all in scope.
- **Storage-conscious world gen.** Chunk pregeneration is player-centred (base radius only), not world-border blasts. Storage impact on the host machine is a real constraint.
- **Batched, tested additions.** Mods are added in batches. Each batch must be stable and launchable before the next begins.
---
## 4. Pack Categories & Mod Direction
### Batch 1 — Foundation *(start here)*
Performance, compatibility, essential QoL, and chunk management. The goal is a clean, launchable instance before any content mods are added.
- Performance: Embeddium / Sodium-adjacent, memory fixes, crash reporting
- Chunk loading: FTB Chunks (claim + forceload)
- Chunk pregen: Chunky + Chunky Offline — player-centred radius jobs, run during idle
- Essential QoL: minimap, inventory sorting, recipe viewer (JEI/REI)
- Misc utilities: WTHIT / Jade (block info), basic lighting fixes
### Batch 2 — Tech & Automation
The primary content pillar. Should feel complete as a standalone tech experience.
- **Create** — core automation, contraptions, trains
- **Immersive Engineering** — multiblock tech, wiring, power
- **ComputerCraft (CC: Tweaked)** — turtles, automation scripting *(specifically requested)*
- **Tools & Weapons:** Tinker's Construct + Tetra as the target pair — both offer modular/upgradable tools with different philosophies and complement each other well. If either isn't stable at batch time, evaluate alternatives with the same vibe (modular tools, material progression, unbreakable-but-upgradable)
- **Storage:** Applied Energistics 2 (AE2) as primary; Storage Drawers as visual complement *(pencilled in — monitor FPS impact)*
- **Backpacks:** Sophisticated Backpacks (primary); Traveller's Backpack (alternative/companion)
- Supporting tech mods to be confirmed during batch
### Batch 3 — Magic & Farming
Non-tech players get a full gameplay loop.
- **Botania** — confirmed
- **Ars Nouveau** — confirmed
- **Thaumcraft successor** — Thaumcraft itself is abandoned; candidates include *Theurgy*, *Arcane* mods, or equivalent. To be evaluated during batch.
- **Farmer's Delight** — confirmed, plus food ecosystem addons
- Supporting magic and food mods to be confirmed during batch
### Batch 4 — World Gen & Combat
Overworld exploration layer. Biomes, terrain, structures, mob variety, and combat depth.
**World gen:**
- Terralith + Tectonic (terrain/biome overhaul)
- Oh The Biomes We've Gone (BYG) — replaces BoP
- Dynamic Trees + Terralith/BYG compat (DT-Terralith 1.3.0, DT-BWG 1.1.0)
- BetterNether NeoForge (Nether biomes/structures)
**End gen:**
- Nullscape + BetterEnd NeoForge + YUNG's Better End Island
**Structures:**
- Full YUNG's suite (Dungeons, Mineshafts, Strongholds, Desert Temples, Jungle Temples, Ocean Monuments, Nether Fortresses, Witch Huts, End Island, Bridges)
- ChoiceTheorem's Overhauled Village (CTOV) + Farmer's Delight / Savage & Ravage / Friends & Foes compat datapacks
- Towns and Towers, Dungeons and Taverns, When Dungeons Arise
- Blossom Blade, Tidal Towns, Better Archeology
- Sparse Structures (density control)
**Mobs & combat:**
- Alex's Mobs, Friends & Foes, Born in Chaos, Galosphere, Ribbits
- Savage & Ravage (pack AI + champion mobs — config pass planned)
- Artifacts (Curios-based trinkets), Epic Knights + Addon, Waystones
- Bountiful (bounty boards)
- Curios slot config pass: 2× back, 4× ring, 4× charm minimum *(deferred to B7)*
### Batch 5 — Dimensions
Group adventure content. Dimensions are a primary social driver — "adventure nights" are a core use case.
**Adventure dimensions:**
- **Twilight Forest** — confirmed
- 2–3 additional adventure dimensions (candidates: Aether, Blue Skies, The Undergarden, Regions Unexplored)
- Each dimension should have enough content to generate or support a questline
**Utility dimensions:**
- Personal/pocket dimensions (upgradable)
- Configurable mining dimension
### Batch 6 — Building, Decoration & Questing
Polish layer. Decoration mods for the builders in the group, and FTB Quests to tie the whole pack together.
- Decoration mods (to be confirmed with friend group input)
- **FTB Quests** — no gating, structured as:
  - Per-major-mod questlines (Create, IE, Botania, Ars Nouveau, Twilight Forest, etc.)
  - Grouped tutorial quests for smaller mods where they fit sensibly
  - Standalone mod introductions where grouping doesn't make sense
- Deferred food/storage addons: Crate Delight, Storage Delight, [Let's Do] Beachparty
### Batch 7 — QoL & Final Compat Pass
Final polish pass once all content is in. No new content mods — focus on quality of life, cross-mod compat smoothing, and config work deferred from earlier batches.
- QoL mods (RightClickHarvest, Torch Master, Particle Effects, etc. — tracked in watchlist)
- Curios slot config pass: 2× back, 4× ring, 4× charm minimum (deferred from B4)
- Recipe and compat pass: review configs.md deferred items, KubeJS custom recipes where needed
- **KubeJS difficulty scaling** — listen for vanilla advancements (e.g. "Suit Up", "Diamonds!") and ramp up mob difficulty mods (Legendary Monsters rarity, Mutant Monsters spawn rates) progressively. Replaces manual config bumping.
- Review watchlisted mods for ports (Botania, Tinkers', Thermal, Alex's Mobs, Savage & Ravage, etc.)
- Final review of Almost Unified, tag unification, and JEI display cleanup
---
## 5. Questing Philosophy
Quests serve as a **guided tutorial and reward system**, not a progression gate. Specifically:
- Nothing is locked behind quest completion
- Major mods (Create, IE, Botania, Ars Nouveau, TF, AE2, CC) get their own dedicated questlines
- Smaller mods are grouped by theme where sensible, or given standalone intro quests
- Quest rewards should feel meaningful but not mandatory
- New players should be able to pick up the pack and understand what to work toward without needing external wikis
---
## 6. Chunk Management Strategy
- **FTB Chunks** handles claiming and forceloading per-player
- **Chunky** handles pregeneration — jobs are targeted at player base coordinates, not a world border
- Default pregen radius: ~300–500 blocks around each claimed base area (storage-conscious)
- Pregen jobs run during server idle time (Chunky Offline / scheduled)
- New player onboarding includes a Chunky job for their base as a standard step
- World size is monitored — no automatic large-radius generation
---
## 7. Batch Progress Tracker
| Batch | Name | Status | Notes |
|---|---|---|---|
| 1 | Foundation | ✅ Complete | 23 mods (v0.1.2). Iris+Sodium 0.6.13; FTB Chunks FORCED_ALL; JourneyMap Integration for chunk overlay; Default Options (sprint/sneak swap, no bobbing); Balm. SP+server tested 2026-06-11. jmi-client.toml colours to be tuned later. |
| 2 | Tech & Automation | ✅ Complete | ~65 mods (v0.2.1–0.2.4). Create + IE + CC + AE2 + full companion suite. Removed Create: Liquid Fuel (redundant — C&A Straw covers blaze burner fluid input). Shader shadow artefacts on contraptions logged (known Iris/Create limitation). SP tested 2026-06-12. Server test to follow post-merge. |
| 3 | Magic & Farming | ✅ Complete | ~47 mods (v0.3.1–0.3.3). Ars Nouveau + addons, Theurgy, Neo Vitae (experimental), Botania watchlisted (no 1.21.1 port). Full food ecosystem: FD + Pam's suite + Let's Do series + Botany Pots + Mystical Agriculture. Fishing: Aquaculture + Lava Fishing. Create integrations throughout. Removed: Sodium Dynamic Lights (module conflict), Compat Delight (broken against FD 1.3.x). Added Spark profiler. Caramel recipe gap in Create Confectionery deferred to B6. SP tested 2026-06-13. Server test to follow post-merge. |
| 4 | World Gen & Combat | ✅ Complete | ~55 mods (v0.4.5–0.4.27). Terralith 2.5.8 pinned (2.6.x feature order cycle with BWG 2.6.0). Full world gen: BYG, Tectonic, Dynamic Trees + compat, BetterNether (unofficial port), Nullscape, BetterEnd, YUNG's full suite, CTOV + compat datapacks, WDA, DaT, Blossom Blade, Tidal Towns, Better Archeology, Sparse Structures. Mob/combat: Born in Chaos, Galosphere, Ribbits, Critters & Companions, Creeper/Golem/Enderman Overhaul, Nyf's Spiders, Guard Villagers, Legendary Monsters, Mutant Monsters, Rotten Creatures, Epic Knights + Addon, Artifacts, Better Combat, Waystones, Bountiful, Lootr, In Control!, EMF+ETF+Fresh Animations. Hybrid Aquatic removed — Lithostitched "inline definitions" incompatibility (world create crash); watchlisted for future port. Upgrade Aquatic retained for aquatic coverage. Difficulty/feel deferred to first real playthrough (docs/testing/playthrough1.md). SP tested 2026-06-14–2026-06-15. Server test to follow post-merge. |
| 5a | Dimensions — Flagship + Bosses + Utility | 🔄 In Progress | TF, Dimensional Dungeons, BOMD, Bosses Rise, Dimensional Pockets II, Supernova's Mining Dimension. Branch: batch/5a-twilight-bosses-utility |
| 5b | Dimensions — Aether Cluster | ⬜ Not started | Aether + Deep Aether + Aether Villages + Aether's Delight + Paradise Lost. Awaiting B5a |
| 5c | Dimensions — Underground & Quirky | ⬜ Not started | Undergarden, Deeper and Darker, The Bumblezone. Awaiting B5b |
| 6 | Building & Questing | ⬜ Not started | Awaiting Batch 5 |
| 7 | QoL & Final Compat | ⬜ Not started | Awaiting Batch 6 |
---
## 8. Issue & Debug Log
*Issues are logged here as they arise across all batches. Format: date, batch, description, resolution.*
| Date | Batch | Issue | Resolution |
|---|---|---|---|
| 2026-06-11 | 1 | Oculus (NeoForge shader mod) has no builds past 1.20.1 | Switched to Iris Shaders, which is now officially multiloader with NeoForge 1.21.1 support. Iris requires Sodium; swapped Embeddium for Sodium (NeoForge alpha builds). Sodium alpha is considered stable in practice — players can substitute Embeddium client-side if needed. |
| 2026-06-11 | 1 | Sodium 0.8.x (Ruby rewrite) incompatible with Iris and Sodium ecosystem mods | Sodium 0.8.12-alpha.4 caused mixin crashes in Reese's Sodium Options, SodiumOptionsAPI, and Iris. Iris 1.8.12 pins Sodium 0.6.13. Downgraded Sodium to 0.6.13 (latest stable NeoForge build); removed Reese's + SodiumOptionsAPI (not yet ported to 0.6.x-compatible API either). Re-evaluate when Iris supports 0.8.x. |
| 2026-06-11 | 1 | No FTB Chunks + JourneyMap integration addon available for 1.21.1 | Resolved: JourneyMap Integration (modrinth: M1ZKbfkJ) covers FTB Chunks claim overlay on JourneyMap. Added v1.21.1-1.9 in v0.1.1. |
| 2026-06-12 | 2 | Moving Create contraptions show shadow artefacts when a shaderpack is active (Iris + Create interaction) | Known engine limitation — Create contraptions are rendered as entities, which causes shadow mis-alignment in most shaderpacks. Create Better FPS reduces it but doesn't eliminate it. No fix available; revisit if a Create/Iris update addresses contraption rendering. |
| 2026-06-13 | 3 | Crash on launch — `lambdynlights_api` (bundled by Ars Nouveau JarInJar) and `sodiumdynamiclights` (standalone mod) both export `dev.lambdaurora.lambdynlights.api`, causing Java module resolution failure | Removed Sodium Dynamic Lights from the pack. LambDynamicLights API remains available via Ars Nouveau's bundled dep. |
| 2026-06-13 | 3 | Crash on launch — Compat Delight 1.0.1.1 references `vectorwing.farmersdelight.common.block.ShepherdsPieBlock` which was removed in Farmer's Delight 1.3.x, causing `NoClassDefFoundError` | Removed Compat Delight. FD compat covered by Slice & Dice and Farmer's Delight: Extended. |
| 2026-06-13 | 3 | Create Confectionery caramel has a circular recipe (Caramel ↔ Caramel Bucket ↔ Bar of Caramel, no entry point). Non-blocker. Pam's HarvestCraft also has a `Caramel` item — a KubeJS recipe bridging Pam's caramel into Create Confectionery's caramel fluid may resolve this. | Deferred to B6 compat pass. |
| 2026-06-14 | 4 | Feature order cycle crash on world gen — `IllegalStateException: Feature order cycle found` involving vanilla, Terralith, and BYG biomes. Root cause was Terralith 2.6.2 + BWG 2.6.0 incompatibility (not Dynamic Trees as initially suspected). Feature Recycler did not resolve it. | Downgraded Terralith to 2.5.8 at v0.4.4. Do not update Terralith until 2.6.x + BWG 2.6.x is confirmed compatible. DT re-added at v0.4.5 with dtbwg upgraded BETA02 → 1.1.0. |
| 2026-06-14 | 4 | BYG and BetterNether saplings incompatible with Dynamic Trees. | No compat addon exists for BetterNether; dtbwg does not cover all BWG tree types. Known gap — deferred, no fix available. |
| 2026-06-15 | 4 | Hybrid Aquatic 1.5.5 uses Lithostitched "inline definitions" format — worldgen modifier JSONs (e.g. `hybrid-aquatic:lithostitched/worldgen_modifier/deeper_deep_oceans.json`) cause `IllegalStateException: Inline definitions not allowed here` on world create. Affects all Lithostitched versions tested (1.6.8 and 1.7.10+beta3). | Removed Hybrid Aquatic. Watchlisted — re-add when HA updates to use standard Lithostitched format. Lithostitched restored to 1.7.10+beta3. Upgrade Aquatic + Critters & Companions provide aquatic coverage in the interim. |
| 2026-06-15 | 4 | packwiz bootstrapper cache (`packwiz.json`) had stale `onlyOtherSide: true` for Lithostitched from when it was `side = "server"` — mod wouldn't download to client despite pw.toml being fixed. | Delete `packwiz.json` from the instance to force a full re-sync. Bootstrapper also unreliable at removing mods — manual jar deletion needed when a mod is removed from the pack. Must restart `packwiz serve` after removing a mod so the in-memory index updates. |
| 2026-06-16 | 5a | Twilight Forest trees are not compatible with Dynamic Trees — TF trees generate as vanilla static trees inside the TF dimension rather than DT dynamic trees. | Known limitation — no DT compat addon exists for TF. Non-blocking; both mods work correctly in their own domains. |
---
## 9. Handoff Protocol
Each batch is implemented in its own conversation using a handoff doc generated from this charter. The handoff doc contains:
- Relevant sections of this charter
- Specific mod list for the batch (to be confirmed)
- Any known compat concerns going in
- Success criteria (pack launches, no crashes, core features functional)
On completion, the batch conversation produces a summary that is folded back into this charter (progress tracker + issue log updated).
**Workflow:**
```
Charter (this doc) → Batch Handoff Doc → Implementation Chat → Summary → Charter updated
```
---
*FuzzCraft is a personal project by FuzzyMelon94. Not affiliated with any modpack platform or mod author.*
