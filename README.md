# Benihime

**RTH Gap Map for NQ, ES & RTY**

TradingView indicator, Pine Script v6. Open source under the Mozilla Public License 2.0.

![Benihime](images/Benihime_RTH_1m.png)

*Mock-up of how it looks on the chart.*

**Benihime** maps RTH gaps the way NWOGs are mapped. An RTH gap is the overnight move between two regular sessions: from the prior RTH close (the 16:14 bar, the 16:15 ET close) to the next 09:30 ET open.

- Every gap of the last 20 sessions (up to 60) runs right in price.
- The last five get a closer look: octants, plus steps one and two gap sizes beyond them.
- A card tracks today's gap against the average RTH gap, with odds measured on **6,169 gaps** on NQ, ES and RTY (2018–26).
- Release days (CPI, NFP, PPI, GDP, PCE, retail sales) switch the day's regime.

*It is a map of where the RTH gaps sit and how gaps of each size usually behave, not a signal generator.*

## What it draws on price

- **Every RTH gap** of the last N sessions (default 20, up to 60): its edges (the prior close and the open) and its **CE** (consequent encroachment, the 50%). Each one starts at its own 09:30 open and runs to the right of price.
- **The staircase, the last 5 sessions (rolling):** each gap is split into **octants**. The CE is dashed, the quarters dotted and the eighths faint.
- Each staircase gap also gets **±1 SD** (dashed) and **±2 SD** (solid): one and two gap sizes above its top and below its bottom. Five gaps stepping through the week build a staircase of levels. Staircase gaps are shaded.
- **Each ±2 SD line carries its gap's weekday** at the right end, e.g. *Tue +2 SD* or *Wed CPI −2 SD*, so every step can be traced to the day it came from.
- **Release days keep their staircase** (±1 / ±2 SD and the labels) for as long as they stay on the chart, not only while they are one of the last five. Their labels then add the date.
- **Sessions 6 to N** (default 10): quarters only (25%, CE, 75%).
- **Older gaps:** edges and CE only.
- **Filled gaps fade.** The labels on the right give the date, the release tag, and *CE* or *filled*. Labels at nearly the same price share one, so they never print over each other. Hover a label for the prior close, the open, the size against the average, when the CE and the fill were reached, and the ±1 SD prices.

## Release regime

- **Major releases, CPI and NFP** (orange): the release calendars Gran Rey Cero and Desgarrón use.
- **Other 08:30 releases** (purple):
  - **PPI** (BLS);
  - **GDP** and **PCE** / personal income and outlays (BEA);
  - **retail sales** (Census).
- **Your own dates** are tagged *NEWS* in the purple colour.
- The dates are the actual release days, including the shutdown moves, taken from the agencies' archives and ALFRED. CPI, NFP and PPI are loaded to Dec 2027; GDP, PCE and retail sales to Dec 2026.

**What the tests showed** (NQ, ES and RTY, 2018–26):

- **CPI and NFP gaps run 1.4–1.5× the size of normal-day gaps** (p < 0.001, in both periods and on every symbol). 35–40% of them are over 1.5× the 20-session average, against 21% of normal-day gaps.
- **The other releases move price at 08:30**: their 08:30–08:34 range runs 1.8–3.6× a normal day's, in every period and on every symbol. *Their RTH gaps were not reliably bigger* (PPI 1.14×, GDP 1.20×, retail sales 1.18×, PCE 1.00×; none held in both periods).
- **For its size, a release-day gap behaves like any other gap.** No fill or CE odds differed once size was accounted for. *The regime tells you how big the gap is likely to be; the odds come from its size.*

## Card · today's gap against the average

**During RTH:**

- **GAP:** points, %, and size against the 20-session average:
  - *small* (under 0.5×);
  - *below avg* (0.5–1×);
  - *above avg* (1–1.5×);
  - *large* (1.5–2.5×);
  - *very large* (2.5× and over).
- **AVG:** the average gap over N sessions (default 20). Every day counts, Mondays included. If fewer are loaded, the card says how many.
- **CE** and **FILL:** the time each was reached. Until then, the live odds of reaching it by 16:14, given it has not yet.
- **±1 SD:** the odds of reaching each side by 16:14, or the time it was reached.
- **5 SESS:** the odds of a fill, and of reaching the CE, while the gap is still one of the last five.
- **ABOVE** and **BELOW:** the CE and date of the nearest unfilled gap on each side of price.
- The header shows the day's releases, or *NORMAL*.

**Outside RTH:**

- the 16:14 close;
- *if it opened now*: the gap's size and its fill odds;
- the coming session's releases;
- the last gap's result.

## What the tests showed

Reached during RTH (09:30–16:14), by size against the 20-session average:

**Fill**

- under 0.5×: **88%**;
- 0.5–1×: 64%;
- 1–1.5×: 49%;
- 1.5–2.5×: 38%;
- 2.5× and over: **22%**.

**CE**

- under 0.5×: **94%**;
- 0.5–1×: 82%;
- 1–1.5×: 69%;
- 1.5–2.5×: 63%;
- 2.5× and over: **49%**.

These held in 2018–24 and in 2025–26, and on each of NQ, ES and RTY, to within about 4 points.

**All gaps**

- CE 78% and fill 62% in RTH.
- Within 5 sessions: 91% and 84%. Within 20 sessions: 96% and 92%.

**By time of day**

- About 36% have filled by 10:00, 48% by 11:00 and 53% by 12:00.
- An unfilled gap's odds shrink as the day goes on. For example, a 1–1.5× gap not yet filled at 10:30 went on to fill by 16:14 on 32% of days.

**The staircase's SDs** (while the gap is one of the last five):

- beyond the open (the gap's direction): +1 SD 84%, +2 SD 71%;
- beyond the prior close: 71% and 60%.

**After the staircase**

- A gap still unfilled after 5 sessions filled within the next 15 sessions 49% of the time.
- One whose CE was still untouched reached it 52% of the time.

## Settings

**View** sits at the top, the same as in my other indicators:

- card theme;
- text size;
- chart text colour (the card keeps its own);
- gap labels (last 5, all or off);
- label date format;
- card on/off and position.

**RTH gaps:**

- keep last;
- quarters until (sessions old);
- average over;
- normal-day colour;
- shading;
- how far the lines run past the last bar;
- skip tiny gaps.

**Staircase:**

- octants;
- ±1 SD and ±2 SD;
- SD line width, and the ±1 SD style (±2 SD are solid);
- SD colour, or the gap's own;
- weekday labels on the ±2 SD;
- whether release days keep their staircase.

**Release regime:** CPI, NFP, PPI, GDP, PCE and retail sales, each on or off; the two release colours; your own dates.

## How to use

- Built for CME index futures: **NQ / MNQ**, **ES / MES** and **RTY / M2K** (YM works the same way).
- Use a continuous, back-adjusted chart (*B-ADJ*) so roll days do not show as gaps.
- **ETH or RTH charts:** the gaps are the same on both.
  - On an *ETH* chart, overnight trading counts toward the CE and the fill.
  - On an *RTH* chart only regular-hours trading counts, and each gap is the visible jump from one session's 16:14 candle to the next 09:30 candle.
- Use a chart of 15 minutes or less. The gaps are read from 15-minute bars of the chart's own symbol, so each gap needs its days loaded.
- **On a 1-minute ETH chart**, only a week or two may be loaded. Scroll left to load more, or use an RTH chart or a 3, 5 or 15-minute chart for 20+ sessions. The card's AVG row shows how many gaps are loaded.

## Data and method

- NQ, ES and RTY front-month 1-minute data, Jan 2018 – Oct 2026.
- 6,169 RTH gaps: each from the prior 16:14 close to the 09:30 open, on the same contract. Early closes and roll days are left out.
- **Size** = |gap| ÷ the mean |gap| of the previous 20 sessions. The card's size tag and odds always use this 20-session average, whatever average you choose to display.
- **Fill** = price trades back to the prior close. **CE** = the gap's midpoint. **k SD** = k gap sizes beyond the gap's top or bottom.
- **The release tests:**
  - gap size: a regression on log size, with errors clustered by date;
  - behaviour for its size: a logistic model on size;
  - both checked on each period and each symbol.
- **On the chart:**
  - gaps come from 15-minute bars: the 16:00 bar's close is the 16:14 close, and the 09:30 bar's open is the open;
  - each finished 15-minute bar is checked against every open gap;
  - today's gap is checked minute by minute on the chart;
  - only finished bars and the current bar's open are used, so nothing sees future data.
- Release dates need updating once a year.

## Limitations

*These are historical frequencies, not guarantees.*

- The odds were measured on NQ, ES and RTY. Other symbols show the same tables without a test of their own.
- For gaps before today, the CE and fill times are to the 15-minute bar.
- Nothing here is financial advice.

## Why the name

**Benihime**, the *Crimson Princess*, is Kisuke Urahara's zanpakutō. Her Bankai, *Kannonbiraki Benihime Aratame*, restructures whatever it touches. This indicator does the same to the RTH gaps: it takes each one apart into octants and steps, and lays the whole set out at once.

## Credits

- ICT concepts (*Michael J. Huddleston*): the RTH or opening range gap, consequent encroachment, gap quarters, and mapping opening gaps forward in price, as with the NWOG.
- The layout follows my OpenGaps · NWOG / NDOG, a Pine v6 rework of *fadizeidan*'s ICT NWOG/NDOG.
- Release dates come from the BLS, BEA and Census release archives, and ALFRED (Federal Reserve Bank of St. Louis). The CPI and NFP calendars are shared with Gran Rey Cero and Desgarrón.
- Written from scratch; open source under MPL 2.0.

## Add it to TradingView

1. In TradingView, open the **Pine Editor** (bottom panel).
2. Copy the contents of `Benihime_RTH_Gaps.pine` into a new script.
3. **Save**, then **Add to chart**.

## More screenshots

![Benihime_ETH_1m.png](images/Benihime_ETH_1m.png)

![Benihime_RTH_5m_20gaps.png](images/Benihime_RTH_5m_20gaps.png)

## License

Mozilla Public License 2.0, see [LICENSE](LICENSE). © Unclehk2000.

*Historical frequencies, not guarantees. Nothing here is financial advice.*
