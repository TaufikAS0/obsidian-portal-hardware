# 02 Rules — How This Vault Is Maintained

| Rule file | Purpose |
|---|---|
| `registry-rules.md` | Exact formats and lifecycle for every registry table |
| `ai-handoff.md` | How AIs hand off information to each other |

Mandatory entry rules for any AI are in the root `AGENTS.md`.

## What belongs here vs elsewhere

- Location, GitHub names, ownership pointers → **this vault** (`01_Registry/`)
- Governance rules (source of truth, lifecycle, safety) →
  `ai-collaboration-vault/03_Rules/telemetric-firmware-ecosystem.md` (canonical)
- Repo-internal working rules → each repo's own `AGENTS.md`
