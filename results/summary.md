# Verified Summary of Recorded Results

This table is calculated solely from [raw_results.csv](raw_results.csv), which transcribes the 15 values in the supplied handwritten record.

| Mean processing time (min) | Runs | Completed parts: mean (sample SD) | Mean queue length: mean (sample SD) | Mean utilization: mean (sample SD) |
|---:|---:|---:|---:|---:|
| 3.0 | 5 | 99.40 (11.89) | 1.032 (0.433) | 0.686 (0.082) |
| 4.0 | 5 | 91.20 (11.03) | 2.072 (0.825) | 0.780 (0.032) |
| 4.5 | 5 | 94.60 (7.77) | 2.940 (1.800) | 0.832 (0.109) |

## Reading the summary

- The queue-length mean increases across the recorded service-time settings.
- The utilization mean also increases across the recorded settings.
- Completed-part means vary across groups; no hypothesis test or causal conclusion is reported because only five recorded runs per setting are available and run-level seed provenance is absent.

## Calculation audit

For each group, the displayed mean is the arithmetic average of five raw records. The parenthesized quantity is the sample standard deviation, calculated with denominator (n - 1 = 4). Rounded display values do not replace the raw values in the CSV.
