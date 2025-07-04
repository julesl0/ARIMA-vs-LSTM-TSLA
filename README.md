## TESLA Stock Price Forecasting using ARIMA and LSTM ##

This project was completed for **STAT 543: Computational Statistics** at the University of Calgary.

Two time series forecasting models; **ARIMA** (a traditional statistical model) and **LSTM** (a deep learning model) were used to predict Tesla (TSLA) stock prices. 
The goal includes not only to evaluate their statistical accuracy, but also practical usefulness through mock trading simulations. 

## Research Question
Can deep learning models such as LSTM outperform a traditional statistical models like ARIMA in both prediction accuracy and real-world trading profit?

## Dataset
- **Source**: yfinance API from Yahoo Finance
- **Period**: Jan 1, 2021 – April 4, 2025
- **Features**:
  - TSLA: Open, High, Low, Close, Volume
  - NASDAQ-100 Index: Close
  
## Models Overview

### **LSTM Model 1**
Predicts current day's TSLA closing price based on pst 60 days of the dataset. It does not forecast the future, but rather reconstructs present using historical patterns.

  - **Input Features**:
    - TSLA_Close, 10 day Moving Average (MA10), 20 day Moving Average (MA20)
  - **Design**:
    - Two hidden layers (128 -> 64 units)
    - Final output layer


### **LSTM Model 2**
Forecasts the next day's TSLA closing price using previous 30 days of multivariate features.
 
  - **Input Features**:
    - TSLA: Open, High, Low, Close, Volume
    - NASDAQ Index closing price
  - **Design**:
      - Two hidden layers (64 -> 32 units), each followed by Dropout (rate = 0.2)
      - Final layer outputs one prediction (next day price)


### **ARIMA**
**ARIMA (0,1,0) model** was used to model daily TSLA closing prices.

  - After removing non-stationarity through differencing and detrending, a rolling forecast was applied.
  - **Preprocessing**:
    - Linear detrending + weekly rolling forecasts
    - auto_arima() from pdarima was used to select the best model
     
## Mock Trading Simulation
Evaluates the real-world applicability of each model.

### Setup:
- **Initial cash**: $10,000
- **Buy 1 share** of TSLA if model preducts that price will go up the next day
- **Sell 1 share** of TSLA if model predicts the price will go down

This approach assumes a basic and simple strategy with no transaction fees. 

## Insights:
- **LSTM Model 1** had the lowest RMSE, yet made least profit ($8.54)
- **LSTM Model 2** generated the highest profit (+$567.73)
- **ARIMA** produced moderate profit (+$72.18), despite having weaker statistical performance.

- ## Moving Forward:
  - Include additional macronomic indicators (e.g., GDP, CPI, inflation rates).
  - Explore more advanced architectures.
  - Incorporate transaction costs in mock trading for more realistic simulation.
