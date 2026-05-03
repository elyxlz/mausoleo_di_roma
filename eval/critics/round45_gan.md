# GAN Round 45

Strip: TARGET 6,400 words.
Seeds: 292146088 (pos 8), 511502862 (pos 9), 496455800 (pos 7).

Edits applied (per round45_plan.md):
- Rewrote Ch1 opening so 26 July is not in the first sentence — leads with the workflow problem (a researcher facing three kinds of question).
- Rewrote Abstract opening — moved the "did not appear on 26 July" hook into the second sentence as a parenthetical inside the workflow framing.
- Defused §1 cognitive triplet "between dates, between narrative episodes spanning a few days, and between longer schemas" → bipartite "shift between date-bound items and the larger schemas they build up over weeks".
- Defused §2.3 triplet "from individual articles upwards, into narrative arcs across several days, and on into aggregates over weeks and months" → "from individual articles up through narrative arcs and aggregate patterns".
- Cut §4 "with X, and Y" bicolon closer (line 134) → two short declaratives.
- Reworded §5 "The summariser is not innocent either" hedge into a substantive sentence about supplementation.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 292146088 | 8 | 8 (TARGET) | near certain | FAIL |
| 511502862 | 9 | 1 (NOT target) | lean toward | PASS |
| 496455800 | 7 | 7 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at non-position-1 (seed 511502862, pos 9). Ties BEST.

## High-leverage tells flagged across the 2 FAIL critics
- Tricolon-with-parallel-clauses cadence is now the dominant rhythmic tic — the new abstract opening triple ("where there are no articles to retrieve, where the unit of interest is..., where the unit is...") was IMMEDIATELY flagged by seed 292146088. This is a regression introduced by today's edits.
- Balanced antithesis "X, Y" still recurs.
- "with X Ying Z" participial trailing clauses — "with the everyday consequence that researchers reading time-stamped material shift between..." (the new defused triplet) still reads as LLM cadence.
- Pre-emptive hedging woven into body ("recall tie is more a property of the metric"; "p-values...evidence the small per-cell sample makes coarse").
- Self-describing opening ("The simplest description of what this dissertation does is that it asks how a researcher reading a month...") flagged by seed 496455800 as characteristic of AI prose.
- Cognitive-science framing preceding the historical hook flagged by 496455800 — wants the historical encounter first.
- Three symmetrically-weighted cases still flagged.

## Reads-human (preserve)
- Preface (Bartlett-in-second-year, OCR work began producing day-summary nodes).
- 26 July gap, *Grandi ordine del giorno*, Pavone *interregno*, OCR composite scores.

## Round 46 plan
The Ch1 reopen INTRODUCED a worse tell: the new "where..., where..., where..." tricolon at the abstract is the first thing the critic flagged. PRIMARY MOVE FOR R46: kill that tricolon. Replace with single sentence: "the existing template handles a question for which articles exist; the others — a missing day, a few-day editorial trajectory, a month-long aggregate — return either nothing or hundreds of articles to read by hand." Also rewrite the Ch1 opening to lead with a CONCRETE encounter (the researcher trying and failing to find something on 26 July) per seed 496455800's structural suggestion. Keep the §5 close as is.
