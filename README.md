# JesterTek WRX Tuning Archive

This repository is the technical source of truth for the 2012 WRX wagon / EJ20X tuning work.

## Vehicle / setup

- 2012 Subaru WRX wagon
- EJ20X
- Catless exhaust
- Wideband O2
- Cobb 3-port boost control solenoid
- ID1000 injectors
- Walbro 255 fuel pump
- RomRaider / ECUFlash tuning workflow

## Current direction

The active tune lineage moved from the early `2012AIrev3.1.bin` baseline into the Codex revisions. The most recently referenced calibration is:

`2012Codexv5.6_18psi_curve_smoothtylmafAVCSwgd.bin`

Current work has focused on:

- controlling earlier 23-24 psi overboost
- targeting roughly 17-19 psi
- smoothing target boost / WGDC / turbo dynamics behavior
- addressing rich low-10 AFR behavior during part-throttle / transition
- learned-knock review
- fuel cleanup after injector / pump changes
- keeping exhaust AVCS disabled while leaving intake AVCS unchanged
- validating behavior after replacing the O2 sensor and fixing a pre-turbo exhaust leak

## Repository layout

- `docs/` - tuning history, decisions, current-state notes, archive indexes
- `tunes/` - ROM images suitable for source control
- `tables/` - exported maps / tables / calibration notes

Raw CSV tuning logs are intentionally **not retained**. They were purged from GitHub, Google Drive tuning archives, and ChatGPT Library on 2026-09-23 because they are obsolete transient data rather than durable project history.

## Google Drive archive

Master archive:

https://drive.google.com/drive/folders/1z_hMvAR17cOaivXdtu7rskqB3WAj92TY

WRX tuning archive:

https://drive.google.com/drive/folders/1BiMhUSDIyB_QrIHeP9KJMS4yWb9yD01J

Existing source collections catalogued for preservation:

- AiTune
- 06_Automotive_Tuning
- WRX tune / boost issue ChatGPT export

## Archive policy

GitHub contains technical history that is safe to keep in a public repository. Google Drive keeps the complete private artifact archive for tune binaries, spreadsheets, screenshots, documentation, and conversation-derived reference material.

Raw CSV tuning logs are disposable and excluded from the archive.

Receipts, credentials, personal records, and unrelated private material do not belong in this public repository.
