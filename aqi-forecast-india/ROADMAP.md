# Roadmap (8 weeks)

Commit at least a few times every week. Write a line in the README decisions log whenever you make a choice.

## Week 1: Setup and data
- [ ] Create a GitHub repo, push this folder, make the first commit
- [ ] Pick 5-10 cities (include Dehradun, Delhi, Mumbai, Kolkata, Chennai, Lucknow)
- [ ] Download historical PM2.5 / AQI data (OpenAQ, CPCB or Kaggle)
- [ ] Download matching hourly weather data from Open-Meteo
- [ ] Write `src/data/` scripts that fetch and save raw data

## Week 2: Cleaning and EDA
- [ ] Handle missing values and outliers (document how)
- [ ] Merge air quality and weather on timestamp
- [ ] Plot daily, weekly and yearly seasonality
- [ ] Compare cities; note Diwali, stubble-burning and winter effects
- [ ] Save the cleaned dataset to `data/processed/`

## Week 3: Features and baselines
- [ ] Build lag, rolling-mean and calendar features
- [ ] Set up time-series cross-validation (no random splits)
- [ ] Persistence baseline ("same as yesterday")
- [ ] Linear regression baseline
- [ ] Record baseline MAE / RMSE in the README table

## Week 4: Gradient boosting and Prophet
- [ ] XGBoost / LightGBM with tuned hyperparameters
- [ ] Prophet model
- [ ] Forecast at 24h, 48h and 72h horizons
- [ ] Compare all models in one results table

## Week 5: Deep learning
- [ ] LSTM in PyTorch on sliding windows
- [ ] Check if it beats the tree models; write down why or why not

## Week 6: Explainability
- [ ] SHAP summary and per-prediction plots
- [ ] Write 3-4 insights about what drives AQI in your cities

## Week 7: Dashboard
- [ ] Streamlit app: city picker, forecast chart, map, SHAP view
- [ ] Add an alert threshold and simple health guidance
- [ ] Optional: what-if sliders (wind speed, temperature)

## Week 8: Deploy and polish
- [ ] Dockerfile
- [ ] Deploy to Hugging Face Spaces or Render
- [ ] Add screenshots, demo GIF and live link to README
- [ ] Add a few tests in `tests/`
- [ ] Write 3-4 resume bullets with real numbers

## Stretch goals
- [ ] Daily data refresh with GitHub Actions
- [ ] Drift monitoring
- [ ] Short blog post on what you found
