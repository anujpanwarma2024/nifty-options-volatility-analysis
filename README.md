# NIFTY Options Volatility Smile & SABR Analysis
This project analyzes NIFTY 50 options data for a near-term expiry to study how the market prices risk.

The goal was to construct the implied volatility smile, measure skew (downside risk), and calibrate a SABR model to understand the structure of implied volatility.

The volatility smile and skew were successfully observed, showing higher implied volatility for downside strikes. However, SABR calibration faced instability due to noisy and short-dated option data, highlighting the challenges of fitting models to real market data.

Overall, the project demonstrates an end-to-end pipeline from raw option chain data to volatility modeling and interpretation.
