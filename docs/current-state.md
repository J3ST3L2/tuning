# Current WRX Tuning State

_Last consolidated: 2026-09-22_

## Hardware

- 2012 WRX wagon
- EJ20X
- Catless
- Wideband installed
- Cobb 3-port EBCS
- ID1000 injectors
- Walbro 255 fuel pump

## Calibration lineage

Known checkpoints include:

- `2012AIrev3.1.bin`
- `2012Codexv4.9_combo_17psi_fuelcleanup_bridge.bin`
- `2012Codexv5.6_18psi_curve_smoothtylmafAVCSwgd.bin`

The v4.9-era work included target boost, maximum WGDC, initial WGDC, and fuel-cleanup revisions. The v5.6 calibration became the working tune for later logs and refinement.

## Major issues addressed

### Boost control

Earlier behavior showed overboost into approximately 23-24 psi. The tuning direction has been to bring this down into the intended 17-19 psi range while smoothing WGDC and turbo-dynamics behavior rather than simply chopping boost abruptly.

### Fueling

Later driving showed very rich behavior, including low-10 AFR readings on the wideband during roughly quarter to one-third throttle transitions. The working theory shifted toward transition / tip-in / enrichment behavior rather than treating the entire high-load fuel map as the sole cause.

### Knock review

Recent work has included reviewing learned knock and using logs rather than blindly adding or removing timing.

### Mechanical changes

A new O2 sensor was installed and a pre-turbo exhaust leak was repaired. Those changes matter because the calibration should be judged using post-repair logs rather than assuming older fuel-trim / AFR behavior still represents the car.

### AVCS

Exhaust AVCS was disabled in the current tuning direction. Intake AVCS was left unchanged.

## Recent logs referenced

- `BtSsm_20260828_182023.csv`
- `BtSsm_20260828_201153.csv`
- `BtSsm_20260910_125139.csv`
- `BtSsm_20260919_120058.csv`
- `BtSsm_20260919_142711.csv`

Older RomRaider logs from June / July 2026 are retained as historical context.

## Preservation rule

Do not overwrite old ROMs. Every meaningful calibration revision should remain immutable and receive a new filename. Keep logs paired with the exact tune flashed when the log was recorded whenever that relationship is known.
