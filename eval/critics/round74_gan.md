# GAN Round 74 — STRATEGY 3 MAXIMUM (cross-model 80% body coverage)

Strip: TARGET 5,887 words (cross-model v10 6,759 words).
v10 = R61 baseline (commit 420027e). Cross-model file = `/tmp/gan_round74/v10_cross_model.md`.
Seeds: 651537520 (pos 4), 706340726 (pos 5), 687577398 (pos 3).

## Edits applied (BEFORE the revert)

Cross-model rewrite via Claude Haiku 4.5 on MAXIMUM scope (~80% of dissertation body):
- Abstract (338w)
- §1 Chapter 1 (720w)
- §2.1 Existing digitised newspaper archives (253w)
- §2.2 The hierarchical-retrieval lineage (511w)
- §3 Chapter 3: How Mausoleo is built (1,321w)
- §4 Chapter 4: case studies + table + Italian quotation block (1,502w)
- §5 Chapter 5: Discussion full chapter incl closer (375w)

Preserved verbatim: Preface, §2.3 cognitive-science spine, §2.4 corpus, References, Appendix.

All 7 sections passed sanity check on FIRST attempt. All citations + numerics
+ keywords preserved. No em-dashes or " - " separators introduced.

## Verdicts

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 651537520 | 4 | 4 (TARGET) | near certain | FAIL |
| 706340726 | 5 | 5 (TARGET) | near certain | FAIL |
| 687577398 | 3 | 9 (= 2022SMMH0) | lean toward | PASS |

Result: **1/3 PASS at pos 3 lean**. Ties R70's 1/3 result.

PER PARETO RULE: v10 stays at R61 baseline (commit 420027e). No commit to v10.

## Why R74 still didn't break 2/3

The PASS verdict (seed 687577398, pos 3) explicitly noted Mausoleo as
"second candidate ... but its specificity and voice tilt human" — the
maximum-scope cross-model rewrite did soften 1 seed enough to flip.

The 2 FAIL verdicts (pos 4 and pos 5) keyed on:
- "Polished system output: too clean, too symmetrical, too fond of certain
  rhetorical maneuvers" (global texture across all sections, including the
  rewritten ones)
- §4 case-study cadence even after cross-model rewrite (Haiku 4.5 preserves
  the structural symmetry of three cases + table)

Cross-model rewrite shifts surface tells but cannot defuse the STRUCTURAL
three-case symmetric design or the global "polished" texture that all of
Haiku 4.5's prose carries.

## Strategy assessment after R70-R74

| Strategy | Round | Result |
|----------|-------|--------|
| AuthorMist narrow | R70 | 1/3 lean |
| AuthorMist wide | R71 | 0/3 cert (garble flagged) |
| Cross-model narrow (§3+§5) | R72 | 0/3 lean |
| Cross-model wide (§1+§2+§3+§5, 47%) | R73 | 0/3 cert |
| Cross-model maximum (Abstract+§1+§2+§3+§4+§5, 80%) | R74 | 1/3 lean |

R61 (2/3 PASS) remains the irreducible BEST_GAN local maximum.

R75 plan: NO further escalation in playbook. Per R74 plan: SHIP R61 if R74
lands 1/3 with no clear improving trajectory. R74 ≤ R70 ≤ R61. The cohort
variance noise floor + the structural three-case symmetric design are the
binding constraints.

R61 v10 (commit 420027e) is the FINAL DISSERTATION.
