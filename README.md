# Jollibee Stock Price Prediction: Hybrid ARIMA-XGBoost Model

## Overview
This repository contains a machine learning project focused on forecasting the stock price of Jollibee Foods Corporation (JFC). Traditional time-series models often struggle with complex, non-linear market behaviors, while pure machine learning models might miss baseline linear trends. 

To solve this, this project implements a **Hybrid ARIMA-XGBoost Model**:
1. **ARIMA** (AutoRegressive Integrated Moving Average) is used to capture the linear patterns and general trends of the time series.
2. **XGBoost** (Extreme Gradient Boosting) is then trained on the residuals (errors) of the ARIMA model to capture complex, non-linear relationships.
3. The final prediction is the combination of the ARIMA forecast and the XGBoost residual prediction.

## Project Structure
The core of the project is contained within the Jupyter Notebook:
* `jollibee_stock_pred.ipynb`: The main notebook containing all code for data processing, modeling, and evaluation.

**Notebook Workflow:**
1. **Importing Libraries**: Loading necessary Python packages.
2. **Data Loading & Preprocessing**: Cleaning the historical stock data, handling missing values, and formatting dates.
3. **Exploratory Data Analysis (EDA)**: Visualizing stock trends, moving averages, and volatility.
4. **ARIMA Modeling**: Finding optimal $(p, d, q)$ parameters and fitting the linear model.
5. **XGBoost Modeling**: Extracting residuals from ARIMA and fitting the XGBoost regressor.
6. **Evaluation**: Comparing model performance using metrics like RMSE, MAE, and MAPE.

## Dataset
* **Source:** Yahoo Finance
* **Features Used:** Date, Close Price

## Prerequisites & Installation
Install the dependencies using `pip`:
pip install requirements.txt
