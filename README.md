# AlgoTrader 7

AlgoTrader 7 is a local, single-user backend for natural-language-driven NSE analysis and portfolio operations.

- Backend runs on your local machine.
- Telegram is only the frontend interface.
- AI inference runs locally through Ollama using `qwen3:8b`.

## Features

- Async Telegram listener (`python-telegram-bot`)
- Local Ollama intent classification with confidence gating
- Deterministic financial core:
  - Budget invariants
  - Portfolio accounting
  - ATR-based position sizing
  - Risk manager (max position, sector exposure, drawdown stop)
  - Trend/Stability/Risk scoring
  - News modifier
  - Exhaustion engine
  - Structural override (always enforced)
- Realistic backtesting with brokerage + slippage
- Strategy version/hash persistence for reproducible backtests
- Hourly background jobs:
  - Portfolio recalculation
  - Budget-based picks
  - News refresh
- Backtesting engine with CAGR, drawdown, Sharpe, win rate
- Separate paper-trading portfolio
- Performance charts (equity, drawdown, allocation)
- SQLite persistence

## Setup

1. Create and activate a Python environment.
2. Install dependencies:

```powershell
pip install -r requirements.txt
```

3. Ensure `.env` includes:

- `TELEGRAM_BOT_TOKEN`
- `OLLAMA_BASE_URL` (default `http://localhost:11434`)
- `OLLAMA_MODEL` (default `qwen3:8b`)
- `MARKET_DATA_PROVIDER` (`yfinance`, `polygon`, `alphavantage`, `upstox`)
- Provider credentials if provider is not `yfinance`
- `BROKERAGE_RATE`, `SLIPPAGE_RATE`, and risk limits

4. Install and run Ollama, then pull model:

```powershell
ollama serve
ollama pull qwen3:8b
```

5. Start backend:

```powershell
python main.py
```

## Startup validation

On launch, AlgoTrader 7 validates:

1. `TELEGRAM_BOT_TOKEN` exists.
2. Ollama endpoint is reachable.
3. `qwen3:8b` is available in Ollama.
4. SQLite schema is initialized.

If any critical dependency is missing, startup stops with setup instructions.

## Run tests

```powershell
./scripts/run_tests.ps1
```
