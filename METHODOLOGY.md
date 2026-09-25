# Energy Measurement Methodology

**Last updated:** 2026-09-25
**Status:** Defined before collection

## Why energy matters for governance

Energy is the most physical and measurable footprint of residential compute. It affects household costs, local grid capacity, emissions, and whether a home is being used for something closer to commercial activity. Current governance discussions rely on estimates or data centre figures. This dataset records what a single residential node actually draws under real conditions, so framework provisions on zoning, grid impact, and scale thresholds can be based on evidence.

## What is measured

The boundary is the node's power circuit only. Whole-home energy use is not measured or published.

**Wall power.** A smart plug with energy metering sits between the wall outlet and the UPS. It measures everything powered through the UPS: the node, the firewall, and the UPS's own conversion losses. This is the total real-world cost of operating the node.

**GPU power.** The NVIDIA driver reports GPU board power. This separates GPU draw from the rest of the system and shows how much of the load comes from workloads versus baseline operation.

**System state.** Each reading is tagged with the node's state (idle, rented, benchmark, maintenance, offline) so energy can be compared across conditions.

## Collection

- Readings every 60 seconds from both the smart plug and the NVIDIA driver
- Collected by a script running on the firewall appliance, so collection continues if the node is offline
- Exported to CSV weekly and committed to `raw/`

## Baseline

Before the node is listed on the platform, the following are recorded:

1. **Idle baseline:** 48 hours powered on with no workload
2. **Load baseline:** 24 hours running a standard GPU benchmark at full load

These establish the floor and ceiling for comparison with rented operation.

## Accuracy and validation

Consumer smart plugs are not revenue-grade meters. To check accuracy:

- The smart plug's cumulative reading is compared against the utility meter over a fixed window, with other household loads held as steady as practical.
- The measurement device model and any known accuracy specifications are recorded here once installed.
- Known gaps, device resets, and anomalies are logged in the CHANGELOG.

## Derived measures

- **Energy per rented GPU-hour** (kWh)
- **Idle overhead** as a share of total energy
- **Monthly energy and estimated cost** using local utility rates
- **Estimated emissions** using a published grid emissions factor for Alberta, with the source cited

## Limitations

- One node in one home. Results describe this configuration, not residential compute in general.
- Workload mix depends on what renters choose to run.
- Basement ambient temperature varies seasonally and may affect cooling load.
