# Firmware Package Architecture Decisions

> Catatan keputusan arsitektur package firmware Telemetric. Setiap keputusan
> mencantumkan bukti repository (commit/file) supaya bisa diverifikasi ulang.
> Riwayat implementasi nyata: [[TMM Bootstrap Implementation History]].

## D1 — Framework universal: perilaku, bukan BIN

- **Konteks**: firmware awal tiap produk berisiko dibangun dengan pola
  berbeda-beda.
- **Keputusan**: satu repo framework (`2026-telemetric-device-bootstrap`)
  menstandarkan state machine, API, nama setup, keamanan, dan format release.
  BIN tetap spesifik per chip/hardware profile.
- **Bukti**: commit `f9fc81c`; `docs/BOOTSTRAP_STANDARD.md`;
  `02_Rules/device-bootstrap-standard`.

## D2 — Urutan koneksi wajib

- **Keputusan**: NVS tersimpan → factory Wi-Fi (LAB) → AP
  `TELEMETRIC-SETUP-XXXXXX` → provisioning → simpan NVS → LAN.
- **Konsekuensi**: reboot selalu mulai dari NVS; AP hanya fallback terakhir
  dan ditutup setelah provisioning sukses.
- **Bukti**: `src/core/bootstrap.mjs` (`boot`, `provision`); test
  `tests/bootstrap.test.mjs` di repo bootstrap.

## D3 — OTA A/B dengan pending-verify, confirm, rollback

- **Keputusan**: OTA menulis slot tidak aktif; setelah reboot berjalan stabil
  wajib `confirmHealth()`; gagal kesehatan → `rollbackOta()`.
- **Konsekuensi**: state `otaPendingVerify` in-memory; pemulihan setelah
  reboot menjadi tanggung jawab adapter.
- **Bukti**: `src/core/bootstrap.mjs` (`beginOta`, `finishOta`,
  `confirmHealth`, `reportUnhealthy`).

## D4 — Satu release = dua BIN, satu releaseId

- **Keputusan**: setiap release menghasilkan app-only BIN (OTA/LAN) dan
  merged/full BIN (USB/recovery) dari satu run, diikat satu `releaseId`
  kanonik `<PRODUCT>-<version>-<buildId>`.
- **Konsekuensi**: package tanpa salah satu BIN ditolak; USB recovery tidak
  pernah hilang.
- **Bukti**: `src/core/artifact-manifest.mjs`;
  `02_Rules/firmware-package-rules`.

## D5 — Dua manifest library per package

- **Keputusan**: di `telemetric-firmware-library`, package dirilis dengan dua
  manifest asset unik — `manifest-full.json` dan `manifest-app-only.json` —
  bukan satu `manifest.json` generik.
- **Konsekuensi**: `publish-package` mengunggah 4 asset per release; kedua
  manifest wajib identik pada semua shared fields.
- **Bukti**: `scripts/publish-package.mjs`; commit library `db11683`;
  contoh `manifests/TMM/0.1.0-bootstrap.1-*.json`.

## D6 — Stage build dan factory Wi-Fi LAB

- **Keputusan**: `stage` (`lab`/`production`) wajib. Credential factory LAB
  publik (keputusan pemilik 2026-08-31) disimpan hanya di
  `src/config/factory-wifi.mjs`; build **production** menolak berjalan
  selama default LAB aktif.
- **Konsekuensi**: password LAB tidak pernah disalin ke dokumen/log/manifest;
  unlock production = ganti file config tersebut.
- **Bukti**: `src/config/factory-wifi.mjs`; `src/core/stage-guard.mjs`;
  commit `ca04068`.

## D7 — firmwareRole dan tiga container portal

- **Keputusan**: manifest membawa `firmwareRole`
  (`bootstrap`/`application`/`recovery`; legacy default `application`).
  Portal membagi workspace menjadi tiga container: Bootstrap & Recovery
  (amber), Application Firmware (cyan), Firmware History (collapsed).
- **Konsekuensi**: satu release tetap satu kartu + satu tombol UPDATE;
  history (retired/quarantined) tersembunyi default.
- **Bukti**: commit portal `770ffc5`; commit library `ed63cba`;
  `src/client/firmware-package.ts` (`splitPackagesByRole`).

## D8 — Database portal: kunci unik dan refresh metadata

- **Keputusan**: kunci unik record firmware menjadi
  `(product_id, version, build_id, image_type)` sehingga dua artefak satu
  release bisa coexist; record lama dengan SHA sama menerima **refresh
  metadata** (stage/releaseId/firmwareRole) tanpa menduplikasi BIN/record.
- **Konsekuensi**: portal tetap satu sumber kebenaran lifecycle & QC;
  manifest hanya memperkaya metadata deskriptif.
- **Bukti**: commit portal `c2ac55f`, `770ffc5`;
  `tests/db-migration.test.ts`.

## D9 — Tooling publish dan gate

- **Keputusan**: gate per manifest (`npm run gate`), validasi seluruh
  library (`validate-library` + `validateReleasePackages`), dan publisher
  package (`publish-package`) yang memverifikasi checksum unduhan dan
  menghapus release baru yang gagal.
- **Bukti**: `scripts/gate.mjs`, `scripts/validate-library.mjs`,
  `scripts/publish-package.mjs`; commit library `db11683`.

---

**Terkait**: [[TMM Bootstrap Implementation History]] ·
[[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]] ·
[[04_Guides/Bootstrap Build and Publish SOP|Build and Publish SOP]] ·
[[02_Rules/firmware-package-rules|Firmware Package Rules]]
