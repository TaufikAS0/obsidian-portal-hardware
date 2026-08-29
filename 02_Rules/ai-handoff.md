# AI Handoff Protocol

AIs work in different sessions, different repos, sometimes different machines.
They cannot talk directly. Handoff happens through three channels.

## Channel 1 — This vault's registry (structure)

"Where is it and what is it called?"

- New/changed/retired repositories → `01_Registry/` tables (see `registry-rules.md`)
- Product-level knowledge (chip, flashing notes, pitfalls) → `03_Products/<CODE>.md`

## Channel 2 — JSON notes in the repos (work conversation)

"What happened in this version?"

- Firmware: `telemetric-firmware-library/notes/<CODE>/<VERSION>/*.json`
  (append-only operator↔AI conversation; rules in `<library>/AGENTS.md`)
- Website: `telemetric-hardware-portal/website-notes/*.json`
  (bug reports and AI replies; rules in `<portal>/AGENTS.md`)

Never delete or rewrite these notes. Always append with a new unique `id`,
current ISO timestamp, `authorType: "ai"`, and the correct `source`
(`firmware-ai` or `portal-ai`).

## Channel 3 — Git history (audit)

Commit format follows `ai-collaboration-vault/00_Hub/DEVICES.md`:

`[device:<name>] [project:<slug>] <summary>`

## Handoff checklist (end of every session)

1. Registry updated? (if any repo/location changed)
2. Product note updated? (if product-specific facts were learned)
3. JSON note appended? (if work happened inside portal or library)
4. `REGISTRY UPDATE:` line included in the final report? (if applicable)
5. No secrets, BIN files, or guessed values written anywhere?
