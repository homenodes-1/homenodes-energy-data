# HomeNodes Energy Data

Energy consumption data from the HomeNodes proof of concept node in Medicine Hat, Alberta.

## Purpose

Energy use is one of the least visible impacts of residential AI compute. This repository records what a single node actually draws, so governance discussions about grid load, cost, and emissions can be based on measured data rather than estimates.

Medicine Hat operates its own municipal electric utility, which makes it a practical location for studying the relationship between residential compute and local grid capacity.

## Contents

| Folder / File | Contents |
|---|---|
| `raw/` | Unmodified exports from the monitoring device |
| `processed/` | Cleaned and aggregated data |
| `DATA_DICTIONARY.md` | Definitions for each field and how it is collected |
| `METHODOLOGY.md` | How consumption is measured and why |

Files are added as data collection progresses.

## Measurement scope

Only the node's dedicated power circuit is measured. No whole-home consumption data is collected or published. Household energy patterns can reveal occupancy and daily routines, so this boundary is deliberate.

## Data format

- CSV files
- Timestamps in UTC, ISO 8601 format
- Power in watts (W), energy in kilowatt-hours (kWh)

## Status

**Phase 1:** Monitoring setup in progress. Baseline data collection begins when the node is powered on.

## Related

- Governance framework: [homenodes-framework](../../../homenodes-framework)
- Proof of concept: [homenodes-poc](../../../homenodes-poc)
- Project site: [homenodes.ca](https://homenodes.ca)
- Contact:
