# Devices and Runtime Registry

Follow the device naming convention from `ai-collaboration-vault/00_Hub/DEVICES.md`.
Commit format: `[device:<name>] [project:<slug>] <summary>`.

## Machines

| Device | Role | Notes |
|---|---|---|
| `laptop-utama` | Main laptop: hosts the portal server, holds credentials, runs auto-sync | replace/confirm real machine name |
| other operator laptops | Browser-only operators; never hold GitHub tokens | onboard via `http://192.168.1.122:8080/setup` |

## Runtime endpoints

| Endpoint | Purpose |
|---|---|
| `https://192.168.1.122:8443` | Secure portal UI |
| `http://192.168.1.122:8080/setup` | One-time client CA onboarding |
| `http://192.168.1.121:8877/` | ESP IP Scanner (Wi-Fi firmware post-flash) |

## Data outside Git (intentionally)

BIN files, SQLite databases, private keys, passwords, evidence, and backups all
live in `D:\Telemetric Hardware Portal Data` — never commit them anywhere.
