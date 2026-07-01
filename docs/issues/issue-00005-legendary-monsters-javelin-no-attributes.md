---
id: "00005"
status: issue
title: "Legendary Monsters resurrected_javelin has no attributes"
date_opened: "2026-07-01"
date_resolved: ""
affects: both
pack_version_opened: "0.7.5"
pack_version_resolved: ""
---

## Summary

On world unload / disconnect, the game logs an error that `legendary_monsters:resurrected_javelin` has no attributes. Unknown whether this causes any in-game behavioural issues or is purely cosmetic.

---

## Symptoms

- `[net.minecraft.Util/]: Entity legendary_monsters:resurrected_javelin has no attributes` in `debug.log`
- Fires on disconnect/world unload, not on world join
- No observed crash

## Environment

- **Trigger:** World unload / server disconnect
- **Frequency:** Always — 100% reproducible
- **Affects:** Unknown — logged on client; may also occur server-side
- **Mod version:** Legendary Monsters `2.1.15` (MC 1.21.1)

## Root Cause

_Under investigation._

The `resurrected_javelin` entity type is missing attribute registrations. This is either a bug in Legendary Monsters 2.1.15 or a NeoForge 1.21.1 compatibility issue where the entity's attribute supplier wasn't registered correctly. Check whether a newer version of Legendary Monsters addresses this, and whether the entity causes any issues when actually spawned in-game.

---

## Attempted Fixes

_None yet._

---

## Solution

_Pending._

---

## Ignore Reason

N/A
