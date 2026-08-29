# Central Repositories Registry

Exactly **one** portal and **one** library exist. If a new central repo is ever
added, update `00_Hub/ECOSYSTEM.md` too.

## Portal (web + flashing + QC)

| Field | Value |
|---|---|
| Product code scope | All 37 catalog codes |
| Local path | `D:\Home Work\Software Github\telemetric-hardware-portal` |
| GitHub | https://github.com/TaufikAS0/telemetric-hardware-portal (private) |
| Stack | Vite + TypeScript frontend, Fastify server, SQLite (runtime data outside Git) |
| AI rules | `<portal>/AGENTS.md` (website-notes JSON protocol) |
| Ecosystem contract | `<portal>/docs/TELEMETRIC_ECOSYSTEM.md` |
| Owns | flash permission, lifecycle (draft/approved/recommended/retired/quarantined), QC, audit |

## Firmware Library (immutable artifact archive)

| Field | Value |
|---|---|
| Product code scope | All 37 catalog codes |
| Local path | `D:\Home Work\Software Github\telemetric-firmware-library` |
| GitHub | https://github.com/TaufikAS0/telemetric-firmware-library (private) |
| Storage model | Git = catalog/manifests/checksums/policy; GitHub Releases = actual `.bin` files |
| AI rules | `<library>/AGENTS.md` + `<library>/docs/QUICK_PUBLISH.md` |
| Ecosystem contract | `<library>/docs/ECOSYSTEM_ARCHITECTURE.md` |
| Owns | immutable BIN identity, manifest, SHA-256, byte size, source traceability |

## Runtime locations (never in Git)

| Item | Location |
|---|---|
| Operational data | `D:\Telemetric Hardware Portal Data` |
| Secure portal | https://192.168.1.122:8443 |
| Client cert onboarding | http://192.168.1.122:8080/setup |
| ESP IP Scanner (Wi-Fi firmware) | http://192.168.1.121:8877/ |
