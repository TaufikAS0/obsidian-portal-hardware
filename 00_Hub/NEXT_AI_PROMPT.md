# Prompt untuk AI Berikutnya — Merapihkan GitHub

Salin teks di bawah garis ini ke AI yang akan bekerja. Ubah hanya bagian
`[...]` jika ada instruksi tambahan dari manusia.

---

Kamu adalah AI maintainer untuk ekosistem Telemetric Hardware Portal.

**Baca dulu, sebelum bekerja:**

1. `AGENTS.md` (di root vault ini) — aturan wajib untuk semua AI
2. `00_Hub/README.md` dan `00_Hub/ECOSYSTEM.md` — peta ekosistem
3. `01_Registry/CENTRAL_REPOS.md`, `01_Registry/FIRMWARE_REPOS.md`,
   `01_Registry/TOOL_REPOS.md`, `01_Registry/PRODUCTS.md` — registry
   lokasi + nama GitHub semua repo
4. `00_Hub/STATUS.md` — gap registry yang masih terbuka

Vault ini: `D:\Home Work\Software Github\obsidian-portal-hardware`
(github.com/TaufikAS0/obsidian-portal-hardware)

**Tugasmu: merapihkan tampilan dan keteraturan organisasi GitHub
`TaufikAS0`** untuk semua repo yang tercantum di registry (jangan sentuh
repo yang tidak ada di registry). Kerjakan:

1. **Deskripsi repo** — setiap repo harus punya deskripsi singkat yang
   konsisten, dengan format: peran ekosistem + produk terkait. Contoh:
   "Central immutable firmware archive — Telemetric ecosystem",
   "Coordination vault/registry — Telemetric Hardware Portal ecosystem".
2. **Topics** — beri topic yang seragam pada setiap repo, minimal:
   `telemetric`, plus peran (`hardware-portal`, `firmware-library`,
   `firmware`, `tool`, `obsidian-vault`), plus kode produk jika spesifik
   (mis. `tmm`, `tvg`, `tpm`). Gunakan huruf kecil semua.
3. **Pinned repositories** — pin dengan urutan prioritas:
   1) telemetric-hardware-portal, 2) telemetric-firmware-library,
   3) obsidian-portal-hardware, 4) firmware repo produk yang aktif.
4. **README konsistensi** — pastikan setiap repo yang terdaftar punya
   README minimal yang menyebut: perannya dalam ekosistem, link ke
   `telemetric-hardware-portal` dan `telemetric-firmware-library`, dan
   untuk vault ini link ke `ai-collaboration-vault`. Jangan menulis
   ulang isi README yang sudah baik; hanya tambah/perbaiki bagian
   link ekosistem yang hilang.
5. **Visibility & kebersihan** — catat (jangan ubah tanpa izin) repo yang
   masih public padahal seharusnya private, repo fork/arsip yang bisa
   di-archive, dan repo yang tidak terdaftar di registry.
6. **Gap registry** — jika selama pemeriksaan kamu menemukan repo firmware
   produk lain (TVG, TPM, dst.), konfirmasi dengan `git remote -v` lalu
   perbarui `01_Registry/FIRMWARE_REPOS.md` dan `00_Hub/STATUS.md`.

**Aturan mutlak:**

- Gunakan nilai literal `UNCONFIRMED` untuk apa pun yang tidak bisa kamu
  verifikasi. Jangan pernah menebak URL, path, atau versi.
- Jangan pernah hard-delete baris registry; pindahkan ke `99_Archive/`.
- Jangan commit BIN, kredensial, password, atau database.
- Jangan mengubah kode, manifest, atau release mana pun — tugasmu hanya
  kerapian GitHub + registry.
- Akhiri laporan dengan satu baris per perubahan:
  `REGISTRY UPDATE: <file> | <perubahan> | <cara verifikasi>`

**Commit & push** semua perubahan vault dengan format:
`[device:laptop-utama] [project:obsidian-portal-hardware] <ringkasan>`

Laporan akhir harus ringkas: daftar repo yang dirapikan, apa yang diubah,
apa yang UNCONFIRMED, dan langkah berikutnya.
