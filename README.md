# FuzzCraft 4

A personal, long-term modpack for a casual friend group. Tech and automation as the primary pillar, with magic, exploration, and adventure alongside it. Built on NeoForge 1.21.1.

See [docs/charter.md](docs/charter.md) for the full project charter.

---

## Player Setup (Prism Launcher)

1. Create a new instance — **Minecraft 1.21.1**, loader **NeoForge 21.1.233**
2. Download [`packwiz-installer-bootstrap.jar`](https://github.com/packwiz/packwiz-installer-bootstrap/releases) and place it in the instance's `.minecraft` folder
3. In Prism: **Edit Instance → Settings → Custom commands → Pre-launch command**:
   ```
   "$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://fuzzymelon94.github.io/FuzzCraft-4/pack.toml
   ```
4. Launch — the installer will fetch and sync all mods automatically on every launch

If you've played before and a mod was removed from the pack, delete it manually from the `mods/` folder; the bootstrapper does not remove files it didn't place.

---

## Java & Memory

**Recommended allocation: 6144–8192 MB (6–8 GB).** Distant Horizons generates LOD data in the background, so 6 GB is the practical minimum — 8 GB is preferred if your machine allows it.

In Prism: **Edit Instance → Settings → Java → Override memory → 6144 MB** (or 8192 MB if available)

Add these JVM arguments under **Edit Instance → Settings → Java → JVM arguments**:

```
-XX:+UseZGC -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:+PerfDisableSharedMem
```

ZGC (Java 21+) is a concurrent garbage collector that eliminates GC pause stuttering. It's particularly recommended with Distant Horizons, which generates LOD data in the background and benefits from low-latency collection.

In established worlds with many loaded chunks, 10 GB (10240 MB) is the safer cap.

---

## Batch Progress

| Batch | Name | Status |
|---|---|---|
| 1 | Foundation | ✅ Complete |
| 2 | Tech & Automation | ✅ Complete |
| 3 | Magic & Farming | ✅ Complete |
| 4 | World Gen & Combat | ✅ Complete |
| 5a | Dimensions — Flagship + Bosses + Utility | ✅ SP Tested |
| 5b | Dimensions — Aether Cluster | ✅ SP Tested |
| 5c | Dimensions — Underground & Quirky | ✅ SP Tested |
| 6 | Building & Decoration | ✅ SP Tested |
| 7 | QoL & Final Compat | ✅ Complete |
| 8 | QoL Extras | ✅ Complete |
| 9 | Questing | ⬜ Not started |

---

## Server Setup

Copy [`server.properties.sample`](server.properties.sample) to your server root as `server.properties` before first launch (or diff it against an existing file). It documents all settings that differ from vanilla defaults and why — simulation distance, spawn protection, flight, difficulty, etc.

---

## Development

```bash
packwiz serve                    # Local dev server
packwiz mr add [URL|name] -y    # Add mod from Modrinth
packwiz cf add [URL|name] -y    # Add mod from CurseForge
packwiz update --all             # Update all mods
packwiz refresh                  # Rebuild index.toml after manual edits
```

---

## Active Issues

| ID | Title | Opened | Affects |
|---|---|---|---|
| [00004](docs/issues/issue-00004-rechiseled-emi-integration-broken.md) | Rechiseled EMI integration fails — NoClassDefFoundError | 2026-07-01 | Client |
| [00005](docs/issues/issue-00005-legendary-monsters-javelin-no-attributes.md) | Legendary Monsters resurrected_javelin has no attributes | 2026-07-01 | Both |

Full issue history (including resolved) in [`docs/issues/`](docs/issues/).
