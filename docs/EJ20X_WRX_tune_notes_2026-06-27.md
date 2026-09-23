---
title: "2012 WRX EJ20X Tune Notes"
date: 2026-06-27
tags:
  - subaru
  - wrx
  - ej20x
  - tuning
  - romraider
  - ecuflash
rom: AE5K800L
file: 2012AIrev3.1.bin
---

# 2012 WRX EJ20X Tune Notes

## Setup

- 2012 WRX wagon, USDM 32-bit ECU/ROM.
- ROM internal ID: `AE5K800L`.
- Engine: EJ20X swap.
- Lower/exhaust cam controls disabled; intake AVCS is active.
- Stock injectors and stock fuel pump.
- Catless exhaust.
- External wideband present, but not logged through Tactrix/RomRaider.

## Current Observations

- Car reportedly reaches desired boost and has reached 22 psi in previous testing.
- Logs show strong airflow/load at WOT:
  - MAF around 250-260 g/s.
  - Load around 2.45-2.51 g/rev.
- IAM stayed at 1.0.
- Most WOT knock correction was clean, but latest log showed -1.5 FLKC around 6000+ rpm/high load.
- RomRaider MAP/boost channels appear wrong for this ROM/logger definition:
  - MAP/relative pressure stayed near atmospheric or fixed negative values while MAF/load clearly showed boost.
  - Treat boost/MAP logging as untrusted until logger definitions are fixed.

## Interpretation

The car is not obviously failing to make boost. The better working theory is that the torque curve feels uneven because the tune requests/controls torque in a way that is soft early and then comes alive hard later.

For a smoothness revision, avoid chasing peak power. Shape the boost request, initial wastegate duty, and mid-pedal torque delivery so the car builds torque more progressively.

## Tables To Leave Alone For Rev A

- Max WGDC: leave unchanged.
- Turbo dynamics: leave unchanged.
- High-load timing: leave unchanged for now because of the observed -1.5 FLKC up high.
- WOT/open-loop fueling: leave mostly unchanged unless wideband is logged or carefully watched.

## Rev A: Target Boost Shape

Goal: fill the low/mid spool area slightly while softening the hard jump into full midrange boost.

Apply to the high requested torque columns only, roughly `280+` raw requested torque. Blend neighboring columns so there are no cliffs.

| RPM | Current approx | Rev A target |
|---:|---:|---:|
| 2400 | 1.51 | 1.50 |
| 2800 | 8.01 | 9.00 |
| 3200 | 14.00 | 13.50 |
| 3600 | 17.50 | 16.50 |
| 4000 | 17.50 | 17.20 |
| 4400 | 17.50 | 17.50 |
| 4800 | 17.50 | 17.50 |
| 5200 | 16.49 | 16.49 |
| 5600 | 15.99 | 15.99 |
| 6000 | 15.51 | 15.51 |
| 6400 | 15.01 | 15.01 |

Notes:

- This is not a peak boost increase.
- The 2800 cell gets a small bump.
- 3200-4000 is shaped to reduce the sudden hit.

## Rev A: Initial WGDC Shape

Goal: support smoother ramp-in without touching max WGDC.

Apply to high requested torque columns, roughly `280+`. Blend the `240-260` requested torque columns between stock and the values below.

| RPM | Current approx | Rev A target |
|---:|---:|---:|
| 2400 | 48 | 48 |
| 2800 | 55 | 55 |
| 3200 | 51 | 53 |
| 3600 | 47 | 50 |
| 4000 | 46 | 48 |
| 4400 | 42 | 44 |
| 4800 | 38 | 39 |
| 5200 | 36 | 36 |
| 5600 | 34 | 34 |
| 6000 | 32 | 32 |
| 6400 | 30 | 30 |

Notes:

- Keep max WGDC unchanged.
- If boost overshoots or oscillates, undo the 3200-4000 WGDC additions first.
- If boost feels smoother but still lazy, review mechanical spool factors before increasing duty further.

## Optional: Requested Torque Mid-Pedal Smoothing

Goal: improve daily drivability and make partial pedal less jumpy.

Leave the 100% pedal column mostly unchanged. Smooth only the mid-pedal columns from about `37%` to `78.6%` pedal in the `2400-4400 rpm` range.

Suggested approach:

- Reduce sudden rises between adjacent pedal columns.
- Keep 85.7% and 100% pedal strong.
- Do not reduce WOT requested torque unless the car feels too abrupt at full pedal.

Example high-level adjustment:

| Area | Change |
|---|---|
| 2400-3200 rpm, 52-78.6% pedal | smooth/reduce by about 3-6 raw torque where jumps feel abrupt |
| 3600-4400 rpm, 52-78.6% pedal | smooth/reduce by about 5-10 raw torque if mid-pedal feels too punchy |
| 85.7-100% pedal | leave stock/current for Rev A |

## Optional Later: Fuel Transition Smoothing

Current open-loop fueling has a fairly sharp transition near 1.45 g/rev in the 3200-4000 rpm area. This can feel a little soft/rich when the car crosses into boost.

Do not change this in Rev A unless wideband is watched carefully.

If revised later, consider only a mild transition smoothing:

| RPM | Load area | Current behavior | Possible later shape |
|---:|---:|---|---|
| 3200-4000 | 1.31 to 1.59 g/rev | jumps from ~12.7 to ~11.3-11.5 | smooth through ~12.0 to ~11.6 |

## Relog After Rev A

Log:

- RPM
- Engine Load
- MAF g/s
- MAF V
- Accelerator Pedal
- Throttle
- Target Boost
- WGDC
- WGDC Max
- IAM
- FBKC
- FLKC
- Ignition Total Timing
- Base Timing
- Learned Ignition Timing
- Intake AVCS left/right
- Injector pulse width
- CL/OL status
- Primary Open Loop Map Enrichment
- Wideband AFR/lambda if possible

Boost/MAP logger definitions still need correction, but the external boost gauge can be used to verify no overshoot.

## Stop Conditions

Abort or revert if:

- IAM drops below 1.0.
- FLKC appears in the new spool/midrange area.
- FBKC repeats at high load.
- Boost overshoots target by more than about 1.5-2 psi.
- Wideband goes leaner than intended under high load.

