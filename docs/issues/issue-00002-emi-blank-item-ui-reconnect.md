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

After the JEI → EMI swap, reconnecting to the server leaves EMI's item panel visually blank — the UI frame and buttons are present and interactable, but no items are rendered. First join is unaffected. Suspected to be a ModernFix `dynamic_resources` interaction.

---

## Symptoms

- On first join: EMI item panel populates and displays correctly
- On every subsequent join (disconnect + rejoin): item panel appears but contains no items
- Vanilla creative inventory UI also affected — visible frame with no item icons
- UI elements remain interactable (e.g. gamemode/weather buttons can be clicked by position even though their icons don't render)
- First join is always clean; issue is 100% reproducible on reconnect

## Environment

- **Trigger:** Disconnect from server then rejoin in the same client session
- **Frequency:** 100% reproducible on reconnect
- **Affects:** Client only

## Root Cause

_Not yet identified._

Likely candidates:
1. **ModernFix `dynamic_resources=false`** — this mixin was added to fix invisible GUI with JEI ([resolved-00001](resolved-00001-keepalive-timeout-reconnect.md)). EMI may interact with it differently, causing item rendering to fail on reconnect rather than the full GUI going invisible.
2. **EMI reconnect behaviour** — EMI may not be repopulating its ingredient list correctly on `RecipesUpdatedEvent` under this mod configuration.

---

## Attempted Fixes

_None yet._

---

## Solution

_Pending._

---

## Ignore Reason

N/A
