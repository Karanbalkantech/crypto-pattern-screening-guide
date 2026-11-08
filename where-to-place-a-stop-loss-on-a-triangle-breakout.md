# Where to place a stop loss on a triangle breakout

Where to place a stop loss on a triangle breakout comes down to one principle and a few options. The principle is that the stop sits on the opposite side of the triangle from the breakout, at a level where the breakout is shown to have failed. This page lists the common options, a sizing formula, and a short helper for the arithmetic. It is educational material, not trading advice, and it is not ChartScout's source code.

Maintained by the ChartScout team.

## 1. The principle

A breakout is a claim that the triangle has resolved. A stop belongs where that claim is clearly wrong, not where a loss would feel acceptable.

## 2. Common placements (long breakout)

| Option | Level | Trade-off |
|---|---|---|
| A | Just inside the broken line | Smallest risk per unit, but more exposed to normal noise |
| B | Below the last swing low inside the triangle | Respects the pattern's structure; larger distance |
| C | Below the opposite trendline | Invalidates the whole triangle; largest distance and smallest position |
| D | Structural level plus a volatility buffer | Reduces the chance of brief spikes ending the trade; the multiple is something you test yourself |

For a downside breakout, mirror every row: use the broken line from below, the last swing high, or the upper trendline.

## 3. Sizing from the stop

```text
risk per unit  = entry - stop
position size  = amount you accept losing / risk per unit
```

Choose the stop first. If the resulting position is too small to be worthwhile, skip the trade. Do not move the stop closer to enlarge the position.

## 4. A small helper

This snippet only does arithmetic. It does not connect to any exchange or fetch prices.

```python
def position_size(entry: float, stop: float, risk_amount: float) -> float:
    per_unit = abs(entry - stop)
    if per_unit == 0:
        raise ValueError("entry and stop cannot be equal")
    return risk_amount / per_unit

# Hypothetical example: entry 103, stops at 99 / 94 / 91, accept losing 100
for stop in (99, 94, 91):
    print(stop, round(position_size(103, stop, 100), 2))
```

Running it with those invented numbers gives 25.0, 11.11 and 8.33 units.

## 5. What failure looks like

Price returns inside the triangle and then breaks the opposite trendline. Treat that as the end of the idea instead of hoping for a rebound.

## 6. The retest trade-off

Entering on a retest of the broken line can allow a tighter stop. But strong breakouts do not always retest, so waiting can mean missing the trade. Decide in advance which cost you prefer.

## 7. Where discovery fits

ChartScout is a crypto chart pattern screener. Its Pattern Screener brings detected chart patterns into one view so you can browse triangles and other formations and open the charts worth studying. Check the current detector list and your account access before assuming a given pattern is covered.

Pattern Screener does not send notifications. If you want notifications, you configure your own Pattern Watchers, and those watchers deliver them. Neither tool chooses a stop for you.

## 8. Limits

A stop-loss does not guarantee an exit price. Crypto can gap or move sharply, and fills can be worse than planned. Example prices are invented.

This page is educational and promotional, not an independent review or personalised financial advice.
