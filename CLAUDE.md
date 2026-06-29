# FuzzCraft 4 — Claude Instructions

This is a personal Minecraft modpack project. The source of truth for vision, design decisions, and batch plans is [`docs/charter.md`](docs/charter.md). Read it at the start of any session involving mod additions or batch work.

---

## Repo Structure

```
fuzzcraft-4/
├── docs/
│   ├── charter.md          # Vision, batch plans, issue log, progress tracker
│   ├── watchlist.md        # Mods deferred or awaiting ports
│   ├── issues/
│   │   ├── _template.md                    # Blank template for new issues
│   │   ├── issue-NNNNN-title.md            # Open issue
│   │   ├── resolved-NNNNN-title.md         # Fixed issue
│   │   └── ignored-NNNNN-title.md          # Won't-fix issue
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

## Versioning

Pack version follows `MAJOR.MINOR.PATCH` targeting `1.0.0` as the full release.

| Segment | Rule |
|---|---|
| **Major** | Stays 0 until the pack is complete and released as 1.0.0 |
| **Minor** | Increments once per batch — B1 = 0.1.x, B2 = 0.2.x, B3 = 0.3.x, etc. |
| **Patch** | Increments for each distinct action within the batch branch |

**Patch increment triggers** (in order, within a batch):
- `.0` — branch created, version bumped at branch start
- `.1` — all mods for the batch added
- `.2+` — each fix, config change, or meaningful change made during testing

Bump the version in `pack.toml` and commit with `chore: bump to x.y.z` at each step. Do not batch multiple version bumps into one commit.

At the end of a batch, the test file should record the full version range tested (e.g. `0.2.1–0.2.4`) so saves can be matched to the state they were created on.

---

## Batch Workflow

Each batch lives on its own branch (`batch/N-short-name`), is tested locally, then merged to `main` when stable. Pages serves from `main` — nothing reaches players until merged.

1. Create branch: `git checkout -b batch/N-short-name`
2. Bump `pack.toml` version to `0.N.0` — commit `chore: bump to 0.N.0`
3. Add mods via `packwiz mr add` / `packwiz cf add`
4. Bump to `0.N.1` — commit `chore: bump to 0.N.1 (mods added)`
5. Commit as you go — don't batch everything into one end-of-session commit
6. Update `docs/watchlist.md` with anything deferred
7. Update `docs/charter.md` progress tracker (In Progress → Complete, add notes)
8. Create `docs/testing/batchN.md` for SP testing (include current version)
9. Add batch multiplayer deferred tests to `docs/testing/multiplayer.md`
10. Bump version for each fix made during testing — `0.N.2`, `0.N.3`, etc.
11. Once SP testing passes, merge to `main`
12. Pull on server, run server test pass
13. Close out: final charter update, note version range tested in test file, commit

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

## Issues System

Significant bugs and their debugging history live in `docs/issues/`. Use this system for anything that takes more than one attempt to fix or spans multiple sessions.

### File naming

```
{status}-{id}-{brief-title}.md
```

- `status` — one of `issue` (open), `resolved` (fixed), `ignored` (won't fix)
- `id` — 5-digit zero-padded integer, incremented per file regardless of status (next: check the highest existing ID and add 1)
- `brief-title` — kebab-case, 3–5 words max

Examples: `issue-00002-emi-blank-item-ui.md`, `resolved-00001-keepalive-timeout-reconnect.md`

### When to create an issue file

- The bug required more than one debugging attempt
- The root cause wasn't immediately obvious
- You spent significant time on dead ends worth recording
- The issue spans multiple sessions

Don't create files for straightforward single-step fixes — those belong in commit messages.

### Lifecycle

1. Create as `issue-NNNNN-title.md` using `docs/issues/_template.md`
2. Add each attempted fix under **Attempted Fixes** as you go (most recent at top)
3. When resolved: fill in **Solution**, update frontmatter `status` and `date_resolved`/`pack_version_resolved`, and **rename the file** from `issue-` to `resolved-`
4. When deprioritised: fill in **Ignore Reason**, update frontmatter `status`, and rename to `ignored-`
5. Keep `README.md`'s Active Issues table in sync whenever a file is created or its status changes

### Commit convention

```
chore: open issue-NNNNN — brief title
chore: resolve issue-NNNNN — brief title
chore: ignore issue-NNNNN — brief title
```

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
