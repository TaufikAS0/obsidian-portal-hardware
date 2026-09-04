# TGC — Telemetric Ground Checker

> Produk baru (2026-09-01). Firmware belum tersedia — semua metadata
> hardware dan repo masih UNCONFIRMED. Berbeda dari HGC, TGC15, dan
> TGC30 (lihat batasan identitas di bawah).

## Identity

| Field | Value |
|---|---|
| Code | `TGC` |
| Product name | `Telemetric Ground Checker` |
| Catalog group | `Main Products` |
| Type | `Safety Checker & Logging` |
| Model | `Ground Checker` |
| Firmware repo (local) | UNCONFIRMED — belum ditemukan repo firmware TGC |
| Firmware repo (GitHub) | UNCONFIRMED — pencarian GitHub 2026-09-01 tidak menemukan repo firmware TGC (`TaufikAS0/2026-telemetric-ground-checker` = 404; satu-satunya hasil "TGC telemetric" adalah proyek drone yang tidak berhubungan) |
| Library manifests | `telemetric-firmware-library/manifests/TGC/` (belum ada — jangan buat tanpa BIN nyata) |
| Portal | https://192.168.1.122:8443/products/TGC |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| — | belum ada | `<TGC-v…>` | belum ada firmware | Jangan buat manifest tanpa BIN nyata; jangan menyalin firmware produk lain |

## Hardware

| Field | Value |
|---|---|
| MCU / board | UNCONFIRMED |
| Chip family | UNCONFIRMED (jangan diasumsikan ESP32-S3 atau mewarisi bootstrap TMM) |
| Flash size / mode | UNCONFIRMED |
| Partition scheme | UNCONFIRMED |
| Flash method | Web Serial via portal (typical, setelah firmware tersedia) |
| Wi-Fi firmware | UNCONFIRMED |

## Lessons for the next AI

- TGC didaftarkan di katalog portal dan library lebih dulu, sebelum firmware
  ada — ikuti alur yang sama untuk produk lain: katalog → registry → note
  produk → baru kemudian firmware.
- Bootstrap TMM ([[TMM Bootstrap Implementation History]]) terikat profil
  `TMM_V6_R0_M0` dan TIDAK otomatis berlaku untuk TGC. Jika TGC nanti butuh
  bootstrap, buat hardware profile dan package sendiri mengikuti
  [[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]].
- Flash tetap nonaktif sampai firmware TGC dengan hardware profile yang
  cocok tersedia di library.

## Evidence pointers

- QC records: portal database (not Git)
- Registry: [[01_Registry/PRODUCTS|PRODUCTS]] ·
  [[01_Registry/FIRMWARE_REPOS|FIRMWARE_REPOS]]
