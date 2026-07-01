---
id: "00003"
status: issue
title: "Ars Nouveau + Curios NPE during SessionSearchTrees build"
date_opened: "2026-06-30"
date_resolved: ""
affects: client
pack_version_opened: "0.7.4"
pack_version_resolved: ""
---

## Summary

`StarbuncleCharm.appendHoverText` (Ars Nouveau) constructs a Starbuncle entity without a world context during `SessionSearchTrees.updateCreativeTooltips`, causing a `level == null` NPE. Fires on every world join and persists indefinitely — caught silently, does not crash the client.

---

## Symptoms

- `NullPointerException` in `SessionSearchTrees.updateCreativeTooltips` on every world join
- Stack trace leads through `StarbuncleCharm.appendHoverText` → Curios capability lookup → `level == null`
- Error is caught and suppressed — game continues normally
- Appears in `debug.log` on both first join and reconnect; not reconnect-specific
- Does not appear to cause any user-visible breakage (investigated as possible cause of issue-00002 blank UI; ruled out)

## Environment

- **Trigger:** World join or server reconnect (any world load)
- **Frequency:** Always — 100% reproducible
- **Affects:** Client only

## Root Cause

Ars Nouveau's `StarbuncleCharm.appendHoverText` creates a Starbuncle entity for tooltip purposes without a world context. When `SessionSearchTrees.updateCreativeTooltips` builds tooltip search trees (triggered on world join), it calls `appendHoverText` on all registered items, including `StarbuncleCharm`. The Curios API's capability lookup on the entity requires a non-null `level`, which is not available at tooltip-building time.

This is an Ars Nouveau bug — `appendHoverText` should guard against null level when constructing entities for tooltip purposes.

---

## Attempted Fixes

_None attempted yet. Low priority — bug is silent and has no user-visible effect._

---

## Solution

_Pending._

---

## Ignore Reason

N/A
