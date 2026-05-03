# GAN Round 67

Strip: TARGET 5,785 words. v10 = 6,657 words.
Seeds: 948202072 (pos 8), 126255885 (pos 9), 339000377 (pos 2).

Edits applied (per round67_plan.md, BEFORE the revert) — combined-deletion package, 4 targets:
1. DELETED Ch1 para 1 closer "The 26 July does not appear in the digitised fund because there was no 26 July to digitise." (line 25).
2. DELETED §1 para 5 mid-sentence "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed." (line 35).
3. DELETED §4 closer fragment "since the gap is already inside the index" (line 128) — leaving "The calendar-shaped hierarchy makes both workarounds unnecessary."
4. REPLACED §2.3 opener pair (line 62) with R56-precedented clean form "Several converging strands from cognitive science support the choice of a calendar-given hierarchy for an archival interface."

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 948202072 | 8 | 8 (TARGET) | near certain | FAIL |
| 126255885 | 9 | 9 (TARGET) | lean toward | FAIL |
| 339000377 | 2 | 9 (2022SMMH0 — Artificial Creativity) | lean toward | PASS |

Result: 1/3 PASS at non-pos-1. BELOW BEST_GAN R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Why R67 fell short of R61

The combined deletion package softened one FAIL critic from near-certain to lean-toward and produced one cohort-mirror PASS where the critic picked Essay 9 (`2022SMMH0` Artificial Creativity, real cohort exemplar) on the same surface tells (mechanical "twofold goal" / numbered triplet framing, symmetric section weighting, hedged closers). Mausoleo escaped on cohort-mirror.

But the third seed (948202072) stayed near-certain on STRUCTURAL flags that pure deletion cannot address:
- Symmetric chapter-ending recapitulations (every chapter lands on a tidy thematic sentence — Ch1 still ends on "and a flat keyword search holds none", Ch5 still ends on the R54 closer)
- "Three literatures" framing in Ch2 (the IMRAD-style scaffolding)
- Preface arc too tidy (3-paragraph "origin / pivot / acknowledgment")

R61 preserved more aphoristic-closer texture (which R65/R66/R67 critics flagged) but ALSO preserved more cohort-mirror exemplar content. The R67 deletions removed surface tells but did not increase positive cohort-mirror content. Net: cohort variance still drives the verdict.

## Confidence-softening trend

R65: 0/3 all near-certain.
R66: 0/3 all near-certain.
R67: 1 PASS + 1 lean-toward FAIL + 1 near-certain FAIL.

R67 is technically softer than R65 and R66, but the PASS count threshold is what counts under Pareto. R61 still BEST at 2/3.

## Pattern across R62–R67

6 consecutive rounds at or below R61. The single-edit and 4-edit-package gambits both produce 0–1/3. The 2/3 R61 result depended on a specific seed cohort drawing two seeds where Mausoleo's asymmetric case weighting + technical detail + Italian summary landed as positive cohort-mirror, AND the other seed picking Essay 9 (Artificial Creativity) due to its more pronounced structural symmetry.

## R68 plan options

Three viable directions:

**Option A — preserve R61, attempt 8+ deletion package on R60 model.** R60 used 8+ deletions to break the 0/3 floor and reach 1/3. Following R61, layering more deletions on top might preserve PASS critics' cohort-mirror while reducing FAIL surface tells.

**Option B — accept R61 as ship draft.** R61 is the BEST_GAN baseline at 2/3 across 67 rounds. Deadline Wed May 6 17:00 BST is approaching. R61 v10 is at commit 420027e.

**Option C — structural rewrite of Ch2 and Ch5 closer.** R67 critics consistently flag the "three literatures" Ch2 scaffolding and the symmetric chapter-ending recap. A deeper structural reshape could move the noise floor, at the cost of risking the cohort-mirror praise R61 PASS critics gave to the existing structure.

R68 plan: pursue Option A first (extend the combined-deletion package by 4 more targets), since Option C is high-risk to break the 2/3 floor entirely and Option B is the deadline-fallback.

R68 PRIMARY targets to LAYER on R67 deletions (combined 8-edit package on R61 baseline):
- Same 4 R67 deletions (proven clean)
- ADD: defuse Ch5 line 161 closer "the absolute call-count gap is largest on the regime-change case, with roughly twelve Mausoleo tool calls against a baseline saturating its thirty-call budget every trial" (semicolon-balanced numeric)
- ADD: defuse §1 para 4 closer (R66 attempt, was clean)
- ADD: defuse "The relevance to an archival interface is direct" (line 64) — the second instance flagged by R66 critic 56544970
- ADD: defuse §4 closer line 167 R54 closer (split-flagged, ambiguous; risk: removing a R55-PASS-praised line)

Caution on the last item: R55 PASS critic praised the R54 closer change as positive cohort exemplar. R63 + R66 + R67 critics flagged it as aphoristic. The split is real.
