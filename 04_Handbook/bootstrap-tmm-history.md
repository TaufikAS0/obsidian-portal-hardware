# Riwayat — Implementasi Bootstrap TMM

Dokumen ini merangkum secara kronologis bagaimana framework Telemetric Device
Bootstrap dibuat dan dipakai untuk merilis firmware bootstrap TMM pertama.
Semua fakta di bawah diverifikasi langsung dari repository (commit, file, dan
database portal), bukan dari ingatan percakapan.

## Latar belakang masalah

Sebelum framework ini ada, setiap produk membangun firmware awalnya sendiri.
Yang dibutuhkan adalah satu perilaku seragam untuk semua perangkat Telemetric:

- mencoba Wi-Fi yang tersimpan di NVS,
- fallback ke factory Wi-Fi LAB,
- membuka access point `TELEMETRIC-SETUP-XXXXXX` bila semua gagal,
- provisioning lewat halaman `http://192.168.4.1/`,
- OTA terautentikasi dengan jalur USB recovery yang tidak pernah hilang.

Masalahnya: perilaku itu rawan diulang dengan versi berbeda di tiap produk,
dan tidak ada aturan resmi soal factory Wi-Fi LAB, stage build, dan format
release.

## Keputusan membuat repo framework

`2026-telemetric-device-bootstrap` dibuat sebagai repo bersama. Prinsipnya:
**yang universal adalah perilaku, API, nama setup, keamanan, dan format
release — bukan BIN-nya.** BIN tetap spesifik per chip dan per hardware
profile.

Commit fondasi (diverifikasi via `git log`):

| Commit | Isi |
|---|---|
| `f9fc81c` | Core state machine (`src/core/bootstrap.mjs`), manifest builder (`src/core/artifact-manifest.mjs`), kontrak HAL, template profile, test perilaku |
| `ca04068` | Factory Wi-Fi LAB (`src/config/factory-wifi.mjs`), stage guard (`src/core/stage-guard.mjs`), AP teardown nyata, test diperluas |
| `9648a0c` | Adapter ESP32-S3, sketch TMM `tmm_bootstrap_lab`, profile `TMM_V6_R0_M0`, build script, package dual-artifact pertama |

Catatan: commit ketiga pernah tercatat dengan hash `f1e925b` sebelum di-amend;
hash lama itu tidak ada lagi di repository sehingga tidak bisa diverifikasi
ulang. Yang terverifikasi sekarang adalah `9648a0c`.

## State machine koneksi

Urutan wajib (diverifikasi di `src/core/bootstrap.mjs`, fungsi `boot()` dan
`provision()`):

```text
boot
  -> connecting-stored   : coba kredensial NVS
  -> connecting-factory  : coba factory Wi-Fi LAB (jika dikonfigurasi)
  -> setup-ap            : buka TELEMETRIC-SETUP-<suffix> di 192.168.4.1
  -> provision           : simpan kredensial baru ke NVS
  -> stopSetupAp         : AP ditutup setelah koneksi station sukses
  -> online              : advertiseOnLan() di LAN
```

Kredensial factory yang berhasil dipakai juga disimpan ke NVS, sehingga
reboot berikutnya langsung memakai NVS dan tidak membuka factory/AP lagi.

## OTA A/B: pending-verify, confirm, rollback

Diverifikasi di `src/core/bootstrap.mjs`:

- `beginOta()` — hanya saat state `online`;
- `finishOta({ imageValid })` — image tidak valid → `abortOta()` tanpa reboot;
  valid → `otaPendingVerify = true` lalu reboot (`ota-pending-verify`);
- `confirmHealth()` — setelah slot baru berjalan stabil → `confirmOta()`
  (`ota-confirmed`);
- `reportUnhealthy()` — gagal kesehatan → `rollbackOta()`
  (`ota-rolled-back`).

Batas desain: `otaPendingVerify` adalah state in-memory. Setelah reboot,
adapter harus memulihkannya dari NVS/slot-info; core belum menyediakan API
pemulihan itu.

## Dua BIN, satu releaseId

- **app-only BIN** — untuk OTA/LAN, ditulis ke slot OTA yang tidak aktif;
- **merged/full BIN** — untuk USB bootstrap dan recovery.

Keduanya dibangun dalam satu run dan diikat oleh satu `releaseId` dengan
format kanonik `<PRODUCT>-<version>-<buildId>`. Validasi menolak package yang
kehilangan salah satu artefak, punya imageType ganda, atau punya metadata
yang berbeda di antara keduanya.

## Stage=lab, production guard, firmwareRole, hardware profile

- `stage` (`lab`/`production`) wajib di profile dan manifest.
- `src/core/stage-guard.mjs`: build **production** menolak berjalan selama
  default factory Wi-Fi LAB masih aktif (`FACTORY_WIFI_IS_LAB_DEFAULT`).
- `firmwareRole` (`bootstrap`/`application`/`recovery`) ditambahkan agar UI
  memisahkan firmware dasar dari firmware aplikasi; legacy manifest tanpa
  field ini dianggap `application`.
- `src/core/profile.mjs` memvalidasi hardware profile; field hardware yang
  `UNCONFIRMED` memblokir build BIN.

## Integrasi firmware library dan portal

Commit library (diverifikasi): `db11683` (publish-package dual-artifact +
validasi package), `ed63cba` (firmwareRole), `2b39e24` (manifest TMM
bootstrap). Commit portal: `c2ac55f` (kolom `stage`/`release_id`/
`firmware_role` + importer + migrasi DB), `770ffc5` (container UI
Bootstrap/Application/History).

## Hasil akhir: TMM v0.1.0-bootstrap.1

Diverifikasi dari `products/tmm/build/tmm_bootstrap_lab/manifest.json`,
`manifests/TMM/0.1.0-bootstrap.1-*.json` di library, dan database portal:

| Field | Value |
|---|---|
| Version | `0.1.0-bootstrap.1` |
| ReleaseId | `TMM-0.1.0-bootstrap.1-9648a0c` |
| Source commit | `9648a0cf697a9353337c6a8ad2240cdac9805337` |
| Profile | `TMM_V6_R0_M0` (ESP32-S3, 16MB, qio, `tmm-ota-4mb`) |
| Stage / firmwareRole | `lab` / `bootstrap` |
| App-only BIN | `tmm_bootstrap_lab.ino.bin`, 980.240 byte, SHA-256 `608b0c86…` |
| Merged BIN | `tmm_bootstrap_lab.ino.merged.bin`, 16.777.216 byte, SHA-256 `f9914960…` |
| Release | draft GitHub `TMM-v0.1.0-bootstrap.1`, 4 asset |

Portal mengimpor tepat dua record (`firmware_library_auto_imported`
2026-09-01T01:54Z), file fisik terverifikasi ukuran + SHA-256, dan workspace
TMM menampilkannya sebagai satu kartu LAB BOOTSTRAP di container
"Bootstrap & Recovery".

## Yang belum terbukti pada hardware fisik

Jujur: paket bootstrap ini **belum pernah di-flash ke perangkat mana pun**.
Yang terbukti live sejauh ini hanyalah perangkat bench TMM yang menjalankan
firmware aplikasi 0.6.x (OTA aplikasi sukses 2026-08-31, layout partisi
terverifikasi live — lihat evidence di profile). Belum terbukti:

- NVS first-boot dengan firmware bootstrap;
- AP fallback `TELEMETRIC-SETUP-<suffix>` muncul dan halaman provisioning
  berfungsi di perangkat;
- provisioning endpoint di firmware bootstrap;
- OTA pending-verify/confirm/rollback dengan image bootstrap;
- mDNS advertise `_telemetric-ota._tcp` dari firmware bootstrap;
- dukungan rollback-under-crash pada bootloader Arduino stok
  (`CONFIG_BOOTLOADER_APP_ROLLBACK_ENABLE` — UNCONFIRMED).

## Known limitations

1. **Terikat profil**: bootstrap TMM hanya untuk `TMM_V6_R0_M0`. Revisi
   hardware lain butuh package bootstrap sendiri.
2. **Ethernet dan physical setup control disabled** (`disabledFeatures` di
   manifest; `ethernetSupported` dan `setupControl` tetap UNCONFIRMED di
   profile).
3. **Catatan USB/OTA belum disatukan per releaseId** — firmware note di
   portal masih dikaitkan per versi, bukan per releaseId.
4. **Overview portal** belum memisahkan "Latest Application" dan
   "Latest Bootstrap".
5. Factory Wi-Fi LAB publik (keputusan pemilik 2026-08-31) — wajib diganti
   sebelum production; stage guard menolak build production selama default
   masih aktif.

---

**Facts**: semua commit, manifest, dan record database di atas diverifikasi
langsung dari repository dan database portal pada 2026-09-01.
**Assumptions**: tidak ada.
**Unknowns**: daftar "belum terbukti" di atas.
**Human Verification**: diperlukan sesi flash fisik bootstrap + provisioning
+ OTA di perangkat TMM sebelum status ini naik dari `draft`/`built`.
