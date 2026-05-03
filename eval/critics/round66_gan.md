# GAN Round 66

Strip: TARGET 5,823 words. v10 = 6,719 words.
Seeds: 56544970 (pos 7), 870701436 (pos 6), 474732148 (pos 5).

Edits applied (per round66_plan.md, BEFORE the revert):
- DELETED §1 paragraph 4 closer "When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search holds none." (the high-leverage tell flagged by 2 of 3 R65 critics).
- Pure deletion only. The next paragraph's opening "This dissertation builds and tests an interface that does hold them." carries the implied contrast through the "them" referent.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 56544970  | 7 | 7 (TARGET) | near certain | FAIL |
| 870701436 | 6 | 6 (TARGET) | near certain | FAIL |
| 474732148 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near certain. REGRESSED HARD from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Why the deletion didn't move

The deleted §1 closer was clean — no R66 critic re-flagged it. But three new seeds independently picked TARGET on a SAME-CLASS of tells:
- Aphoristic closers: "no 26 July to digitise" (Ch1 para 1 closer); "the gap is already inside the index" (§4); "that compression too is part of what the index records about July 1943" (Ch5 closer R54).
- Balanced antithesis: para 1 sentence 4 of abstract ("Questions about… return tens; questions about… return hundreds"); R51 abstract opening; "the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form" (newly the cohort-mirror flag — was previously preserved as positive).
- Parallel triplets: "paragraph in article in issue in day in week in month"; "space, time and conceptual relation"; "Three systems define the field".
- Self-referential meta-commentary: "The relevance for an archival interface is direct enough" (now that the para closer is gone, this phrase becomes the new visible meta tell).
- Asymmetric chapter-4 case weighting (NEW R66 seeds rate this as STRUCTURAL high-leverage; R61 PASS critics had rated it positive — cohort variance dominates).

CRUCIAL: critic 56544970 quotes "The relevance to an archival interface is direct enough" and "The relevance for an archival interface is direct" as a recurring meta-summary tic. The R66 deletion REMOVED the second of these — the surviving "direct enough" is in para 4 of §1, the now-deleted closer used to carry the conclusion-coda function. With that closer gone, the "direct enough" stands alone and is more visible. The deletion may have INCREASED the visibility of the surviving meta-summary line.

## Pattern across R62–R66

5 consecutive rounds (R62 collapse, R63 hedge delete, R64 §2.3 opener replace, R65 abstract delete, R66 §1 closer delete) at 0/3, all FAIL_NEAR_CERTAIN, all reverted. The single-edit signal is exhausted at the cohort-variance noise floor. R61 BEST_GAN at 2/3 stands.

## Implication for R67 onward

Per R64 verdict: "to break out of the noise floor, edits need to address tells that EVERY critic flags — not just specific ones rotating." The R65 + R66 verdicts confirm this. Three families of tell are universal:
(a) aphoristic closers (3+ instances across the draft, removing one leaves others)
(b) parallel triplets (5+ instances)
(c) the asymmetric case-weighting STRUCTURAL flag (one location, but rated positive by R61 and negative by R65/R66 cohorts)

R67 will attempt a COMBINED-DELETION PACKAGE on the R60 model: defuse 3 aphoristic closers + 1 self-referential meta-commentary in a single round, on top of R61 baseline. Multiple targets in one round was R60's recipe for moving from 0/3 floor to PASS. R65 + R66 single-edit attempts both produced 0/3, so a single-edit gambit on R67 would predictably reproduce the floor.

EXCLUDE from R67: Preface (positive cohort-mirror), Italian block (positive), OCR detail (positive), Ch1 thesis sentence (R61 PASS critic praised), R54 closer (split-flagged, ambiguous), §2.4 (already R61), Ch5 surviving hedge (already R61).

R67 PRIMARY targets (combined deletion package):
1. Defuse "the gap is already inside the index" (§4 aphoristic closer) by folding into preceding sentence.
2. Defuse "no 26 July to digitise" (Ch1 para 1 closer) by removing the rhetorical-coda function.
3. Defuse "The relevance for an archival interface is direct enough" (§1 meta-summary) by deletion.
4. Defuse "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed" (§1 meta-closer) by replacing with non-aphoristic factual sentence.
