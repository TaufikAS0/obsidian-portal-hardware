# TPM — Telemetric Power Monitor

## Identity

| Field | Value |
|---|---|
| Code | `TPM` |
| Product name | Telemetric Power Monitor |
| Catalog group | Support Tools |
| Firmware repo (local) | UNCONFIRMED (portal README references its INA3221 source repository) |
| Firmware repo (GitHub) | UNCONFIRMED |
| Library manifests | `telemetric-firmware-library/manifests/TPM/` |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 0.16.24 | `manifests/TPM/0.16.24.json` | `TPM-v0.16.24` | UNCONFIRMED | |

## Hardware

| Field | Value |
|---|---|
| Sensor | INA3221 (per portal README) |
| MCU / board | UNCONFIRMED |
| Flash method | Web Serial via portal |
| Wi-Fi firmware | UNCONFIRMED |

## Lessons for the next AI

- The portal includes a dedicated TPM support tool view linked to its source
  repository. Once the source repo is confirmed, register it in
  `../01_Registry/FIRMWARE_REPOS.md` and update the portal note.

## Evidence pointers

- QC records: portal database (not Git)

## Registry gap

The firmware source repository for TPM is UNCONFIRMED. Confirming it is a
tracked open item in `../00_Hub/STATUS.md`.
