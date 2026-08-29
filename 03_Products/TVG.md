# TVG — Telemetric Vision Grid

## Identity

| Field | Value |
|---|---|
| Code | `TVG` |
| Product name | Telemetric Vision Grid |
| Catalog group | Main Products |
| Firmware repo (local) | UNCONFIRMED |
| Firmware repo (GitHub) | UNCONFIRMED |
| Library manifests | `telemetric-firmware-library/manifests/TVG/` |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 1.4.2 | `manifests/TVG/1.4.2.json` | `TVG-v1.4.2` | UNCONFIRMED | first verified end-to-end pilot flash |
| 1.4.3 | `manifests/TVG/1.4.3.json` | `TVG-v1.4.3` | UNCONFIRMED | |

## Hardware

| Field | Value |
|---|---|
| MCU / board | ESP32-S3 (per pilot evidence) |
| Flash method | Web Serial via portal |
| Wi-Fi firmware | UNCONFIRMED |

## Lessons for the next AI

- `v1.4.2` completed the first real-board Web Serial pilot through the portal.
  Flash success did not imply QC PASS; the separate QC checklist remains
  mandatory.

## Evidence pointers

- Pilot: `telemetric-hardware-portal/docs/TVG_PILOT_FLASH.md`
- QC records: portal database (not Git)

## Registry gap

The firmware source repository for TVG is UNCONFIRMED. Confirming it is a
tracked open item in `../00_Hub/STATUS.md`.
