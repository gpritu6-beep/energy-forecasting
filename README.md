# Energy Consumption Forecasting (AEP Hourly)

Predict hourly electricity consumption (in MW) using time-based features.

## Dataset
- `AEP_hourly.csv`: hourly energy consumption of AEP
- 121,273 rows, 2 columns (`Datetime`, `AEP_MW`), no missing values
- Consumption range: 9,581 to 25,695 MW (mean 15,499.51 MW)

## Approach
1. Converted `Datetime` to a datetime type and plotted consumption over time
2. Engineered time features: `hour`, `day_of_week`, `month`, `year`, `is_weekend`
3. Split data 80/20 (train/test)
4. Trained a Random Forest Regressor (100 trees)
5. Evaluated with MAE and compared actual vs predicted values

## Results
| Metric | Value |
|---|---|
| Model | Random Forest Regressor |
| MAE | 1,161.72 MW |
| Mean consumption | 15,499.51 MW |
| Error % (MAE / mean) | 7.50% |

**Feature importance:** `hour` was the most important feature, followed by `month` and `year`. `day_of_week` and `is_weekend` mattered least.

## Limitations
- The train/test split is random, not chronological. Neighbouring hours can land in both sets, so the error is likely optimistic for true future forecasting.
- `year` as a feature cannot extrapolate to future years.
- No lag features (previous hours/days) or weather data were used.

## Next steps
- Chronological split (train on earlier years, test on the latest)
- Add lag features and rolling averages
- Try gradient boosting (XGBoost / LightGBM)

## Files
- `Energy_Forecasting.ipynb`: full notebook

## Tools
pandas, numpy, matplotlib, scikit-learn
