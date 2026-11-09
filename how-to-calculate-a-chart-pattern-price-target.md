# How to calculate a chart pattern price target

How to calculate a chart pattern price target: measure a distance inside the pattern, then add it to the breakout level for an upside break or subtract it for a downside break. That is the whole method. The rest of this page covers which distance to measure for each pattern, a short script to check your arithmetic, and the reasons the result often won't match what price does.

Maintained by the ChartScout team. This is a reference note, not trading advice, and not ChartScout's source code.

## What the number is

The result is called a measured move. It is a convention that many traders use, not something derived from market mechanics. Price can stop short, overshoot, or reverse after the breakout. Treat the number as a reference level to compare against the chart.

## Which distance to measure

| Pattern | Distance | Project from |
|---|---|---|
| Bull or bear flag, pennant | Flagpole: start of the sharp move to its end | Flag breakout |
| Triangle | Height at the widest part, usually the start | Breakout level |
| Double bottom or top | Troughs (or peaks) to the neckline | Neckline break |
| Head and shoulders, and the inverse | Head to the neckline | Neckline break |

Two details that cause errors:

- If the neckline slopes, measure vertically from the head to the neckline.
- For flags, some traders use the height of the flag channel instead of the pole. The two give very different targets. Pick one before you look at the chart, and write it down.

## Worked examples

All prices are invented.

| Pattern | Measurement | Height | Breakout | Target |
|---|---|---|---|---|
| Bull flag | Pole from 20 to 30 | 10 | 28 | 38 |
| Ascending triangle | Flat top 100, first low 84 | 16 | 100 | 116 |
| Double bottom | Lows at 50, neckline 60 | 10 | 60 | 70 |
| Inverse head and shoulders | Head 80, neckline 92 | 12 | 92 | 104 |
| Head and shoulders top | Head 150, neckline 130 | 20 | 130 (down) | 110 |

## A short script

It only does the arithmetic. It does not fetch prices or connect to an exchange.

```python
def project(breakout, height, direction):
    return breakout + height if direction == "up" else breakout - height

def reward_to_risk(entry, stop, target):
    risk = abs(entry - stop)
    if risk == 0:
        raise ValueError("entry and stop are equal")
    return abs(target - entry) / risk

# name, breakout, height, direction, stop
cases = [
    ("bull flag",          28, 10, "up",   26),
    ("ascending triangle", 100, 16, "up",   94),
    ("double bottom",      60, 10, "up",   56),
    ("inverse H&S",        92, 12, "up",   88),
    ("H&S top",            130, 20, "down", 134),
]

for name, breakout, height, direction, stop in cases:
    target = project(breakout, height, direction)
    print(name, target, round(reward_to_risk(breakout, stop, target), 2))
```

Output with the invented numbers above:

```text
bull flag 38 5.0
ascending triangle 116 2.67
double bottom 70 2.5
inverse H&S 104 3.0
H&S top 110 5.0
```

A reward-to-risk of 5.0 looks attractive, but notice why: the bull flag stop is only 2 below the entry. A stop that close can be hit by ordinary noise. A big ratio built on a very tight stop is a warning sign, not a bonus.

## Checks after the arithmetic

1. **Obstacles.** List every prior swing high or low, support area, and round number between entry and target. If one sits close to your entry, the full projection is a stretch. Some traders plan a partial exit there.
2. **Overlapping projections.** If three methods land near the same price, check whether they all come from the same swing. If they do, you have one opinion repeated three times.
3. **The stop.** Decide where the idea is wrong before you decide where it ends. Compare the distance to the stop with the distance to the target. If the reward does not justify the risk, skip the trade; do not move the target.
4. **The breakout itself.** The projection starts from the break. If a candle has not closed beyond the level on your timeframe, there is nothing to project yet.

## Finding patterns to measure

ChartScout is a crypto chart pattern screener. Its Pattern Screener shows detected chart patterns in one view, so you can browse candidates and open the charts worth measuring. The measuring and the decision are yours. Check the detector list in your account before assuming any particular pattern is covered.

Pattern Screener does not send notifications. If you want notifications, you set up your own Pattern Watchers, and those watchers deliver them.

## Limits

Many breakouts stall, reverse, or fail. Crypto can gap or move sharply, and your fill may differ from your plan. Nothing here is a forecast or a recommendation to buy or sell.

This page is educational and promotional, written by the ChartScout team. It is not an independent review.
