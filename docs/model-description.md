# Model Description

## Purpose

The supplied AnyLogic project models a single station that receives parts, waits them in a queue, processes them, and removes completed parts from the system.

## Flow logic

```text
srcPieces (Source) -> queueMachine (Queue) -> delayMachine (Delay) -> sinkFinished (Sink)
```

The flow is directly encoded by the three connectors in the project file.

## Parameters and distributions

| Parameter / element | Definition observed in the project |
|---|---|
| `meanArrivalMin` | Parameter, default 5.0 |
| `meanServiceMin` | Parameter, default 3.0 |
| `srcPieces` | Generates entities with `exponential(1.0 / meanArrivalMin)` as interarrival time, in minutes |
| `queueMachine` | Waiting queue; statistics collection is explicitly enabled |
| `delayMachine` | Processing delay with `exponential(1.0 / meanServiceMin)`, in minutes; statistics collection is explicitly enabled |
| `sinkFinished` | Counts and disposes of completed entities |

The document reports the literal AnyLogic expressions rather than imposing an interpretation beyond the project file.

## Indicators

| Indicator | AnyLogic expression | Meaning |
|---|---|---|
| Completed parts | `sinkFinished.count()` | Number of entities that reached the sink by the end of the run |
| Mean queue length | `queueMachine.statsSize.mean()` | Time-average number of entities in the queue |
| Mean utilization | `delayMachine.statsUtilization.mean()` | Time-average utilization statistic of the Delay block |

## Run settings

The model's time unit is minutes. The Simulation experiment has a fixed seed value of 42 and a final time of 480 minutes. No Parameter Variation or Monte Carlo experiment is present in the supplied project file.

## Scope

This repository preserves the project source exactly as supplied in `src/anylogic/`. It does not alter capacities, distributions, or the scheduling policy.
