# TMM — Telemetric Module Master

> [[TMM Bootstrap Implementation History]] — riwayat package bootstrap TMM ·
> [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]] ·
> [[02_Rules/firmware-package-rules|Firmware Package Rules]] ·
> [[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]]

## Identity

| Field | Value |
|---|---|
| Code | `TMM` |
| Product name | Telemetric Module Master |
| Catalog group | Main Products |
| Firmware repo (local) | `D:\Home Work\Software Github\2026-telemetric-module-master` |
| Firmware repo (GitHub) | https://github.com/TaufikAS0/2026-telemetric-module-master |
| Bootstrap framework | `2026-telemetric-device-bootstrap` (lihat [[TMM Bootstrap Implementation History]]) |
| Library manifests | `telemetric-firmware-library/manifests/TMM/` |
| Portal | https://192.168.1.122:8443/products/TMM |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 0.1.0 | `manifests/TMM/0.1.0.json` | `TMM-v0.1.0` | quarantined | |
| 0.2.0 | `manifests/TMM/0.2.0.json` | `TMM-v0.2.0` | quarantined | |
| 0.3.0 | `manifests/TMM/0.3.0.json` | `TMM-v0.3.0` | quarantined | |
| 0.4.0 | `manifests/TMM/0.4.0.json` | `TMM-v0.4.0` | quarantined | |
| 0.5.0 | `manifests/TMM/0.5.0.json` | `TMM-v0.5.0` | retired | |
| 0.6.0 | `manifests/TMM/0.6.0.json` | `TMM-v0.6.0` | approved | RS485 Modbus QC + tutorial |
| 0.6.1 | (portal record only; manifest tidak ada di library — diimpor manual) | — | approved | latest application |
| 0.1.0-bootstrap.1 | `manifests/TMM/0.1.0-bootstrap.1-full.json` + `-app-only.json` | `TMM-v0.1.0-bootstrap.1` (draft) | draft | **bootstrap**, `stage=lab`, `firmwareRole=bootstrap`, releaseId `TMM-0.1.0-bootstrap.1-9648a0c` — lihat [[TMM Bootstrap Implementation History]] |

Lifecycle di atas dibaca langsung dari database portal (2026-09-01).

Operator↔AI notes: `telemetric-firmware-library/notes/TMM/<VERSION>/`

## Hardware

| Field | Value |
|---|---|
| MCU / chip family | ESP32-S3 (CONFIRMED — profile evidence D-026) |
| Flash size / mode | 16MB / qio (CONFIRMED — live device-info) |
| Partition scheme | `tmm-ota-4mb` (CONFIRMED — D-024/D-026) |
| Wi-Fi | station + AP (CONFIRMED — live QC session 2026-08-31) |
| Ethernet | UNCONFIRMED — fitur disabled di bootstrap |
| Flash method | Web Serial via portal (merged BIN) + OTA/LAN (app BIN) |

Sumber bukti: `profiles/TMM_V6_R0_M0/profile.json` di repo bootstrap.

## Lessons for the next AI

- Produk pertama dengan package bootstrap dual-artifact lengkap
  (`manifest-full.json` + `manifest-app-only.json`, satu `releaseId`) —
  jadikan referensi format untuk produk baru:
  [[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]].
- Bootstrap TMM hanya terikat profil `TMM_V6_R0_M0`; revisi hardware lain
  butuh package bootstrap sendiri.
- Sesi OTA-bootstrap fisik belum dilakukan — jangan menandai package
  bootstrap ini ready tanpa bukti fisik.

## Evidence pointers

- QC records: portal database (not Git)
- Bootstrap profile evidence: `profiles/TMM_V6_R0_M0/profile.json` (repo
  bootstrap)
- Portal importer audit: `firmware_library_auto_imported` 2026-09-01T01:54Z
  (dua record, checksum unduhan terverifikasi)
