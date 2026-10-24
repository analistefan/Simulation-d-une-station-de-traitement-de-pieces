# Experimental Methodology and Validation

## Recorded design

The supplied handwritten record contains 15 observations:

- 5 runs at `meanServiceMin = 3.0`
- 5 runs at `meanServiceMin = 4.0`
- 5 runs at `meanServiceMin = 4.5`

The arrival parameter remains 5.0 minutes in the supplied AnyLogic project. Each run is described by completed parts, time-average queue length, and mean utilization.

## Calculation method

For each service-time setting and each indicator:

1. Transcribe the five observed values into the raw-results table.
2. Compute the arithmetic mean: sum of the five values divided by 5.
3. Compute the sample standard deviation with denominator 4.
4. Preserve every individual observation so that the summary can be audited.

The exact values and derived quantities are in [../results/summary.md](../results/summary.md).

## Validation performed

- Counted 15 observations in total, with five observations in each of the three service-time groups.
- Confirmed that all utilization observations lie between 0 and 1.
- Confirmed that the indicator names in the handwritten record match the three chart expressions in the AnyLogic file.
- Checked the model source for the stated 480-minute horizon, 5.0-minute default arrival parameter, service-time parameter, and seed 42.
- Recomputed each group mean and sample standard deviation from the transcribed raw values.

## Reproducibility boundary

The supplied `.alp` file stores a fixed random seed of 42 and does not include an automated replication experiment or the seed values used for the handwritten runs. Consequently, the data table is an evidence-preserving transcription, not a claim that a reader can regenerate all 15 values from the project alone. A future revision should add a Parameter Variation or Monte Carlo experiment, one documented seed per run, exported CSV output, a warm-up policy, and confidence intervals.
