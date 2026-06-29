---
id: "00001"
status: resolved
title: "keepAlive timeout on server reconnect"
date_opened: "2026-06-18"
date_resolved: "2026-06-29"
affects: both
pack_version_opened: "0.7.0"
pack_version_resolved: "0.7.4"
---

## Summary

On every reconnect to the dedicated server, the client was kicked ~33 seconds after the server printed "logged in". First join worked fine; the timeout fired on every subsequent connect in the same session.

---

## Symptoms

- Server log: `[ServerGamePacketListenerImpl]: FuzzyMelon94 lost connection: Timed out`
- Client log: `Client disconnected with reason: Disconnected` at ~33s after world join
- First join always succeeded; the issue only fired on reconnect (disconnect + rejoin)
- Client-side `debug.log` showed JEI taking **62 seconds** on reconnect vs **19.85 seconds** on first join

## Environment

- **Trigger:** Disconnect from server then rejoin in the same client session
- **Frequency:** 100% reproducible on reconnect
- **Affects:** Both (server kicks, client receives disconnect)

## Root Cause

The vanilla/NeoForge keepAlive mechanism sends a packet every 15 seconds and kicks the client if it hasn't responded within **30 seconds**. The client's `handleKeepAlive` is dispatched via `PacketUtils.ensureRunningOnSameThread`, meaning the response can only be sent when the **render thread is free**.

On reconnect, `ClientboundUpdateRecipesPacket` triggers `RecipesUpdatedEvent`, which JEI handled by **fully rebuilding from scratch** on the render thread — synchronously, blocking all other render-thread work including keepAlive response dispatch.

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

The reconnect was consistently 2–10× slower per-mod despite identical ingredient counts (43,260 vs 43,261). The non-uniform distribution (ars_nouveau 57×, productivebees 14×, farmersdelight 5.8×) ruled out pure GC pressure. The ingredient filter phase (22.8s) was the largest single added cost — JEI built a full search trie over all ingredients on every world join on the render thread.

---

## Attempted Fixes

### [2026-06-29] Swap JEI → EMI — Result: **Resolved**

**Hypothesis:** EMI builds its ingredient filter lazily on first search use rather than on world join, eliminating the render thread block that causes the timeout.

**Change made:** Removed `jei` and `collapsible-groups` (JEI-only plugin). Added `emi` + `extra-mod-integrations` EMI addon. Pack version 0.7.4.

**Result:** Reconnect timeout resolved. Players can now reconnect repeatedly without being kicked. Introduced a follow-on visual issue — see [issue-00002](issue-00002-emi-blank-item-ui-reconnect.md).

---

### [2026-06-29] Add Packet Fixer — Result: No effect

**Hypothesis:** Packet Fixer patches oversized packet limits and lists "connection timeouts" as a resolved issue.

**Change made:** Added `packet-fixer` (both-sided). Pack version 0.7.3.

**Result:** No effect. The timeout was caused by render thread blocking, not packet size. Mod retained as it may help with unrelated packet errors.

---

### [2026-06-29] Disable `lazy_search_tree_registry` (ModernFix) — Result: No effect

**Hypothesis:** `mixin.perf.lazy_search_tree_registry=true` defers JEI's search tree build; suspected to cause a full rebuild on reconnect.

**Change made:** Added `mixin.perf.lazy_search_tree_registry=false` to `config/modernfix-mixins.properties`. Pack version 0.7.2.

**Result:** No meaningful change. Building runtime: 23.59s vs 24.10s (within noise). The mixin controls deferral timing, not whether JEI rebuilds from scratch on reconnect.

---

### [2026-06-18] Remove RFTools Dimensions — Result: No effect

**Hypothesis:** RFTools Dimensions sends large dimension packet data on join that might be causing the timeout.

**Change made:** Removed `rftools-dimensions`. Pack version 0.7.1.

**Result:** No effect. JEI rebuild timing was the actual cause.

---

### [2026-06-18] Research server-side keepAlive timeout extension — Result: No viable mod found

**Finding:** The 30s timeout is hardcoded in vanilla `ServerGamePacketListenerImpl`. NeoForge does not expose a config. TimeOutOut and RandomPatches are Fabric/Quilt-only or Forge-only with no NeoForge 1.21.1 versions. `-Dfml.readTimeout` / `-Dfml.loginTimeout` JVM args affect the login handshake phase only, not in-game keepAlive.

**Result:** Dead end without writing a custom NeoForge mixin mod.

---

## Solution

**Fix:** Replaced JEI with EMI. EMI does not block the render thread during world join — its ingredient filter is built lazily on first search use rather than synchronously on `RecipesUpdatedEvent`. Also removed `collapsible-groups` (JEI-only plugin, incompatible with EMI).

**Pack version:** 0.7.4

**Notes:** Introduced [issue-00002](issue-00002-emi-blank-item-ui-reconnect.md) — EMI item UI is blank on every reconnect after the first. Suspected to be a ModernFix `dynamic_resources` interaction, requires investigation.

---

## Ignore Reason

N/A
