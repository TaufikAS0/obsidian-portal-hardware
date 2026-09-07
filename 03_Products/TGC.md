# TGC — Telemetric Ground Checker

> Produk baru (2026-09-04). Package bootstrap Initial ESP32-S3 sudah di-publish
> dan tampil di portal. Package ESP32 klasik 4MB yang lebih baru sudah dibangun
> di repo sumber, tetapi belum dipublish ke library atau diimpor portal.
> Firmware fisik belum di-flash — pengujian perangkat masih pending. Berbeda
> dari HGC, TGC15, dan TGC30.
>
> **Kontrak manifest untuk AI firmware TGC** (GLM bawah): gunakan
> `firmwareRole` sesuai fungsi — `"bootstrap"` untuk Initial/Setup,
> `"testing"` untuk LAB eksplorasi, `"qc"` untuk Hardware QC. Portal tidak
> menampilkan firmware `"application"`. Lihat [[02_Rules/firmware-package-rules|Firmware
> Package Rules]] dan [[04_Guides/Bootstrap Build and Publish SOP|Build and
> Publish SOP]].

## Identity

| Field | Value |
|---|---|
| Code | `TGC` |
| Product name | `Telemetric Ground Checker` |
| Catalog group | `Main Products` |
| Type | `Safety Checker & Logging` |
| Model | `Ground Checker` |
| Firmware repo (local) | `D:\Home Work\Software Github\2026-telemetric-ground-checker` |
| Firmware repo (GitHub) | https://github.com/TaufikAS0/2026-telemetric-ground-checker |
| Library manifests | `telemetric-firmware-library/manifests/TGC/` |
| Portal | https://192.168.1.122:8443/products/TGC |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 0.2.0-initial.1 | Build output repo sumber: `manifest-full.json` + `manifest-app-only.json` | `TGC-v0.2.0-initial.1` (belum dipublish) | belum diimpor | **bootstrap**, `stage=lab`, `firmwareRole=bootstrap`, releaseId `TGC-0.2.0-initial.1-cdd1945`; target ESP32 klasik 4MB, verifikasi fisik pending |
| 0.1.0-initial.1 | `manifests/TGC/0.1.0-initial.1-full.json` + `-app-only.json` | `TGC-v0.1.0-initial.1` (draft) | draft | **bootstrap**, `stage=lab`, `firmwareRole=bootstrap`, releaseId `TGC-0.1.0-initial.1-24113fe` |
| 0.9.0-research.1 (ESP32) | `manifests/TGC/0.9.0-research.1-esp32-full.json` + `-esp32-app-only.json` | `TGC-v0.9.0-research.1-esp32` (draft) | draft | **testing**, `stage=lab`, `firmwareRole=testing`, releaseId `TGC-0.9.0-research.1-ee199aa-esp32`, ESP32 / 4MB / dio |
| 0.9.0-research.1 (ESP32-S3) | `manifests/TGC/0.9.0-research.1-esp32s3-full.json` + `-esp32s3-app-only.json` | `TGC-v0.9.0-research.1-esp32s3` (draft) | draft | **testing**, `stage=lab`, `firmwareRole=testing`, releaseId `TGC-0.9.0-research.1-ee199aa-esp32s3`, ESP32-S3 / 16MB / qio |

Operator↔AI notes: `telemetric-firmware-library/notes/TGC/0.1.0-initial.1/` dan `notes/TGC/0.9.0-research.1/`

## Hardware profiles

| Profile | Chip / flash | Partition | Evidence | Status |
|---|---|---|---|---|
| `TGC_LAB_ESP32S3_16M` | ESP32-S3 / 16MB / qio | `tgc-ota-16mb` | read-only chip detection pada board | package 0.1.0 dipublish; flash fisik pending |
| `TGC_LAB_ESP32_4M` | ESP32 klasik / 4MB / dio | custom OTA, slot 1,966,080 byte | compile target + manifest; **bukan** deteksi board fisik | package 0.2.0 sudah dibangun; library/portal/flash pending |
| `TGC_RESEARCH_ESP32_4M` | ESP32 / 4MB / dio | `tgc-research-ota-4mb` | compile + manifest; ADS1115 research firmware | package 0.9.0-research.1 ESP32 **dipublish**; flash fisik pending |
| `TGC_RESEARCH_ESP32S3_16M` | ESP32-S3 / 16MB / qio | `tgc-research-ota-16mb` | compile + manifest; ADS1115 research firmware | package 0.9.0-research.1 ESP32-S3 **dipublish**; flash fisik pending |

Kedua profile memakai merged BIN untuk USB dan app-only BIN untuk OTA/LAN.
Ethernet dan physical setup control tetap UNCONFIRMED/disabled sampai ada bukti
perangkat. Sumber bukti ada di `profiles/` dan `docs/HANDOFF-ESP32-CLASSIC.md`
di repo firmware TGC.

**Research firmware (v0.9.0-research.1)**: ADS1115 A0 sampling, dashboard,
raw logging, NVS model/calibration, recovery AP, dan portal contract
(`/api/device-info`, mDNS `_telemetric-ota._tcp`, OTA multipart).
Ground resistance values UNCALIBRATED — tidak ada klaim QC PASS.
OTA secret per perangkat di-provision via `POST /api/ota/password`, bukan
embedded dalam BIN.

## Lessons for the next AI

- Bootstrap TGC menggunakan framework yang sama dengan TMM
  ([[TMM Bootstrap Implementation History]]) tapi dengan profile dan
  partition sendiri (`TGC_LAB_ESP32S3_16M`, `tgc-ota-16mb`).
- HEAD terbaru repo sumber adalah `95cf011` (handoff documentation). Firmware
  klasik terbaru dibangun dari commit `cdd1945`, yang terbukti ancestor HEAD.
- Package klasik `0.2.0-initial.1` berisi app-only 998,704 byte (SHA-256
  `6fd37920004bd9e4e2359917f178dfd838b443a0839403e5b54aaec9972a737d`)
  dan merged 4,194,304 byte (SHA-256
  `1073857fdb867b872c5ed936c6da8afa191f725e9ce6b7b34d8bb1682ebb5594`).
  Kedua hash diverifikasi ulang 2026-09-07; test repo 44/44 lulus.
- COM6 masih UNCONFIRMED — jangan flash tanpa verifikasi port dan profil.
- ESP32 klasik belum diuji fisik. Label portal harus menyebut ESP32 / 4MB dan
  status build target/pending, bukan menyebutnya board-proven.
- Jangan mengganti atau menggabungkan package ESP32-S3 16MB dengan package
  ESP32 klasik 4MB; keduanya profile hardware berbeda.

## Evidence pointers

- QC records: portal database (not Git)
- Registry: [[01_Registry/PRODUCTS|PRODUCTS]] ·
  [[01_Registry/FIRMWARE_REPOS|FIRMWARE_REPOS]]
- Portal importer audit: `firmware_library_auto_imported` × 2 untuk
  `TGC-0.1.0-initial.1-24113fe`
- Source package pending: `TGC-0.2.0-initial.1-cdd1945`; belum ditemukan di
  manifest library maupun data portal pada pemeriksaan 2026-09-07.
