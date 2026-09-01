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

## Bootstrap LAB packages (decisions 2026-08-31)

These decisions apply to LAB packages produced through the shared
`2026-telemetric-device-bootstrap` framework (`Telemetric Device Setup`):

- The bootstrap repository is a **shared framework/tool**, not one universal
  BIN. Nothing about it replaces product firmware.
- Every BIN stays bound to one **productCode** and one **hardware profile**;
  chip family, flash geometry, and partition layout are never universal.
- One release still ships the pair: merged/full BIN (USB) + app-only BIN
  (OTA/LAN), bound by one `releaseId` in the library manifest.
- The **factory Wi-Fi for LAB** is deliberately committed to Git as a LAB
  build input and embedded inside the LAB BIN, so a fresh LAB unit connects
  on first boot and stores the credential in NVS. This is allowed for LAB
  builds only. The password must never appear in release manifests, logs,
  operator/AI notes, or production builds; production credentials stay out
  of Git entirely.
- LAB builds MUST carry `stage: "lab"` in their manifest. The portal stores
  this field and shows a clear **LAB** badge on the version, so an operator
  can never mistake a LAB package for production firmware.

## Firmware role and workspace containers (decisions 2026-09-01)

Every manifest and portal record carries an optional `firmwareRole`:

| Role | Meaning |
|---|---|
| `bootstrap` | First-install / provisioning / recovery base firmware (e.g. the Telemetric Device Bootstrap LAB package) |
| `application` | The product's main function firmware (default for legacy manifests without the field) |
| `recovery` | Dedicated recovery image |

Rules:

- Both artifacts of one `releaseId` must carry the same `firmwareRole`.
- The portal groups packages into three containers in the product workspace:
  1. **`<PRODUCT> Bootstrap & Recovery`** (amber) — bootstrap and recovery
     packages, with a warning that bootstrap only fits its matching hardware
     profile;
  2. **`<PRODUCT> Application Firmware`** (cyan) — the product's main
     firmware;
  3. **Firmware History** (collapsed by default) — retired and quarantined
     packages.
- One release stays one package card with one UPDATE button: USB picks the
  merged/full BIN, OTA/LAN picks the app-only BIN.

**Hardware-profile binding**: the current TMM bootstrap package
(`TMM-0.1.0-bootstrap.1-9648a0c`) is built for profile `TMM_V6_R0_M0` only.
A different hardware revision (e.g. V7) needs its own compatible bootstrap
package built from that profile — never flash a bootstrap BIN onto a
mismatched revision.

## Import behavior (portal + firmware library)

- The library manifest schema accepts optional `stage` (`lab`/`production`)
  and `releaseId`; the portal importer stores both and surfaces `stage`.
- The portal imports each artifact only after its physical BIN is downloaded
  and verified (byte size + SHA-256). A missing BIN or manifest never creates
  a firmware record.
- Both artifacts of one release may coexist in the portal for the same
  product/version/build (they differ by image type), and the portal groups
  them into one version card with a single UPDATE button: USB picks the
  merged/full record, OTA/LAN picks the app-only record.
