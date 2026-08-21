# Subaru ECU Tune Archive

Organized archive for Subaru ECU ROMs, calibration revisions, definitions, logs, and tune notes.

## Repository layout

```text
vehicles/
  <year>-<model>-<ecu-id>/
    stock/          Original/known-good stock ROMs
    tunes/          Modified calibration binaries
    definitions/    EcuFlash / RomRaider definitions specific to the ECU
    logs/           Datalogs used to validate a tune
    notes/          Tune notes, change logs, dyno notes, etc.
    README.md       Vehicle/ECU metadata and modification summary
manifest.csv        Searchable index of tune files and revisions
docs/               Naming and archive conventions
```

## Tune filename convention

Use:

`YYYY_MODEL_ECUID_NAME_vMAJOR.MINOR_DESCRIPTION.bin`

Example:

`2012_WRX_AE5K800L_Codex_v1.1.bin`

Keep the original filename in `manifest.csv` when renaming an existing tune so its history is not lost.

## Tune status

Every tune should be labeled in `manifest.csv` as one of:

- `stock` - verified stock ROM
- `development` - experimental/in-progress
- `tested` - flashed and validated with logs
- `retired` - superseded or known-bad tune retained for history
- `unknown` - origin/status not yet verified

## Safety / provenance

Do not overwrite old tune binaries. Create a new revision for every calibration change. Preserve original ROMs unchanged and record SHA-256 hashes where practical.

Avoid committing VINs, registration documents, credentials, license keys, or other unrelated/private data alongside ROMs.

## Known ECU family

The initial archive includes work for the 2012 USDM Subaru Impreza WRX manual transmission using ECU definition `AE5K800L`.
