# Vault Status

Updated: 2026-09-01 (TGC added)

| Item | State |
|---|---|
| Vault created | 2026-08-30 |
| Central repos registered | 2 of 2 (portal + library) |
| Product firmware repos registered | 1 confirmed (TMM), 3 UNCONFIRMED (TVG, TPM, TGC) |
| Products in catalog | 38 codes (TGC ditambahkan 2026-09-01) |
| Library manifests published | TMM 0.1.0–0.5.0, 0.6.0, 0.6.1, 0.1.0-bootstrap.1 (dual-artifact), TPM 0.16.24, TVG 1.4.2, 1.4.3 |

## Open registry gaps (any AI may pick these up)

1. Confirm the local path and GitHub repo for **TVG** (Telemetric Vision Grid) firmware source. Note (2026-08-30): searched GitHub — only `pcb-vision-grid` (PCB) and `3d-telemetric-vision-grid` (3D design) exist; no firmware source repo found.
2. Confirm the local path and GitHub repo for **TPM** (Telemetric Power Monitor, INA3221) firmware source. Candidate verified to exist: `2026-esp32s3-solar-power-monitor-ina3221` — promotion to `confirmed` requires product-code verification in its manifest/build output, which was not found in repo files.
3. Confirm whether `2026-esp32-solar-power-monitor-backend-server` is TPM-related tooling or unrelated.
4. Register product firmware repos here as they are created for the remaining catalog codes.

## Maintenance log

### 2026-09-01 — Produk baru: TGC (Telemetric Ground Checker)

- TGC (Safety Checker & Logging, Main Products) ditambahkan ke katalog portal
  (seed idempoten `INSERT OR IGNORE`) dan katalog library → 38 produk.
- Registry: baris baru di `01_Registry/PRODUCTS.md` dan
  `01_Registry/FIRMWARE_REPOS.md` (status `unconfirmed`);
  `03_Products/TGC.md` dibuat dari template; Hub README menautkan TGC.
- Pencarian GitHub (2026-09-01): tidak ada repo firmware TGC
  (`TaufikAS0/2026-telemetric-ground-checker` = 404; satu-satunya hasil
  "TGC telemetric" adalah proyek drone yang tidak berhubungan) → local path
  dan GitHub repo = UNCONFIRMED.
- TGC adalah produk BARU yang berbeda dari HGC, TGC15, dan TGC30 — ketiganya
  tetap utuh di katalog dan registry.
- Belum ada manifest/BIN TGC di library — manifest tanpa BIN nyata dilarang.
- Hardware TGC semua UNCONFIRMED; jangan mengasumsikan ESP32-S3 atau
  mewarisi bootstrap TMM.

### 2026-09-01 — AI README-first entry protocol

- Root `README.md` dijadikan pintu masuk wajib dengan routing bacaan sesuai
  jenis pekerjaan.
- Menambahkan `02_Rules/ai-entry-protocol.md` sebagai aturan kanonik sebelum AI
  menjalankan command atau mengubah file.
- Menghapus langkah firmware package lama yang duplikat di `AGENTS.md` dan
  mempertahankan kontrak dua BIN + dua manifest + satu `releaseId`.

### 2026-09-01 — Vault restrukturisasi: Guides, History, Map of Content

- Membuat `04_Guides/` (New Product Bootstrap Guide, Bootstrap Build and
  Publish SOP, New Product Bootstrap Checklist, AI Prompt - New Product
  Bootstrap) dan `05_History/` (TMM Bootstrap Implementation History,
  Firmware Package Architecture Decisions).
- Menghapus `04_Handbook/` (konten dimigrasi ke struktur baru).
- `00_Hub/README.md` dijadikan Map of Content dengan wikilink ke
  Registry, Rules, Products, Guides, dan History; seluruh guide saling
  terhubung; `03_Products/TMM.md` terhubung ke history, rules, dan guide.
- Memperbarui aturan lama: package memakai dua manifest (`manifest-full.json`
  + `manifest-app-only.json`), bukan satu `manifest.json`.
- Scan byte-level seluruh vault: tidak ada mojibake nyata. Karakter em-dash dan
  arrow lama adalah UTF-8 valid (E2 80 94 / E2 86 94); laporan mojibake
  sebelumnya adalah artefak tampilan konsol PowerShell 5.1.

### 2026-09-01 — Bootstrap handbook for new products

- Added `04_Handbook/` with four reusable documents:
  `bootstrap-tmm-history.md` (riwayat terverifikasi implementasi TMM),
  `bootstrap-new-product-guide.md` (panduan A–H untuk produk baru),
  `bootstrap-new-product-template.md` (checklist siap salin),
  `bootstrap-new-product-ai-prompt.md` (prompt siap salin untuk AI firmware).
- Linked the handbook from this hub README and made the guide mandatory
  reading in `AGENTS.md` for AI building bootstrap firmware for new products.
- Facts in the handbook were verified directly against repository commits
  (`f9fc81c`, `ca04068`, `9648a0c` in the bootstrap repo; `db11683`, `ed63cba`,
  `2b39e24` in the library; `c2ac55f`, `770ffc5` in the portal), the TMM
  release manifest `TMM-0.1.0-bootstrap.1-9648a0c`, and the portal database
  (two records imported 2026-09-01T01:54Z).
- Physical flashing of the bootstrap package has NOT been performed; the
  handbook states this explicitly.

### 2026-08-31 — Device bootstrap standard

- Created the shared `2026-telemetric-device-bootstrap` framework repository.
- Standardized stored Wi-Fi → factory Wi-Fi → unique fallback AP provisioning.
- Reserved `TELEMETRIC-SETUP-XXXXXX` and `Telemetric Device Setup` as the
  general operator identity.
- Kept BIN builds hardware-profile-specific and retained USB recovery beside
  authenticated A/B OTA.
- Registered the repository in `01_Registry/TOOL_REPOS.md`.
- Verified (2026-08-31): GitHub repo created PUBLIC at
  https://github.com/TaufikAS0/2026-telemetric-device-bootstrap (API
  `repos/TaufikAS0/2026-telemetric-device-bootstrap` returned owner, public
  visibility, default branch `main`); foundation pushed and local HEAD =
  origin/main = ls-remote = `f9fc81c`; 16/16 tests pass in the repo. The
  `confirmed` status in `TOOL_REPOS.md` is therefore backed by evidence.

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
