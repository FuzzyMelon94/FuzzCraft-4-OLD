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

After the JEI → EMI swap, reconnecting to the server leaves the entire GUI blank — EMI's item panel, the vanilla creative inventory, and HUD overlay icons all go invisible. UI elements are still interactable (click positions work, EMI recipe viewer opens when clicking the blank sidebar). First join is unaffected. Confirmed 100% reproducible on every reconnect in the same client session.

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
- Texture atlas rebuild: `mixin.perf.dynamic_resources=true` eliminates the full atlas rebuild on reconnect (reduces reconnect overhead from ~40s to ~12s) but does not fix the blank UI. Tested with both JEI and EMI, on and off — no effect either way. Left enabled as a genuine perf win.
- Iris shader pipeline: Iris destroys and recreates its pipeline on every reconnect ("dimension change: overworld → overworld"), even with shaders disabled (`enableShaders=false`). Disabling shaders entirely had no effect on the blank UI
- ImmediatelyFast: Removed from pack entirely; no effect
- Timing: EMI finishes its full reload in ~24s; waiting 2+ minutes after completion shows no change
- EMI data: Log confirms 176,568 recipes baked successfully on reconnect — data is present, items just don't render
- Single-player: SP save/exit/reload works correctly. Bug is **server-specific** — triggered by the server disconnect path, not world unload/reload in general. This rules out anything purely in EMI's world-load lifecycle.

**Remaining hypotheses (priority order):**
- EMI's `disconnect()` mixin: EMI's `MinecraftClientMixin` injects into `Minecraft.disconnect()` and clears item stacks. The issue appeared specifically after the JEI → EMI swap, suggesting EMI's disconnect/reconnect lifecycle is involved. The mixin clears state that may not be fully restored on reconnect even though EMI's reload reports success. **Test: remove EMI entirely (client-only mod, server doesn't need it) to confirm EMI is the root cause.**
- Something else changed in the JEI → EMI swap batch that is the true cause (lower probability — need to review batch diff if EMI removal doesn't resolve it).

---

## Bisect Log

| Removed | Result | Verdict |
|---|---|---|
| Sodium, Reese's Sodium Options, Iris, CreateBetterFPS | Blank UI persists | Ruled out |
| ImmediatelyFast | Blank UI persists | Ruled out |
| LegendaryTooltips | Blank UI persists | Ruled out |
| ModernFix | Keepalive timeout on reconnect — can't connect at all | **Required; cannot remove** |

**Log analysis findings:**
- EMI completes its reload identically on first join and reconnect (same plugin list, same recipe count ~176k, no errors). The blank UI is not caused by EMI's data reload failing.
- The blank affects item sprites (EMI panel, vanilla inventory) AND mod HUD icons (JourneyMap minimap, gamemode buttons) — pointing to something fundamental in the render pipeline, not EMI specifically.
- `extra_mod_integrations_rechiseled` throws `NoClassDefFoundError` on every EMI reload (both joins) — caught and ignored by EMI, not related.
- `paxi` throws a repository error on every reconnect — same on both joins, not reconnect-specific.
- ModernFix manages `Worker-ResourceReload` threads; without it, reconnect resource reload takes ~3 minutes and triggers the original keepalive timeout.

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

## Solution

_Pending._

---

## Ignore Reason

N/A
