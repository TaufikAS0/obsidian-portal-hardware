# Telemetric Device Bootstrap Standard

## Keputusan utama

Nama sistem umum adalah **Telemetric Device Setup**. Repo sumber bersama:
`2026-telemetric-device-bootstrap`.

Yang dibuat universal adalah alur provisioning, API, nama setup, keamanan, dan
format release. BIN tidak universal lintas-hardware; setiap chip dan revisi
hardware tetap mempunyai profile dan build sendiri.

## Alur yang wajib

1. Perangkat mencoba Wi-Fi terakhir yang tersimpan di NVS.
2. Jika gagal, perangkat mencoba Wi-Fi bootstrap/factory yang dikonfigurasi
   di luar source code Git.
3. Jika masih gagal, perangkat membuka AP `TELEMETRIC-SETUP-XXXXXX`.
4. Operator membuka `http://192.168.4.1/`, memilih jaringan, lalu menyimpan.
5. AP ditutup, perangkat masuk LAN, dan tampil di scanner portal.
6. Update normal berikutnya memakai OTA app-only yang terautentikasi.
7. USB merged/full tetap tersedia untuk instalasi awal dan recovery.

## Identitas standar

| Item | Nilai |
|---|---|
| Nama UI | Telemetric Device Setup |
| AP fallback | `TELEMETRIC-SETUP-XXXXXX` |
| Hostname | `telemetric-<product>-<device-suffix>` |
| Setup | `http://192.168.4.1/` |
| Device info | `GET /api/device-info` |
| Provisioning | `POST /api/provisioning` |
| OTA | `POST /api/ota/image` |

## Aturan keamanan

- Password Wi-Fi, token OTA, key, dan credential perangkat tidak boleh masuk
  Git, manifest, release note, log, screenshot, atau catatan Obsidian.
- Password Wi-Fi bersama hanya fallback provisioning, bukan trust boundary.
- AP harus unik per unit dan berhenti setelah provisioning berhasil.
- OTA harus terautentikasi, memakai A/B slot, health confirmation, dan rollback.
- Satu keberhasilan OTA bukan QC PASS.

## Paket firmware

Setiap version + hardware profile wajib menghasilkan dalam satu build:

- merged/full BIN untuk USB bootstrap/recovery;
- app-only BIN untuk OTA/LAN;
- manifest dengan satu `releaseId`, source commit, profile, offset, ukuran, dan
  SHA-256 kedua BIN.

Detail teknis dan template profile berada di repo bootstrap. AI wajib membaca
aturan repo dan tidak boleh menebak pin, flash geometry, partition, atau status
kesiapan hardware.
