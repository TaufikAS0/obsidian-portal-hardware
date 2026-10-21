# Vault Status

## 2026-10-21 - AOM V1 R0 QC integration

Registered `D:\Home Work\Firmware Github\esp32-hardware-test-manifold` from its
verified Git remote. Owner selected catalog AOM (not ANM/AGM) and confirmed PCB
V1 R0. Baseline c02c4f2/1.6.3; integration source 912efc6/1.6.4 on
feature/portal-manifold-qc adds ordered primary/secondary non-blocking Wi-Fi and
read-only AOM identity. Package is draft/built, role qc, stage lab; target
ESP32/4MB/DIO is a build choice, fitted MCU/flash remains UNCONFIRMED. No flash,
physical network/output/sensor/OTA test or QC PASS. See [[03_Products/AOM]].
Unrelated graph/canvas/firmware-package-rules changes are preserved.
Build passed, actual partitions/merged-app/size/hash verified. Draft release
`AOM-1.6.4-912efc6` contains four assets; publisher re-download verification
passed. Library gate passed twice (31 tests; 54 manifests). No physical tests.
Portal import verified exactly two records under one releaseId, Hardware QC/LAB,
both stored-file hashes/sizes correct, /products/AOM HTTPS 200.

## 2026-10-12 - Compact LAB distribution

Owner-approved public LAB credential policy added in 02_Rules/lab-default-credentials.md.
TMC QC repository registered from verified Git remote and feature/qc-operator-ota.
App-only distribution preserves legacy NVS/storage; hardware test remains pending.
Unrelated local graph/canvas and firmware-package-rules edits were preserved.

Updated: 2026-09-16 (TTB Telemetric Test Bench v0.8.0-testing.1 dual-artifact draft published)

| Item | State |
|---|---|
| Vault created | 2026-08-30 |
| Central repos registered | 2 of 2 (portal + library) |
| Product firmware repos registered | 3 confirmed (TMM, TGC, TTB), 2 UNCONFIRMED (TVG, TPM) |
| Products in catalog | 39 codes |
| Library manifests published | TMM 0.1.0–0.5.0, 0.6.0, 0.6.2 (dual-artifact QC), 0.6.1 (portal only), 0.1.0-bootstrap.1 (dual-artifact bootstrap), TGC 0.1.0-initial.1 (dual-artifact bootstrap), TPM 0.16.24, TVG 1.4.2, 1.4.3, TTB 0.8.0-testing.1 (dual-artifact testing/LAB) |

## Open registry gaps (any AI may pick these up)

1. Confirm the local path and GitHub repo for **TVG** (Telemetric Vision Grid) firmware source. Note (2026-08-30): searched GitHub — only `pcb-vision-grid` (PCB) and `3d-telemetric-vision-grid` (3D design) exist; no firmware source repo found.
2. Confirm the local path and GitHub repo for **TPM** (Telemetric Power Monitor, INA3221) firmware source. Candidate verified to exist: `2026-esp32s3-solar-power-monitor-ina3221` — promotion to `confirmed` requires product-code verification in its manifest/build output, which was not found in repo files.
3. Confirm whether `2026-esp32-solar-power-monitor-backend-server` is TPM-related tooling or unrelated.
4. Register product firmware repos here as they are created for the remaining catalog codes.

## Maintenance log

### 2026-09-16 — TTB v0.8.0-testing.1 dual-artifact draft published

- Package `TTB-0.8.0-testing.1-bac4da5` (firmwareRole=testing, stage=lab, ESP32 classic 4MB/qio/min_spiffs, `wifiCapable`) published via `publish-package` to draft release `TTB-v0.8.0-testing.1-esp32` (4 assets: 2 BIN + 2 manifest; publisher download checksum verified; independent re-download re-verified size + SHA-256).
- Source repo `2026-05-esp-logger` pushed normally: local HEAD = origin/develop = ls-remote = `bac4da58c26dc23fc1342c4291e7d5c21d750ae7`.
- Portal auto-synced exactly 2 records (full offset 0 + app-only offset 0x10000), no duplicates by releaseId+imageType; Testing/LAB container shows 1 card; USB→merged/full, OTA→app-only.
- Evidence level `built` (compile/build + artifact validation only): no bench test, no QC pass, no flash, no hardware/peripheral verification. Hardware revision/profile and all physical verification remain UNCONFIRMED/PENDING; portal profile stored as `UNCONFIRMED`.
- Registry: `FIRMWARE_REPOS.md` TTB row added as `confirmed`; `PRODUCTS.md` TTB row added (Support Tools, 39 codes); `03_Products/TTB.md` created from template.
- Library manifests add the fields the source build tools did not emit (`schemaVersion`, `erasePolicy: prompt`, `wifiCapable`, `releaseNotes`, sourceCreatedAt from build metadata); no BIN and no firmware source was rebuilt or modified.

### 2026-09-07 - TGC Research v0.9.0-research.1 dual-target published

- Two TGC Research packages (firmwareRole=testing, stage=lab) published as separate draft releases:
  - ESP32 klasik 4MB: releaseId `TGC-0.9.0-research.1-ee199aa-esp32`, tag `TGC-v0.9.0-research.1-esp32`
  - ESP32-S3 16MB: releaseId `TGC-0.9.0-research.1-ee199aa-esp32s3`, tag `TGC-v0.9.0-research.1-esp32s3`
- Portal imported 4 records (2 per target); Testing/LAB container shows 2 cards with correct chip/flash/profile.
- Publisher publish-package fixed to use per-target releaseTag from manifest.
- Build source commit ee199aa; HEAD 65fb0f5 (docs-only diff).
- Physical flash/provision/OTA still pending. Research stage: ground resistance UNCALIBRATED.
## Maintenance log

### 2026-09-07 — TGC ESP32 classic source package verified

- Repo `2026-telemetric-ground-checker` verified at `main` HEAD `95cf011`;
  firmware source commit `cdd1945` is an ancestor of that HEAD.
- Latest source package is `TGC-0.2.0-initial.1-cdd1945`, profile
  `TGC_LAB_ESP32_4M`, ESP32 classic 4MB/dio, `firmwareRole=bootstrap`,
  `stage=lab`.
- Independent re-hash matched both manifests: app-only 998,704 bytes
  (`6fd37920…a737d`) and merged 4,194,304 bytes (`1073857f…5594`). Repo tests
  passed 44/44.
- No matching manifest was found in the central firmware library and no matching
  portal data was found. Publication/import remains assigned to the portal/library
  worker; the already-published ESP32-S3 16MB package remains unchanged.
- Classic ESP32 physical detection, flash, provisioning, and OTA remain
  UNCONFIRMED. Compile success is not physical hardware proof.

### 2026-09-04 - TMM v0.6.2 Hardware QC published

- Dual-artifact package `TMM-0.6.2-bdc13c0` (firmwareRole=qc, stage=lab) published via publish-package to draft release TMM-v0.6.2 (4 assets, download checksum verified).
- Portal auto-synced: exactly 2 records (full + app-only). Bootstrap 0.1.0-bootstrap.1 intact in Initial/Setup. Application firmware (0.1.0-0.6.1) hidden per portal policy.
- TMM firmware repo commit 556e0e1 only untracked BINs (bdc13c0 build unchanged).
- OTA partition compatibility: tmm-ota-4mb only; different layouts need USB merged flash.
- Physical flash/QC/OTA on hardware still pending.
## Maintenance log

### 2026-09-04 — TGC Initial package published and verified in portal

- Package `TGC-0.1.0-initial.1-24113fe` (bootstrap, lab) published via
  `publish-package` to draft release `TGC-v0.1.0-initial.1` (4 assets: 2 BIN +
  2 manifest); download checksum verified by publisher.
- Portal auto-synced: exactly 2 records (full + app-only) with
  `firmwareRole=bootstrap`, `stage=lab`.
- UI verified: one card in Initial/Setup container (cyan), LAB BOOTSTRAP
  badge, ESP32-S3 / 16MB / `tgc-ota-16mb` displayed, USB→merged, OTA→app-only.
- FIRMWARE_REPOS.md: TGC row promoted to `confirmed` (local path and GitHub
  repo verified).
- Physical flash/provision/OTA on TGC hardware still pending.
- COM6: UNCONFIRMED. ESP32 classic: UNCONFIRMED.

### 2026-09-04 — Produk baru: TGC (Telemetric Ground Checker)

- TGC (Safety Checker & Logging, Main Products) ditambahkan ke katalog portal
  (seed idempoten `INSERT OR IGNORE`) dan katalog library → 38 produk.
- Registry: baris baru di `01_Registry/PRODUCTS.md` dan
  `01_Registry/FIRMWARE_REPOS.md` (status `unconfirmed`);
  `03_Products/TGC.md` dibuat dari template; Hub README menautkan TGC.
- Pencarian GitHub (2026-09-04): tidak ada repo firmware TGC
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
