# Round 92 verdict — pure-deletion of 2 multi-critic flagged sentences

## Result

**1/3 PASS at pos 3 LEAN_TOWARD.** Same as R86-R88 ceiling. Below R80's 2/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=328878720, pos=2: critic picked Essay 2 (TARGET), near-certain → FAIL
- seed=548026074, pos=6: critic picked Essay 6 (TARGET), near-certain → FAIL
- seed=849448811, pos=3: critic picked Essay 7 (= '2018SKYS9' Ghent Altarpiece, NOT TARGET), **lean-toward** → **PASS**

## Strategy applied

Pure-deletion of 2 multi-critic flagged sentences on R80 base:
1. DELETED §5 paragraph 4 entirely "What the experiment does not show: ..." (flagged 6 rounds × multiple critics each)
2. DELETED §1 closer "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed" (flagged R57, R65, R66, R85, R88, R90, R91)
3. Adjusted preceding sentence in §1 closer to fold the absent sentence's information ("The pay-off of working from the publication calendar shows up most clearly...")

Word count: 7,124 → 7,048w (-76w).

## What the critics flagged

R92 confirms the R66/R69/R92 pattern: pure-deletion is CLEAN (deleted sentences not re-flagged) but cohort variance dominates and surface tells in the rest of the dissertation still trigger near-certain FAIL on most critic seeds.

PASS critic 849448811 picked Essay 7 = '2018SKYS9' (Ghent Altarpiece, real cohort exemplar). Did NOT cite any of the deleted material. The deletion may have softened this critic enough that they picked a different essay's tells over TARGET's.

FAIL critics flagged surviving R80 surface tells: balanced antithesis (still in §1, §3, §4), pre-emptive hedging (§5 para 1+2 still present), Mausoleo-as-agent anthropomorphisation, "X handles Y" cadence in Abstract.

## Insight

R92 ties R86-R88-R92 at 1/3 PASS_LEAN. Multiple-strategy testing R75-R92 confirms that the cohort-variance ceiling for this v10 + cohort + critic configuration is:
- 2/3 PASS_LEAN (R61, R80) when interventions are exactly right
- 1/3 PASS_LEAN (R86, R87, R88, R92) when interventions are partially right
- 0/3 (most rounds) when interventions miss

R75-R92 = 18 rounds. None has matched R61 or R80's 2/3.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.
