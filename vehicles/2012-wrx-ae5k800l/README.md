# 2012 Subaru WRX - AE5K800L

## Vehicle / ECU

- Year: 2012
- Model: Subaru Impreza WRX
- Transmission: Manual
- Market: USDM
- ECU definition: AE5K800L
- ECU architecture: Subaru SH7058 CAN

## Archive folders

- `stock/` - original and verified stock ROMs
- `tunes/` - modified ECU binaries
- `definitions/` - ECUFlash / RomRaider XML definitions
- `logs/` - datalogs and flash logs
- `notes/` - revision notes and tuning observations

## Known tune lineage

The existing records reference at least these ROMs:

- `2012AIrev3.1.bin`
- `2012Codexv1.1.bin`

Their actual binaries have not yet been added to this repository. When imported, preserve the original filenames in `manifest.csv` and use normalized archive filenames in `tunes/`.

## Modification notes

Document hardware and calibration dependencies here before marking a tune as tested. Useful fields include intake, turbo, boost control solenoid, exhaust/downpipe, injectors, fuel pump, fuel grade, target boost, launch control, flat-foot shift, and any engine swap details.

## Rule

Never replace an existing binary with a newer tune. Add a new version so every flashable calibration remains recoverable and its history stays traceable.
