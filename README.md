# Obsidian Portal Hardware Vault

Dedicated Obsidian coordination vault for the **Telemetric Hardware Portal ecosystem**.

This vault is the single place where every AI and human records and looks up:

- **where** every repository lives on disk (local path),
- **which GitHub repository** it belongs to,
- **which firmware repository** belongs to which product code.

There is exactly **one** web portal, exactly **one** firmware library, and
**many** product firmware repositories that will keep growing. This vault keeps
that growth tidy and searchable.

Planned GitHub repository: `TaufikAS0/obsidian-portal-hardware` (private).

## Start here

1. `AGENTS.md` — mandatory rules for any AI opening this vault
2. `00_Hub/README.md` — ecosystem overview and entry map
3. `01_Registry/FIRMWARE_REPOS.md` — the firmware repository registry (most important file)
4. `01_Registry/CENTRAL_REPOS.md` — the one portal and the one library

## Folder layout

| Folder | Purpose |
|---|---|
| `00_Hub/` | Entry point, ecosystem overview, vault status |
| `01_Registry/` | Machine-readable-by-humans registry of paths, repos, products, devices |
| `02_Rules/` | How the registry must be maintained and how AIs hand work to each other |
| `03_Products/` | One note per product that has firmware, using the template |
| `99_Archive/` | Retired registry rows and old notes (never hard-delete) |

## Relationship to other documentation

- Canonical cross-repo governance: `ai-collaboration-vault` → `03_Rules/telemetric-firmware-ecosystem.md` (status: adopted 2026-08-26)
- Portal-side contract: `telemetric-hardware-portal/docs/TELEMETRIC_ECOSYSTEM.md`
- Library-side contract: `telemetric-firmware-library/docs/ECOSYSTEM_ARCHITECTURE.md`

This vault does not duplicate those rules. It **registers concrete locations**
and links to the canonical documents.
