# Macro Intelligence - 宏观情报中心

Unified macro intelligence feed — reads 7 sources (NewsNow, Polymarket, OpenNews, Finnhub, Telegram, FRED, Fear & Greed), classifies events with 24+ regex patterns + LLM confirmation, scores sentiment, and exposes signals via HTTP API. No trading logic — downstream skills consume the signals. Powered by [onchainos](https://github.com/okx/onchainos-skills).

统一宏观情报流 — 聚合 7 大数据源（NewsNow、Polymarket、OpenNews、Finnhub、Telegram、FRED、恐贪指数），24+ 正则模式 + LLM 二次确认分类事件，量化情绪评分，通过 HTTP API 输出信号。不含交易逻辑 — 下游策略消费信号。基于 [onchainos](https://github.com/okx/onchainos-skills) 构建。

## Features / 功能

- **7 Data Sources / 7 大数据源** — NewsNow, Polymarket, 6551.io OpenNews, Finnhub, Telegram, FRED, Fear & Greed Index
- **3-Layer Classification / 三层分类** — Keyword regex → LLM confirm (ambiguous) → LLM discover (missed)
- **24+ Event Types / 24+ 事件类型** — Fed cuts/hikes, CPI, gold, geopolitical, tariffs, whale alerts, RWA catalysts, credit events
- **Bilingual Patterns / 中英双语模式** — All keyword patterns support English and Chinese (降息/加息/通胀/黄金...)
- **Macro Playbook / 宏观剧本** — Maps events to direction, magnitude, urgency for downstream consumption
- **Sender Reputation / 信源信誉系统** — Tracks source reliability with decay, boosts high-rep senders 1.3x
- **FRED Hard Indicators / FRED 硬指标** — Fed Funds Rate, CPI, GDP, Unemployment, 10Y-2Y spread, 10Y yield
- **Fear & Greed Gauge / 恐贪指数** — Crypto Fear & Greed with sparkline history
- **Polymarket Predictions / Polymarket 预测** — Live prediction market odds for macro events
- **Price Tickers / 价格行情** — SPY, Gold, Silver, BTC, ETH with 24h change
- **Cross-Source Dedup / 跨源去重** — MD5 hash dedup within 4-hour window
- **HTTP Signal API / HTTP 信号 API** — 11 endpoints for filtered signals, sentiment, regime, and summaries
- **Web Dashboard / 实时仪表盘** — http://localhost:3252

## Install / 安装

```bash
npx skills add okx/plugin-store --skill macro-intelligence
```

## API Endpoints / 接口

| Endpoint | Description |
|----------|-------------|
| `GET /api/signals` | Filtered signals (by direction, affects, magnitude, hours) |
| `GET /api/sentiment` | Aggregate sentiment + regime |
| `GET /api/regime` | Current market regime |
| `GET /api/polymarket` | Prediction market data |
| `GET /api/fng` | Fear & Greed Index |
| `GET /api/fred` | FRED macro indicators |
| `GET /api/prices` | Price tickers (SPY, GLD, SLV, BTC, ETH) |
| `GET /api/senders` | Source reputation leaderboard |
| `GET /api/events` | Event type counts |
| `GET /api/summary` | All-in-one summary |

## Optional API Keys / 可选 API Key

All sources degrade gracefully — the skill runs without any keys, adding sources as keys are configured.

| Key | Source | Get it |
|-----|--------|--------|
| `ANTHROPIC_API_KEY` | LLM classification + insights | [anthropic.com](https://console.anthropic.com) |
| `FINNHUB_API_KEY` | Market news + stock quotes | [finnhub.io](https://finnhub.io) |
| `FRED_API_KEY` | Federal Reserve economic data | [fred.stlouisfed.org](https://fred.stlouisfed.org/docs/api/api_key.html) |
| `OPENNEWS_TOKEN` | 6551.io real-time news WebSocket | [6551.io/mcp](https://6551.io/mcp) |
| `TG_API_ID` / `TG_API_HASH` | Telegram group monitoring | [my.telegram.org](https://my.telegram.org) |

## Risk Warning / 风险提示

> This skill provides macro intelligence signals only — it does not execute trades. Signal classification is probabilistic and may misinterpret events. Always validate signals with your own analysis before acting.

> 本技能仅提供宏观情报信号，不执行交易。信号分类为概率性判断，可能误读事件。请务必结合自身分析验证信号后再行动。

## License

MIT
