# StorageVitals

**Know the health of your drives and the integrity of your files.**

StorageVitals is a local, Windows-based toolkit for inspecting external storage. It combines three independent applications that answer three different questions.

## Applications

| Application | Question it answers | What it does |
|---|---|---|
| **Scanning Tool** | Have my files changed? | Verifies file integrity against a stored baseline using BLAKE3 (via FastFileCheck in WSL), with an independent SHA-256 safe scanner, optional Diffoscope backup comparison, and a metadata-only offline ledger (PDF, HTML, CSV). |
| **Hard Drive Monitor** | Is the drive physically healthy? | Collects SMART data with `smartctl`, assesses health, runs a read-only full-disk bad-block scan and read-speed benchmark, and generates standalone HTML reports with history and trends. |
| **Hard Drive Dashboard** | How do my reports compare with the live drive? | Combines PDF report inventory (Windows OCR) with live Windows readings, matches reports to physical drives, compares values side by side, and exports to CSV. |

## Design Principles

- **Read-only by design:** scanned source drives are never modified.
- **Conservative interpretation:** unknown stays *Unknown*, missing readings are never replaced with zero, and a stopped or errored scan is never reported as a clean verification.
- **Identity validation:** SMART data and reports are linked to a drive only through verified serial, capacity, or confirmed matches.
- **Local only:** no cloud uploads, no third-party services, no network exposure.
- **Secure boundaries:** per-process API tokens, path validation, and upload checks.

## Requirements

- Windows with PowerShell
- Python 3.9+ (standard library only for the Scanning Tool and Hard Drive Monitor)
- `smartctl` from [smartmontools](https://www.smartmontools.org/) (SMART access and surface scans require an elevated terminal)
- WSL Ubuntu with FastFileCheck (Scanning Tool, BLAKE3 hashing only)

## Technical Documentation

📄 [View Storage Vitals Professional Documentation](https://github.com/kaviyarasanbalasundaram/Storage-Vitals/blob/main/Storage%20Vitals%20Professional%20Documentation.pdf)

Covers architecture, workflows, data handling, testing approach, and the technical challenge and response register for all three applications.

## Important Notes

- Quick scan is metadata-assisted and is **not** a full content reread. Use a Full scan for complete content verification.
- A passing SMART check does not guarantee a drive will not fail. These tools are **not a substitute for backups**.
- A file-integrity check, a drive-health check, and a report comparison are different things. Passing one does not prove the others.

## Acknowledgements

Built with the help of FastFileCheck, [smartmontools](https://www.smartmontools.org/), and [Diffoscope](https://diffoscope.org/). Please check each project's license.

## Author

Kaviyarasan Balasundaram
