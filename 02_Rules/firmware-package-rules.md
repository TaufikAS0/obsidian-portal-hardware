# Firmware Package Rules

## Simple explanation (for everyone, not just engineers)

- One firmware version = one package. There is no "USB firmware" and
  "separate OTA firmware"; there is only one version per release.
- Every package MUST have a merged/full BIN (`firmware.bin`). The portal uses
  it for USB flashing.
- Every package MUST have an app-only BIN (`firmware.app.bin`). The portal
  uses it for OTA/LAN updates.
- Both BINs MUST come from the same source commit and the same build run.
- `manifest.json` binds both BINs together under one `releaseId`, and carries
  the SHA-256 and byte size of each BIN.
- The operator only ever sees one version in the portal and simply chooses the
  update method: USB or OTA/LAN. The portal picks the correct BIN
  automatically.

## Required artifacts

| Artifact | Required | Purpose |
|---|---|---|
| `firmware.bin` (merged/full image) | yes | Full flashable image including bootloader and partition table (USB) |
| `firmware.app.bin` (app-only image) | yes | Application-only image for OTA/LAN updates |
| `manifest.json` | yes | Metadata: `releaseId`, version, build id, channel, SHA-256 and byte size of both BINs, chip family, hardware revision |

## Rules

1. Both BINs MUST come from the same source commit and the same build run.
2. `manifest.json` MUST list the SHA-256 and byte size of each BIN.
3. The manifest MUST be registered together with the version under one
   `releaseId`; a version without its manifest is treated as incomplete and
   must not be flashed.
4. USB (merged) and OTA/LAN (app-only) artifacts are two views of the same
   version — never two independent firmware releases.
5. If one of the two BINs is missing, the affected update method is disabled
   in the portal with a short reason; the other method stays usable.
