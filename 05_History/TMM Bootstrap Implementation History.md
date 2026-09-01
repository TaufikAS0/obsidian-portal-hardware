# TMM Bootstrap Implementation History

> Riwayat lengkap implementasi framework Telemetric Device Bootstrap dan
> package bootstrap TMM pertama, dari kebutuhan awal sampai tampil di portal.
> Semua fakta diverifikasi langsung dari commit, file, manifest, dan database
> portal pada 2026-09-01.

**Terkait:** [[Firmware Package Architecture Decisions]] ·
[[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]] ·
[[TMM]] · [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]] ·
[[02_Rules/firmware-package-rules|Firmware Package Rules]]

## 1. Masalah awal

Sebelum framework ini, firmware awal tiap produk dibangun dengan pola masing-
masing. Kebutuhan yang harus dipenuhi secara seragam:

- kredensial Wi-Fi tersimpan di **NVS** dicoba lebih dulu;
- fallback ke **factory Wi-Fi LAB**;
- fallback terakhir berupa access point `TELEMETRIC-SETUP-XXXXXX` dengan
  halaman provisioning di `http://192.168.4.1/`;
- provisioning menyimpan kredensial baru ke NVS;
- perangkat masuk LAN dan bisa di-update lewat OTA terautentikasi;
- jalur **USB recovery** tidak boleh hilang.

Risikonya: setiap produk menyalin pola ini dengan variasi berbeda, dan tidak
ada aturan resmi soal credential LAB, stage build, serta format release.

## 2. Keputusan membuat repo framework

Dibuat repo bersama `2026-telemetric-device-bootstrap`. Prinsip inti:
**yang universal adalah perilaku, API, nama setup, keamanan, dan format
release — bukan BIN-nya.** BIN tetap spesifik per chip dan per hardware
profile (lihat [[Firmware Package Architecture Decisions]]).

Commit fondasi (diverifikasi via `git log`):

| Commit | Isi |
|---|---|
| `f9fc81c` | Core state machine (`src/core/bootstrap.mjs`), manifest builder (`src/core/artifact-manifest.mjs`), kontrak HAL, template profile, test perilaku |
| `ca04068` | Factory Wi-Fi LAB (`src/config/factory-wifi.mjs`), stage guard (`src/core/stage-guard.mjs`), AP teardown nyata, test diperluas |
| `9648a0c` | Adapter ESP32-S3, sketch TMM `tmm_bootstrap_lab`, profile `TMM_V6_R0_M0`, build script, package dual-artifact pertama |

Catatan historis: commit ketiga sempat tercatat ber-hash `f1e925b` sebelum
di-amend; hash lama itu tidak ada lagi di repository sehingga tidak dapat
diverifikasi ulang. Hash yang valid sekarang: `9648a0c`.

## 3. State machine koneksi

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

## 4. OTA: pending-verify, confirm, rollback

Diverifikasi di `src/core/bootstrap.mjs`:

- `beginOta()` — hanya saat state `online`;
- `finishOta({ imageValid })` — image tidak valid → `abortOta()` tanpa
  reboot; valid → `otaPendingVerify = true` lalu reboot
  (`ota-pending-verify`);
- `confirmHealth()` — slot baru stabil → `confirmOta()`
  (`ota-confirmed`);
- `reportUnhealthy()` — gagal kesehatan → `rollbackOta()`
  (`ota-rolled-back`).

Batas desain: `otaPendingVerify` adalah state in-memory; setelah reboot
adapter harus memulihkannya dari NVS/slot-info. Core belum menyediakan API
pemulihannya.

## 5. Dua BIN, satu releaseId, dua manifest

- **app-only BIN** — untuk OTA/LAN, ditulis ke slot OTA tidak aktif;
- **merged/full BIN** — untuk USB bootstrap dan recovery;
- keduanya dari satu run, diikat **satu `releaseId` kanonik**
  `<PRODUCT>-<version>-<buildId>`;
- di library, package dirilis dengan **dua manifest asset unik**:
  `manifest-full.json` dan `manifest-app-only.json`.

Validasi package menolak: pasangan hilang, imageType ganda, dan metadata
drift antar artefak (lihat [[Firmware Package Architecture Decisions]]).

## 6. Stage=lab, production guard, firmwareRole, hardware profile

- `stage` (`lab`/`production`) wajib ada di profile dan manifest.
- **Stage guard** (`src/core/stage-guard.mjs`): build production menolak
  berjalan selama default factory Wi-Fi LAB masih aktif
  (`FACTORY_WIFI_IS_LAB_DEFAULT`). Kebijakan credential LAB: dipublikasikan
  sebagai nilai convenience oleh keputusan pemilik (2026-08-31), tersimpan
  di `src/config/factory-wifi.mjs` — satu sumber kebenaran; jangan disalin
  ke dokumen lain.
- `firmwareRole` (`bootstrap`/`application`/`recovery`) memisahkan firmware
  dasar dari firmware aplikasi; manifest legacy tanpa field ini dianggap
  `application`.
- `src/core/profile.mjs` memvalidasi hardware profile; field `UNCONFIRMED`
  memblokir build BIN.

## 7. Integrasi firmware library dan portal

Commit library (diverifikasi): `db11683` (publish-package dual-artifact +
`validateReleasePackages`), `ed63cba` (firmwareRole), `2b39e24` (manifest TMM
bootstrap + AI note). Commit portal: `c2ac55f` (kolom `stage`, `release_id`,
`firmware_role` + importer + migrasi DB), `770ffc5` (container UI).

Publisher `npm run publish-package` membuat satu release berisi dua BIN dan
dua manifest, lalu mengunduh ulang dan memverifikasi checksum tiap BIN;
release yang gagal di tengah jalan dihapus agar tidak mengunci tag.

## 8. Tiga container portal

Workspace `/products/<CODE>` dipisah berdasarkan `firmwareRole`
(commit portal `770ffc5`):

1. **Bootstrap & Recovery** (tema amber) — package bootstrap/recovery,
   dengan peringatan kecocokan hardware profile;
2. **Application Firmware** (tema cyan) — firmware fungsi utama;
3. **Firmware History** (collapsed) — retired dan quarantined.

Satu release tetap satu kartu package dan satu tombol UPDATE: USB memilih
merged BIN, OTA memilih app-only BIN.

## 9. Hasil akhir: TMM v0.1.0-bootstrap.1

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

Portal mengimpor tepat dua record (audit
`firmware_library_auto_imported` 2026-09-01T01:54Z), file fisik
terverifikasi ukuran + SHA-256, dan workspace TMM menampilkannya sebagai
satu kartu LAB BOOTSTRAP.

## 10. Yang belum terbukti pada hardware fisik

Paket bootstrap ini **belum pernah di-flash ke perangkat mana pun**. Yang
terbukti live hanyalah perangkat bench TMM dengan firmware aplikasi 0.6.x
(OTA aplikasi sukses 2026-08-31; layout partisi terverifikasi live — lihat
`evidence` di `profiles/TMM_V6_R0_M0/profile.json`). Belum terbukti:

- NVS first-boot dengan firmware bootstrap;
- AP fallback dan halaman provisioning berfungsi di perangkat;
- provisioning endpoint firmware bootstrap;
- OTA pending-verify/confirm/rollback dengan image bootstrap;
- mDNS advertise `_telemetric-ota._tcp`;
- rollback-under-crash pada bootloader Arduino stok
  (`CONFIG_BOOTLOADER_APP_ROLLBACK_ENABLE` — UNCONFIRMED).

## 11. Known limitations

1. Bootstrap TMM hanya terikat profil `TMM_V6_R0_M0`; revisi lain butuh
   package bootstrap sendiri.
2. Ethernet dan physical setup control masih disabled
   (`disabledFeatures`; profile UNCONFIRMED).
3. Catatan USB/OTA di portal masih perlu disatukan berdasarkan releaseId
   (saat ini terkait per versi).
4. Overview portal masih perlu memisahkan Latest Application dan Latest
   Bootstrap.
5. Factory Wi-Fi LAB publik — wajib diganti sebelum production; stage guard
   menolak build production selama default aktif.

---

**Facts**: commit, manifest, dan record database diverifikasi langsung dari
repository (2026-09-01).
**Assumptions**: tidak ada.
**Unknowns**: daftar "belum terbukti" di atas.
**Human Verification**: sesi flash fisik bootstrap + provisioning + OTA di
perangkat TMM.
