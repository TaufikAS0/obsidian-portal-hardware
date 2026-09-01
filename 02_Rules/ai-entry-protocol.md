# AI Entry Protocol

Aturan ini menentukan dokumen apa yang wajib dibaca AI sebelum bekerja di
ekosistem Telemetric Hardware Portal.

## Aturan utama

1. Baca root `README.md` **lebih dahulu**.
2. Baca root `AGENTS.md` dan protokol ini sampai selesai.
3. Tentukan jenis pekerjaan dari tabel routing pada README.
4. Baca seluruh dokumen wajib pada jalur tersebut sebelum menjalankan command
   yang mengubah state atau mengedit file.
5. Baca `AGENTS.md` milik repository target sebelum bekerja di repository itu.
6. Untuk pekerjaan produk, baca `03_Products/<CODE>.md`. Jika belum ada, buat
   dari `03_Products/_TEMPLATE.md` dan tandai fakta yang belum diketahui sebagai
   `UNCONFIRMED`.
7. Verifikasi repository, branch, hardware profile, versi, manifest, dan status
   live. Jangan mengandalkan laporan AI sebelumnya sebagai satu-satunya bukti.

## Minimum reading by task

| Jenis pekerjaan | Dokumen minimum |
|---|---|
| Registry atau pencarian repo | [[02_Rules/registry-rules|Registry Rules]] dan registry terkait di `01_Registry/` |
| Firmware produk | [[02_Rules/firmware-package-rules|Firmware Package Rules]] dan note produk |
| Bootstrap, provisioning, AP, NVS, OTA | [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]] dan [[04_Guides/New Product Bootstrap Guide|Bootstrap Guide]] |
| Build atau publish package | [[04_Guides/Bootstrap Build and Publish SOP|Build and Publish SOP]] dan [[04_Guides/New Product Bootstrap Checklist|Checklist]] |
| Portal, Web Serial, OTA LAN, atau QC | [[01_Registry/CENTRAL_REPOS|Central Repositories]] lalu rules repository portal |
| Keputusan desain atau investigasi historis | [[05_History/Firmware Package Architecture Decisions|Architecture Decisions]] dan history produk terkait |
| Handoff ke AI lain | [[02_Rules/ai-handoff|AI Handoff]] |

## Stop conditions

Berhenti dan laporkan fakta yang kurang apabila pekerjaan membutuhkan salah satu
hal berikut tetapi belum terverifikasi:

- hardware profile atau pin yang memengaruhi keselamatan;
- chip family, flash geometry, atau partition scheme;
- BIN, manifest, ukuran, atau checksum yang seharusnya sudah ada;
- autentikasi atau kewenangan publish yang nyata;
- target fisik yang akan di-flash.

Gunakan `UNCONFIRMED`; jangan mengganti bukti yang hilang dengan asumsi.

## Completion gate

Sebelum menyatakan selesai:

- periksa kembali diff dan file milik pengguna;
- jalankan test/gate yang diwajibkan repository target;
- bedakan build, publish, import portal, flash fisik, dan QC;
- update registry jika struktur ekosistem berubah;
- laporkan bukti konkret dan unknowns yang tersisa.

Kembali ke [[00_Hub/README|Hub / Map of Content]].
