---
id: "00001"
status: issue
title: "keepAlive timeout on server reconnect"
date_opened: "2026-06-18"
date_resolved: ""
affects: both
pack_version_opened: "0.7.0"
pack_version_resolved: ""
---

## Summary

On every reconnect to the dedicated server, the client is kicked ~33 seconds after the server prints "logged in". First join works fine; the timeout fires on every subsequent connect in the same session.

---

## Symptoms

- Server log: `[ServerGamePacketListenerImpl]: FuzzyMelon94 lost connection: Timed out`
- Client log: `Client disconnected with reason: Disconnected` at ~33s after world join
- First join always succeeds; the issue only fires on reconnect (disconnect + rejoin)
- Client-side `debug.log` shows JEI taking **62 seconds** on reconnect vs **19.85 seconds** on first join

## Environment

- **Trigger:** Disconnect from server then rejoin in the same client session
- **Frequency:** 100% reproducible on reconnect
- **Affects:** Both (server kicks, client receives disconnect)

## Root Cause

The vanilla/NeoForge keepAlive mechanism sends a packet every 15 seconds and kicks the client if it hasn't responded within **30 seconds**. The client's `handleKeepAlive` is dispatched via `PacketUtils.ensureRunningOnSameThread`, meaning the response can only be sent when the **render thread is free**.

On reconnect, `ClientboundUpdateRecipesPacket` triggers `RecipesUpdatedEvent`, which JEI handles by **fully rebuilding from scratch** on the render thread — synchronously, blocking all other render-thread work including keepAlive response dispatch.

**Reconnect JEI breakdown (from debug.log, 18 June 2026):**

| Phase | First join | Reconnect |
|---|---|---|
| Registering ingredients | 3.9s | 3.1s |
| Registering recipes (all mods) | 10.3s | **31.4s** |
| — farmersdelight alone | 1.9s | **11.2s** |
| — jei:minecraft | 3.4s | 7.3s |
| — twilightforest | 0.8s | 2.9s |
| Building ingredient filter | 7.9s | **22.8s** |
| **Total JEI** | **23.5s** | **58.3s** |

The reconnect is consistently 2–10× slower per-mod despite identical ingredient counts (43,260 vs 43,261). The non-uniform distribution (ars_nouveau 57×, productivebees 14×, farmersdelight 5.8×) rules out pure GC pressure — some mods are doing significantly more work on reconnect than on first join.

The ingredient filter phase (22.8s) is the single biggest added cost and is architectural: JEI builds a full search trie over all ingredients on every world join, on the render thread.

---

## Attempted Fixes

### [2026-06-29] Swap JEI → EMI — Result: Pending test

**Hypothesis:** EMI builds its ingredient filter lazily on first search use rather than on world join, eliminating the render thread block that causes the timeout. EMI also handles `RecipesUpdatedEvent` differently and should not reproduce JEI's reconnect regression.

**Change made:** Removed `jei`, added `emi` + `extra-mod-integrations` EMI addon. Also removed `collapsible-groups` (JEI-only plugin, incompatible). Pack version 0.7.4.

**Result:** Pending.

---

### [2026-06-29] Add Packet Fixer — Result: No effect

**Hypothesis:** Packet Fixer patches oversized packet limits and lists "connection timeouts" as a resolved issue; worth testing.

**Change made:** Added `packet-fixer` (both-sided). Pack version 0.7.3.

**Result:** No effect. The timeout is caused by render thread blocking, not packet size. Packet Fixer remained in pack as it may help with unrelated packet errors.

---

### [2026-06-29] Disable `lazy_search_tree_registry` (ModernFix) — Result: No effect

**Hypothesis:** `mixin.perf.lazy_search_tree_registry=true` (ModernFix default) defers JEI's search tree build; suspected to cause a full rebuild on reconnect instead of reusing state. Setting to `false` should build once and reuse.

**Change made:** Added `mixin.perf.lazy_search_tree_registry=false` to `config/modernfix-mixins.properties`. Pack version 0.7.2.

**Result:** No meaningful change. Building runtime: 23.59s on reconnect vs 24.10s before (–0.5s, within noise). The mixin controls deferral timing, not whether JEI rebuilds from scratch on reconnect.

---

### [2026-06-18] Remove RFTools Dimensions — Result: No effect

**Hypothesis:** RFTools Dimensions sends large dimension packet data on join that might be causing the timeout.

**Change made:** Removed `rftools-dimensions`. Pack version 0.7.1.

**Result:** No effect. JEI rebuild timing was the actual cause.

---

### [2026-06-18] Research server-side keepAlive timeout extension — Result: No viable mod found

**Hypothesis:** Extending the server-side keepAlive timeout from 30s to 90s+ would give JEI enough time to complete its reconnect rebuild.

**Finding:** The 30s timeout is hardcoded in vanilla `ServerGamePacketListenerImpl`. NeoForge does not expose a config for it. The only mods that patch this (TimeOutOut, RandomPatches) are Fabric/Quilt-only or Forge-only with no NeoForge 1.21.1 versions. `-Dfml.readTimeout` and `-Dfml.loginTimeout` JVM args affect the login handshake phase only, not in-game keepAlive.

**Result:** Dead end without writing a custom NeoForge mixin mod.

---

## Solution

_Pending outcome of EMI swap._

---

## Ignore Reason

N/A
