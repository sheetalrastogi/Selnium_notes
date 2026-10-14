# Indian Stock Market Technical Analysis Prompt — Daily Trend, Support & Resistance, Intraday Levels

## Role
Act as a professional Indian equity technical analyst specializing in NSE stocks, price action, market structure, volume analysis, and intraday trading strategies.

Analyze the attached chart screenshot dated October 14, 2026, showing the following stocks:

1. Blue Dart Express — BLUEDART
2. Schaeffler India — SCHAEFFLER
3. Triveni Engineering & Industries — TRIVENI
4. Balkrishna Industries — BALKRISIND
5. Fortis Healthcare — FORTIS
6. Bata India — BATAINDIA
7. Natco Pharma — NATCOPHARM
8. Maruti Suzuki India — MARUTI

The screenshot shows weekly price charts. Use it to understand the broader trend and visible price structure, but obtain current and historical daily market data from reliable sources before calculating precise trading levels.

## 1. Data verification and market context

For every stock:

- Verify the latest available NSE closing price and the date of that price.
- Retrieve daily OHLC (Open, High, Low, Close) data for the latest two completed trading sessions.
- Retrieve daily traded volume for both sessions, in shares.
- Calculate the percentage change in closing price and volume between the two sessions.
- Identify the 52-week high, 52-week low, and distance from the current price to the 52-week low.
- Identify relevant corporate announcements, earnings, bulk/block deals, or other news that could affect the stock.
- Use reliable sources such as NSE India, official exchange disclosures, and established market-data providers.

Clearly distinguish verified data from estimates. Do not invent missing prices, volume figures, or dates. If October 14 is still in progress, separate intraday data from the previous completed session.

## 2. Daily trend analysis

Analyze the daily chart over approximately 3–6 months, using the weekly screenshot as additional context.

Identify:

- Primary trend: bullish, bearish, or sideways.
- Short-term trend and recent swing highs/lows.
- Key resistance zones (R1, R2, R3).
- Key support zones (S1, S2, S3).
- Recent breakdowns, failed breakouts, gaps, and consolidation zones.
- Whether price is near a 52-week low or testing an established support zone.
- Whether the stock is showing accumulation, distribution, or continued selling pressure, where evidence supports that interpretation.

Use daily candlestick data and, where available, the 20-day, 50-day, and 200-day moving averages, RSI (14), and ATR (14).

Support and resistance must be identified as price zones rather than falsely precise single prices. Explain the technical reason for every important level.

## 3. Intraday support and resistance

For each stock, determine the most relevant intraday levels for the next trading session.

Include:

- Previous trading session high (PDH).
- Previous trading session low (PDL).
- Previous trading session close.
- Second-previous session high, low, and close.
- Current session opening price, when available.
- Intraday support and resistance derived from previous highs/lows, swing points, gaps, and price consolidation.
- VWAP, once current-session data is available.
- Opening-range high/low, after the first 15–30 minutes of trading.
- Pivot levels and previous-session-based support/resistance, if useful.

Distinguish between daily-chart support and resistance and intraday support and resistance. Explain whether an intraday level has stronger significance because it overlaps with a daily-chart level.

Do not treat the weekly screenshot as sufficient evidence for exact intraday levels.

## 4. Daily volume and participation analysis

For each of the last two completed trading sessions, report:

- Total traded volume in shares.
- Volume change in percentage terms.
- Delivery quantity and delivery percentage, if reliably available.
- Relative volume compared with the 20-day average.
- Whether price and volume together suggest strong selling, potential accumulation, weak participation, or a possible reversal.

Do not claim institutional buying or accumulation solely from one day's volume spike.

## 5. Trading scenarios

Develop conditional trading plans rather than unconditional buy/sell recommendations.

**Bullish scenario**
- Price level that must be reclaimed or broken.
- Required volume confirmation.
- Possible entry trigger.
- Stop-loss based on price structure or ATR.
- First and second target zones.
- Conditions that invalidate the setup.

**Bearish scenario**
- Support level whose breakdown would confirm weakness.
- Required volume or price-action confirmation.
- Potential short-entry trigger, where permitted.
- Stop-loss and target zones.
- Conditions that invalidate the setup.

**No-trade scenario**
- Identify when price is trapped between support and resistance, liquidity is insufficient, or risk/reward is unattractive.

Avoid recommending a trade simply because a stock is trading near its 52-week low. Distinguish a genuine reversal from a continuing downtrend.

## 6. Risk management

For each proposed setup:

- Calculate the potential reward-to-risk ratio.
- Prefer setups offering at least 1.5:1 reward-to-risk, ideally 2:1, after reasonable costs.
- Show a position-sizing example using a user-specified trading capital and maximum risk per trade.
- Account for brokerage, taxes, slippage, and liquidity.
- Flag stocks with wide spreads, gaps, or unusually high volatility.
- Treat short selling as subject to applicable Indian market rules and intraday product restrictions.

If trading capital is not supplied, show the risk calculation formula rather than assuming a capital amount.

## 7. Required output format

### Table A — Daily trend and key levels

| Stock | Latest Close | Daily Trend | Support 1 | Support 2 | Resistance 1 | Resistance 2 | 52-Week Low | Trend Assessment |

### Table B — Last two completed trading sessions

| Stock | Session Date | Open | High | Low | Close | Volume (Shares) | Volume Change % |

Include both sessions for every stock.

### Table C — Intraday trading plan

| Stock | Previous Day High | Previous Day Low | Intraday Support | Intraday Resistance | Bullish Trigger | Bearish Trigger | Stop-Loss Logic | Target Zones |

### Table D — Ranked watchlist

Rank the stocks from 1 to 8 based on the quality of their potential intraday setups, not merely how close they are to their 52-week lows.

Include:
- Preferred direction: bullish, bearish, or wait.
- Setup quality and supporting evidence.
- Volume/liquidity confirmation.
- Risk/reward assessment.
- Key event or data risk.

If reliable data is insufficient to rank a stock, label it “Insufficient data” instead of inventing a ranking.

## 8. Final analyst summary

Conclude with:

1. The three stocks with the clearest potential intraday setups.
2. The strongest daily-chart support levels to monitor.
3. The most important resistance levels.
4. Stocks where support appears vulnerable to a breakdown.
5. Stocks showing credible reversal evidence, if any.
6. Exact price conditions that would change the analysis.
7. The data timestamp and sources used.

Important instructions:
- Use the latest available data as of the analysis time.
- Cite sources for prices, volumes, corporate announcements, and technical data.
- State whether data is live, delayed, or end-of-day.
- Never fabricate exact levels or claim a support level will definitely hold.
- This is a technical-analysis watchlist, not a guaranteed-profit strategy or personalized investment advice.
