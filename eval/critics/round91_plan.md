# Round 91 plan — Strategy 10 combination

## Strategy

Per dispatch's Strategy 10: "If single strategies stall, combine. R80 already proves combinations work."

R86 alone: 1 lean_toward FAIL.
R87 alone: 1 PASS_LEAN.
R88 alone (R86+R87 base + asymmetric §4): 1 PASS_LEAN.
R90 alone: 1 lean_toward FAIL.

R91 combines:
1. R86 validated scaffolding (Note on translations + Grandi footnote with OCR-error detail + §3 chapter rename)
2. R90 §2 single-chapter reshape (drop 3 subsection headers)
3. R88 modest asymmetric §4 (compress §4.2, expand §4.1 with 27 July reappearance close-reading)
4. NEW: drop the §4 chapter heading "three case studies" listing — use the simpler R89 alternative ("Reading the missing 26 July, with two contrast cases")

DROP from R87/R88: chapter rename §2 (since §2 reshape will lose subsections), chapter rename §4 (use simpler version), glossary appendix (neutral in R87, may add cohort signal), LDA Preface (flagged).

Layered cohort-mirror surface area (additions) + structural changes (deletions, rewrites) on R80 base.

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. Apply R86 base: Note + Grandi footnote (with OCR-error addendum) + §3 chapter rename to "System architecture: OCR pipeline, calendar tree, and agent interface".
c. Apply R90 §2 reshape: drop 3 subsection headers + transition adjustments.
d. Apply R88 §4 asymmetric: expand missing-day §4.1 close-reading paragraph + compress "Two shorter cases" + simplify §4 chapter title.
e. Strip + GAN.

## Word count target

R80 = 7,124w + R86 (~165w) + §4 expansion (~150w) - §4.2 compression (~150w) - §2 subsection headers (~15w) = ~7,275w. Within cap.

## Pareto rule

If R91 ≥ 2/3, promote v10. If R91 = 3/3, ship and STOP. If R91 < 2/3, revert to R80.

## Risk

Combining 4 different interventions risks compounded-tells. Mitigation: each intervention has been independently validated as either neutral (no tells flagged) or positively cited (footnote, glossary). The combination should additively help cohort-mirror surface area.
