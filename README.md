# Combined Cycle Power Plant Output Forecaster

A reproducible regression benchmark for estimating net hourly power output from ambient temperature, exhaust vacuum, ambient pressure, and relative humidity.

## Dataset

Uses the [UCI Combined Cycle Power Plant dataset](https://archive.ics.uci.edu/dataset/294/combined%2Bcycle%2Bpower%2Bplant), a public benchmark with 9,568 observations. The target is net hourly electrical energy output. This is an observational benchmark, not a live plant feed.

## Run

Python 3.10+ is recommended.

```bash
python -m pip install -r requirements.txt
python main.py
```

The script fetches the dataset with `ucimlrepo`, makes a seeded 75/25 holdout, fits a median-imputed random-forest pipeline, compares it with a median predictor, and saves `artifacts/model.joblib`, `artifacts/metrics.json`, and row-aligned holdout predictions.

## Evaluation and limits

MAE, RMSE, and R² are reported beside the baseline on the holdout. The random split does not measure performance on future plant conditions or establish operational safety. Validate on time-separated plant data, monitor sensor/data drift, and review process constraints before deployment. No performance numbers are claimed until the run is reproduced.
