# Taxi Demand Forecasting

Forecast hourly taxi orders to improve driver allocation and reduce idle time.  
This project builds a time-series regression model with calendar + lag features and evaluates performance with RMSE.

---

## Overview
- Problem: predict the number of orders for the next hour.
- Approach: feature engineering on time-series (calendar, lags, rolling means) + tree-based regression.
- Result: achieved **RMSE ≈ 47** (meets the ≤ 48 requirement in the bootcamp sprint).

---

## Data
Expected CSV schema (example):
- `datetime` — timestamp at hourly frequency (e.g., `2018-03-01 10:00:00`)
- `num_orders` — integer count of completed orders that hour

Place your data at `data/taxi_orders.csv`.

---

## Features
- **Calendar**: hour, day of week, month, is_weekend
- **Lags**: t-1, t-2, t-24
- **Rolling means**: 3h, 24h, 168h (weekly)
- Optionally remove early rows with NaNs from rolling windows

---

## Model
- Baseline: `RandomForestRegressor` (robust to non-stationarity and nonlinearity)
- Metric: Root Mean Squared Error (RMSE)

---

## Repository Structure

```

taxi-demand-forecasting/
│
├── taxi_demand_forecasting.py # training & evaluation script
├── data/
│ └── taxi_orders.csv # (not included) place your dataset here
├── results/ # charts, predictions (created at runtime)
├── requirements.txt
└── README.md

```
# create venv (optional)
python -m venv .venv
source .venv/bin/activate            # Windows: .venv\Scripts\activate

# install deps
pip install -r requirements.txt

# run
python taxi_demand_forecasting.py

By default the script reads data/taxi_orders.csv, trains on the earlier portion of the series,
evaluates on the final 20%, prints RMSE, and saves a chart to results/holdout_pred.png.

Notes

This project corresponds to the Time Series (Sprint 13) module.

You can swap the model (e.g., LightGBM, XGBoost) or tune features to push RMSE down further.

Author

Ekay (Emmanuel Nyarko Asare)
AI/ML Data Scientist
LinkedIn
 | GitHub


---

# requirements.txt

```txt
pandas>=2.2
numpy>=1.26
scikit-learn>=1.5
matplotlib>=3.9
