# Rules for AI in this vault

Any AI (Claude, Codex, or any other assistant) that works on any Telemetric
Hardware Portal ecosystem repository MUST follow this protocol.

## Before doing any work

1. Read `00_Hub/README.md` for the ecosystem map.
2. Read `01_Registry/CENTRAL_REPOS.md` and `01_Registry/FIRMWARE_REPOS.md`
   to learn where everything lives and which GitHub repo it belongs to.
3. Read `02_Rules/firmware-package-rules.md` (mandatory). One firmware
   version = one package = one merged/full BIN (USB) + one app-only BIN
   (OTA/LAN) + one manifest, all bound by one `releaseId`.
4. Read `02_Rules/device-bootstrap-standard.md` for provisioning, fallback AP,
   LAN discovery, OTA, or recovery work.
5. If your task involves a specific product, read that product's note in
   `03_Products/<CODE>.md`. If it does not exist yet, create it from
   `03_Products/_TEMPLATE.md`.

## The registry is the message board

AIs cannot talk to each other directly. The registry is how they inform each
other. Therefore:

1. **Register before you finish.** If you created, cloned, renamed, or
   discovered any repository, you MUST update the matching registry file in
   `01_Registry/` in the same session, before your final report.
2. **Never leave a new firmware repository unregistered.** A firmware repo that
   exists on disk or on GitHub but is missing from
   `01_Registry/FIRMWARE_REPOS.md` is treated as a defect.
3. **Use the literal value `UNCONFIRMED`** for any field you cannot verify.
   Never guess a GitHub URL or local path. Guessing poisons the registry.
4. **Never hard-delete a registry row.** Move retired rows to `99_Archive/`
   with a date and reason.
5. Follow the exact table format defined in `02_Rules/registry-rules.md` so
   other AIs can parse the tables reliably.

## When working inside other ecosystem repos

- Portal repo rules: `telemetric-hardware-portal/AGENTS.md` (website-notes JSON protocol)
- Library repo rules: `telemetric-firmware-library/AGENTS.md` (notes JSON protocol, gate, publish)
- Canonical governance: `ai-collaboration-vault/03_Rules/telemetric-firmware-ecosystem.md`

Those rules are authoritative inside their own repos. This vault only adds the
location/registry layer on top.

## Safety (inherited from the canonical rule)

- BIN files belong in GitHub Release assets, never in Git history.
- Never commit credentials, keys, passwords, databases, or production logs.
- Publishing firmware is not approval. The local portal alone owns flash
  permission, lifecycle, and QC.
- Do not treat a GitHub Release as permission to flash.

## Completion report

End every session that touched ecosystem structure with one line per change:

`REGISTRY UPDATE: <file> | <what changed> | <verified how>`
