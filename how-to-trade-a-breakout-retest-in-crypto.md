# How to trade a breakout retest in crypto

How to trade a breakout retest in crypto is a question about rules: what counts as a break, what counts as a hold, and what counts as a failure. This document writes those rules as a small specification so you can apply them the same way every time. It is educational material, not trading advice, and it is not ChartScout's source code.

Maintained by the ChartScout team.

## 1. Definitions

- **Level**: a support or resistance area you marked before the break.
- **Break**: a candle on your review timeframe closes clearly beyond the level.
- **Retest**: price returns to the broken level, treated as a zone rather than a single line.
- **Hold**: a candle rejects the zone and closes back in the breakout direction.
- **Failure**: a candle closes back through the level against the break.

Define each term before the setup appears. Rewriting the definitions after price moves is the most common way a rule set stops being a rule set.

## 2. State machine

A breakout retest moves through states in order:

| State | Condition | Allowed next states |
|---|---|---|
| IDLE | No marked level, or no break yet | BROKEN |
| BROKEN | A candle has closed beyond the level | RETESTING, RUNNING, FAILED |
| RETESTING | Price has returned to the level zone | HELD, FAILED |
| HELD | A rejection candle closed in the breakout direction | RUNNING, FAILED |
| RUNNING | Price has moved on in the breakout direction | none |
| FAILED | A candle closed back through the level | none |

Two states are easy to forget. A breakout can go straight from BROKEN to RUNNING with no retest at all, because the strongest breakouts often never come back. And a failed retest ends the idea; it is not a deeper entry.

## 3. Common rules

The following are rules traders commonly use. They are not guarantees.

- **Entry reference**: the close of the rejection candle at the retest zone.
- **Stop reference**: beyond the extreme of the retest, on the far side of the level.
- **Invalidation**: a candle closing back through the level against the break.
- **Target reference**: the height of the range added beyond the original break, or the next relevant swing.

Write your own values for these before looking at a live chart. Decide the risk you accept before an entry exists.

## 4. The trade-off

Waiting for a retest can give a tighter stop, because the stop sits close to the retest extreme instead of far below the level. The cost is that the retest may never arrive, and the move can run without you.

That is a genuine trade-off, not a flaw in the method. Decide in advance whether you accept missing some moves in exchange for a clearer invalidation.

## 5. Where discovery fits

ChartScout is a crypto chart pattern screener. Its Pattern Screener brings detected chart patterns into one view so you can browse candidates and open charts for closer review. A breakout from a pattern boundary can be the first stage of this specification.

Check the current detector list and your account access before expecting a particular pattern. The retest checks in this document are performed by you, not by the screener.

Pattern Screener does not send notifications. If you want notifications, you configure your own Pattern Watchers, and those watchers deliver them. Treat each notification as a prompt to reopen the chart and check which state it is in.

## 6. Review template

For each candidate, copy and fill in:

```text
Market and exchange:
Timeframe:
Level:
State (IDLE / BROKEN / RETESTING / HELD / RUNNING / FAILED):
Break candle close:
Retest zone:
Rejection candle:
Entry reference:
Stop reference:
Invalidation condition:
Next review time:
```

## 7. Limitations

A retest that holds can still fail later. Crypto trades continuously and can move sharply between your reviews, so levels and stops may not execute at the prices you planned.

This document is educational and promotional, not an independent review, a backtest, or personalised financial advice. Nothing in it guarantees a profitable outcome.
