# New Product Bootstrap Guide

> Panduan membuat package bootstrap untuk produk Telemetric baru memakai
> framework `2026-telemetric-device-bootstrap`. Ditulis agar bisa diikuti
> operator awam maupun AI tanpa membaca percakapan sebelumnya.
>
> Aturan induk: [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]] · [[02_Rules/firmware-package-rules|Firmware Package Rules]].
> Riwayat nyata: [[TMM Bootstrap Implementation History]].
> Lanjutan: [[Bootstrap Build and Publish SOP]] ·
> [[New Product Bootstrap Checklist]] · [[AI Prompt - New Product Bootstrap]].

## A. Tentukan identitas produk

Kumpulkan dan tulis eksplisit — jangan menebak:

| Field | Contoh TMM | Sumber bukti |
|---|---|---|
| `productCode` | `TMM` | katalog produk |
| `productName` | `Telemetric Module Master` | katalog |
| `hardwareRevision` | `TMM_V6_R0_M0` | silkscreen/PCB + docs produk |
| `profileId` | `TMM_V6_R0_M0` | folder `profiles/` |
| `chipFamily` | `ESP32-S3` | docs produk / live device-info |
| `flashSize` | `16MB` | live device-info atau datasheet |
| `flashMode` | `qio` | idem |
| `partitionScheme` | `tmm-ota-4mb` | file partitions.csv produk |
| Wi-Fi support | `true` | hardware |
| Ethernet support | `UNCONFIRMED` bila belum jelas | hardware |
| setup control | `UNCONFIRMED` bila belum ada tombol fisik | hardware |

Contoh identitas terbukti: `profiles/TMM_V6_R0_M0/profile.json` di repo
bootstrap.

## B. Buat hardware profile

1. Salin `profiles/_template/profile.json` ke
   `profiles/<PROFILE_ID>/profile.json`.
2. Isi field hardware dengan nilai **CONFIRMED** — setiap klaim butuh entri
   `evidence` (sumber + evidenceLevel). Contoh TMM memakai bukti
   `board-proven-live` dari perangkat bench.
3. Field yang belum diketahui **wajib `UNCONFIRMED`** dan fiturnya
   dinonaktifkan di adapter. `UNCONFIRMED` memblokir build BIN.
4. Dilarang menebak: pin, flash geometry, partition table, Ethernet,
   identitas produk.
5. Jalankan `node --test tests/profile.test.mjs` di repo bootstrap.

## C. Buat adapter produk

Pemisahan wajib: `src/core/` tidak boleh menyentuh radio/flash/NVS. Semua
hardware lewat adapter di `src/adapters/` (kontrak HAL:
`src/adapters/README.md` dan komentar `src/core/bootstrap.mjs`).

Yang diimplementasikan adapter: radio station/AP, NVS, setup AP + halaman
provisioning, mDNS advertise, OTA writer ke slot tidak aktif, confirm,
rollback, dan sumber device suffix.

Referensi TMM (repo bootstrap):

| File | Fungsi | Status |
|---|---|---|
| `src/adapters/esp32/telemetric_esp32_hal.h` | HAL ESP32-S3 | Wajib diganti per hardware |
| `products/tmm/tmm_bootstrap_lab/tmm_bootstrap_lab.ino` | sketch utama | Wajib diganti per produk |
| `products/tmm/tmm_bootstrap_lab/partitions.csv` | partisi A/B | Wajib diganti sesuai flashSize |
| `products/tmm/tmm_bootstrap_lab/firmware_version.h` | versi runtime | Wajib diganti |
| `src/core/*` | state machine + manifest | Jangan diubah |

## D. Konfigurasi factory LAB

1. Credential LAB hanya di `src/config/factory-wifi.mjs` (satu sumber
   kebenaran — jangan salin nilainya ke dokumen/log/manifest/note).
2. `FACTORY_WIFI_IS_LAB_DEFAULT` membuat build production menolak berjalan
   selama default LAB aktif (`src/core/stage-guard.mjs`).
3. Production credential, OTA token, private key: **tetap dilarang** masuk
   Git.
4. Password tidak pernah dicetak ke serial log, test output, atau error.

## E. Build

1. Commit semua source — `scripts/assert-clean-worktree.mjs` menolak
   worktree kotor.
2. Build dari commit tersebut; `buildId` = `git rev-parse --short=7 HEAD`,
   `sourceCommit` = hash penuh (contoh TMM: `npm run build:tmm-lab`).
3. Wajib dua BIN dalam satu run: **app-only BIN** (OTA/LAN) dan
   **merged/full BIN** (USB/recovery).
4. Versi runtime, manifest, releaseId, buildId, sourceCommit konsisten.
5. Hash ulang kedua BIN setelah build.

## F. Manifest

1. Manifest build dibuat `scripts/emit-manifest.mjs` — berisi kedua artefak
   dan satu `releaseId` kanonik `<PRODUCT>-<version>-<buildId>`.
2. Dua manifest library, satu per BIN: `manifest-full.json` (imageType
   `full`, transport `usb`) dan `manifest-app-only.json` (imageType
   `app-only`, transport `ota`). Contoh:
   `manifests/TMM/0.1.0-bootstrap.1-*.json` di library.
3. `firmwareRole`: `bootstrap` (firmware dasar), `application` (fungsi
   utama), `recovery` (pemulihan khusus).
4. Semua shared fields pasangan wajib identik — daftar di
   `PACKAGE_SHARED_FIELDS` (`scripts/library.mjs`).

## G. Publish ke firmware library

1. `node scripts/validate-library.mjs` — tanpa error.
2. `npm run gate -- --manifest <manifest> --bin <bin>` — per manifest + BIN.
3. `npm run publish-package -- --manifest-app <m> --bin-app <b> --manifest-full <m> --bin-full <b>`
   — satu GitHub Release: dua BIN + `manifest-full.json` +
   `manifest-app-only.json`, checksum unduhan terverifikasi.
4. Commit dan push manifest + note ke repo library.

Langkah lengkap dengan penanganan kegagalan:
[[Bootstrap Build and Publish SOP]].

## H. Verifikasi portal

1. Tunggu sync otomatis, atau admin jalankan
   `POST /api/firmware/library-sync`.
2. Buka `https://192.168.1.122:8443/products/<CODE>`:
   - database **tepat dua record** (full + app-only) — tanpa duplikasi;
   - **satu kartu package** di container sesuai `firmwareRole`;
   - **USB** memilih merged BIN, **OTA** memilih app-only BIN;
   - stage `lab` terlihat jelas (badge LAB).
3. **Jangan flash perangkat** saat hanya memverifikasi portal.

Tutup dengan [[New Product Bootstrap Checklist]] dan gunakan
[[AI Prompt - New Product Bootstrap]] bila dikerjakan AI.
