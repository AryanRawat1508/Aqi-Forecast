# AQI Forecast India

Forecasting and explaining air quality for Indian cities, with a live dashboard.

> Status: In progress (Week 1: data collection and EDA)

## Problem

Air quality in many Indian cities swings sharply with season, weather and local events (stubble burning, Diwali, winter inversions). Existing apps show *what* the air quality will be, but not *why*. This project forecasts air quality for the next 24-72 hours and explains each forecast.

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

## Background

- **How AQI is calculated:** each pollutant's concentration is converted into a sub-index using linear segments (breakpoints). The highest (worst) sub-index becomes the AQI, and the pollutant that produced it is the dominant pollutant.
- **Forecasting AQI directly:** a model trained only on the AQI column sees just the maximum, so it cannot tell which pollutant is driving the value. It learns about individual pollutants only if their concentrations are included as input features (for example lagged PM2.5 and PM10).
- **Explaining with SHAP:** SHAP shows how each input feature (such as wind speed, temperature or lagged PM2.5) pushed a prediction up or down.
- **Converting a PM2.5 forecast to AQI:** convert the PM2.5 forecast to a PM2.5 sub-index, then compare it with the other pollutants' sub-indices. The highest one is the AQI, and this also tells us the dominant pollutant.
- **To verify:** the averaging window used for each pollutant, and the minimum number of pollutants required, in the CPCB methodology.

## Decisions Log

- (25-10-2026) **Decision:** Study five cities: Dehradun (home region), Lucknow (northern plains), Delhi (extreme winter pollution), Mumbai (coastal) and Chennai (southern coast).
  **Reason:** They cover different geography and climate, which allows comparison across regions.
  **Alternative considered:** Other cities such as Kolkata.
  **Trade-off:** No city from eastern or central India, so conclusions may not generalise there.

- (25-10-2026) **Decision:** Forecast pollutant concentrations, then compute the AQI from the forecasts using the official CPCB formula.
  **Reason:** A single pollutant's concentration is a more physical and smoother target than the AQI, which jumps whenever the maximum switches from one pollutant to another. Computing the AQI afterwards keeps it consistent with the official method, shows which pollutant is dominant, and lets SHAP explain each pollutant's forecast separately.
  **Alternative considered:** Forecasting the AQI directly (one model per city and horizon).
  **Trade-off:** More models to train and validate. The exact count depends on how many pollutants and horizons I model and whether cities are pooled into one model, so I will reduce it after the EDA shows which pollutants matter. Errors in each pollutant forecast carry into the AQI through the max step, and an error in a non-dominant pollutant can matter if it becomes dominant. A city missing data for one pollutant would also limit the AQI calculation.
  **Open question:** Which pollutants to forecast (all, or only PM2.5 and PM10). Revisit after the Week 2 EDA, once I have counted how often each pollutant is dominant.

- (date) **Decision:** TODO: validation strategy (time-series cross-validation instead of a random split).
  **Reason:** TODO
  **Alternative considered:** TODO
  **Trade-off:** TODO

## Demo

Screenshots, GIF and live link will go here.