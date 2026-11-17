# Combined Cycle Plant Output Forecaster

Estimate net hourly electrical output from ambient temperature, exhaust vacuum, pressure, and humidity.

## Dataset

[UCI Combined Cycle Power Plant dataset](https://archive.ics.uci.edu/dataset/294/combined%2Bcycle%2Bpower%2Bplant) (dataset ID 294), 9,568 records. The source is public and is fetched by the runner; the raw dataset is not committed.

## Run

```bash
python -m pip install -r requirements.txt
python main.py --output-dir artifacts
```

The runner saves metrics, holdout predictions, and a reusable model in the ignored output directory. The public [`reports/benchmark.json`](reports/benchmark.json) contains aggregate results only; no row-level records are published.

## Holdout results

A random 75/25 split (seed 42) is used. Numeric inputs are median-imputed; a 400-tree random-forest regressor is compared with a median predictor.

| Target | MAE | RMSE | R² | Median baseline MAE |
|---|---:|---:|---:|---:|
| PE | 2.367 | 3.341 | 0.962 | 14.728 |

Full aggregate metrics and the exact split seed are in [`reports/benchmark.json`](reports/benchmark.json).

## Limits

This is an observational public benchmark. The random holdout does not establish future-condition or operational performance. These are one-time benchmark results, not service-level, production, or causal claims.

## Reproducibility

The model and split use seed 42. Re-running downloads source data from UCI and regenerates local artifacts. Model binaries, raw inputs, and row-level predictions are excluded from this public repository.
