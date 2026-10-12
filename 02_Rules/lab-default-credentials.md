# Public LAB defaults - owner decision 2026-10-12

The owner permits deliberate shared Wi-Fi/AP/OTA defaults in LAB QC/testing
source and downloadable BINs so operators need no programming/provisioning.
These defaults are PUBLIC, not secrets. Use an isolated trusted lab LAN and
never reuse them in production/customer devices or expose OTA to the Internet.
Private/random credentials, GitHub tokens, portal passwords, TLS keys and
production credentials are NOT covered. Use named defaults, not recovered
private secrets. Packages remain lab/draft/built until evidence warrants more.
Checksum, hardware evidence, output locks, NVS and partition safety remain.

Compact v0.5.0 uses the intentional default from lab_ota_defaults.h. Private
ota_secrets.h overrides may be used locally but those BINs are not distributable.

## Legacy app-only exception

An app-only release is permitted where merged USB writes would destroy NVS.
Clearly disable/describe missing installation methods. Never label an app as
full or falsify offset. Compact installs through device /update (Digest login),
not portal automatic Bearer OTA. Initial USB uses explicit documented offsets.
This supersedes the blanket dual-artifact requirement for such legacy packages.

Canonical policy: ai-collaboration-vault/03_Rules/telemetric-firmware-ecosystem.md.
