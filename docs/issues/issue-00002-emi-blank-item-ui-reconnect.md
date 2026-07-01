---
id: "00002"
status: issue
title: "EMI item UI blank on every reconnect after first join"
date_opened: "2026-06-29"
date_resolved: ""
affects: client
pack_version_opened: "0.7.4"
pack_version_resolved: ""
---

## Summary

On server reconnect (disconnect + rejoin in the same session), the entire client GUI goes blank — EMI's item panel, vanilla creative inventory items, and HUD overlay icons (JourneyMap, gamemode buttons) all go invisible. UI elements are still interactable: clicking EMI's blank sidebar by position opens the recipe viewer with items visible inside. First join is unaffected. Confirmed 100% reproducible on every reconnect.

**Origin:** First noticed after the JEI → EMI swap (batch 7), but this was also the first time server testing was done. The bug may originate from any earlier batch — all prior testing was single-player only. Batch bisect is required to locate the batch that introduced it.

---

## Symptoms

- On first join: everything renders correctly; EMI populates over ~30 seconds
- On every subsequent join (disconnect + rejoin): EMI panel, vanilla creative inventory items, and HUD icons (minimap controls, gamemode buttons, etc.) all go blank immediately
- UI remains interactable — clicking EMI sidebar by position opens recipe viewer with items visible inside it
- Items do NOT reappear after EMI finishes its reconnect reload (~24s), even after waiting 2+ minutes
- Confirming: this is a **rendering** failure, not a data failure — EMI successfully rebuilds ~176k recipes on reconnect

## Environment

- **Trigger:** Disconnect from server then rejoin in the same client session
- **Frequency:** 100% reproducible on reconnect
- **Affects:** Client only

## Root Cause

Not yet identified.

**Ruled out:**
- Texture atlas rebuild: `mixin.perf.dynamic_resources=true` eliminates the full atlas rebuild on reconnect (reduces overhead ~40s → ~12s) but does not fix the blank UI. Tested with both JEI and EMI, on and off — no effect. Left enabled as a genuine perf win.
- Iris shader pipeline: Iris destroys and recreates its pipeline on every reconnect ("dimension change: overworld → overworld"), even with `enableShaders=false`. No effect on blank UI.
- ImmediatelyFast: Removed entirely — no effect. Not the cause.
- LegendaryTooltips: Removed entirely — no effect. Not the cause.
- Sodium + Reese's Sodium Options + Iris + CreateBetterFPS: All removed as a group — blank UI persists. Render pipeline not the cause.
- EMI itself: Removed from pack entirely (server connects fine without it) — blank UI persists. EMI is not the root cause.
- `lazy_search_tree_registry`: Enabled (`=true`) — no effect on blank UI. This mixin defers tooltip search-tree building and is now left enabled as a perf improvement.
- ModernFix: Removing it causes 3-minute reconnect overhead → server kicks client on keepalive timeout. **Required; cannot remove.**
- Timing: EMI finishes its full reload in ~24s on reconnect; waiting 2+ minutes shows no change.
- EMI data: Log confirms 176,568 recipes baked successfully on reconnect — data is present, items just don't render.
- Single-player: SP save/exit/reload works correctly. Bug is **server-specific** — triggered by the server disconnect path, not world unload/reload in general.

**Secondary bug found (not root cause):** `lazy_search_tree_registry=true` did not prevent an Ars Nouveau + Curios NPE during `SessionSearchTrees.updateCreativeTooltips` on disconnect. `StarbuncleCharm.appendHoverText` constructs a Starbuncle entity without a world context during tooltip building, causing a `level == null` NPE. This bug fires on both first join and reconnect — it is not reconnect-specific and is not causing the blank UI. Tracked separately as issue-00003.

**Next step:** Batch bisect — revert to a known-clean state (vanilla + no mods, or batch 1 state), confirm server reconnect works, then add batches forward until the blank UI appears.

---

## Bisect Log

### Mod removal bisect (debug/00002-emi-blank-ui-reconnect branch, 2026-06-30)

| Removed | Result | Verdict |
|---|---|---|
| Sodium, Reese's Sodium Options, Iris, CreateBetterFPS | Blank UI persists | Ruled out |
| ImmediatelyFast | Blank UI persists | Ruled out |
| LegendaryTooltips | Blank UI persists | Ruled out |
| ModernFix | Keepalive timeout on reconnect — can't connect at all | **Required; cannot remove** |
| EMI + Extra Mod Integrations | Blank UI persists | Ruled out — EMI is not the cause |

All removed mods were re-added after each test. Branch was returned to full pack state after session.

**Log analysis findings:**
- EMI completes its reload identically on first join and reconnect (same plugin list, same recipe count ~176k, no errors). Blank UI is not caused by EMI's data reload failing.
- The blank affects item sprites (EMI panel, vanilla inventory) AND mod HUD icons (JourneyMap minimap, gamemode buttons) — pointing to something fundamental in the render pipeline, not EMI or any single mod.
- `extra_mod_integrations_rechiseled` throws `NoClassDefFoundError` on every EMI reload (both joins) — caught and ignored by EMI, not related.
- `paxi` throws a repository error on every reconnect — same on both joins, not reconnect-specific.
- ModernFix manages `Worker-ResourceReload` threads; without it, reconnect resource reload takes ~3 minutes and triggers keepalive timeout.

### Batch bisect (debug/00002-emi-blank-ui-reconnect branch, 2026-07-01)

Binary search across all 7 batches using `git checkout <batch-end-commit> -- mods/` to snap the mods directory to each state, then `packwiz refresh`. Both client and server synced from `packwiz serve` each round.

| State tested | Result | Verdict |
|---|---|---|
| B1–B4 only (203 mods) | GUI works on reconnect ✅ | Bug not in B1–B4 |
| B1–B5 (227 mods) | GUI works on reconnect ✅ | Bug not in B5 |
| B1–B6 (262 mods) | GUI works on reconnect ✅ | Bug not in B6 |
| B1–B7 (333 mods, EMI not JEI) | Blank UI on reconnect ❌ | **Bug is in B7** |
| B1–B6 + B7 first half (A–F) | Blank UI on reconnect ❌ | Bug in B7 A–F group |
| B1–B6 + B7 second half (G–Z) | GUI works on reconnect ✅ | B7 G–Z group is clean |

**B7 first half (A–F) — suspect mod list:**
advancement-plaques, attributefix, better-advancements, better-beds, better-modlist, betterdays, betterf3, bow-infinity-fix, bridging-mod, carry-on, chatanimation, chunks-fade-in, clumps, collective, controlling, crafting-tweaks, create-power-loader, create-ultimine, crops-love-rain, cut-through, despawn-tweaks, double-doors, durability-tooltip, dynamic-fps, easy-magic, easy-villagers, emoji-type, enchantment-descriptions, enhanced-attack-indicator, equipment-compare, explorers-compass, ftb-ultimine-forge

**Infrastructure notes for continuing the bisect:**
- JEI causes keepalive timeout with full pack — **use EMI** (infrastructure swap, not content)
- `packet-fixer` required to connect with B6+ mods
- Server `view-distance` and `simulation-distance` must be set to 6 in `server.properties`
- Server ModernFix: `mixin.perf.dynamic_resources=false` (prevents ClientLevel crash in Worker-ResourceReload threads)
- Pack ModernFix: `mixin.perf.clear_mixin_classinfo=false` (prevents JEI API class crash in EMI's JEMI compat layer)
- `balm` must be `side = "both"` (was client-only in B4 state — server crashes without it)
- Every Compat (`every-compat` + `stone-zone`) removed — too RAM-heavy for bisect
- Minimum 10GB RAM needed with B6+ mods loaded

**Branch state at session end (2026-07-01):**
Working tree is at B1–B6 + B7 second half (G–Z) + shared deps — a known-clean baseline.
Next session: add B7 A–F mods back and bisect within them (split ~32 mods into two groups of ~16).

### Bisect within B7 A–F (debug/00002-emi-blank-ui-reconnect branch, 2026-07-01)

Split 32 A–F mods (31 to add; collective already present as shared dep) into two halves:

**Group A1 (15 mods — advancement-plaques → crafting-tweaks):**
advancement-plaques, attributefix, better-advancements, better-beds, better-modlist, betterdays, betterf3, bow-infinity-fix, bridging-mod, carry-on, chatanimation, chunks-fade-in, clumps, controlling, crafting-tweaks

**Group A2 (16 mods — create-power-loader → ftb-ultimine-forge):**
create-power-loader, create-ultimine, crops-love-rain, cut-through, despawn-tweaks, double-doors, durability-tooltip, dynamic-fps, easy-magic, easy-villagers, emoji-type, enchantment-descriptions, enhanced-attack-indicator, equipment-compare, explorers-compass, ftb-ultimine-forge

| State tested | Result | Verdict |
|---|---|---|
| B1–B6 + G–Z + A1 (advancement-plaques → crafting-tweaks) | _pending_ | _pending_ |

**Branch state at session start (2026-07-01):**
A1 mods restored from B7 merge commit (0ae6e9b1d) via `git checkout`. Pack ready to sync and test.
- If bug appears → culprit is in A1 (bisect A1 further)
- If no bug → culprit is in A2 (swap to A2 and bisect)

### Next: Test A1 round; record result above

---

## Attempted Fixes

### [2026-06-30] Enable `mixin.perf.dynamic_resources=true` — Result: Partial improvement, does not fix blank UI

**Hypothesis:** ModernFix's `dynamic_resources` mixin (disabled by default) causes a full texture atlas rebuild on every server disconnect. With shaders enabled, ModernFix logged "Time from main menu to in-game: 40s" on reconnect (treating it as a full game load), blanking all sprites during rebuild.

**Change made:** Added `mixin.perf.dynamic_resources=true` to `config/modernfix-mixins.properties`.

**Result:** Reconnect overhead reduced from ~40s to ~12s. No full atlas rebuild occurs on disconnect. However, GUI items remain blank on reconnect — the atlas rebuild was not the root cause, just a secondary symptom. Keeping this change as a genuine performance improvement.

---

### [2026-06-30] Disable Iris shaders (`enableShaders=false`) — Result: No effect

**Hypothesis:** Iris destroys and recreates its shader pipeline on every reconnect (treats it as a "dimension change: overworld → overworld"). ImmediatelyFast holds references to Iris framebuffers; teardown might invalidate batched render state.

**Change made:** Set `enableShaders=false` in `iris.properties`. Iris confirmed: "Shaders are disabled because enableShaders is set to false." Iris still creates/destroys a vanilla pipeline on reconnect even without shaders.

**Result:** No effect. GUI still blank on reconnect. Iris pipeline recreation is not the cause.

**Note:** Shaders left disabled as-is for continued testing (if fixing blank UI without shaders, we'll know shaders are a separate concern).

---

### [2026-06-30] Remove ImmediatelyFast — Result: No effect

**Hypothesis:** ImmediatelyFast batches all GUI rendering (HUD, screens, item icons) through its own vertex buffer pipeline. If its batch state doesn't properly reset after Iris tears down its pipeline on disconnect, everything drawn through it would go blank while remaining clickable.

**Change made:** Removed `immediatelyfast` from pack via `packwiz remove immediatelyfast`. Re-added after test.

**Result:** No effect. GUI still blank on reconnect. ImmediatelyFast is not the cause.

---

### [2026-06-30] Remove EMI entirely — Result: No effect

**Hypothesis:** EMI's `MinecraftClientMixin` injects into `Minecraft.disconnect()` and clears item stacks. The blank UI appeared after the JEI → EMI swap; EMI's disconnect/reconnect lifecycle is the most likely culprit. Items are still interactable (EMI recipe viewer works when clicking blank sidebar), suggesting data is present but rendering is broken — consistent with EMI clearing and not fully restoring render state.

**Change made:** Removed `emi` and `extra-mod-integrations` from pack via `packwiz remove`. Re-added after test.

**Result:** No effect. GUI still blank on reconnect even without EMI installed. EMI is not the root cause.

---

### [2026-06-30] Enable `mixin.perf.lazy_search_tree_registry=true` — Result: No effect on blank UI; reveals separate NPE bug

**Hypothesis:** The `SessionSearchTrees.updateCreativeTooltips` tree builds asynchronously after world join. If a disconnect races with an incomplete build, the creative inventory may be left in a broken state that persists into the next connection.

**Change made:** Added `mixin.perf.lazy_search_tree_registry=true` to `config/modernfix-mixins.properties`.

**Result:** No effect on blank UI. However, a separate NPE was found: Ars Nouveau's `StarbuncleCharm.appendHoverText` constructs a Starbuncle entity without a world context during `SessionSearchTrees.updateCreativeTooltips`, causing `level == null` crash. This NPE fires both before and after enabling lazy registry — it is a separate Ars Nouveau + Curios bug, not related to the blank UI. Tracked as issue-00003.

`lazy_search_tree_registry=true` left enabled as a general perf improvement.

---

## Solution

_Pending._

---

## Ignore Reason

N/A
