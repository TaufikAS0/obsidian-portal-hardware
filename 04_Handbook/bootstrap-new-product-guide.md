# Panduan — Membuat Bootstrap untuk Produk Baru

Panduan langkah demi langkah untuk membuat package bootstrap (firmware dasar)
untuk produk Telemetric yang baru, memakai framework
`2026-telemetric-device-bootstrap`. Ditulis agar bisa diikuti operator awam
maupun AI tanpa membaca percakapan sebelumnya.

**Aturan induk** (wajib dibaca lebih dulu):
`02_Rules/device-bootstrap-standard.md` dan
`02_Rules/firmware-package-rules.md`. Panduan ini tidak menggantikan keduanya.

Contoh nyata yang sudah jadi: TMM `v0.1.0-bootstrap.1` — lihat
`04_Handbook/bootstrap-tmm-history.md`.

---

## A. Tentukan identitas produk

Kumpulkan dan tulis eksplisit (jangan menebak):

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

Contoh identitas yang sudah terbukti: `profiles/TMM_V6_R0_M0/profile.json`
(di repo bootstrap).

## B. Buat hardware profile

1. Salin `profiles/_template/profile.json` ke
   `profiles/<PROFILE_ID>/profile.json`.
2. Isi field hardware dengan nilai **CONFIRMED** — setiap klaim harus punya
   entri di `evidence` (sumber + evidenceLevel). Contoh TMM mencantumkan
   bukti `board-proven-live` dari perangkat bench.
3. Field yang belum diketahui **wajib tetap `UNCONFIRMED`** dan fiturnya
   dinonaktifkan di adapter. `UNCONFIRMED` memblokir build BIN sampai ada
   bukti.
4. Dilarang menebak: pin, flash geometry, partition table, Ethernet, atau
   identitas produk.
5. Jalankan test profile: `node --test tests/profile.test.mjs`.

## C. Buat adapter produk

Pemisahan wajib: `src/core/` tidak boleh menyentuh radio/flash/NVS. Semua
hardware lewat adapter di `src/adapters/` yang mengimplementasikan kontrak
HAL (daftar lengkap di `src/adapters/README.md` dan komentar
`src/core/bootstrap.mjs`).

Yang diimplementasikan adapter: radio station/AP, NVS, setup AP + halaman
provisioning, mDNS advertise, OTA writer ke slot tidak aktif, confirm,
rollback, sumber device suffix.

Referensi TMM (repo bootstrap):

| File | Fungsi | Boleh ditiru / wajib diganti |
|---|---|---|
| `src/adapters/esp32/telemetric_esp32_hal.h` | HAL ESP32-S3 (NVS, Wi-Fi, AP, OTA, mDNS) | **Wajib diganti** pin/partisi/suffix per hardware |
| `products/tmm/tmm_bootstrap_lab/tmm_bootstrap_lab.ino` | sketch utama bootstrap | **Wajib diganti** product code, AP suffix, log line |
| `products/tmm/tmm_bootstrap_lab/partitions.csv` | tabel partisi A/B | **Wajib diganti** sesuai flashSize produk |
| `products/tmm/tmm_bootstrap_lab/firmware_version.h` | versi runtime | **Wajib diganti** version + product |
| `src/core/*` | state machine + manifest | **Jangan diubah** — dipakai semua produk |

## D. Konfigurasi factory LAB

1. Credential LAB diatur lewat file konfigurasi resmi
   `src/config/factory-wifi.mjs` di repo bootstrap (satu sumber kebenaran —
   jangan salin nilai passwordnya ke dokumen lain, log, manifest, operator
   note, atau dokumentasi agar tidak drift).
2. Flag `FACTORY_WIFI_IS_LAB_DEFAULT` membuat **build production menolak
   berjalan** selama default LAB masih aktif (`src/core/stage-guard.mjs`).
3. Production credential, OTA token, dan private key **tetap dilarang** masuk
   Git.
4. Password tidak pernah dicetak ke serial log, test output, atau error.

## E. Build

Jalankan dari repo bootstrap (contoh TMM: `npm run build:tmm-lab` yang
memanggil `scripts/build-tmm-lab.ps1`):

1. Commit semua source lebih dulu — script menjalankan
   `scripts/assert-clean-worktree.mjs` dan **menolak worktree kotor**.
2. Build dijalankan dari commit tersebut; `buildId` = `git rev-parse
   --short=7 HEAD` dan `sourceCommit` = hash penuh.
3. Wajib menghasilkan dua BIN dalam satu run:
   1. **app-only BIN** untuk OTA/LAN;
   2. **merged/full BIN** untuk USB/recovery.
4. Versi runtime (header), manifest, releaseId, buildId, dan sourceCommit
   harus konsisten satu sama lain.
5. Hash ulang kedua BIN setelah build (emit-manifest melakukannya otomatis
   dari byte fisik).

## F. Manifest

1. **Manifest build** dibuat oleh `scripts/emit-manifest.mjs` (memakai core
   builder yang sama dengan test) — berisi kedua artefak dan satu
   `releaseId` kanonik `<PRODUCT>-<version>-<buildId>`.
2. **Dua manifest library** dibuat terpisah, satu per BIN:
   - `manifest-full.json` (imageType `full`, transport `usb`);
   - `manifest-app-only.json` (imageType `app-only`, transport `ota`).
   Contoh nyata: `telemetric-firmware-library/manifests/TMM/0.1.0-bootstrap.1-*.json`.
3. `firmwareRole`:
   - `bootstrap` untuk firmware dasar;
   - `application` untuk firmware fungsi utama;
   - `recovery` untuk firmware pemulihan khusus.
4. Semua shared fields pasangan wajib identik (daftar lengkap di
   `PACKAGE_SHARED_FIELDS` di `scripts/library.mjs`), termasuk `stage`,
   `firmwareRole`, `releaseId`, `releaseTag`. Manifest legacy tanpa
   `firmwareRole` dianggap `application`.

## G. Publish ke firmware library

1. `node scripts/validate-library.mjs` — harus lulus tanpa error.
2. `npm run gate -- --manifest <manifest> --bin <bin>` — sekali per manifest
   + BIN.
3. `npm run publish-package -- --manifest-app <m> --bin-app <b> --manifest-full <m> --bin-full <b>`
   — membuat **satu GitHub Release** berisi dua BIN + dua manifest
   (`manifest-full.json`, `manifest-app-only.json`), lalu mengunduh ulang dan
   memverifikasi checksum tiap BIN.
4. Commit dan push manifest + note ke repo library.

## H. Verifikasi portal

1. Tunggu sync otomatis, atau admin jalankan `POST /api/firmware/library-sync`
   di portal.
2. Buka `https://192.168.1.122:8443/products/<CODE>`:
   - database harus punya **tepat dua record** (full + app-only) untuk
     releaseId tersebut — tidak ada duplikasi;
   - UI menampilkan **satu kartu package** di container yang sesuai
     `firmwareRole` (Bootstrap & Recovery / Application Firmware);
   - tombol **USB** memilih merged BIN, tombol **OTA** memilih app-only BIN;
   - stage `lab` terlihat jelas (badge LAB).
3. **Jangan flash perangkat** saat hanya memverifikasi portal.

Gunakan `04_Handbook/bootstrap-new-product-template.md` sebagai checklist
penutup, dan `04_Handbook/bootstrap-new-product-ai-prompt.md` bila pekerjaan
dikerjakan AI.

---

**Facts**: mekanisme di atas diverifikasi dari kode, script, dan manifest
yang benar-benar ada di repository (2026-09-01).
**Assumptions**: nama script dan path bisa berubah; jika berbeda, ikuti
README repo bootstrap.
**Unknowns**: perangkat keras produk baru — selalu isi profile dan evidence
dulu.
**Human Verification**: flash + provisioning + OTA fisik per produk.
