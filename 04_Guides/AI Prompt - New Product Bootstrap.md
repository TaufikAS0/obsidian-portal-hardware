# AI Prompt - New Product Bootstrap

> Prompt siap salin untuk AI yang membangun package bootstrap produk baru.
> Untuk manusia: isi bagian `[...]` sebelum menyalin. Checklist penutup:
> [[New Product Bootstrap Checklist]]. Panduan: [[New Product Bootstrap Guide]].

---

Kamu akan membuat package firmware bootstrap untuk produk `[<productCode>]`
dengan framework Telemetric Device Bootstrap.

**Baca dulu, sebelum bekerja:**

1. `AGENTS.md` di repo `2026-telemetric-device-bootstrap` dan aturan
   `docs/BOOTSTRAP_STANDARD.md`.
2. Di vault Obsidian: `02_Rules/device-bootstrap-standard.md`,
   `02_Rules/firmware-package-rules.md`, dan panduan
   `04_Guides/New Product Bootstrap Guide.md`.
3. Contoh implementasi yang sudah jadi: adapter dan package TMM di repo
   bootstrap (`products/tmm/`, `src/adapters/esp32/`).

**Aturan mutlak:**

- JANGAN menebak pin, flash geometry, partition table, chip variant, atau
  fitur hardware. Field yang belum terbukti wajib tetap `UNCONFIRMED` dan
  fiturnya dinonaktifkan. Berhenti dan laporkan bila fakta hardware wajib
  belum confirmed — jangan melanjutkan build.
- Jangan mengubah `src/core/` — semua perbedaan hardware ada di adapter.
- Jangan menyalin credential ke log, manifest, note, atau dokumentasi.

**Tugasmu, berurutan:**

1. Buat hardware profile `profiles/<PROFILE_ID>/profile.json` dengan evidence
   untuk setiap klaim hardware.
2. Buat adapter produk yang mengimplementasikan HAL lengkap (radio, NVS,
   setup AP, mDNS, OTA writer, confirm, rollback).
3. Commit source sampai worktree bersih, lalu build: wajib menghasilkan
   **dua BIN** — app-only BIN (OTA/LAN) dan merged/full BIN (USB/recovery) —
   dalam satu run dari commit yang sama.
4. Buat **dua manifest** library (`manifest-full.json` dan
   `manifest-app-only.json`) dengan `stage`, `firmwareRole`, dan satu
   `releaseId` kanonik `<PRODUCT>-<version>-<buildId>`; semua shared fields
   kedua manifest harus identik.
5. Publish dengan `npm run publish-package` — satu GitHub Release berisi dua
   BIN + dua manifest asset, checksum unduhan terverifikasi.
6. Commit dan push manifest ke `telemetric-firmware-library`, lalu pastikan
   portal mengimpor **tepat dua record** yang tampil sebagai **satu package
   kartu** di container yang sesuai `firmwareRole` (USB memilih merged BIN,
   OTA memilih app-only BIN).
7. Tutup dengan checklist `04_Guides/New Product Bootstrap Checklist.md`.

Laporkan compact: PRODUCT VERSION | releaseId | lifecycle/evidence | dua SHA |
release URL | hal yang belum terbukti di hardware.
