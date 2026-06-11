# FuzzCraft 4

A personal, long-term modpack for a casual friend group. Tech and automation as the primary pillar, with magic, exploration, and adventure alongside it. Built on NeoForge 1.21.1.

See [docs/charter.md](docs/charter.md) for the full project charter.

---

## Player Setup (packwiz bootstrap)

Download [`packwiz-installer-bootstrap.jar`](https://github.com/packwiz/packwiz-installer-bootstrap/releases) once and add the following pre-launch command to your ATLauncher or Prism instance:

```
"$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://fuzzymelon94.github.io/FuzzCraft-4/pack.toml
```

The launcher will fetch and sync the latest pack automatically on every launch.

---

## Batch Progress

| Batch | Name | Status |
|---|---|---|
| 1 | Foundation | ⬜ Not started |
| 2 | Tech & Automation | ⬜ Not started |
| 3 | Magic & Farming | ⬜ Not started |
| 4 | Exploration & Combat | ⬜ Not started |
| 5 | Building & Questing | ⬜ Not started |

---

## Development

```bash
packwiz serve                    # Local dev server
packwiz mr add [URL|name]        # Add mod from Modrinth
packwiz cf add [URL|name]        # Add mod from CurseForge
packwiz update --all             # Update all mods
```
