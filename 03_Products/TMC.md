# TMC - Telemetric Module Compact

## Identity

| Field | Value |
|---|---|
| Code | TMC |
| Product name | Telemetric Module Compact |
| Catalog group | Main Products |
| Firmware repo (local) | D:\Home Work\Firmware Github\compact-qc-tester-v2-r1 |
| Firmware repo (GitHub) | https://github.com/TaufikAS0/compact-qc-tester-v2-r1 |
| Library manifests | telemetric-firmware-library/manifests/TMC/ |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 0.5.0 | 0.5.0-app-only.json | TMC-v0.5.0 | draft/built | QC LAB; public LAB default; device Digest /update |

## Hardware

| Field | Value |
|---|---|
| MCU / board | classic ESP32, build target 16MB |
| Profile | TOP TMC_T_V2_R1 + BOTTOM TMC_B_V3_R0, V2_R1 pinmap per source; physical verification pending |
| Flash method | app-only device /update; no portal automatic OTA or merged USB claim |
| Partition | factory 0x20000, dual 2MB OTA slots, preserve NVS/storage |
| Wi-Fi firmware | yes; ESP Scanner applies |

## Lessons for the next AI

- Owner approved intentional public LAB defaults on 2026-10-12. See ../02_Rules/lab-default-credentials.md.
- Output polarity/ADC conditioning need physical confirmation; keep output locks.
- RS485/RS232 transactions remain deferred; overall QC PASS not established.
- Do not overwrite NVS with merged images or use standard 0x10000 app offset.

## Evidence pointers

- Source: feature/qc-operator-ota, build commit 5915765 (derived from 19042da).
- QC records: portal database, separate from downloaded firmware.
- Physical v0.5.0 testing: PENDING.
