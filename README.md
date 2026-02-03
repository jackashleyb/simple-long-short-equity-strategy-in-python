# Simple Long Short Equity Strategy In Python 

A quantitative trading strategy project built in Python. This project implements a **market-neutral approach** by going long on underperforming stocks and short on overperforming ones, aiming to capture mean reversion (SPY, META, GOOGL, MSFT).

- i used this video when reasearching and planning this proejct - [Youtube Video](https://www.youtube.com/watch?v=Ozrb5uelqz8)
- i'm also reading and refrencing this book when looking for proejct ideas - [Building Automated Quantitative Trading Systems](https://www.amazon.co.uk/Building-Automated-Quantitative-Trading-Systems/dp/9334453508)

## Overview

The core hypothesis is that stock returns often revert to the mean. By calculating the average performance of a portfolio and trading the deviations:
- **Strategy:** Long positions in stocks below the group average; Short positions in stocks above it.
- **Objective:** To generate stable, risk-adjusted returns while minimizing exposure to overall market direction.
- **Result:** Achieved a **Sharpe Ratio of 0.36** over a 5-year backtest period (2021–2026).

## The Results

### 1. Strategy Performance
- **Annualized Sharpe Ratio:** `0.36`
  - A positive Sharpe ratio indicates the strategy generated excess returns per unit of risk, though there is room for optimization.
  
### 2. Returns Distribution
- The distribution of daily strategy returns is centered around zero but shows a slight positive skew.
- Most daily returns fall between **-2% and +2%**, confirming the volatility-dampening effect of the long-short structure compared to a long-only portfolio.

### 3. Portfolio Exposure

- Dynamic rebalancing ensured that the net exposure remained low, with weights adjusting daily based on the magnitude of each stock's deviation from the group mean.

## Technical Implementations

**1. Data Pipeline:**
- Fetched 5 years of data for `SPY`, `META`, `GOOGL`, and `MSFT` using `yfinance`.
- Handled MultiIndex DataFrames to cleanly extract 'Close' prices.

**2. Signal Generation:**
- Computed **Log Returns** (`np.log(price / prev_price)`) for additive properties.
- Calculated the **Cross-Sectional Mean** of returns daily.
- Generated signals: `Weight = -(Stock_Return - Average_Return)`.

**3. Risk Management:**
- Normalized weights so that the sum of absolute weights equals 1.0 daily (Gross Leverage = 1.0).
- This ensures the strategy is fully invested but hedged, rather than taking leveraged bets.

## What I Learned

- **Quantitative Analysis:** How to transform raw prices into log returns and why mean-reversion works in correlated sectors.
- **Python for Finance:** Practical experience with `pandas` for time-series alignment, `numpy` for vectorized math, and handling real-world data gaps (`dropna()`).
- **Performance Evaluation:** Moving beyond simple "total return" to understand **Sharpe Ratio** and **volatility** as the true measures of a strategy's quality.

