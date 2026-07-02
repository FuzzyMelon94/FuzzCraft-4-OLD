# FuzzCraft 4 — Optimisation Tracker

Target: client stably below 8GB RAM (ideally ~6GB), server comfortably within a constrained home mini PC. Slow launch is acceptable; slow server connect is not.

**Do not action items here without a stable baseline first.** Changes should be made one at a time, tested, and either confirmed or reverted before moving to the next. Use Spark to profile before and after significant changes.

> If this list grows significantly, convert to a `docs/optimisation/` folder with one file per item.

---

## Status key

| Status | Meaning |
|---|---|
| `noted` | Identified, not yet actioned |
| `ready` | Agreed to action — waiting for a stable baseline |
| `done` | Applied and confirmed |
| `wont-fix` | Decided against — reason recorded |

---

## Items

### OPT-001 — JVM flags (client + server)
**Status:** `done`  
**Priority:** High — single biggest win, no mod changes required  
**Impact:** Memory cap enforcement, reduced GC stuttering

Apply these flags in the launcher (client) and Pterodactyl startup (server). These replace whatever is currently set.

**Client** (Prism Launcher → instance settings → Java arguments):
```
-Xms2G -Xmx6G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dfml.readTimeout=180
```

**Server** (Pterodactyl startup command / Wings config):
```
-Xms2G -Xmx4G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1
```

`-Xmx6G` on the client hard-caps the Java heap. OS + native memory adds ~1–2GB on top, so real usage should sit around 7–7.5GB. Reduce to `-Xmx5G` if players report instability on lower-spec machines.

**Notes:** `-Dfml.readTimeout=180` on client prevents connection timeouts on slow-loading servers. Server flags omit this — not needed headless.

**Result:** Applied and confirmed stable. Running well with no memory complaints. Simulation distance set to 8, view distance to 10 on the server — tested fine, keeping these values.

---

### OPT-002 — ModernFix config audit
**Status:** `done`  
**Priority:** Medium — `dynamic_resources` is already enabled; check remaining options  
**Impact:** Startup memory, chunk loading performance

- `mixin.perf.dynamic_resources` — already enabled (defers texture/model loading to first use)
- `mixin.perf.faster_item_rendering` — enabled (speeds up item render caching)
- `mixin.bugfix.chunk_deadlock` — default true, no action needed
- `mixin.perf.remove_spawn_chunks` — not available in this ModernFix version
- `mixin.perf.ingredient_item_deduplication` — already enabled (reduces EMI load time)

**Result:** `faster_item_rendering` added. All available options confirmed.

---

### OPT-003 — EntityCulling distance tuning
**Status:** `ready`  
**Priority:** Medium — with 13+ mob mods, default culling distances may be generous  
**Impact:** Client rendering performance; reduces GPU/CPU load from off-screen entities

EntityCulling skips rendering entities that are behind walls or outside view. The default distance thresholds may be set wider than needed for a pack this dense with mob content.

Check `config/entityculling.toml` — specifically `maxEntityRenderDistanceSquared` and any per-entity-type overrides. Tighten conservatively and test in a mob-dense area. Compare with Spark's entity render timing before/after.

**Note:** `config/entityculling.toml` does not exist yet — it is generated on first game launch. Action this after the file has been generated.

---

### OPT-004 — Chipped vs Rechiseled (decoration duplication)
**Status:** `noted`  
**Priority:** Low — decoration rules are loose; only worth acting on if memory impact is confirmed  
**Impact:** Minor — client texture atlas reduction

Both mods add decorative block variants. Key differences:
- **Chipped** — broader variety, more block types, crafting bench UI
- **Rechiseled** — connected textures (blocks visually merge when adjacent), Create integration via `rechiseled-create`

Rechiseled has unique features (connected textures + Create automation) that Chipped doesn't. If one is to go, Chipped is the candidate. Decision deferred to player feedback — builders may specifically want Chipped's variety.

**Action when ready:** Ask the group if anyone uses Chipped specifically. If not, remove it and `rechiseled-create` handles the Create-side niche. Note: issue-00004 (Rechiseled EMI integration broken) should be resolved first regardless.

---

### OPT-005 — Spark profiling session
**Status:** `done`  
**Priority:** High — should be done before and after any significant change  
**Impact:** Identifies actual bottlenecks; prevents optimising the wrong things

**Result:** Server and client profiles both captured (2026-07-02). Client was healthy — 70% render thread idle time, 165fps with shaders. Server showed a 2890ms max tick spike (likely GC at high heap) but median MSPT was 17ms and TPS was stable. No client-side mod bottleneck identified. Original FPS spikes were transient — consistent with dynamic resource loading on first world join. Monitor server max-tick spikes under multi-player load.

---

### OPT-006 — Fresh Animations / ETF / EMF client impact
**Status:** `noted`  
**Priority:** Low — visual mods, no server impact  
**Impact:** Client VRAM and texture memory; may contribute to client-side lag on lower-spec machines

ETF + EMF + Fresh Animations re-skin most vanilla and modded mobs with animated textures. Beautiful but memory-heavy on the client — each mob gets a new set of texture frames loaded into VRAM.

Not worth removing for most players. If someone in the group has a lower-spec machine and struggles with memory, these are good candidates to disable client-side only. No server impact.

**Action if needed:** Document as an optional client-side toggle in the player setup guide.
