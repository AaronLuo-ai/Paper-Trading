# Paper Trading

Automated paper-trading bot for US stocks. Every weekday after market close, GitHub Actions scores 22 large-cap stocks and ETFs with technical indicators, places simulated trades in a virtual **$100,000** portfolio, and commits an HTML report to `reports/`.

> Paper trading only. No real money and no financial advice.

## How it works

1. Load the portfolio from `portfolio.json`.
2. Score each ticker from 60 days of `yfinance` data: price vs 20/50-day moving averages, RSI(14), volume, and the daily move.
3. **BUY** at score $\ge 0.40$ (5% of portfolio value, max 10 positions). **SELL** the whole position at score $\le -0.25$.
4. Write `reports/YYYY-MM-DD_report.html` with P&L, holdings, trades, watchlist signals and market news.

## Run

```bash
pip install yfinance
python paper_trade.py
```

On GitHub, the workflow `.github/workflows/daily_trade.yml` runs at 21:10 UTC, Mon–Fri. You can also start it manually from the **Actions** tab. Parameters such as `WATCHLIST`, the thresholds and position size are set at the top of `paper_trade.py`.

## Limitations

No commissions, slippage or dividends. The signals are a simple heuristic, not a backtested model.
