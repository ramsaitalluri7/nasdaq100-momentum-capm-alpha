# Nasdaq-100 Momentum Strategy: Does It Have Real Alpha?

A weekly long-short momentum strategy on Nasdaq-100 stocks (2015–2025), tested against CAPM to see if it beats the market after adjusting for risk.

*SMU MSc Quantitative Finance — QF600 Asset Pricing group project, with Qian Chudong and Shobi Iva Gundavarapu.*

## The idea
Every week, rank Nasdaq-100 stocks by their recent returns.
- **Buy** the top 10% (recent winners)
- **Short** the bottom 10% (recent losers)
- Rebalance on a rolling window and compare against the Nasdaq-100 index (^NDX)

## What makes it careful
- **Point-in-time universe:** each year uses the stocks that were actually in the Nasdaq-100 *that year*, not today's list, to reduce survivorship and look-ahead bias.
- **Rolling backtest:** signals are formed on a past window (20 weeks) and traded only on the next window (5 weeks).
- **Robustness grid:** Sharpe and alpha tested across 90 combinations of fit window × trade window, on the full sample and on two separate 5-year halves.

## Results (2015–2025, weekly)

| Metric | Strategy | Nasdaq-100 |
|---|---|---|
| $1 grows to | **$6.62** | $5.55 |
| CAGR | **19.2%** | 17.2% |
| Sharpe ratio | 0.78 | 0.89 |
| Max drawdown | -43.4% | -35.5% |
| Annual volatility | 27.0% | 20.1% |

**CAPM regression** (strategy returns on index returns):
- Alpha = **0.37% per week** (~19% per year), **p-value = 0.021** → statistically significant at 5%
- Beta = **0.11** → the strategy is almost independent of the market

## Honest takeaways
- The strategy earned more than the index with very low market exposure, and the alpha is significant.
- But it was **bumpier**: higher volatility, deeper drawdown, and a slightly lower Sharpe than simply holding the index.

## Limitations
- Parameters were chosen and evaluated on the same data. A proper train/test split is the next step.
- No transaction costs. Weekly rebalancing would reduce returns in practice.
- Risk-free rate assumed to be 0.
- Some delisted stocks have no data on Yahoo Finance and were dropped, so a little survivorship bias remains.

## Tools
Python · pandas · NumPy · yfinance · SciPy · lets-plot
