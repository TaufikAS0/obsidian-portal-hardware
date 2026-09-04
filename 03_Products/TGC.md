# TGC — Telemetric Ground Checker

> Produk baru (2026-09-04). Package bootstrap Initial pertama sudah di-publish
> dan tampil di portal. Firmware fisik belum di-flash — pengujian perangkat
> masih pending. Berbeda dari HGC, TGC15, dan TGC30.
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
| 0.1.0-initial.1 | `manifests/TGC/0.1.0-initial.1-full.json` + `-app-only.json` | `TGC-v0.1.0-initial.1` (draft) | draft | **bootstrap**, `stage=lab`, `firmwareRole=bootstrap`, releaseId `TGC-0.1.0-initial.1-24113fe` |

Operator↔AI notes: `telemetric-firmware-library/notes/TGC/0.1.0-initial.1/`

## Hardware

| Field | Value | Evidence |
|---|---|---|
| Chip family | ESP32-S3 | board-proven (read-only chip detection) |
| Flash size | 16MB | profile `TGC_LAB_ESP32S3_16M` |
| Flash mode | qio | profile |
| Partition scheme | `tgc-ota-16mb` | profile |
| Ethernet | UNCONFIRMED — disabled | manifest `disabledFeatures` |
| Physical setup control | UNCONFIRMED — disabled | manifest `disabledFeatures` |
| COM port | UNCONFIRMED — belum diverifikasi | |
| Flash method | Web Serial via portal (merged BIN) + OTA/LAN (app BIN) | |

Sumber bukti: `profiles/TGC_LAB_ESP32S3_16M/profile.json` di repo firmware TGC.

## Lessons for the next AI

- Bootstrap TGC menggunakan framework yang sama dengan TMM
  ([[TMM Bootstrap Implementation History]]) tapi dengan profile dan
  partition sendiri (`TGC_LAB_ESP32S3_16M`, `tgc-ota-16mb`).
- `sourceCommit` build (`24113fe`) adalah ancestor dari HEAD (`ce72c11`);
  perbedaan hanya docs, tidak memengaruhi build.
- COM6 masih UNCONFIRMED — jangan flash tanpa verifikasi port dan profil.
- ESP32 klasik (non-S3) belum diuji — portal menampilkan ESP32-S3 / 16MB
  secara eksplisit di kartu bootstrap.

## Evidence pointers

- QC records: portal database (not Git)
- Registry: [[01_Registry/PRODUCTS|PRODUCTS]] ·
  [[01_Registry/FIRMWARE_REPOS|FIRMWARE_REPOS]]
- Portal importer audit: `firmware_library_auto_imported` × 2 untuk
  `TGC-0.1.0-initial.1-24113fe`
