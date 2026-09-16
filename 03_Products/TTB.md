# TTB — Telemetric Test Bench

## Identity

| Field | Value |
|---|---|
| Code | `TTB` |
| Product name | Telemetric Test Bench |
| Catalog group | Support Tools |
| Firmware repo (local) | `D:\Home Work\Firmware Github\2026-05-esp-logger` |
| Firmware repo (GitHub) | https://github.com/TaufikAS0/2026-05-esp-logger |
| Library manifests | `telemetric-firmware-library/manifests/TTB/` |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 0.8.0-testing.1 | `manifests/TTB/0.8.0-testing.1-full.json` + `-app-only.json` | `TTB-v0.8.0-testing.1-esp32` | draft | Dual-artifact draft (ESP32 classic 4MB, ESP32 Dev Module, min_spiffs). `firmwareRole: testing` → Testing / LAB container; `stage: lab`. Source commit `bac4da58c26dc23fc1342c4291e7d5c21d750ae7`. Evidence: compile/build + artifact validation only (`evidenceLevel: built`). No bench test, no QC pass, no flash. |

## Hardware

| Field | Value |
|---|---|
| MCU / board | ESP32 klasik (ESP32 Dev Module, `esp32:esp32:esp32`), 4MB flash, flash mode qio, partition `min_spiffs` — build configuration only, not measured on target hardware |
| Flash method | Web Serial via portal (typical) |
| Wi-Fi firmware | Yes — firmware contract exposes Wi-Fi fields (`wifiCapable: true`); ESP IP Scanner applies to LAN discovery |
| Hardware revision / profile | UNCONFIRMED (portal profile stored as `UNCONFIRMED`) |
| Physical verification | PENDING — no physical board, flash, OTA, or peripheral (RTC/TFT) verification performed |

## Lessons for the next AI

- 2026-09-16: TTB source tooling uses `evidenceLevel: compile-only`; the firmware library vocabulary requires `built` for draft/build-only packages — map `compile-only` → `built` and keep every hardware claim pending.
- 2026-09-16: source manifests in the firmware repo lacked `schemaVersion`, `erasePolicy`, `wifiCapable`, `releaseNotes`; the library gate rejects them. The library manifests add these fields; `erasePolicy: prompt` follows the portal flash workflow and all 31 accepted manifests.
- 2026-09-16: the built BINs use `min_spiffs`, not the vendored `02_Firmware/portal/partitions/ttb_esp32_4mb_ota.csv`; always bind `partitionScheme` to the actual build log/artifacts, never to intent.

## Evidence pointers

- QC records: portal database (not Git)
- Flash pilot: UNCONFIRMED
- Draft release: https://github.com/TaufikAS0/telemetric-firmware-library/releases (tag `TTB-v0.8.0-testing.1-esp32`, draft)