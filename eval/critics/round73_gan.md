# GAN Round 73 — STRATEGY 3 EXTENDED (cross-model rewrite, wider scope)

Strip: TARGET 5,848 words (cross-model v10 6,721 words).
v10 = R61 baseline (commit 420027e). Cross-model file = `/tmp/gan_round73/v10_cross_model.md`.
Seeds: 2457833 (pos 7), 960181748 (pos 5), 292164039 (pos 6).

## Edits applied (BEFORE the revert)

Cross-model rewrite via Claude Haiku 4.5 on EXTENDED scope:
- §1 Chapter 1 (full chapter, 720w)
- §2.1 Existing digitised newspaper archives (253w)
- §2.2 The hierarchical-retrieval lineage (511w)
- §3 Chapter 3: How Mausoleo is built (1,321w)
- §5 Chapter 5: Discussion (full chapter incl para 4 closer, 375w)

All 5 sections passed sanity check on first attempt (citations + numerics +
keywords preserved, word count ±15%, no em-dashes, no " - ").

Total cross-model rewrite: ~3,180 words / 6,721 = 47% of dissertation body.

Preserved verbatim: Abstract, Preface, §2.3 spine, §2.4 corpus, §4 case studies
+ table + Italian quotation block, References, Appendix.

## Verdicts

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 2457833   | 7 | 7 (TARGET) | near certain | FAIL |
| 960181748 | 5 | 5 (TARGET) | near certain | FAIL |
| 292164039 | 6 | 6 (TARGET) | near certain | FAIL |

Result: **0/3 PASS, all near certain**. Hard regression from R72's lean-toward
softening; no progress on R61's 2/3 BEST.

PER PARETO RULE: v10 stays at R61 baseline (commit 420027e). No commit to v10.

## Why R73 didn't break 2/3

The R73 critics keyed primarily on tells in §4 (which was preserved):
- "Polished, machine-smooth performance throughout" — global stylistic uniformity
- §4 three-case symmetric experimental design (STRUCTURAL)
- §4.1 Italian quotation block "too-perfect framing"
- §4 numerical results "implausibly clean" (κ values, recall ties, etc.)

Cross-model rewrite of §1 + §2.1 + §2.2 + §3 + §5 was high-quality but did not
address §4 — the chapter the critics most consistently flag. Critics also noted
the global "machine-smooth" texture: even rewrites by Haiku 4.5 produce LLM-fluent
prose distinguishable from the cohort's "human messiness".

## R73 critic insight (recurring across rounds)

Multiple critics across R72/R73 explicitly cite the OCR engineering anecdotes
(0.872/0.926 composite scores, "0.6 to 1.1 composite points" failure cost,
2-attempt post-correction dead end) as the strongest cohort-mirror PASS-cited
content. This content survives in R61 baseline but is NOT enough to override
the §4 STRUCTURAL tells.

## Strategy assessment after R70-R73

| Strategy | Round | Result | Insight |
|----------|-------|--------|---------|
| AuthorMist narrow | R70 | 1/3 lean | distribution shift insufficient |
| AuthorMist wide | R71 | 0/3 cert | garble actively detected |
| Cross-model narrow | R72 | 0/3 lean | one seed softened, scope too narrow |
| Cross-model wide | R73 | 0/3 cert | global polish + §4 still flagged |

R61 (2/3 PASS) remains BEST_GAN. Per the documented decision tree in R73 plan:
"If R73 lands 0/3: SHIP R61 as final." But per Elio's standing rules, we
continue.

## R74 plan

Last attempt: extend cross-model rewrite to §4 (case studies + table caption
prose) while preserving all numerical results. The §4 STRUCTURAL three-case
symmetry is the most consistently flagged tell across R61–R73; rewriting the
prose around the table (the case-by-case narrative) may shift it.

Also consider: rewriting the Abstract (a single paragraph, easy retry) since
the abstract opening "X handles Y and is awkward for Z" pattern was flagged
universally R20–R69.

Risk: rewriting §4 risks losing the OCR-engineering-frustration cohort-mirror
PASS-cited content. Mitigation: explicit instruction to preserve all numerics
verbatim and the Italian quotation block as-is.
