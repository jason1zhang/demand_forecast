# Demand Forecasting with CatBoost

> **Productionized a CatBoost model to predict daily order volumes during promotions, improving inventory planning accuracy.**

## Project Overview
- **Goal:** Forecast daily demand for 100 products across 5 stores, with special focus on promotional periods.
- **Model:** CatBoostRegressor with time‑series feature engineering.
- **Key Achievement:** Test‑set promotional MAPE reduced to **8.6%**, MAE to **8.26 units**.

## Data
- 76,000 rows, 35 features after engineering.
- Time span: 2022‑01‑01 → 2024‑01‑30.
- Includes price, discount, weather, seasonality, competitor pricing, and promotion flags.

## Approach
1. **EDA:** Distribution analysis, promotion lift (29.7%), correlation matrix, category/region/weather comparisons.
2. **Feature Engineering:**  
   - Target‑based lags (shift 1,2,3,7,14) and rolling statistics (7d,14d mean/std) per product‑store.  
   - `days_since_last_promo`, `price_diff`.  
   - Avoided data leakage by removing same‑day `Units Sold` and `Units Ordered`.
3. **Modelling:** CatBoost with early stopping, tuned via validation set.
4. **Evaluation:** Overall and promotion‑only MAE, RMSE, MAPE.
5. **Interpretability:** SHAP summary plot revealing Price, Category, Discount, and Promotion as key drivers.

## Key Results
| Set | MAE | RMSE | MAPE |
|-----|-----|------|------|
| Train | 5.42 | 7.87 | 7.1% |
| Validation | 5.53 | 7.89 | 9.8% |
| Test | **5.16** | **7.35** | **6.1%** |
| *Test (promo only)* | *8.26* | *11.61* | *8.6%* |
