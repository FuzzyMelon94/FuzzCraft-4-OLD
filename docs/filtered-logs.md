# FuzzCraft 4 — Log Begone Filter List

Filters are configured in [`config/logbegone.json`](../config/logbegone.json). This file documents what is filtered and why, so we have context when debugging and can make informed decisions about temporarily disabling filters.

> **Debugging note:** If you're chasing an issue and suspect something is being swallowed, temporarily remove the relevant entry from `logbegone.json`, relaunch, and reproduce. Re-add the filter once the issue is resolved.

---

## Active Filters

| Phrase / Pattern | Source | Reason |
|---|---|---|
| `Disconnecting VANILLA connection attempt` | Vanilla / NeoForge | Routine log noise when a vanilla client attempts to connect to a modded server. No action needed. |
| `Channels ` | NeoForge network | Channel negotiation messages on join. Normal handshake behaviour, fires repeatedly and adds no diagnostic value. |
| `Received updated config value for` | Artifacts | Server syncs every Artifacts config value to the client on each world join — produces ~100 DEBUG lines per session. All normal. |
| `constructing map region data for` | FTB Chunks | Routine map tile construction on join. Expected behaviour, high volume. |
| `reading data from` | FTB Chunks | Companion to the above — reading cached map tile zip files. Expected behaviour, high volume. |
| `[Dev] Creative tab railways:` | Railways (Create: Steam 'n' Rails) | Dev-mode logging left in the stable release jar. Reports creative tab entry counts 3× per world join and resource reload. No diagnostic value. |
