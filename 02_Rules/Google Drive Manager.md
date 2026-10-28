# Google Drive Manager Jaya

Catatan kerja untuk manusia dan AI yang membantu Jaya membuat folder, menyalin file seperti block diagram, mencari dokumen, dan merapikan Google Drive. Instruksi pengguna pada tugas terbaru menentukan ruang lingkup pekerjaan.

## Sebelum bekerja

- Periksa akun Google aktif dan hak akses. Akun kerja yang digunakan pada proyek arsip ini adalah `jayaintegrasinusantara@gmail.com`; verifikasi kembali setiap sesi.
- Temukan folder sumber dan tujuan yang benar berdasarkan nama, lokasi, dan tautan. Jika ada beberapa kandidat yang sama-sama masuk akal, minta pengguna menunjukkan pilihan sebelum membuat atau menyalin item yang salah.
- Periksa isi, owner, izin, dan apakah file/folder tujuan sudah ada. Jangan berasumsi nama yang sama berarti isinya sama.
- Untuk tugas penyalinan arsip Jaya yang sudah ada, gunakan skill lokal `google-drive-jaya-archive` bila tersedia; baca checkpoint aktual sebelum melanjutkan.

## Membuat folder dan menyalin file

Untuk **setiap proyek PCB baru**, tanyakan terlebih dahulu kepada pengguna: proyek ini **Internal**, **External Indonesia**, **International**, atau lokasi lain; folder induk dan produk/proyek mana; serta subfolder apa saja yang dibutuhkan. Tanyakan juga folder sumber template/file jika belum jelas. Jika pengguna sudah memberikan informasi itu untuk pekerjaan saat ini, gunakan jawaban tersebut tanpa meminta ulang. Jangan menebak lokasi atau membuat struktur sebelum lokasi dan folder yang dibutuhkan jelas. Setelah dibuat, catat path dan tautan folder proyek dalam log pekerjaan di bawah.

Struktur referensi Modul Compact yang diamati pada 2026-10-28: `3D Design`, `Block Diagram`, `Document`, `Picture`, `Pin List`, `Report QC`. Tawarkan sebagai acuan dan tanyakan folder yang diperlukan untuk setiap proyek baru; ini bukan daftar wajib otomatis. Folder `(Original)` adalah sumber historis, bukan bagian dari template standar. Template pin list Compact berisi data Compact sampai disesuaikan dan diverifikasi terhadap revisi PCB target.

1. Ikuti lokasi dan struktur yang diminta pengguna. Buat hanya folder yang diperlukan untuk tugas itu; jangan menciptakan struktur tambahan tanpa alasan yang jelas.
2. Untuk block diagram atau file lain, verifikasi sumber dan tujuan sebelum menyalin. Pertahankan nama dan tipe file kecuali pengguna meminta perubahan.
3. Periksa salinan yang dibuat: nama, lokasi, jenis, dan owner; untuk file biner gunakan ukuran/checksum bila tersedia. Buka atau pratinjau bila perlu untuk memeriksa hasil. Salinan Google Docs/Sheets/Slides dapat memiliki ukuran metadata berbeda.
4. Catat tautan sumber dan salinan, lokasi, owner, tanggal, dan hasil pemeriksaan. Jika ada file yang tidak dapat disalin, shortcut dengan target tak dapat diakses, atau akses tidak mencukupi, laporkan item tersebut; jangan menyebut tugas selesai seluruhnya.
5. Penyalinan membuat item baru; itu tidak memindahkan kepemilikan sumber. Folder milik Jaya tidak otomatis menjadikan seluruh file di dalamnya milik Jaya. Salinan dapat mewarisi akses dari folder tujuan, jadi periksa konsekuensi akses sesuai tugas.

### Menyalin folder berbagi ke akun Jaya

- Periksa akun aktif, lokasi, struktur dan isi sumber, owner setiap item, ruang tersedia, dan salinan yang sudah ada. Buat ulang folder tujuan sesuai struktur sumber dan pastikan folder baru milik Jaya.
- Salin file dari setiap folder sumber, lalu pastikan setiap salinan milik Jaya dan berada di folder tujuan yang benar. Di antarmuka Drive, **Make a copy** dapat membuat salinan di folder sumber; pindahkan hanya salinan yang teridentifikasi, bukan sumber. Jika Drive memberi peringatan perubahan akses, jelaskan konsekuensinya dan ikuti persetujuan pengguna sebelum memindahkan.
- Saat membuat salinan kerja, hapus awalan otomatis `Copy of ` dari nama salinan, pertahankan nama lainnya dan ekstensi, kecuali pengguna meminta nama lain. Periksa nama, jumlah, owner, lokasi dan ukuran untuk file biner; ukuran yang sama belum membuktikan checksum sama.
- Hapus atau lepaskan sumber hanya jika pengguna secara jelas meminta tindakan itu dan salinan sudah diverifikasi. Periksa pesan Drive dan jelaskan hasil sebenarnya: `Remove` dari tampilan tidak membuktikan file terhapus dari akun owner atau akses kolaborator dicabut. ID dan tautan salinan berbeda dari sumber.

## Template dokumen proyek OneDrive

Untuk permintaan dokumen proyek berikutnya, gunakan dua dokumen berikut sebagai template standar ketika diperlukan: [Assessment Report](https://onedrive.live.com/personal/846f550bc22ced94/_layouts/15/Doc.aspx?sourcedoc=%7BD6E40665-A5A4-4202-91B4-951773C15D70%7D) dan [Penawaran & Timeline](https://onedrive.live.com/personal/846f550bc22ced94/_layouts/15/Doc.aspx?sourcedoc=%7B779553B5-138C-4F69-8459-359DC9365966%7D). Salin sumber ke folder Document proyek yang ditentukan, pertahankan sumber dan ganti nama salinan sesuai nama proyek. Periksa lokasi, akses dan salinan yang sudah ada sebelum menyalin. Isi sumber berkaitan dengan proyek Device IoT Maintenance; periksa dan sesuaikan nama, data pelanggan, ruang lingkup, harga dan jadwal sebelum digunakan. Mengubah nama file saja tidak mengubah isinya.

## Menjaga file dan merapikan

- Jangan menghapus file atau folder sumber sebagai bagian dari penyalinan. Jangan menimpa file yang sudah ada tanpa permintaan yang jelas. Jika hasil tindakan tidak pasti, periksa dulu sebelum mencoba lagi agar tidak membuat salinan ganda.
- Sebelum memindah atau mengganti nama dalam pekerjaan perapihan, periksa lokasi, hak akses, dan dampaknya bagi tim; lakukan sesuai instruksi pengguna. Perubahan berbagi atau kepemilikan memerlukan kewenangan yang sesuai.
- Bila pengguna meminta salinan di lokasi yang sama dan sumber diberi label `(Original)`, pastikan salinan lengkap dan dapat diperiksa dahulu; ubah nama sumber hanya jika akun memiliki izin dan permintaan tersebut memang berlaku pada item itu. Pertahankan ekstensi file.
- Item yang tampak kosong mungkin template atau memiliki isi di luar akses akun. Jangan hapus atau gabungkan berdasarkan nama atau hasil pencarian saja.
- Cek ruang kosong aktual dan batas layanan sebelum pekerjaan besar. Jangan membuat trigger, jadwal, atau kelanjutan otomatis tanpa permintaan pengguna; preferensi terakhir untuk arsip ini adalah bekerja selama chat aktif.

## Laporan dan kesinambungan

Setelah setiap pekerjaan, tulis ringkasan singkat di bagian **Log pekerjaan**: tanggal, permintaan, sumber dan tujuan, tindakan, tautan, hasil verifikasi, dan kendala/lanjutan. Catat hanya informasi yang relevan; jangan simpan password, token, cookie, atau tautan autentikasi sementara.

Bedakan fakta yang sudah diverifikasi, dugaan, dan `UNCONFIRMED`. Untuk pekerjaan massal, sebutkan progres antrean, jumlah salinan yang tercatat, jumlah yang sudah diverifikasi, error, dan apakah proses aktif. Jangan menganggap checkpoint antrean sebagai jumlah file yang sukses atau menyatakan backup selesai sebelum verifikasi selesai.

## Konteks proyek yang sudah ada

- Contoh folder Product: [Product di Drive](https://drive.google.com/drive/folders/19dM0B2J4fiE8tLrSahaNpLLYknUYFl-u). Salinan dan sumber berlabel `(Original)` pernah ditata di dalamnya; owner sumber asli tetap pemilik sebelumnya.
- [Arsip snapshot Jaya](https://drive.google.com/drive/folders/1o0ahJMUjkrhfl0QR15ar3aXQcRC_dZRh) masih memerlukan pemeriksaan status langsung. Angka progres lama bukan bukti kondisi saat ini.
- Laporan audit folder lokal: `C:/Users/taufi/Documents/Codex/2026-10-27/ak/outputs/peta-folder-jaya.html`; ini snapshot, bukan tampilan live.

## Log pekerjaan

### 2026-10-28 — Aturan dibuat

Pengguna meminta catatan Obsidian untuk bantuan membuat folder, menyalin block diagram dan pekerjaan Google Drive sejenis. Aturan disimpan di vault tim hardware. Pembuatan catatan ini tidak menjalankan pekerjaan baru pada Drive. Status arsip saat aturan dibuat: **UNCONFIRMED** sampai diperiksa langsung.

### 2026-10-28 — Pencarian Motion Sensor

Ditemukan [Modul Telemetric Motion Sensor](https://drive.google.com/drive/folders/1ZmHyG5_rhS5GDaOPFdibp0IAD-RG6xvo) di Product, di bawah Internal Projects. Hasil pencarian Drive menampilkan owner folder sebagai akun Jaya. Folder berisi subfolder Block Diagram; pencarian juga menemukan file `Telemetric Motion Sensor.drawio` di Block Diagram dengan owner Jaya. Pencarian ini tidak mengubah isi Drive.

### 2026-10-28 — Struktur Motion Sensor dan template Pin List

Pengguna memilih Projects / Internal Projects / Product / [Modul Telemetric Motion Sensor](https://drive.google.com/drive/folders/1ZmHyG5_rhS5GDaOPFdibp0IAD-RG6xvo) dan meminta struktur seperti Modul Compact. Folder `Block Diagram` sudah ada; folder `3D Design`, `Document`, `Picture`, [Pin List](https://drive.google.com/drive/folders/1lje6zsS0hU3_Zpq9QG7qmZ44ZV-aDjHK), dan `Report QC` dibuat dengan owner Jaya.

Sumber: [Modul Compact / Pin List](https://drive.google.com/drive/folders/1w0r4CrP3x2aomzgpLClrk1kV8AVIPzfG), `Modul Compact Pin List.xlsx`. Salinan `TMS Pin List.xlsx` telah ditempatkan di [Pin List TMS](https://drive.google.com/drive/folders/1lje6zsS0hU3_Zpq9QG7qmZ44ZV-aDjHK), dengan owner Jaya dan akses folder tujuan sesuai persetujuan pengguna. File sumber Compact tetap di lokasi asal. Isinya masih data Compact dan bukan pinlist TMS yang telah diverifikasi.

### 2026-10-28 — Folder TMS di OneDrive

Pengguna memilih proyek internal. Folder **Modul Telemetric Motion Sensor** telah dibuat di akun OneDrive Jaya pada `My files / JIN Project / 0. Project Internal (JIN) / Modul Telemetric Motion Sensor`. [Buka folder OneDrive](https://onedrive.live.com/my?id=%2Fpersonal%2F846f550bc22ced94%2FDocuments%2FJIN%20Project%2F0%2E%20Project%20Internal%20%28JIN%29%2FModul%20Telemetric%20Motion%20Sensor). Folder induk ditampilkan sebagai Shared; periksa akses aktual sebelum menambahkan dokumen. Pengguna memilih **hanya folder utama dulu**, tanpa subfolder.

### 2026-10-28 — Template dokumen TMS di OneDrive

Atas permintaan berikutnya, folder [Document TMS](https://onedrive.live.com/my?id=%2Fpersonal%2F846f550bc22ced94%2FDocuments%2FJIN%20Project%2F0%2E%20Project%20Internal%20%28JIN%29%2FModul%20Telemetric%20Motion%20Sensor%2FDocument) dibuat dan dua sumber template di atas disalin ke dalamnya. OneDrive menampilkan `Assessment Report - Modul Telemetric Motion Sensor.docx` (7,35 MB) dan `Penawaran & Timeline - Modul Telemetric Motion Sensor.docx` (2,69 MB). Sumber tetap pada lokasi asal. Folder dan salinan ditampilkan sebagai Shared; owner individual dan isi salinan belum diverifikasi. Nama file telah diubah, tetapi isi belum disesuaikan untuk TMS.

### 2026-10-28 — Salinan Picture TMS

Di [Picture TMS](https://drive.google.com/drive/folders/1AvPvU5FGnrfW-VzUFdipYp1zNQ4RlWMu), empat gambar dari Option 1 dan dua dari Option 2 milik Satrio disalin atas nama Jaya. Folder hasil [Option 1](https://drive.google.com/drive/folders/1HTz_9qUbHfcQhRyYGYkji0gXXOqN6pUt) dan [Option 2](https://drive.google.com/drive/folders/1XL1uDi67P_KrjjwM_C7exqD3oPR9wUES) milik Jaya; ukuran tampilannya cocok dengan sumber, nama file salinan berawalan Copy of. Pengguna menyetujui perubahan akses saat pemindahan salinan. Dua folder asli dikeluarkan dari tampilan Picture sesuai permintaan; Drive menyatakan kolaborator tetap memiliki akses, sehingga ini bukan bukti sumber terhapus dari akun Satrio. Checksum belum diperiksa dan tautan salinan berbeda dari sumber.

Pada permintaan berikutnya di hari yang sama, awalan `Copy of` dihapus dari nama keenam salinan; ekstensi dan kepemilikan tetap.
