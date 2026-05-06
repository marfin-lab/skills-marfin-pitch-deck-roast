# Pitch Deck Roast — Score Formula

The overall score (0-100) is a weighted average of the 10 criterion scores
(each 1-5).

## Weighting

Three criteria carry 1.5x weight because they are the strongest signals
for early-stage decks:

- **Problem** — if the problem is unclear, nothing downstream lands
- **Insight** — without a proprietary belief, the deck reads generic
- **Traction** — investors at pre-seed/seed weigh actual data over slides

Weight table:

| Criterion | Weight |
|---|---|
| Problem | 1.5 |
| Insight | 1.5 |
| Traction | 1.5 |
| Market | 1.0 |
| Solution | 1.0 |
| Model | 1.0 |
| GTM | 1.0 |
| Team | 1.0 |
| Roadmap | 1.0 |
| Ask | 1.0 |

Total weight: 11.5

## Formula

```
overall_score_raw = sum(score_i * weight_i) / sum(weight_i)
overall_score_100 = round((overall_score_raw / 5) * 100)
```

Example: a deck with all 4s on weighted criteria and 3s on the rest:

```
weighted_sum = (4 * 1.5 * 3) + (3 * 1.0 * 7) = 18 + 21 = 39
weighted_avg = 39 / 11.5 = 3.39
overall_100  = round((3.39 / 5) * 100) = 68
```

## Bands

| Score | Band | Action |
|---|---|---|
| 80-100 | Polished | Send to investors. Minor copy edits only. |
| 60-79  | Solid skeleton | 2-4 slide rewrites before sending. |
| 40-59  | Needs structural work | Rewrite slides 1-3, then re-roast. |
| 0-39   | Restart | Step back. Run customer-interview-5why first. |

## Stage-aware adjustments

Deck for **idea / pre-MVP** → Traction weight drops to 0.5x (early).
Deck for **Series A+** → Roadmap and Ask weights bump to 1.5x.
Deck for **demo day / partner intro** → all weights equal (1.0x).

The skill applies the right adjustment based on Step 1 of the workflow.

## Why not 1-10?

A 1-10 scale invites ambiguity (is 7 good or mid?). 1-5 forces clear
judgment per criterion. The 0-100 final score is just for shareability —
internally everything is 1-5.
