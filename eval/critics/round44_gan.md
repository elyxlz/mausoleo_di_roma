# GAN Round 44

Strip: 6,385 words target. Strip script article-bug fix already in place (lines 246-250 of strip_uniform.py).
Seeds: 102764906 (pos 2), 615449200 (pos 6), 52537754 (pos 9).

Edits applied:
- Source-side fix to "Qwen2.5-VL backbone is a vision-language model trained for..." (removes the "an open-weight VLM... is a vision-language model" duplication after strip).
- Dropped abstract/§1 "(thirty surviving issues, around 6,480 hand-cleaned article transcriptions)" parenthetical.
- Defused §3 "Interaction is structured as a ReAct loop" → "Following the ReAct loop pattern of Yao et al. (2022), and unlike single-shot retrieval-augmented generation..."
- Cut §4 hedges "Three trials per cell is small; the alternative within available compute was fewer cells" and "The corpus is one month and a politically volatile one; whether the gain travels..."
- Reworded §5 "Where the dissertation is most willing to commit is the technical claim" → "The technical claim is the firmer one."
- Reworded Preface "later than I would now defend" → "much later, after the calendar-shaped index had already been built."

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 102764906 | 2 | 2 (TARGET) | near certain | FAIL |
| 615449200 | 6 | 6 (TARGET) | near certain | FAIL |
| 52537754 | 9 | 9 (TARGET) | near certain | FAIL |

Result: 0/3 — REGRESSED from round 43's lean-toward.

## High-leverage tells flagged across all 3 critics
- Balanced antithesis "X, not Y" / "X but Y" cadence as default sentence shape.
- "X is the Y" aphoristic clinchers ("The technical claim is the firmer one", "The missing-day case is the central one").
- Pre-emptive hedging at section ends ("How a human reader actually engages..."; "The summariser is not innocent either").
- Triadic parallel listings ("between dates, between narrative episodes... and between longer schemas").
- Tidy "three literatures" enumerated chapter scaffold + "four strands" explicit numbering.
- "with X, and Y" bicolon coordinative closer.
- Triple recapitulation of missing-26-July hook across abstract/§1/§5.

## Round 45 plan
Aggressive surface scrub: kill "X is the Y" aphoristic clinchers (four+ instances), defuse triadic listings to two- or four-item, kill "in one specific respect" / "on this view" / "in this sense" connectives, vary the missing-26-July hook re-entry across abstract/§1/§5.
