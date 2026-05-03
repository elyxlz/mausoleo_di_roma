# GAN Round 65

Strip: TARGET 5,824 words. v10 = 6,720 words.
Seeds: 182886936 (pos 7), 361564389 (pos 3), 76069949 (pos 9).

Edits applied (per round65_plan.md, BEFORE the revert):
- DELETED Abstract para 1 sentence "For the July 1943 *Il Messaggero* corpus this dissertation works with, that template handles questions for which articles exist and is awkward for the others the corpus invites." (the universal R61–R64 "X handles Y and is awkward for Z" antithesis tell).
- Pure deletion only (no replacement). The next sentences in para 1 already concretise the asymmetry the deleted sentence pre-summarised.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 182886936 | 7 | 7 (TARGET) | near certain | FAIL |
| 361564389 | 3 | 3 (TARGET) | near certain | FAIL |
| 76069949  | 9 | 9 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near certain. REGRESSED HARD from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Why the pure-deletion didn't move

The single-sentence deletion of the universal "X handles Y and is awkward for Z" tell did not flip any seed. All three FAIL critics cited the SAME repeating set of tells, none of which depended on the deleted sentence:

1. Balanced-antithesis-with-semicolon construction surviving in para 1 sentence 4 ("Questions about the regime-change days of 25 to 27 July return tens of articles that the reader has to assemble; questions about the war-and-domestic balance across the month return hundreds.") and across §1, §2, §4.
2. Aphoristic single-sentence closers ("The 26 July does not appear in the digitised fund because there was no 26 July to digitise.", "the gap is already inside the index", "the answer is grounded in the index, in the baseline's it leans on...").
3. Self-referential meta-commentary ("the substantive cognitive-science claim the dissertation rests on").
4. Parallel-triplet scaffolding ("paragraph in article in issue in day in week in month", "Three systems define the field", "Three loosely coupled stages of Mausoleo connect…").
5. Numeric-pile cadence ("11.3 vs 28.3", "0.76 vs 0.62", "κ = 0.57").
6. Asymmetric chapter-4 case weighting (one deep + "Two shorter cases" paragraph) — flagged as STRUCTURAL by all three seeds (R61's PASS critics had read this same shape as positive cohort exemplar; cohort variance dominates).

The deleted sentence was redundant prose but its removal alone is below the cohort-variance noise floor.

## Confirmed-clean R66 candidate

Critics 182886936 and 76069949 BOTH cite **the §1 paragraph closer "A flat keyword search holds none."** as a high-leverage aphoristic-closer tell. R55 plan listed it as a SECONDARY target (fold into the preceding sentence) but R55 didn't apply it. R66 will execute that fold in isolation, on top of R61 baseline, as a pure pre-existing-target deletion.

The fold:
> "When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them. A flat keyword search holds none."
becomes
> "When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search holds none."

This is a within-sentence fold rather than a deletion, removing the aphoristic-closer cadence without removing content. R55 plan flagged it as the cleanest available aphoristic-closer fix.

## Cohort-variance noise floor still binding

R61 PASS critics keyed on cohort positions (Essay 9 / Essay 5 PASS picks) and praised Mausoleo's asymmetric-case-weighting + technical-detail texture. R65 critics keyed on the same surface tells but cohort positions did not produce same praise.

The lesson from R61–R65: at this v10, single-edit moves cannot shift all three seeds. Either:
(a) edits must address several universal tells in a single round (combined-deletion package, R60 model), OR
(b) accept R61 as the operational ship draft.

Given Wed May 6 17:00 BST deadline and Tue May 5 16:30 BST flight, R66 will attempt one more single-edit (the §1 closer fold confirmed clean by both R65 critics) before the combined-deletion gambit.
