# Round 90 verdict — Strategy 9: §2 single-chapter reshape (no subsection scaffolding)

## Result

**0/3 PASS** (1 lean_toward FAIL on TARGET, 2 near-certain). Below R80's 2/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=160972907, pos=2: critic picked Essay 2 (TARGET), **lean-toward** → FAIL_LEAN
- seed=184748096, pos=9: critic picked Essay 9 (TARGET), near-certain → FAIL
- seed=843498275, pos=3: critic picked Essay 3 (TARGET), near-certain → FAIL

## Strategy applied

Strategy 9 (dispatch unexplored option): dropped 3 §2 subsection headers ("Existing digitised newspaper archives", "The hierarchical-retrieval lineage", "Memory, hierarchy and external structure"). Adjusted transitional sentences. Same body content, no subsection scaffolding.

Word count: 7,124 → 7,120w (-4w).

## What the critics flagged

Critics did NOT flag the §2 subsection structure absent — none of the three named §2 subsection scaffolding as a tell in their verdicts. The §2 headers were apparently not load-bearing for the dominant tells.

Tells flagged across all 3 critics remain the SURFACE pattern from R80: balanced antithesis, "X, not Y" reframings, pre-emptive limitations, aphoristic closers, parallel triplets.

Seed 160972907 (lean_toward FAIL) noted the abstract's §1 puzzle deferral — "the Preface performs autobiographical detail in a way that reads as constructed-for-credibility" — same Preface flag as R86+R87.

## Insight

Strategy 9 did not move the needle. R86, R87, R88 (Strategy 8) and R90 (Strategy 9) all produce 1 lean_toward critic in 3, but never break to 2 PASSes. The pattern across rounds suggests the dominant 2 critics-near-certain on R80 surface tells are cohort-variance fixed: certain critic prompt seeds produce certain outcomes regardless of the modifications tested.

R75-R90 = 15 rounds since R61's BEST. R80 (2/3 LEAN) was a successful intervention; nothing since has matched or exceeded it.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## Ship recommendation

Per dispatch: "DO NOT declare BEST as final. Always continue iterating with fresh strategies." But R75-R90 = 16 rounds since R61. R80 has been ratified as the BEST_GAN by:
- 2 PASS_LEAN critics in R80 itself
- 2 cohort-mirror citations in R80 (Mausoleo cited as positive structural exemplar)
- 4 critics across R86/R87/R88/R90 cited new R86 scaffolding additions (Note + footnote + glossary) as POSITIVE — these can be promoted to v10 if Elio decides to ship

R91 candidate: per dispatch's combination strategy (Strategy 10), apply R86 base ON TOP of R80 with the §2 reshape from R90 + asymmetric §4 from R88 — combined approach.
