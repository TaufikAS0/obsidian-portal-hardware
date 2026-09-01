# New Product Bootstrap Checklist

> Checklist siap salin untuk package bootstrap produk baru. Panduan:
> [[New Product Bootstrap Guide]]. Urutan perintah: [[Bootstrap Build and Publish SOP]]. Kotak hanya dicentang setelah buktinya ada.

## Header

- Product: `<productCode>`
- Profile: `<profileId>`
- Version: `<version>`
- ReleaseId: `<PRODUCT>-<version>-<buildId>`
- Source commit: `<full commit hash>`
- USB BIN/SHA: `<merged.bin> / <sha256>`
- OTA BIN/SHA: `<app.bin> / <sha256>`
- Release URL: `<url GitHub release/draft>`
- Library commit: `<hash commit manifest di library>`
- Portal verification: `<tanggal + ringkasan>`
- Physical-test status: `<belum / tanggal + ringkasan>`
- Unknowns: `<field UNCONFIRMED + fitur yang dinonaktifkan>`

## Perencanaan

- [ ] Product identity ditentukan
- [ ] Hardware profile confirmed

## Implementasi

- [ ] Adapter hardware dibuat
- [ ] Factory LAB policy diperiksa

## Pengujian perangkat

- [ ] NVS tested
- [ ] AP fallback tested
- [ ] Provisioning tested
- [ ] OTA pending/confirm/rollback tested

## Build & release

- [ ] Source committed
- [ ] Clean-worktree gate passed
- [ ] App-only BIN built
- [ ] Merged BIN built
- [ ] Checksums verified
- [ ] Dual manifests valid

## Distribusi

- [ ] GitHub Release published
- [ ] Library manifests pushed

## Verifikasi portal

- [ ] Portal imported two records
- [ ] Portal displays one package
- [ ] USB mapping verified
- [ ] OTA mapping verified

## Penutup

- [ ] Physical test result recorded
- [ ] Production readiness separately approved

## Aturan pengisian

- Setiap centang harus punya bukti (commit, log, hasil unduh, catatan fisik).
- `Production readiness separately approved` diputuskan manusia; status
  `draft`/`built` tidak boleh dipakai produksi.
- Field `UNCONFIRMED` wajib ditulis di `Unknowns` beserta fitur yang
  dinonaktifkan karenanya.

## Terkait

- [[New Product Bootstrap Guide]] — penjelasan tiap langkah
- [[Bootstrap Build and Publish SOP]] — perintah persis
- [[AI Prompt - New Product Bootstrap]] — versi prompt untuk AI
- [[TMM Bootstrap Implementation History]] — contoh nyata TMM
- [[02_Rules/firmware-package-rules|Firmware Package Rules]] ·
  [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]]
