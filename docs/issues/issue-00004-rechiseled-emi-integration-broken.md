---
id: "00004"
status: issue
title: "Rechiseled EMI integration fails — NoClassDefFoundError"
date_opened: "2026-07-01"
date_resolved: ""
affects: client
pack_version_opened: "0.7.5"
pack_version_resolved: ""
---

## Summary

The `extra_mod_integrations_rechiseled` EMI plugin crashes on every world join with a `NoClassDefFoundError` for `ChiselingRecipes`. Rechiseled recipes do not appear in EMI as a result.

---

## Symptoms

- `[EMI/]: Exception loading plugin provided by extra_mod_integrations_rechiseled` on every world join
- `java.lang.NoClassDefFoundError: com/supermartijn642/rechiseled/chiseling/ChiselingRecipes`
- Rechiseled chiseling recipes absent from EMI recipe browser
- No crash — error is caught by EMI's plugin loader

## Environment

- **Trigger:** World join / resource reload
- **Frequency:** Always — 100% reproducible
- **Affects:** Client only

## Root Cause

_Under investigation._

Likely suspect: Rechiseled in pack is `1.2.4-neoforge-mc1.21` (targets MC 1.21, not 1.21.1). The integration mod is `extra_mod_integrations_rechiseled 1.0.3+1.21.1`. The class `ChiselingRecipes` may have been renamed or restructured between Rechiseled versions, causing the integration to fail to find it at runtime.

Check whether a `1.2.x` build targeting `mc1.21.1` specifically exists on Modrinth, and whether the latest Rechiseled contains `ChiselingRecipes` in the expected package.

---

## Attempted Fixes

_None yet._

---

## Solution

_Pending._

---

## Ignore Reason

N/A
