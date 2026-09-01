# Obsidian Portal Hardware Vault

> [!IMPORTANT] AI: READ THIS FILE FIRST
> Sebelum menjalankan command, mengubah file, membuat firmware, atau melakukan
> publish, baca `README.md` ini sampai selesai lalu ikuti urutan baca di bawah.

Vault ini adalah pusat navigasi dan koordinasi untuk ekosistem **Telemetric
Hardware Portal**. Di sini manusia dan AI mencari lokasi repository, aturan
firmware, catatan produk, panduan kerja, serta sejarah keputusan teknis.

GitHub: https://github.com/TaufikAS0/obsidian-portal-hardware

## Urutan baca wajib untuk AI

1. **File ini** — pahami fungsi vault dan tentukan jenis pekerjaan.
2. [[02_Rules/ai-entry-protocol|AI Entry Protocol]] — pilih jalur baca yang
   sesuai dengan pekerjaan.
3. `AGENTS.md` — aturan kerja, keselamatan, registry, dan laporan akhir.
4. [[00_Hub/README|Hub / Map of Content]] — peta seluruh catatan.
5. Baca rules, product note, guide, dan history yang diwajibkan oleh jalur
   pekerjaan. Jangan mulai bekerja hanya dengan membaca README.

Jika fakta penting tidak tersedia, tulis `UNCONFIRMED`. Jangan menebak hardware,
repository, versi, checksum, lifecycle, atau hasil pengujian.

## Pilih jalur pekerjaan

| Pekerjaan | Bacaan wajib setelah README dan AGENTS |
|---|---|
| Mencari atau mendaftarkan repository | [[02_Rules/registry-rules|Registry Rules]], [[01_Registry/CENTRAL_REPOS|Central Repositories]], [[01_Registry/FIRMWARE_REPOS|Firmware Repositories]] |
| Mengerjakan firmware produk | Catatan di `03_Products/<CODE>.md`, [[02_Rules/firmware-package-rules|Firmware Package Rules]] |
| Membuat bootstrap produk baru | [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]], [[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]], [[04_Guides/New Product Bootstrap Checklist|Checklist]] |
| Build dan publish dua BIN | [[04_Guides/Bootstrap Build and Publish SOP|Build and Publish SOP]], [[02_Rules/firmware-package-rules|Firmware Package Rules]] |
| Mengubah portal, flashing, atau QC | [[01_Registry/CENTRAL_REPOS|Central Repositories]], lalu `AGENTS.md` di repository portal |
| Memahami alasan arsitektur | [[05_History/Firmware Package Architecture Decisions|Architecture Decisions]] dan [[05_History/TMM Bootstrap Implementation History|TMM Bootstrap History]] |
| Menyerahkan pekerjaan ke AI lain | [[02_Rules/ai-handoff|AI Handoff]] |

## Bentuk ekosistem

- Satu portal lokal: `telemetric-hardware-portal`.
- Satu firmware library: `telemetric-firmware-library`.
- Banyak repository firmware produk yang masing-masing memiliki versi sendiri.
- BIN berada di GitHub Release, bukan Git history.
- Satu firmware package modern berisi dua BIN dan dua manifest yang diikat satu
  `releaseId`.
- Portal menentukan lifecycle, izin flashing, audit, dan QC.

## Struktur vault

| Folder | Isi |
|---|---|
| `00_Hub/` | Map of Content dan status ekosistem |
| `01_Registry/` | Lokasi, GitHub, produk, perangkat, dan repository |
| `02_Rules/` | Aturan wajib untuk manusia dan AI |
| `03_Products/` | Satu catatan per produk |
| `04_Guides/` | Tutorial, SOP, checklist, dan prompt siap pakai |
| `05_History/` | Sejarah implementasi dan keputusan arsitektur |
| `99_Archive/` | Catatan pensiun; jangan hard-delete |

## Prinsip singkat

- Baca sebelum mengubah.
- Verifikasi sebelum mengklaim.
- Gunakan `UNCONFIRMED` daripada menebak.
- Preserve data historis dan perubahan milik pengguna.
- Build berhasil bukan bukti hardware berhasil.
- Publish bukan approval untuk flash.

Mulai navigasi dari [[00_Hub/README|Hardware Portal Hub]].
