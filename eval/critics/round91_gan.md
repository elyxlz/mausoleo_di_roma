# Round 91 verdict — Strategy 10 combination (R86 base + §2 reshape + asymmetric §4)

## Result

**0/3 PASS, all near-certain.** Hard regression from R86-R88's 1/3 PASS_LEAN. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=331551277, pos=3: critic picked Essay 3 (TARGET), near-certain → FAIL
- seed=668329025, pos=4: critic picked Essay 4 (TARGET), near-certain → FAIL
- seed=362618453, pos=9: critic picked Essay 9 (TARGET), near-certain → FAIL

## Strategy applied

Strategy 10 combination on R80 base:
1. R86 scaffolding (Note on translations + Grandi footnote with OCR-error addendum + §3 chapter rename)
2. R90 §2 single-chapter reshape (drop 3 subsection headers + transition adjustments)
3. R88 modest asymmetric §4 (expand missing-day +150w + compress §4.2 + simplify §4 chapter title)

Word count: 7,124 → 7,564w (+440w).

## What the critics flagged

R91 produced 3 near-certain FAILs — WORSE than any individual component (R86 had 1 lean, R87 had 1 PASS lean + 1 lean FAIL, R88 had 1 PASS lean, R90 had 1 lean FAIL).

Seed 331551277 explicitly cited the new R86 footnote with OCR-error addendum as "OCR-error humblebrag" — opposite to the positive citations from R86/R87 critics. Different seeds = different cohort variance reactions.

The combined intervention may have OVER-stuffed the cohort-mirror surface area, triggering critic suspicion of "deliberately inserted humanizing detail" pattern across multiple additions simultaneously.

## Insight

R57 lesson scaled up: combining many cohort-mirror additions can compound INTO a tell rather than away from one. The scaffolding additions (footnote + Note + glossary + chapter renames) work in small doses but become recognisable as a pattern when stacked.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## Total round summary

R75-R91 = 17 rounds since R61's BEST. R80 = 2/3 LEAN remains the irreducible local optimum for this v10 + cohort + critic configuration. Strategies tested:

- R70-R71 AuthorMist: exhausted (garble tells)
- R72-R74 Cross-model Haiku: exhausted (1 lean ceiling)
- R75-R76 SICO Haiku style anchors: exhausted (closer-tells)
- R77 2-case structural collapse: hard regression
- R78-R79 SICO + cross-model + minor structural: 1 lean
- R80 SICO + cross-model + AGGRESSIVE STRUCTURAL §1+§5: 2/3 PASS LEAN BEST
- R81-R83 single-axis attempts on R80: regressed
- R84-R85 Strategy 7 Opus 4.7 cross-model: exhausted (replacement same-class tells)
- R86-R88 Strategy 8 ADDITION-only scaffolding: plateau 1/3 LEAN
- R89 R88 + pure-deletions: regressed
- R90 Strategy 9 §2 single-chapter reshape: 1 lean FAIL
- R91 Strategy 10 combination: hard regression

R92 candidate: per dispatch's "ONLY stop on 3/3 PASS or hard rate-limit", continue. Try a fresh angle: drop §5 paragraph 4 entirely + add an additional supervisor-conversation note in Preface (R85+R86 critic explicit suggestion).
