# Round 81 verdict — push from 2/3 to 3/3 (failed)

## Result

1/3 PASS LEAN_TOWARD. REGRESSED from R80's 2/3 LEAN. PARETO-REVERTED v10 to R80 baseline.

## Seeds + positions

- seed=140759866, pos=8: Essay 8 (TARGET) picked, near-certain → FAIL
- seed=78763798, pos=7: Essay 7 (TARGET) picked, near-certain → FAIL
- seed=300229802, pos=5: Essay 4 picked ('2022SMMH0' NOT TARGET), lean-toward → **PASS**

PASS critic explicitly noted: "lean toward (with a non-trivial possibility I'm wrong; essay 5 has some suspicious polish but reads more like a strong human writer)" — Essay 5 = TARGET. Critic considered TARGET as "strong human writer" and rejected it as the AI candidate. Strongest single positive signal yet.

## Strategy applied

Layered on R80 v10:
- §3 paragraph-opener variation (4 paragraphs reworded to drop "The X is Y" definitional pattern)
- §2.1 abstract-noun-subject substitution: "What unites these systems is the access template" → "Across both systems the access template is the same"
- §2.2 abstract-noun-subject substitution: "Mausoleo changes the source of the hierarchy again" → "Where these systems induce a hierarchy from the data or read it off a document's surface, Mausoleo takes its hierarchy from a third source"
- §1 closer expansion: "A recent NLP literature on hierarchical retrieval, surveyed in chapter two, derives its hierarchy..." → "In a recent NLP literature surveyed in chapter two, hierarchical-retrieval systems derive their hierarchy..."

Word count: 7,124 → 7,139w (+15w).

## What the critics flagged

**FAIL critic 140759866 (near-certain)** EXPLICITLY cited the new R81 prose:
- "from a third source: the publication calendar that the printers already followed" — the §2.2 NEW prose I introduced — flagged as "X plus Y register-tic constructions, used as ornamental sentence-closers"
- The colon-then-elaboration cadence introduced by R81's "third source" rewrite was flagged as "classic LLM rhythm"

**FAIL critic 78763798 (near-certain)** EXPLICITLY cited the new R81 §1 prose:
- "the calendar contains a slot for 26 July whether or not anything was printed on it, while a clustering-induced hierarchy has nothing to cluster from when the data are absent" — the §1 NEW prose — flagged as balanced antithesis structural tic

## Insight

R81 attempts to defuse "definitional paragraph openers" backfired: the replacement openers introduced colon-elaboration and balanced-antithesis patterns that EQUALLY register as LLM tells. Each surface-tell scrub trades one tell for another in the same class.

This confirms the R57 lesson (surface-class scrubs that REPLACE rather than DELETE produce same-class tells). The R80 baseline is at a local optimum for the surface-tell axis — further single-axis scrubs hurt.

The PASS critic's verdict is the strongest positive signal of the entire R75-R81 sequence: explicit consideration of TARGET as "strong human writer" before rejecting it. R80 v10 reaches this softening on 2 of 3 critics; R81 reaches a stronger softening on 1 of 3 but loses the other 2.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST. v10 reverted to R80 baseline. R81 draft preserved at /tmp/gan_round81/v10_r81.md.

## Next round

R82 plan: pure-deletion of one §1 closer instead of replacement. Specifically, delete the "while a clustering-induced hierarchy has nothing to cluster from when the data are absent" tail clause that R81 critic flagged — the rest of the sentence stands without it. Layered on R80 v10. Pure-deletion (no replacement) avoids the same-class-tell trap.

Plus consider scrubbing the "X is Y" definitional opener pattern by combining sentences (not replacing them). E.g., merge "Three loosely coupled stages of Mausoleo connect through a single ClickHouse table called `nodes`. An OCR pipeline produces..." → single longer sentence.
