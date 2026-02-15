# Jollibee Stock Price Prediction: Hybrid ARIMA-XGBoost Model

## Overview
This repository contains a machine learning project focused on forecasting the stock price of Jollibee Foods Corporation (JFC), ticker **JBFCF**. Traditional time-series models often struggle with complex, non-linear market behaviors, while pure machine learning models might miss baseline linear trends. 

To solve this, this project implements a **Hybrid ARIMA-XGBoost Model** based on the residual correction approach:
1. **ARIMA (1,1,1)** is used to capture the linear patterns, general trends, and short-term mean reversion of the time series.
2. **XGBoost** is then trained on the residuals (errors) of the ARIMA model to capture complex, non-linear relationships and sudden market shocks (e.g., flash crashes).
3. The final prediction is the combination of the ARIMA forecast and the XGBoost residual prediction.

This project demonstrates that the hybrid approach significantly reduces the lagging issue in traditional ARIMA models and tightens prediction errors.

## Project Structure
* `jollibee_stock_pred.ipynb`: The main notebook containing all code for data processing, modeling, and evaluation.
* `BaocaoDubao_No.1.pdf`: The detailed project report (in Vietnamese) explaining the methodology and theoretical foundation.

**Workflow:**
1. **Data Collection & Preprocessing:** Data from Yahoo Finance, resampled to Business Days with Forward Fill for missing values.
2. **Linear Modeling (ARIMA):** ADF testing for stationarity, ACF/PACF analysis, and Grid Search (via `pmdarima`) to find the optimal $(p, d, q)$ = (1, 1, 1).
3. **Non-linear Modeling (XGBoost):** Extracting ARIMA residuals and using a sliding window technique for Feature Engineering. The optimal window size was empirically found to be **4 days**.
4. **Recursive Forecasting:** Predicting future prices over a 10-day and 30-day horizon using an iterative feedback loop.

## Dataset
* **Source:** Yahoo Finance (`yfinance` API).
* **Ticker:** JBFCF (OTC Market).
* **Timeframe:** January 01, 2024 - December 18, 2025 (513 business days).
* **Target Variable:** Close Price.

## Prerequisites & Installation
```bash
pip install requirements.txt

```

## Results & Conclusion

The hybrid model drastically improved forecasting accuracy compared to the standalone ARIMA model:

* **ARIMA (1,1,1):** * RMSE: 0.1426
* MAE: 0.0976
* MAPE: 2.43%


* **Hybrid ARIMA-XGBoost:** * **RMSE: 0.0279 (80.44% Improvement)**
* **MAE: 0.0208 (78.70% Improvement)**
* **MAPE: 0.51% (79.03% Improvement)**



**Key Findings:**

* The optimal historical window for XGBoost to learn the ARIMA residuals is just **4 days**, indicating a strong short-term memory in the error terms. Feeding too much historical data (e.g., 80-100 days) introduces noise and increases the error.


* The hybrid model successfully eliminated the "phase lag" common in ARIMA models, allowing it to closely track sudden V-shaped reversals and sharp market drops.


* **Market Outlook (Dec 2025 - Feb 2026):** The model predicts a technical rebound for JBFCF, with a near-term accumulation phase around $3.10 - $3.25, followed by a potential uptrend breaking the $3.30 resistance.
