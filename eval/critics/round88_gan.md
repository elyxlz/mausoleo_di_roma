# Round 88 verdict — Strategy 8 base + Strategy 9 asymmetric §4 case weighting

## Result

**1/3 PASS at pos 2 LEAN_TOWARD.** Same as R87. Below R80's 2/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=372292564, pos=6: critic picked Essay 6 (TARGET), near-certain → FAIL
- seed=741713124, pos=2: critic picked Essay 5 ('2022SMMH0' Artificial Creativity, NOT TARGET), **lean-toward** → **PASS**
- seed=2704372, pos=8: critic picked Essay 8 (TARGET), near-certain → FAIL

## Strategy applied

R86 base (Note + Grandi footnote + §3 rename) + R87 chapter renames §2 + §4 + glossary appendix + dropped LDA Preface paragraph (R87-flagged) + asymmetric §4: expanded missing-26-July case with extended close-reading on the 27 July reappearance issue layout (~150w added) + compressed "Two shorter cases" to a single dense paragraph (~120w from 270w).

Word count: 7,124 → 7,924w (+800w).

## What the critics flagged

**Seed 372292564 (FAIL near-certain)**: Recommended (rec #2 in Structural rewrite suggestions) "asymmetric case weighting" — exactly the move R88 attempted. Did NOT register the change. Critic still saw "symmetric three-case structure with parallel framing"; the §4 chapter heading "Three case studies on the July 1943 *Il Messaggero* corpus..." with all three cases listed may have signalled symmetry over the actual prose treatment. Critic flagged the NEW §4.1 close-reading expansion paragraph "the new government's authority is staged through the King and the new cabinet, not through the resolution that produced the deposition" as a "X, not Y" antithesis tell.

**Seed 741713124 (PASS_LEAN at pos 2)**: critic picked Essay 5 = '2022SMMH0' Artificial Creativity (real cohort exemplar) on classic LLM tells (mechanically restated three-question triplet, symmetric algorithm template, banal hedge-summary closers, generic transitional throat-clearing). Did NOT pick TARGET.

**Seed 2704372 (FAIL near-certain)**: Tells: balanced antithesis throughout, pre-emptive hedging, too-clean numbers. Recommended asymmetric case weighting (same as seed 1). Cited the OCR segmentation-error footnote as POSITIVE: "the most human moment in the essay... non-load-bearing detail. Don't regress on either." Cited the *Il Messaggero* OCR pipeline failure note as POSITIVE.

## Insight

R86 (1 lean), R87 (1 PASS lean + 1 FAIL_LEAN), R88 (1 PASS lean): Strategy 8 + asymmetric §4 plateau at 1/3 LEAN. The Strategy 8 ADDITIONS that critics named POSITIVE (footnote OCR-detail, Note on translations, glossary, §3 rename) do not flip the dominant FAIL critics whose tell-list is dominated by surface antithesis + pre-emptive hedging + clean numbers.

The asymmetric §4 may need to be MORE aggressive: critics named the CHAPTER TITLE "Three case studies..." as still signalling symmetry. The compressed §4.2 was a single paragraph but still listed both cases with full numbers. The §4.3 "Aggregate numbers" table was unchanged.

R89 plan: combine R88 base + (a) drop the §4.3 prose recapitulation paragraph after the table (R86 critic 18701894 suggestion: "drop the 'Aggregate numbers' table or the prose recital of the same numbers; pick one"), (b) drop §5 paragraph 4 "What the experiment does not show" sentence entirely (R86, R87, R88 all flagged this exact sentence as RLHF safety tell), (c) revert §4 chapter title to less-listed shape.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.
