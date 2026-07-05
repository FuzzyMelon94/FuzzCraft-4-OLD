# FuzzCraft 4 — Post-Mortem

**Author:** FuzzyMelon94
**Pack period:** June–July 2026
**Final version:** 0.8.6
**Outcome:** Archived — pack grew beyond playable scope for available hardware and team size

---

## What FC4 Was

FuzzCraft 4 was an attempt to build a "forever pack" in the spirit of FTB Ultimate — a kitchen-sink modpack for a casual friend group of ~7 players, covering tech, magic, exploration, dimensions, combat, building, and decoration, with full questing to tie it together.

It was built on 1.21.1 NeoForge using packwiz, distributed via GitHub Pages, with a home-network HP Mini PC (i5-8600, 32GB RAM) as the server.

---

## What Was Built

| Batch | Content | Mods added |
|---|---|---|
| 1 | Foundation — performance, QoL, chunk management | ~23 |
| 2 | Tech — Create, IE, CC, AE2, storage, backpacks | ~65 |
| 3 | Magic & Farming — Ars Nouveau, Theurgy, full food ecosystem | ~47 |
| 4 | World Gen & Combat — full biome/structure/mob suite | ~55 |
| 5a–5c | Dimensions — TF, Aether, Undergarden, Tropicraft, Stellaris, etc. | ~35 |
| 6 | Building & Decoration — Macaw's suite, Supplementaries, etc. | ~35 |
| 7 | QoL & Compat — 50+ small mods, config pass | ~51 |
| 8 | QoL Extras — ToastBegone, NERB, Distant Horizons | ~5 |
| Reduction Round 1 | Performance trim — 10 mods removed, 6 added | -4 net |

**Peak mod count:** ~190 mods. Post-reduction: ~175 mods.

Batches 1–8 and Reduction Round 1 were all completed and SP tested. Multiplayer testing was deferred each batch and never happened. Questing (Batch 8 proper) was never reached.

---

## What Worked

**The batching process** was solid. Adding mods in discrete, tested batches meant issues were isolated and traceable. Every crash was diagnosable because the delta between versions was small.

**The issues system** (`docs/issues/`) worked well for tracking multi-session bugs. The template and naming convention made it easy to find history and know what was tried.

**The testing doc format** (per-batch SP logs + multiplayer.md) gave a clear picture of what had and hadn't been verified at any point.

**packwiz + GitHub Pages** as the distribution mechanism was painless once configured. The bootstrap workflow was transparent to players.

**Config-over-removal as a principle** was the right call. Most problems were solvable without removing mods, and the issues log demonstrates that.

---

## What Didn't Work

**Scope without a budget.** The pack was designed as a wish list with no cap. Each batch added 20–60 mods before asking whether the hardware could handle the combination. By the time the question was asked, the answer was "not really" — and trimming was painful.

**Hardware constraints treated as soft.** The server specs (i5-8600, 10GB RAM budget) were documented but never enforced as a design constraint. Mods were added based on "is this fun?" not "does this fit the hardware?" Reduction Round 1 was the consequence — removing mods that should never have been added.

**Too many pillars.** FC4 tried to cover tech, magic, exploration, combat, building, decoration, and dimensions simultaneously. Each pillar added compat surface area, config work, and server load. A pack that does everything well requires a team. A solo-built pack should pick 2–3 pillars and do them properly.

**Multiplayer testing never happened.** Every batch deferred server testing to "after merge." It was always deferred again. The pack was never validated in the actual play context.

**Questing was an afterthought.** Batching quests to the end meant they were never designed in — cross-mod quest hooks, reward philosophy, and tutorial structure were never considered during mod selection. When the pack became unplayable before questing was reached, there was nothing to show for it.

**Dynamic Trees was a mistake.** Added for visual flair, it caused compat gaps with every dimension mod (TF, Aether, BYG), had no addon for half the modlist, and contributed to server tick overhead. The partial coverage made it worse than nothing. Removed in Reduction Round 1.

**Distant Horizons was a mistake.** Client-only, but caused RAM pressure that forced the 6–8GB recommendation. Removed in Reduction Round 1.

---

## Key Lessons

1. **Constraints first, wish list second.** Define the hardware budget, client RAM cap, and mod count target *before* touching a mod manifest. Every addition is measured against the budget, not added to it.

2. **Two pillars maximum for a solo-built pack.** Pick them explicitly. Everything else — food, combat, decoration — is a supporting layer, not a pillar. Supporting layers get one or two mods, not suites.

3. **If it'll need a full questline to be worth including, plan for it upfront.** Don't add mods that require significant quest work and then defer the quest work indefinitely.

4. **Performance-test with all pillars running together before adding more.** Don't wait until 170 mods to ask whether the server can handle it.

5. **Multiplayer test each batch, not "after merge."** The whole point of the pack is multiplayer. If it can't be tested that way, it shouldn't be considered done.

6. **Dynamic Trees-style "nice to have with partial coverage" mods are rarely worth it.** If a mod needs compat addons for half the modlist and those addons don't exist, it's a liability not an asset.

7. **The process was good. The scope was the problem.** Batching, issues tracking, testing docs, packwiz workflow — all carry forward. Apply them to a smaller, better-constrained pack.

---

## What Carries Forward to FC4 (New Attempt)

- Batch workflow (branch → bump → add → test → merge)
- Issues system and file naming convention
- Testing doc format
- packwiz + GitHub Pages distribution
- CLAUDE.md structure and instructions
- Core tool selections: JourneyMap, EMI, FTB Chunks, Chunky, Sophisticated Backpacks

---

*FuzzCraft 4 was a useful lesson in modpack scope management. The successor pack takes its design constraints from what was learned here.*
