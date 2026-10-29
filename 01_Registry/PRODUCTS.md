# Product Catalog Registry

All 39 product codes, copied from
`telemetric-firmware-library/catalog/products.json` (verify there before
editing). The "Firmware repo" column must match a row in `FIRMWARE_REPOS.md`.

Legend: `-` = no firmware repo yet. `UNCONFIRMED` = repo exists but not verified.

## Main Products

| Code | Name | Firmware repo |
|---|---|---|
| TMM | Telemetric Module Master | `2026-telemetric-module-master` |
| HUB | Telemetric Module Gateway | - |
| TMC | Telemetric Module Compact | - |
| TVL | Telemetric Voltage Logger | - |
| HGC | Heel Ground Checker | - |
| TGC | Telemetric Ground Checker | - |
| MIU | Mari Isi Ulang | - |
| TBNR | Telemetric Bluetooth NFC Reader | - |
| TIR | Infrared | - |
| TML | Telemetric Module Logger | - |
| TVG | Telemetric Vision Grid | UNCONFIRMED |

## White Label Product

| Code | Name | Firmware repo |
|---|---|---|
| TMO | Telemetric Outdoor | - |
| GTLM | Gas Tank Level Monitoring | - |
| MTN | UBS IoT Device Maintenance | - |
| TGC15 | Ground Checker 15 Channel | - |
| TGC30 | Ground Checker 30 Channel | - |
| LAC | A.I. Cleshi Air Cleaner | - |
| AOM | Automatic Oxygen Manifold | https://github.com/TaufikAS0/esp32-hardware-test-manifold |
| ANM | Automatic Nitrogen Manifold | - |
| VAS | Vacuum Air Simplex | - |
| VAD | Vacuum Air Duplex | - |
| MAQ | Medical Air Quadruplex | - |
| MAD | Medical Air Duplex | - |
| MAS | Medical Air Simplex | - |
| ICP | I-Cross CP | - (web tooling exists, see `TOOL_REPOS.md`) |
| ICU | I-Cross CU | - |

## Expansion Modules

| Code | Name | Firmware repo |
|---|---|---|
| TMB-X | Telemetric Modbus Expansion | - |
| TDI-X | Telemetric Digital Input Expansion | - |
| TPS-X | Telemetric Pulse to Serial Expansion | - |
| BNR | Telemetric Wiegand Reader Expansion | - |
| TPOS | Telemetric Panel Outdoor System | - |
| TBM-X | Telemetric RS485 Bus Manager | - |
| TMR | Meteran | - |
| TWR-USB | Writer (USB Protocol) | - |
| TIR-X | Infrared | - |

## Support Tools / Platform

| Code | Name | Firmware repo |
|---|---|---|
| TDL | Downloader | - |
| TPM | Telemetric Power Monitor | UNCONFIRMED |
| TTB | Telemetric Test Bench | `2026-05-esp-logger` |
| TMPC | Modular PCB Concept | - |

## Rules

### Pending catalog adoption — not part of the default code count

TOC = Telemetric Omni Controller, owner-confirmed 2026-10-29. [Library catalog PR #1](https://github.com/TaufikAS0/telemetric-firmware-library/pull/1), feature/catalog-toc at d47b605, proposes one Main Product (39 → 40). Until catalog adoption, keep the existing mirrored tables unchanged; [[03_Products/TOC|TOC concept]] and [[01_Registry/PCB_REPOS|PCB registry]] record the real new hardware repository. Firmware repo does not exist. After library integration is accepted, refresh the mirror from that exact catalog commit, without treating catalog presence as firmware/hardware acceptance.

1. When a firmware repo is created for a code, replace `-` with the repo name
   and add the full row to `FIRMWARE_REPOS.md` in the same session.
2. A catalog entry does not imply production firmware exists.
3. Do not add new codes here without adding them to the library catalog first —
   `catalog/products.json` is the source of truth for the code list.
