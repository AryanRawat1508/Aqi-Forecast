# AQI Forecast India

Forecasting and explaining air quality for Indian cities, with a live dashboard.

> Status: In progress (Week 1: data collection and EDA)

## Problem

Air quality in many Indian cities swings sharply with season, weather and local events (stubble burning, Diwali, winter inversions). Existing apps show *what* the AQI will be, but not *why*. This project forecasts PM2.5 / AQI for the next 24-72 hours and explains each forecast.

## Goals

- Collect and clean multi-year air quality and weather data for several Indian cities
- Compare models honestly against a naive baseline (persistence)
- Explain predictions with SHAP
- Ship a deployed Streamlit dashboard with forecasts, a map and explanations

## Planned Results (fill in as you go)

| Model | City | Horizon | MAE | RMSE |
|-------|------|---------|-----|------|
| Persistence baseline | TBD | 24h | TBD | TBD |
| XGBoost | TBD | 24h | TBD | TBD |
| Prophet | TBD | 24h | TBD | TBD |
| LSTM | TBD | 24h | TBD | TBD |

## Tech Stack

Python, pandas, scikit-learn, XGBoost, Prophet, PyTorch, SHAP, Streamlit, Plotly, Docker

## Data Sources

- Air quality: OpenAQ / CPCB / Kaggle India AQI datasets
- Weather: Open-Meteo

## Project Structure

```
aqi-forecast-india/
  data/
    raw/            # untouched downloads (not committed)
    processed/      # cleaned datasets (not committed)
  notebooks/        # EDA and experiments
  src/
    data/           # data collection and cleaning
    features/       # lag, rolling and calendar features
    models/         # training and evaluation
    explain/        # SHAP helpers
  app/              # Streamlit dashboard
  tests/
  ROADMAP.md
  requirements.txt
```

## Getting Started

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Decisions Log

Keep short notes here on why you chose each approach. Interviewers will ask.

- (date) Chose time-series cross-validation instead of random split because ...

## Demo

Screenshots, GIF and live link will go here.
