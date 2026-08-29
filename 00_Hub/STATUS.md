# Vault Status

Updated: 2026-08-30

| Item | State |
|---|---|
| Vault created | 2026-08-30 |
| Central repos registered | 2 of 2 (portal + library) |
| Product firmware repos registered | 1 confirmed (TMM), 2 UNCONFIRMED (TVG, TPM) |
| Products in catalog | 37 codes |
| Library manifests published | TMM 0.1.0–0.5.0, TPM 0.16.24, TVG 1.4.2, 1.4.3 |

## Open registry gaps (any AI may pick these up)

1. Confirm the local path and GitHub repo for **TVG** (Telemetric Vision Grid) firmware source. Note (2026-08-30): searched GitHub — only `pcb-vision-grid` (PCB) and `3d-telemetric-vision-grid` (3D design) exist; no firmware source repo found.
2. Confirm the local path and GitHub repo for **TPM** (Telemetric Power Monitor, INA3221) firmware source. Candidate verified to exist: `2026-esp32s3-solar-power-monitor-ina3221` — promotion to `confirmed` requires product-code verification in its manifest/build output, which was not found in repo files.
3. Confirm whether `2026-esp32-solar-power-monitor-backend-server` is TPM-related tooling or unrelated.
4. Register product firmware repos here as they are created for the remaining catalog codes.

## Maintenance log

### 2026-08-30 — GitHub tidying session (laptop-utama, per NEXT_AI_PROMPT)

Done via GitHub API (token TaufikAS0):

1. **Descriptions** set on all 8 registry repos owned by TaufikAS0 (portal, library, TMM firmware, 2 tools, Bardi CCTV, 2 vaults) in the format "role + product - Telemetric Hardware Portal ecosystem".
2. **Topics** set (lowercase): `telemetric` + role (`hardware-portal` / `firmware-library` / `firmware` / `tool` / `obsidian-vault`) + product code (`tmm`, `icp`) where specific.
3. **README ecosystem links** added to 7 repos that were missing them (portal, library, TMM, backend-server, ICP-STM32-Web-Control, Bardi CCTV, ai-collaboration-vault). `obsidian-portal-hardware` already complete (links portal + library + ai-collaboration-vault).
4. **ESP IP Scanner registered**: GitHub repo found and verified via API (`esp_ip_scanner`, private); `TOOL_REPOS.md` updated from "none (local only)".

Not done / manual steps:

- **Pinned repositories**: GitHub has no API to set profile pinned repos. Pin manually in this order: 1) telemetric-hardware-portal, 2) telemetric-firmware-library, 3) obsidian-portal-hardware, 4) 2026-telemetric-module-master.

Visibility observations (recorded only, nothing changed):

- `2026-telemetric-module-master` (TMM firmware source) is PUBLIC while portal and library are private — review whether the firmware source should be private.
- `2026-esp32s3-solar-power-monitor-ina3221` (TPM candidate) is PUBLIC.
- `2026-06-Bardi-CCTV-Web` is PUBLIC and unrelated to the ecosystem — candidate for archiving.
- No registry repos are archived or forks.

### Registry updates this session

- `REGISTRY UPDATE: 01_Registry/TOOL_REPOS.md | ESP IP Scanner GitHub repo registered (esp_ip_scanner) | verified via GitHub API repos/TaufikAS0/esp_ip_scanner`
- `REGISTRY UPDATE: 01_Registry/FIRMWARE_REPOS.md | TPM candidate repo noted (2026-esp32s3-solar-power-monitor-ina3221), status stays unconfirmed | verified via GitHub API; product-code verification not found`
- `REGISTRY UPDATE: 00_Hub/STATUS.md | maintenance log + visibility observations + TVG search result | verified via GitHub repo list and tree search`
