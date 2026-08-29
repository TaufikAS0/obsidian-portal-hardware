# Registry Rules

The registry is the shared memory of all AIs. These rules keep it parseable and
trustworthy.

## 1. Register-in-session rule

Any repository created, cloned, renamed, discovered, or retired MUST be
reflected in the matching registry file **in the same AI session**, before the
final report. End the session with a
`REGISTRY UPDATE: <file> | <change> | <verification>` line.

## 2. No-guessing rule

Any field that cannot be verified MUST be the literal `UNCONFIRMED` — never a
guessed URL, path, or version. `UNCONFIRMED` is a first-class status, not an
error.

## 3. Verification rule

A row may only be marked `confirmed` after checking the actual `git remote -v`
(or the live folder for local-only tools). Note how you verified in
`../00_Hub/STATUS.md`.

## 4. Append-and-archive rule

- Never hard-delete a registry row. Retired rows move to `../99_Archive/`
  with a date, reason, and the last known values.
- Version history stays in Git; do not keep change logs inside the tables.

## 5. Table format rule

Keep the exact column order of each table so scripts and AIs can parse it:

- `FIRMWARE_REPOS.md`: `| Code | Product | Local path | GitHub repo | Latest known release | Status |`
- `TOOL_REPOS.md`: `| Name | Role | Local path | GitHub repo | Status |`
- `PRODUCTS.md`: `| Code | Name | Firmware repo |`

## 6. Single-source rule

- Product code list: only `telemetric-firmware-library/catalog/products.json`
  may introduce or retire codes. `PRODUCTS.md` mirrors it.
- Governance: only the canonical rule in `ai-collaboration-vault` may change
  ecosystem boundaries. This vault links, it does not legislate.
- If this vault and a repo's own docs disagree, the repo's docs win for repo
  internals; this vault wins for locations and GitHub names.

## 7. Scope rule

One row per repository. Never merge two products into one repo row, and never
split one product across multiple repos without one row per repo.
