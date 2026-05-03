# Round 69 plan (deep-review-and-taste)

## 1. Re-read affected section

Ch1 paragraph 1 (line 25 of v10 R61 baseline) ends:
> Mussolini had been deposed and arrested overnight; an editorial line for the morning paper could not be drawn in time and the issue did not run. The 26 July does not appear in the digitised fund because there was no 26 July to digitise.

The closing tautological flourish "no 26 July to digitise" is flagged by R61 FAIL critic (863684421), R65 critics, R66 critics, R67 critics, R68 critics. It is the most-flagged single sentence in the draft.

## 2. Synthesis of R65–R68 verdicts

R67 (4-edit package including this deletion + 3 others): 1/3 PASS at lean.
R68 (8-edit package): 0/3 hard regression.

The non-monotonic relationship between deletion count and PASS rate suggests the binding constraint is COHORT-MIRROR PRESERVATION, not surface-tell density. R67's 4 deletions kept enough positive cohort-mirror content (Preface OCR detail, §4 closer R54, asymmetric case weighting); R68's 8 deletions removed too much.

The single most-flagged surface tell — "no 26 July to digitise" — is also the most surgical: it ends paragraph 1 of Ch1 and its removal leaves the prior sentence "an editorial line for the morning paper could not be drawn in time and the issue did not run" as the new closer. That prior sentence is factual and does not have aphoristic shape.

The R67 evidence: this deletion was clean — no R67 critic re-flagged the deleted sentence in the surviving prose.

## 3. Cohort exemplar reference

Real cohort essays end Ch1 paragraphs with continuations. The factual closer "the issue did not run" is closer to cohort register than the chiastic "no X to Y".

## 4. Candidate moves

### Candidate A — single isolated deletion of "no 26 July to digitise" sentence (PRIMARY)

Same edit as R67's #1, isolated.

**Prose-as-prose:** improves — flatter factual closer, less rhetorical flourish.
**Argument integrity:** preserved — prior sentence carries the implication.
**Reads-human preserves:** all R61 PASS-cited content (Preface, OCR, Italian, asymmetric case weighting, Ch1 thesis sentence, §4 closer R54).
**Same-class-tell risk:** zero — pure deletion.
**Targeted tell:** flagged in R61, R65, R66, R67, R68 verdicts (5 consecutive rounds).

### Candidate B — keep all of R61 baseline, accept R61 as ship

R61 v10 = commit 420027e. Word count 6,724.

**Prose-as-prose:** R61 is the highest-scoring GAN result in 67 rounds.
**Argument integrity:** preserved.
**Reads-human:** all preserved.
**Trade-off:** stops at 2/3. R69 deletion attempt costs 1 GAN call (1 round of 3 critic calls) and tests Direction 1 of R68 plan.

## 5. Decision

Pick Candidate A — single isolated deletion. Time-cheap test of whether the most-flagged single tell, removed in isolation, can flip a third seed beyond R61's 2/3.

If it does NOT flip (most likely outcome given R65–R68 single-edit results), R69 reverts and the next move is Candidate B (accept R61 as ship).

## 6. Predicted downstream effect

Ch1 paragraph 1 ends on "and the issue did not run." This is a factual statement, not a chiastic flourish. The prior sentence's "Mussolini had been deposed and arrested overnight; an editorial line for the morning paper could not be drawn in time and the issue did not run." carries some semicolon-balance shape, but it is information-bearing rather than rhetorical.

## 7. Fallback (R70)

If R69 lands 3/3: STOP, mission complete.
If R69 lands 2/3 (matches R61): commit the deletion as new BEST_GAN baseline (R61.5), continue R70 with 1 more single deletion.
If R69 lands 1/3: revert. Try Candidate B in R70 (ship R61).
If R69 lands 0/3: revert. Confirms R61 is irreducible local max. Ship R61.
