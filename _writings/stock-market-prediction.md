---
title: "ML Application: Predicting Stock Market Using Random Forests"
subtitle: "Using technical indicators and Random Forests to forecast JPM stock price movements"
category: Machine Learning
tags: [machine-learning, random-forest, stocks, finance, python]
order: 10
---

Can machine learning predict stock prices? This project uses Random Forest models combined with technical indicators to forecast JPMorgan (JPM) stock price movements.

## Motivation

Three reasons to try:
- Potentially unlimited financial upside
- Portfolio risk management
- Enabling algorithmic trading strategies

## Approach

### Technical Indicators as Features

Three indicators derived from historical market data:
- **Momentum** — Rate of price change over a window
- **Bollinger Bands** — Volatility-based price channels
- **Relative Strength Index (RSI)** — Overbought/oversold signal

### Target Variable

Future adjusted stock prices using a 9-day moving average comparison against current prices.

### Algorithm Choice

Random Forest was selected for its ability to:
- Combine multiple decision trees for robust predictions
- Handle large datasets effectively
- Reduce overfitting compared to individual trees

## Results

Training: January 2008 — December 2009. Testing: January 2010 — December 2011.

- **In-Sample Cumulative Return:** 12.6%
- **Out-of-Sample Cumulative Return:** 8.0%
- **Optimal Parameters:** 26-day windows for Momentum/RSI; 20-day window for Bollinger Bands
- Larger bag sizes improved prediction probability to 95%

## Reflections

The model shows promise but alternatives like XGBoost or deep learning approaches (LSTMs in particular) could potentially improve results. The 8% out-of-sample return is respectable but the real challenge is accounting for transaction costs, slippage, and regime changes in live trading.
