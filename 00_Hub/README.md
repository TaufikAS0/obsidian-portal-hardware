# 00 Hub — Map of Content

Vault koordinasi ekosistem Telemetric Hardware Portal. Mulai dari peta ini
untuk menemukan registry, rules, products, guides, dan history.

## Ekosistem

- [[00_Hub/ECOSYSTEM|ECOSYSTEM]] — gambaran besar: 1 portal + 1 library +
  N product firmware repos
- [[00_Hub/STATUS|STATUS]] — status vault dan maintenance log

## Registry — lokasi dan nama GitHub

- [[01_Registry/CENTRAL_REPOS|CENTRAL_REPOS]] — portal + library
- [[01_Registry/FIRMWARE_REPOS|FIRMWARE_REPOS]] — repo firmware per produk
- [[01_Registry/TOOL_REPOS|TOOL_REPOS]] — tools pendukung (termasuk device
  bootstrap framework)
- [[01_Registry/PRODUCTS|PRODUCTS]] — 37 kode produk
- [[01_Registry/DEVICES|DEVICES]] — mesin dan lokasi runtime

## Rules — aturan wajib

- [[02_Rules/ai-entry-protocol|AI Entry Protocol]] — README wajib dibaca
  pertama dan routing bacaan berdasarkan jenis pekerjaan
- [[02_Rules/registry-rules|Registry Rules]] — cara merawat registry
- [[02_Rules/device-bootstrap-standard|Device Bootstrap Standard]] —
  provisioning, fallback AP, OTA, recovery
- [[02_Rules/firmware-package-rules|Firmware Package Rules]] — satu versi =
  satu package: dua BIN + dua manifest, satu releaseId
- [[02_Rules/ai-handoff|AI Handoff]] — serah terima antar AI

## Products

- [[TMM|TMM — Telemetric Module Master]]
- [[TPM|TPM — Telemetric Power Monitor]]
- [[TVG|TVG — Telemetric Vision Grid]]
- [[03_Products/_TEMPLATE|Template note produk]]

## Guides — membuat bootstrap produk baru

1. [[04_Guides/New Product Bootstrap Guide|New Product Bootstrap Guide]] —
   panduan A–H (identitas → profile → adapter → build → publish → portal)
2. [[04_Guides/Bootstrap Build and Publish SOP|Build and Publish SOP]] — urutan perintah persis + penanganan kegagalan
3. [[04_Guides/New Product Bootstrap Checklist|Checklist]] — checklist siap salin
4. [[04_Guides/AI Prompt - New Product Bootstrap|AI Prompt]] — prompt siap salin untuk AI firmware

## History — keputusan dan riwayat

- [[05_History/TMM Bootstrap Implementation History|TMM Bootstrap History]] — dari kebutuhan awal sampai tampil di portal
- [[05_History/Firmware Package Architecture Decisions|Architecture Decisions]] — keputusan arsitektur + bukti commit

## Lainnya

- [[00_Hub/NEXT_AI_PROMPT|NEXT_AI_PROMPT]] — prompt tugas berantai
- `99_Archive/` — baris registry yang pensiun (jangan hard-delete)

## Current vault status

Lihat [[00_Hub/STATUS|STATUS]].
