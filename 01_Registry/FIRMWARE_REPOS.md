# Firmware Repository Registry

One row per product firmware repository. This is the most important file in the
vault: it is how every AI knows **which GitHub repo holds which product's
firmware source**.

Rules for maintaining this table: see `../02_Rules/registry-rules.md`.

- Status vocabulary: `confirmed` | `unconfirmed` | `retired`
- Any unverifiable field MUST be the literal `UNCONFIRMED`. Never guess.
- A new firmware repository MUST be registered here in the same AI session
  that creates it.

## Registered product firmware repositories

| Code | Product | Local path | GitHub repo | Latest known release | Status |
|---|---|---|---|---|---|
| TMM | Telemetric Module Master | `D:\Home Work\Software Github\2026-telemetric-module-master` | https://github.com/TaufikAS0/2026-telemetric-module-master | v0.5.0 (manifests 0.1.0–0.5.0) | confirmed |
| TVG | Telemetric Vision Grid | UNCONFIRMED | UNCONFIRMED (no firmware source repo found on GitHub; only `pcb-vision-grid` and `3d-telemetric-vision-grid` exist) | v1.4.3 (manifests 1.4.2, 1.4.3; pilot flash done on ESP32-S3) | unconfirmed |
| TPM | Telemetric Power Monitor | UNCONFIRMED (portal README references its INA3221 source repo) | UNCONFIRMED (candidate: https://github.com/TaufikAS0/2026-esp32s3-solar-power-monitor-ina3221 — repo exists and matches INA3221 hardware, but no manifest/product-code verification found) | v0.16.24 | unconfirmed |

## How to promote an `unconfirmed` row to `confirmed`

1. Locate the repository on disk (search `D:\Home Work\Software Github` for the
   product code or name).
2. Verify with `git remote -v` that the GitHub URL matches.
3. Verify the product code appears in the repo's build output/manifest.
4. Replace the `UNCONFIRMED` cells, set status `confirmed`, add a line to
   `../00_Hub/STATUS.md` describing what was verified.
