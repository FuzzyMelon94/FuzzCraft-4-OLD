# FuzzCraft 4 — Claude Instructions

This is a personal Minecraft modpack project. The source of truth for vision, design decisions, and batch plans is [`docs/charter.md`](docs/charter.md). Read it at the start of any session involving mod additions or batch work.

---

## Repo Structure

```
fuzzcraft-4/
├── docs/
│   ├── charter.md          # Vision, batch plans, issue log, progress tracker
│   ├── watchlist.md        # Mods deferred or awaiting ports
│   └── testing/
│       ├── batch1.md       # SP test log — Batch 1
│       ├── batch2.md       # SP test log — Batch 2
│       └── multiplayer.md  # Multiplayer test log (all batches)
├── mods/                   # packwiz mod manifests (auto-managed)
├── config/                 # Server & client configs
├── pack.toml               # packwiz pack definition
└── index.toml              # packwiz index (auto-managed)
```

---

## Batch Workflow

Each batch lives on its own branch (`batch/N-short-name`), is tested locally, then merged to `main` when stable. Pages serves from `main` — nothing reaches players until merged.

1. Create branch: `git checkout -b batch/N-short-name`
2. Add mods via `packwiz mr add` / `packwiz cf add`
3. Commit as you go — don't batch everything into one end-of-session commit
4. Update `docs/watchlist.md` with anything deferred
5. Update `docs/charter.md` progress tracker (In Progress → Complete, add notes)
6. Create `docs/testing/batchN.md` for SP testing
7. Add batch multiplayer deferred tests to `docs/testing/multiplayer.md`
8. Once SP testing passes, merge to `main`
9. Pull on server, run server test pass
10. Close out: bump pack version in `pack.toml`, final charter update, commit

### Commit conventions

```
feat(batchN): <what was added>
fix(batchN): <what was fixed>
chore: <housekeeping — version bumps, doc updates>
```

### packwiz quick reference

```bash
packwiz serve                      # Local dev server (default :8080)
packwiz mr add <url|slug> -y       # Add from Modrinth (non-interactive)
packwiz cf add <url|slug> -y       # Add from CurseForge
packwiz update --all               # Update all mods
packwiz refresh                    # Rebuild index.toml
```

Prefer Modrinth sources where available. CurseForge as fallback. Note the source in commit messages where it matters.

---

## Testing Checklist Format

All test files live in `docs/testing/`. Single-player batch tests are one file per batch (`batchN.md`). Multiplayer tests accumulate in `multiplayer.md` with a section per batch.

### File header

```markdown
# FuzzCraft 4 — Batch N Testing: <Name>

## Summary
**Pack version:** x.y.z
**Test date:** <tester fills in>
**Tester:** <tester fills in>
**Play mode:** Single player

## Known Issues
<!-- Populated before handing to tester. Known bugs, deferred items, things to be aware of. -->
<!-- If none: write "None known." -->
```

### Section order

1. **Launch & Stability** — always first; catches crashes before wasting time on feature tests
2. **Regression — Batch N** — brief checks that prior-batch mods still work; grows each batch but stays lean
3. **[Mod or category sections]** — grouped by mod or logical category; large mods get their own section
4. **Deferred — Requires Server / Multiplayer** — list only; full tests go in `multiplayer.md`
5. **Tester Notes** — freeform; broken things, surprises, feedback to feed back

Known issues go **above** the checklist sections so the tester sees them before starting.

### Checklist conventions

- Use `- [ ]` checkboxes for things to verify
- Use numbered lists for sequential steps that don't need individual sign-off
- Include commands as inline backtick blocks, one command per line if sequenced:
  ```
  /difficulty hard
  /summon minecraft:zombie
  ```
- Mark mods that are beta/experimental with ⚠️ so the tester knows to watch closely
- If a test is better done with multiple people, move it to the Deferred section — don't leave it in the SP checklist
- Keep regression sections short: 5–10 items max, only things that could realistically break

### Multiplayer file conventions

`multiplayer.md` has one `## Batch N — <Name>` section per batch. Each section follows the same checklist conventions. The file header tracks the most recent test session at the top.

---

## Mod Addition Checklist (per batch)

When adding a new batch of mods, work through these in order:

1. Confirm 1.21.1 NeoForge availability before committing to any mod
2. Check Modrinth first; note CurseForge-only mods explicitly
3. Note any auto-pulled dependencies — they count toward the mod total
4. Run a compat pass each batch (Almost Unified, Jade Addons, Curios, etc.)
5. Update `docs/watchlist.md` for anything deferred
6. Update `docs/charter.md` issue log for any surprises found during adds
7. Commit mod manifests + doc changes together with a clear `feat(batchN):` message
8. Create the batch test file before handing off for testing
