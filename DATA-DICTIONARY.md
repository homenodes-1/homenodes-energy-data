# Data Dictionary

**Last updated:** 2026-09-25
**Status:** Defined before collection. Fields may be added as monitoring is configured.

## Raw data

**Location:** `raw/`
**File naming:** `YYYY-MM-DD_to_YYYY-MM-DD.csv` (one file per export period)
**Sampling interval:** 60 seconds

| Field | Type | Unit | Source | Description |
|---|---|---|---|---|
| `timestamp_utc` | datetime | ISO 8601 | Collection script | Time of reading, UTC |
| `plug_power_w` | decimal | W | Smart plug | Instantaneous power at the wall outlet |
| `plug_voltage_v` | decimal | V | Smart plug | Supply voltage |
| `plug_current_a` | decimal | A | Smart plug | Current draw |
| `plug_energy_kwh_total` | decimal | kWh | Smart plug | Cumulative energy since plug was installed |
| `gpu_power_w` | decimal | W | nvidia-smi | GPU board power as reported by the driver |
| `gpu_util_pct` | integer | % | nvidia-smi | GPU utilization |
| `gpu_temp_c` | integer | °C | nvidia-smi | GPU core temperature |
| `cpu_util_pct` | decimal | % | Operating system | Average CPU utilization across all cores |
| `node_state` | text | n/a | Collection script | One of: `idle`, `rented`, `benchmark`, `maintenance`, `offline` |

## Processed data

**Location:** `processed/`
**File naming:** `hourly_YYYY-MM.csv` (one file per month)

| Field | Type | Unit | Description |
|---|---|---|---|
| `hour_utc` | datetime | ISO 8601 | Start of the hour, UTC |
| `energy_kwh` | decimal | kWh | Energy used during the hour, from the cumulative plug reading |
| `mean_power_w` | decimal | W | Average wall power during the hour |
| `max_power_w` | decimal | W | Highest wall power reading during the hour |
| `rented_minutes` | integer | minutes | Minutes the node was in the `rented` state |
| `benchmark_minutes` | integer | minutes | Minutes the node was running project benchmark workloads |
| `coverage_pct` | decimal | % | Share of expected readings present for the hour |

## Conventions

- Missing readings are left blank, not filled or estimated.
- Hours with `coverage_pct` below 90 are flagged in analysis.
- Timestamps are always UTC. Local time conversions are done at analysis.
- Raw files are never edited after export. Corrections are made in processed files and noted in the CHANGELOG.
