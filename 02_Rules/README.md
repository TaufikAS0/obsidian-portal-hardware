# 02 Rules — How This Vault Is Maintained

| Rule file | Purpose |
|---|---|
| [[02_Rules/ai-entry-protocol|AI Entry Protocol]] | README-first rule and mandatory reading route for every AI |
| `registry-rules.md` | Exact formats and lifecycle for every registry table |
| `ai-handoff.md` | How AIs hand off information to each other |

Every AI starts from the root `README.md`, then follows root `AGENTS.md` and
[[02_Rules/ai-entry-protocol|AI Entry Protocol]].

## What belongs here vs elsewhere

- Location, GitHub names, ownership pointers → **this vault** (`01_Registry/`)
- Governance rules (source of truth, lifecycle, safety) →
  `ai-collaboration-vault/03_Rules/telemetric-firmware-ecosystem.md` (canonical)
- Repo-internal working rules → each repo's own `AGENTS.md`
