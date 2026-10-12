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
| 0.5.1 | 0.5.1-full.json + 0.5.1-app-only.json | TMC-v0.5.1-esp32 | draft/built | Standard portal USB, optional Full erase; merged image resets NVS |
| 0.5.0 | 0.5.0-app-only.json | TMC-v0.5.0 | draft/built | QC LAB; public LAB default; device Digest /update |

## Hardware

| Field | Value |
|---|---|
| MCU / board | classic ESP32, build target 16MB |
| Profile | TOP TMC_T_V2_R1 + BOTTOM TMC_B_V3_R0, V2_R1 pinmap per source; physical verification pending |
| Flash method | Standard portal USB full/merged with Fast write or Full erase + write; device /update for app-only OTA |
| Partition | factory 0x20000, dual 2MB OTA slots; merged resets NVS, full erase also deletes storage |
| Wi-Fi firmware | yes; ESP Scanner applies |

## Lessons for the next AI

- Owner approved intentional public LAB defaults on 2026-10-12. See ../02_Rules/lab-default-credentials.md.
- Output polarity/ADC conditioning need physical confirmation; keep output locks.
- RS485/RS232 transactions remain deferred; overall QC PASS not established.
- For preserve-data installation, do not use merged/full images or standard 0x10000 app offset. Owner explicitly permits destructive merged reset/install through portal in v0.5.1.

## Evidence pointers

- Source: feature/qc-operator-ota, build commit 5915765 (derived from 19042da).
- QC records: portal database, separate from downloaded firmware.
- Physical v0.5.0 testing: PENDING.
- v0.5.1 source e7c72e5; paired artifacts built, package tests and library gate passed. No physical flash/QC PASS.
