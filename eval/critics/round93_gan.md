# Round 93 verdict — R86 additions + R92 deletions combination

## Result

**0/3 PASS, all near-certain.** Hard regression from individual components (R86 had 1 lean, R92 had 1 PASS_LEAN). Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=171113520, pos=7: critic picked Essay 7 (TARGET), near-certain → FAIL
- seed=214412989, pos=6: critic picked Essay 6 (TARGET), near-certain → FAIL
- seed=356578231, pos=4: critic picked Essay 4 (TARGET), near-certain → FAIL

## Strategy applied

R86 additions (Note + Grandi footnote + §3 chapter rename) + R92 deletions (drop §5 hedge paragraph + drop §1 closer).
Word count: 7,124 → 7,307w (+183w).

## What the critics flagged

R91 lesson re-confirmed at smaller scale: combining cohort-mirror ADDITIONS with PURE-DELETIONS on R80 base produces hard regression rather than additive softening. The mechanisms appear to interact unfavourably.

## Insight

R75-R93 = 19 rounds since R61's BEST. Combination effects are non-monotonic:
- R80 (R76 SICO + R72 cross-model + §1 + §5 + §2 + §2.1 + §4.2 combined) = 2/3 PASS_LEAN BEST
- R91 (R86 + R90 + R88) = 0/3
- R93 (R86 + R92) = 0/3

The combinations that work (R80) and the combinations that don't (R91, R93) cannot be predicted from individual round behaviour. R80's specific composition is a fragile local optimum.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## Total summary R75-R93

19 rounds. R80 still BEST at 2/3 LEAN. Strategies tested:

- AuthorMist (R70-R71): exhausted
- Cross-model Haiku (R72-R74): 1 PASS_LEAN ceiling
- SICO Haiku style anchors (R75, R76, R83): 0-1 PASS_LEAN
- 2-case structural collapse (R77): hard regression
- Combined SICO+cross-model+structural (R78-R79): 1 PASS_LEAN
- AGGRESSIVE STRUCTURAL §1 puzzle defusion + §5 rewrite (R80): 2/3 PASS_LEAN BEST
- Single-axis on R80 (R81-R83): regressed
- Strategy 7 Opus 4.7 distancing (R84-R85): exhausted (replacement same-class tells)
- Strategy 8 ADDITION-only scaffolding (R86, R87, R88): 1 PASS_LEAN ceiling
- Strategy 8 + deletions (R89): hard regression
- Strategy 9 §2 single-chapter reshape (R90): 1 lean FAIL
- Strategy 10 R86+R90+R88 combination (R91): hard regression
- 2-edit pure-deletion (R92): 1 PASS_LEAN
- R86+R92 combination (R93): hard regression
