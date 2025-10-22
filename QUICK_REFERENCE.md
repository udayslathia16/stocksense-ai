# 🎯 Technical Indicators Quick Reference

## One-Page Cheat Sheet

| Indicator | What It Measures | Bullish Signal | Bearish Signal |
|-----------|------------------|----------------|----------------|
| **SMA-20/50/200** | Trend direction | Price > SMA | Price < SMA |
| **RSI (0-100)** | Momentum strength | < 30 (Oversold) | > 70 (Overbought) |
| **MACD** | Trend momentum | Line > Signal | Line < Signal |
| **Bollinger Bands** | Volatility | Price near lower band | Price near upper band |
| **ATR** | Volatility level | N/A | High ATR = Risky |
| **Volume** | Trade confirmation | High vol + price up | High vol + price down |
| **Support/Resistance** | Key price levels | Price at support | Price at resistance |

## Recommendation Guide

| Score | Signal | Action |
|-------|--------|--------|
| +7 to +9 | 🟢 STRONG BUY | High confidence buy |
| +4 to +6 | 🟢 BUY | Moderate buy |
| +1 to +3 | 🟡 HOLD (bullish) | Slight buy bias |
| 0 | 🟡 HOLD | Neutral |
| -1 to -3 | 🟡 HOLD (bearish) | Slight sell bias |
| -4 to -6 | 🔴 SELL | Moderate sell |
| -7 to -9 | 🔴 STRONG SELL | High confidence sell |

📖 For detailed explanations, see [Complete Indicators Guide](INDICATORS_GUIDE.md)


---

Create `indicator-flow.png` with this flow:
```
┌─────────────────┐
│  Stock Data     │
│  (Price/Volume) │
└────────┬────────┘
         │
    ┌────▼────────────────┐
    │ Calculate Indicators│
    ├────────────────────┤
    │ • SMA/EMA          │
    │ • RSI              │
    │ • MACD             │
    │ • Bollinger Bands  │
    │ • ATR              │
    │ • Support/Resist   │
    │ • Volume Analysis  │
    └────────┬───────────┘
             │
    ┌────────▼──────────┐
    │ Generate Signals  │
    │ Bullish: 6/9      │
    │ Bearish: 3/9      │
    │ Score: +3         │
    └────────┬──────────┘
             │
    ┌────────▼──────────┐
    │  AI Analysis      │
    │  (Claude/GPT-4)   │
    │  • Context        │
    │  • Risk Level     │
    │  • Entry/Exit     │
    └────────┬──────────┘
             │
    ┌────────▼──────────┐
    │ Final Output      │
    │ BUY/SELL/HOLD     │
    │ + Detailed Report │
    └───────────────────┘