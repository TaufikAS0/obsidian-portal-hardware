# TOC — Telemetric Omni Controller

## Identity

| Field | Value |
|---|---|
| Product code/name | TOC — Telemetric Omni Controller; owner-confirmed 2026-10-29 |
| Catalog adoption | Pending library PR #1, feature/catalog-toc, commit d47b605; default catalog not yet changed |
| Product group proposal | Main Products, pending catalog review |
| PCB role | Motherboard / modular mainboard |
| PCB source | https://github.com/TaufikAS0/pcb-toc-mainboard (private) |
| PCB local | `D:\JIN Work\Document\0. JIN Project Github PCB\2026 TOC Mainboard` |
| Firmware repository | - (not created) |
| Firmware releases/manifests | None created in this task |
| Hardware revision, MCU, slots, bus, power, connector | UNCONFIRMED |
| Physical tests / production acceptance | UNCONFIRMED |

TOC berbeda dari TMO (Telemetric Outdoor), TMC dan TMPC. Identitas produk dikonfirmasi; detail hardware tidak diwarisi dari produk lain. Belum ada file KiCad, sehingga status adalah concept scaffold.

## Naming and module boundary

Repo motherboard `pcb-toc-mainboard` tidak memuat revision atau bottom/top. Usulan board identifier TOC-MB; revisi UNCONFIRMED. Calon module repo `pcb-toc-module-<fungsi>` hanya dibuat bila function dan source/lifecycle independen telah disepakati; jangan membuat repo kosong untuk setiap sirkuit.

Sumber keputusan interface dan pin nanti berada di repo PCB (04_Dokumen/Interface_Ledger_R01.md), bukan di registry ini. Konektor sama tidak membuktikan kompatibilitas elektrik/protokol/mekanik.

## Operations and next decision

- Registry PCB: [[01_Registry/PCB_REPOS|PCB_REPOS]].
- GitHub operations vault: [obsidian-github-manager](https://github.com/TaufikAS0/obsidian-github-manager) private; bukan portal flashing/QC.
- Belum menentukan daughterboard pada slot versus module node berkabel; owner menjawab sebelum konektor/pin disiapkan.
- Jangan mendaftarkan baris firmware fiktif di FIRMWARE_REPOS. Saat source firmware benar-benar dibuat, update registry dalam sesi yang sama.
