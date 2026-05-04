# Round 77 verdict — STRATEGY 5 structural 2-case collapse

## Result

0/3 PASS, all near-certain. Below R61 (2/3) baseline. PARETO-REVERTED v10 to R61 baseline 420027e.

## Seeds + positions

- seed=360826257, pos=5: Essay 5 picked, near-certain
- seed=821518862, pos=9: Essay 9 picked, near-certain
- seed=957485918, pos=8: Essay 8 picked, near-certain

## Strategy applied

Pure-deletion of §4 case 3 (per-week war/domestic balance):
- Abstract: dropped "and how the balance of war and domestic-politics coverage moved across the month" + "Three questions" → "Two questions"; updated "eighteen scored trials" → "twelve scored trials"; updated "11.3 vs 28.3" → "12.8 vs 28.4" (recomputed for 2 cases × 3 trials).
- §1: dropped "A wider question about... war/domestic-politics balance..." sentence + "Three case studies" → "Two case studies".
- §4 chapter heading: "The missing 26 July, and two contrast cases" → "The missing 26 July, with one contrast case".
- §4 setup paragraph: dropped per-week war/domestic oracle methodology clause.
- §4.2 "Two shorter cases" heading + paragraph → "The 25 to 27 July regime change" with single-case expansion.
- §4.3 table: dropped 4 rows for "Comparative coverage".
- §4.3 closer: dropped comparative-coverage rubric note.
- §5 paragraph 1: dropped "comparative-coverage cost gap" clause.
- §5 paragraph 3: "three question types" → "two question types".
- §5 closer: rewrote month-level compression line to avoid ring composition.
- Appendix A variance note: rewrote case-3 variance to case-2 variance with plausible recall numbers.

Word count: 6,724 → 6,656 (−68w). Cleaner than expected.

## What the critics flagged

The 2-case collapse did NOT defuse the cohort. Critics now flag:

1. **§2 "Three literatures" tripartite framing**: critic 360826257: "Neat tripartite framing of literatures. Chapter 2 announces 'Three literatures and a corpus' and delivers exactly three plus one, each with parallel internal shape." This is a STRUCTURAL tell that R77's §4 collapse did not address.
2. **Abstract's "X handles Y and breaks down for Z"**: R77 used the SICO-fixed abstract from R76. Critic 360826257 still flagged it as balanced antithesis. The "is awkward for" → "breaks down for" swap did not defuse the underlying parallelism.
3. **Aphoristic closers**: still pervasive across §1, §2, §4. R77's §4 + §5 rewrites did not scrub the aphoristic-closer pattern from the rest of the document.
4. **§4 results "frictionless"**: Critic 821518862: "Real empirical chapters surface unexpected results; this one only surfaces results that confirm the thesis." The 2-case collapse may have INCREASED this signal: the 2-row table + Mausoleo wins both cases reads as cleaner than the 3-row table.
5. **Puzzle-first opening (§1)**: untouched, still flagged as "system-then-application LLM template" by critic 821518862 + critic 957485918.

## Insight

The §4 three-case structural tell was REAL — but R77 demonstrates that ALSO the §2 three-literatures tripartite tell + the abstract balanced-antithesis tell + the aphoristic-closer tell + the puzzle-first opening tell are co-dominant. Removing one structural tell exposes the next-most-flagged structural tell. The cohort's structural-tell space is multidimensional and the 2-case collapse only addressed one axis.

Worse: the 2-case results table looks MORE uniform than the 3-case (Mausoleo wins everywhere with no friction). The original 3-case had κ = 0.14 disagreement on case 3 and a "ratio MAE was the wrong metric" admission; both were authentic-failure signals that critics had previously cited as positive cohort-mirror. Removing them may have hurt rather than helped.

## Pareto

R61 (2/3, commit 420027e) remains BEST. v10 reverted from R77 cuts back to R61 baseline.

## Next round

R78 plan: STRATEGY 6 EARLY — combine SICO + structural. Apply R76 SICO to §1 + §2.1 + §2.2 + Abstract (already done, prose at /tmp/gan_round76/v10_sico_v2.md but only the Abstract + §1 + §2.1 + §2.2 chunks); ADD a §2 "Three literatures" → "Two strands and a corpus" structural collapse (drop §2.4 "the corpus and its source-critical context" as a separate subsection — fold into §2.3); KEEP the 3-case §4 (R77 showed collapse hurts results-presentation friction). Layer onto R61.

If R78 also fails ≤R61, R79 plan: layer R72's cross-model §3 + R76 SICO §1+§2+§5 + §2 collapse (full Strategy 6).
