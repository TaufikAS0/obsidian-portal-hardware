# Template — Checklist Produk Bootstrap Baru

Salin bagian ini ke catatan produk, isi semua kotak, dan jangan menandai kotak
tanpa bukti. Panduan lengkap: `04_Handbook/bootstrap-new-product-guide.md`.

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
- Portal verification: `<tanggal + ringkasan: dua record, satu kartu, mapping USB/OTA>`
- Physical-test status: `<belum / tanggal + ringkasan>`
- Unknowns: `<daftar field UNCONFIRMED + risiko>`

## Checklist

### Perencanaan

- [ ] Product identity ditentukan
- [ ] Hardware profile confirmed

### Implementasi

- [ ] Adapter hardware dibuat
- [ ] Factory LAB policy diperiksa

### Pengujian perangkat

- [ ] NVS tested
- [ ] AP fallback tested
- [ ] Provisioning tested
- [ ] OTA pending/confirm/rollback tested

### Build & release

- [ ] Source committed
- [ ] Clean-worktree gate passed
- [ ] App-only BIN built
- [ ] Merged BIN built
- [ ] Checksums verified
- [ ] Dual manifests valid

### Distribusi

- [ ] GitHub Release published
- [ ] Library manifests pushed

### Verifikasi portal

- [ ] Portal imported two records
- [ ] Portal displays one package
- [ ] USB mapping verified
- [ ] OTA mapping verified

### Penutup

- [ ] Physical test result recorded
- [ ] Production readiness separately approved

## Aturan pengisian

- Kotak hanya boleh dicentang setelah buktinya ada (commit, log, screenshot,
  atau catatan fisik).
- `Production readiness separately approved` harus diputuskan manusia —
  status `draft`/`built` tidak boleh langsung dipakai produksi.
- Jika ada field `UNCONFIRMED`, tulis di `Unknowns` beserta fitur yang
  dinonaktifkan karenanya.
