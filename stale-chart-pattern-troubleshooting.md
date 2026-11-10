# How to identify stale crypto chart patterns: troubleshooting

How to identify stale crypto chart patterns is mostly a debugging problem. You have an alert or a drawing, and something feels off. This page lists symptoms, likely causes and fixes.

**Working definition (not an industry standard):** a pattern is stale when the conditions that made it worth watching no longer hold.

## Symptom, cause, fix

| Symptom | Likely cause | What to do |
|---|---|---|
| Price is far from the drawn lines | The move already happened | Check if the breakout level was passed; treat as a new chart |
| Candle closed back through the pattern low | The invalidation level was hit | Mark it invalid. A head and shoulders fails when price rises back above the right shoulder after the break.  |
| Triangle lines almost touch | Pattern is near its apex | Lines lose meaning near the apex. Lower its priority. |
| Lines were redrawn several times | Structure was never solid | Patterns usually show two or three boundary tests. |
| Breakout stalled right away | Weak follow-through | Re-rank it. |
| Bigger trend has flipped | Context changed | Re-read the higher timeframe |

## Example (invented numbers): head and shoulders

Neckline 130, right shoulder 138. Price breaks below 130, then rallies to 139.

Price is back above the right shoulder, so the pattern is invalidated. Whatever the alert said, the setup is stale.

## Common mistakes

- Judging staleness by how long ago the alert arrived instead of where price is now
- Using a wick as evidence
- Moving the invalidation level after price approaches it
- Keeping a drawing because deleting it feels like a loss

## Review template

```text
Pattern:
Timeframe:
Invalidation level:
Has a close passed it? yes / no
Age vs expected life: fresh / aging / late
Follow-through: yes / stalled
Higher timeframe still supports it? yes / no
Verdict: fresh / aging / stale
```

## Where a scanner fits

A crypto chart pattern scanner finds candidates. [ChartScout](https://chartscout.io/chart-pattern-screener) flags patterns at roughly 75–80% maturity, so run the template on arrival. The Pattern Screener lists detections, and Pattern Watchers send configured alerts.

## FAQ

**Is an unconfirmed pattern stale?** Not necessarily. An unconfirmed pattern simply never closed beyond its level.

**Should I delete stale patterns?** Archive them in your notes so you can review them later.

*Educational content from the ChartScout team. Not financial advice.*
