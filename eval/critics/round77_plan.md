# Round 77 plan — STRATEGY 5 structural 2-case collapse

## Strategy

Drop §4 case 3 (per-week war/domestic balance) entirely. The §4 three-case symmetric design is the structural tell flagged by EVERY critic across R72-R76. Pure-deletion of case 3 + its row in the §4 table + its references in §5 + Appendix A converts the structure from 1-deep + 2-collapsed-contrasts to 1-deep + 1-contrast. Asymmetric in a different direction — and structurally impossible for the critic to flag as "three-case symmetric template".

## Target deletions (relative to R61 v10 baseline)

R61 = commit 420027e = current v10 (no change since R61). Working file: /tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v10.md.

Case 3 references to remove or rewrite:

1. **Abstract (line 11)**: "and how the balance of war and domestic-politics coverage moved across the month" — DROP that clause from the three-question list. Replace with "and how the deposition's editorial register registered across days" (collapse with case 2's frame, not a new case).
2. **§1 Chapter 1 (line 27)**: "A wider question about how the war/domestic-politics balance moved across the month leaves the user with several hundred articles to classify and aggregate from scratch." — DROP this sentence; it introduces case 3.
3. **§4 Chapter 4 heading (line 112)**: "The missing 26 July, and two contrast cases" → "The missing 26 July, with one contrast case". Update the chapter title to flag the asymmetric design.
4. **§4 case-3 mention in §4.1 setup paragraph (line 114)**: "and ratio mean absolute error and root-mean-square error against a per-week war/domestic oracle on the third for completeness" — DROP this clause. Methodology no longer applies a third metric.
5. **§4.2 "Two shorter cases" (lines 134-136)**: rewrite as "One contrast case" (singular). Drop the second sentence of §4.2 about case 3 ("The per-week war-versus-domestic-balance question..."). Keep ONLY the regime-change sentence.
6. **§4.3 Aggregate numbers table (lines 142-153)**: drop the four rows for "Comparative coverage" (Tool calls / Ratio MAE / Ratio RMSE / Quality). Keep the 6 rows for "26 July absent" and "25 July regime change".
7. **§4.3 closing paragraph (line 155)**: drop the sentence "The comparative-coverage case showed the largest quality gap and the lowest κ, the latter reflecting how poorly the narrative-completeness rubric fitted an aggregate-shape answer." Replace with a 2-case wrap-up.
8. **§5 Discussion (lines 161-167)**:
   - line 161: "the size of the cost gap is largest on the comparative-coverage case (the day-summary nodes give the agent the granularity an aggregate question needs and the baseline has to reconstruct it article by article)" → DROP this clause; recast around the regime-change case as the largest cost-gap case.
   - line 165: keep — Murialdi reference is independent of case 3.
   - line 167: keep "At month level the summariser had compressed..." — independent of case 3.
9. **Appendix A (line 241)**: "On the missing-26-July case, the second of the three Mausoleo trials returned a war/domestic ratio inverted relative to the other two trials at week boundary W29." — REWRITE: this attributes a per-cell variance note to case 3, which no longer exists. Rewrite the Appendix A variance note to reference the regime-change case instead. (Or DROP — but it's a useful authentic-detail signal.)

Rough word-count impact: −350 to −450w net (case 3 prose + table rows + Appendix references). v10 6,724w → ~6,300w. Well within 9,950w cap.

## Rationale: case 3 vs case 2 keeper

Per dispatch: case 1 (missing 26 July) always positive in PASS verdicts (signature). Case 2 (regime change) has a richer historical narrative — Pavone, MinCulPop, Bartlett-style narrative reconstruction — and is more naturally in the "calendar-shaped index" sweet spot. Case 3 (war/domestic balance) is more aggregate-statistical, which is precisely the case-type the §5 critic 152897786 flagged ("Inputs are X. Outputs are Y." parallel cadence + clean numerical symmetry).

Critics' positive cohort-mirror citations of TARGET have always been on case 1 prose, never on case 3.

## Pareto rule

R77 layered on R61 v10 (clean). If R77 < R61 (2/3), revert v10 to R61 baseline 420027e. If R77 ≥ R61 (≥2/3), promote R77 to new BEST_GAN.

## Word count target

R61 v10 6,724w → R77 expected 6,300-6,400w. Well within cap.

## Prose-quality assessment

Pure-deletion + minimal stitching. Risk:
- Stitching seam in §4.2 must read smoothly. The paragraph currently begins "The other two cases ran on the same configuration and broke the same way." — must rewrite to "The contrast case ran on the same configuration."
- Stitching seam in §4.3 paragraph after table — must avoid ring-composition or aphoristic closer.
- Stitching seam in §5 — must replace the case-3 cost-gap clause without introducing a new tell.
- Appendix A variance note: rewriting to cite case-2 trial instead of case-3 trial preserves the authentic-detail signal flagged as positive cohort-mirror.

## Risk

Critic 152897786 in R76 explicitly noted that asymmetric weighting WOULD HELP: "Asymmetric weighting (one deep case, two shorter contrasts treated more loosely) would help." This is direct evidence Strategy 5 is in the right direction. The risk is over-collapsing to 1-case (which would lose the "broke the same way" cross-validation signal); 2-case keeps that.

## Implementation

Use Edit tool on /tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v10.md directly. Save R61 baseline first as /tmp/gan_round77/v10_R61_baseline.md so revert is one cp away.
