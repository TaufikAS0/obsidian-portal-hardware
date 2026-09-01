# Bootstrap Build and Publish SOP

> Standard Operating Procedure: urutan perintah persis untuk membangun dan
> merilis package bootstrap, dari worktree bersih sampai terverifikasi di
> portal. Panduan konsep: [[New Product Bootstrap Guide]]. Checklist:
> [[New Product Bootstrap Checklist]].

## Prasyarat

- Repo bootstrap: `2026-telemetric-device-bootstrap` (local + GitHub).
- Repo library: `telemetric-firmware-library` (local + GitHub).
- Hardware profile produk sudah CONFIRMED (lihat
  [[New Product Bootstrap Guide]] bagian A–B).
- Node.js >= 20, git credential GitHub dengan akses write ke library.

## 1. Commit source

```powershell
git -C "2026-telemetric-device-bootstrap" status --short   # harus kosong
git -C "2026-telemetric-device-bootstrap" add -A
git -C "2026-telemetric-device-bootstrap" commit -m "feat: <deskripsi>"
git -C "2026-telemetric-device-bootstrap" push origin main
```

Gate otomatis: `scripts/assert-clean-worktree.mjs` menolak build bila
worktree kotor — provenance SHA manifest tidak boleh mendeskripsikan source
yang belum di-commit.

## 2. Build dua BIN

```powershell
npm run build:tmm-lab    # contoh TMM; ganti per produk
```

Hasil wajib (satu run, satu buildId = `git rev-parse --short=7 HEAD`):

1. `*.ino.bin` — app-only BIN (OTA/LAN);
2. `*.ino.merged.bin` — merged/full BIN (USB/recovery);
3. `manifest.json` — manifest build dari core builder.

Gagal di sini? Periksa: profile `UNCONFIRMED` (bagian B guide), stage guard
production vs default LAB (`src/core/stage-guard.mjs`), toolchain ESP32.

## 3. Emit manifest build

```powershell
node scripts/emit-manifest.mjs --app <app.bin> --merged <merged.bin> `
  --out products/<p>/build/<pkg>/manifest.json `
  --build-id <short-commit> --source-commit <full-commit> `
  --profile profiles/<ID>/profile.json --version vX.Y.Z
```

## 4. Buat dua manifest library

Buat `manifest-full.json` dan `manifest-app-only.json` di
`telemetric-firmware-library/manifests/<PRODUCT>/`. Aturan:

- `releaseId` kanonik: `<PRODUCT>-<version>-<buildId>` (sama di keduanya);
- `stage` dan `firmwareRole` sama di keduanya;
- semua shared fields identik — daftar: `PACKAGE_SHARED_FIELDS` di
  `scripts/library.mjs`;
- `sizeBytes` dan `sha256` dihitung dari byte fisik tiap BIN.

## 5. Gate

```powershell
node scripts/validate-library.mjs
npm run gate -- --manifest manifests/<P>/<m>.json --bin "<bin>"
npm run gate -- --manifest manifests/<P>/<m>.json --bin "<bin>"
```

Semua harus lulus tanpa error sebelum publish.

## 6. Publish package

```powershell
npm run publish-package -- --manifest-app <app-manifest> --bin-app <app.bin> `
  --manifest-full <full-manifest> --bin-full <merged.bin>
```

Publisher akan:

1. memvalidasi pasangan (tepat satu full + satu app-only, shared fields
   identik, releaseId kanonik) **sebelum** panggilan GitHub pertama;
2. membuat satu release (`draft` untuk lifecycle draft/quarantined);
3. mengunggah 4 asset: dua BIN + `manifest-full.json` +
   `manifest-app-only.json`;
4. mengunduh ulang dan memverifikasi checksum kedua BIN serta isi kedua
   manifest;
5. **menghapus release** yang dibuat run ini bila langkah 2–4 gagal
   apa pun (agar tidak mengunci tag immutable).

## 7. Commit dan push library

```powershell
git -C "telemetric-firmware-library" add manifests notes
git -C "telemetric-firmware-library" commit -m "Add <PRODUCT> <version> dual-artifact package"
git -C "telemetric-firmware-library" push origin main
```

## 8. Verifikasi portal

1. Tunggu sync otomatis, atau admin jalankan
   `POST /api/firmware/library-sync`.
2. Query/cek: **tepat dua record** (full + app-only) untuk releaseId
   tersebut, `stage` dan `firmwareRole` tersimpan.
3. Buka `/products/<CODE>`: satu kartu package di container yang sesuai
   `firmwareRole`; tombol **USB** memilih merged BIN; tombol **OTA**
   memilih app-only BIN; badge LAB tampil bila `stage=lab`.
4. **Jangan flash perangkat** pada tahap verifikasi ini.

## 9. Kegagalan umum dan penanganan

| Gejala | Sebab | Penanganan |
|---|---|---|
| `dirty-worktree gate failed` | ada perubahan belum di-commit | commit/push source dulu (langkah 1) |
| `production build refused` | default LAB credential masih aktif | hanya untuk stage production: ganti `src/config/factory-wifi.mjs` |
| `release package must contain exactly one full and one app-only` | manifest salah satu hilang / imageType ganda | perbaiki pasangan manifest |
| `... differs between release artifacts` | shared fields tidak identik | samakan field yang disebut |
| `releaseId must be canonical` | releaseId bukan `<PRODUCT>-<version>-<buildId>` | perbaiki releaseId |
| `Release ... already exists and is immutable` | tag sudah pernah dipakai | naikkan version/buildId; jangan pernah menimpa |

## 10. Tutup

Centang [[New Product Bootstrap Checklist]]. Catatan fisik:
flash + provisioning + OTA pending/confirm/rollback di perangkat nyata
masih merupakan **Human Verification** terpisah.
