# AOM - Automatic Oxygen Manifold

## Identity

| Field | Value |
|---|---|
| Code | AOM (explicit owner choice, not ANM or a new AGM catalog product) |
| Product name | Automatic Oxygen Manifold |
| Catalog group | White Label Product |
| Firmware repo (local) | D:\Home Work\Firmware Github\esp32-hardware-test-manifold |
| Firmware repo (GitHub) | https://github.com/TaufikAS0/esp32-hardware-test-manifold |
| Library manifests | telemetric-firmware-library/manifests/AOM/ |

## Releases

| Version | Manifest | Release tag | Lifecycle in portal | Notes |
|---|---|---|---|---|
| 1.6.4 | 1.6.4-full.json + 1.6.4-app-only.json | AOM-v1.6.4-esp32 | draft/built; Hardware QC/LAB | Ordered non-blocking dual Wi-Fi; AOM discovery; physical tests PENDING |

## Hardware

| Field | Value |
|---|---|
| PCB profile | AOM_V1_R0 (owner confirmed V1 R0 on 2026-10-21) |
| Build target | ESP32 classic / 4MB / DIO / min_spiffs |
| Fitted MCU / actual flash capacity | UNCONFIRMED; build configuration is NOT hardware measurement |
| USB | merged/full offset 0; optional Full erase after operator confirmation |
| OTA artifact | app-only offset 0x10000; manual device upload only, matching partition layout required |
| Portal automatic OTA | Disabled honestly: legacy updater lacks authenticated product-locked contract |
| Partition | min_spiffs, two 0x1e0000 app slots, SPIFFS 0x3d0000/0x20000 |
| Serial | Existing AGM-prefixed MAC-derived serial retained for backward identity continuity |

## Network and operator workflow

- Physical switch GPIO32 must enable network (active LOW).
- GPIO39 HIGH selects station mode, LOW selects existing AP.
- Station: HuaweiJIN first (12 seconds), then ParaPencariSurga (12 seconds).
- Both fail: 30-second backoff then repeat. Connected secondary is retained;
  disconnection starts a new primary-first cycle. Retry is non-blocking.
- Requested defaults live only in Config_LabWifi.h; never copy passwords here,
  into release metadata, logs or AI notes. They are deliberate public LAB inputs
  and recoverable from BINs; never production/customer credentials.

## Lessons for the next AI

- Newest baseline was feature/manifold-ota-and-segment-fixes/c02c4f2 (1.6.3),
  not the older main. Integration branch is feature/portal-manifold-qc.
- Retain existing pins, polarities, calibration keys and test criteria.
- This is bench actuator/control firmware, NOT oxygen-delivery control or a
  safety-certified tester. Isolate live gas hardware before bench use.
- A successful output sequence is not a measurement or overall hardware QC PASS.
- USB Fast merged write can overwrite NVS/calibration. Full erase removes all
  flash data. Archive evidence/calibration first; manual app-only preserves NVS
  only when the device already has a matching layout.
- No physical flash, relay operation, sensor calibration or OTA was performed.

## Evidence pointers

- Source commit: 912efc6ed9e279bdd4aba2bcbe81d3bc84a68df4.
- Source docs: docs/PORTAL_PACKAGE.md; source build helper tools/build_portal.py.
- Software contract tests: tests/portal-contract.test.mjs; production constexpr
  retry/fallback/disconnect/millis-wrap checks in Network_RetryPolicy.h.
- QC records: portal database, separate from firmware publication.
- Physical-test status: PENDING PHYSICAL TEST.
- Build and package verification completed: app 1,173,984 bytes fits the
  1,966,080-byte slot; full 4,194,304 bytes. Actual partition bytes and the
  identical app bytes inside merged were verified; library gates passed twice
  (31 tests, 39 products/54 manifests).
- App SHA-256: `1ab8424b07ae9e2427c264572a59b17a901a17bbb6f70d38c690d71af2f5a514`.
- USB SHA-256: `443a794804a560e3496b658bdbba092ce53a8d9354b944c50a4f751db343f013`.
- Draft release (4 assets; publisher independently re-downloaded and verified):
  https://github.com/TaufikAS0/telemetric-firmware-library/releases/tag/untagged-4a2573c88482f3f3ab38
- Portal import verified: exactly two records (full + app-only), one releaseId
  `AOM-1.6.4-912efc6`, role qc/stage lab/status draft, AOM_V1_R0 profile.
  Both stored-file sizes/SHA-256 match their manifests; /products/AOM returned
  HTTPS 200. No authenticated screenshot or physical hardware acceptance claimed.
