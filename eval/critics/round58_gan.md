# GAN Round 58

Strip: TARGET 6,053 words. v10 = 6,949 words.
Seeds: 254149146 (pos 9), 866867806 (pos 8), 641902474 (pos 6).

Edits applied (per round58_plan.md, BEFORE the revert):
- DELETED §2.3 line 68 paragraph opener "On the neural side the recent work shows that the same hierarchical-relational organisation extends from space to time and concept."
- DELETED §1 line 27 sentence "What the interface cannot do is register that the absent day is part of the corpus's testimony, the editorial silence of twenty-four hours of regime transition."
- DELETED §2.2 line 56 sentence "On a corpus with a strong native temporal hierarchy this assumption is harder to defend."

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 254149146 | 9 | 9 (TARGET) | lean toward | FAIL |
| 866867806 | 8 | 8 (TARGET) | near certain | FAIL |
| 641902474 | 6 | 6 (TARGET) | near certain | FAIL |

Result: 0/3 PASS. CONFIDENCE-SOFTENED on seed 254149146 (lean-toward instead of near-certain). REGRESSED PASS count from R55's 1/3.

PER PARETO RULE: REVERTED v10 to R55 snapshot (commit 4c3e1b3).

## Pure-deletion approach validated, but cohort variance dominates

The three deletions did NOT introduce any new tells (none of the deleted sentences were re-flagged in their replacement positions). One critic (254149146) was at lean-toward — softer than R56's all-near-certain. But the PASS-count regression means R58 cannot be the new baseline.

The dominant tells in R58 critic verdicts that were NOT addressed by R55 + R57 + R58 deletions:

- "**'X first, Y second' enumeration tic done in flowing prose**" — seed 866867806 cites *"Take hierarchical memory first... A second strand concerns chunking and the active workspace... Tolman (1948) showed... Cognitive-offloading work then closes the picture."* — but R53 already deleted "Take hierarchical memory first" and "A second strand concerns chunking" and "Cognitive-offloading work then closes the picture" — wait, R53 was reverted. So R55 baseline still has all four discourse-marker openers. Confirmed: R55 baseline §2.3 still has the four-paragraph enumeration "Take hierarchical memory first" (line 64), "A second strand concerns chunking" (line 66), "On the neural side" (line 68), "Cognitive-offloading work then closes the picture" (line 70).

- "**three-strand lit review symmetric**" — seed 866867806 + 641902474 + 254149146 all cite the §2.3 paragraph structure. R57 tried renaming Ch3 subsections (wrong target); the actual problem is §2.3 paragraph structure.

CONFIRMED CLEAN R59 TARGETS:
1. **Delete the §2.3 four-paragraph discourse-marker openers** (R53 attempted this and was reverted, but the deletion itself was clean). Specifically delete the OPENING DISCOURSE MARKERS from each of four §2.3 paragraphs — keep the paragraph content but drop "Take hierarchical memory first.", "A second strand concerns chunking and the active workspace.", "On the neural side the recent work shows that the same hierarchical-relational organisation extends from space to time and concept." (already an R58 target), and "Cognitive-offloading work then closes the picture."

## Round 59 plan (PRELIMINARY)

PRIMARY: pure-delete the four §2.3 discourse-marker openers AT ONCE. Each one is a single sentence; deleting them does not break the paragraph structure (the citation-driven content carries each paragraph).

This is the same set R53 tried (and was reverted alongside other unrelated edits). The R53 verdict didn't flag any of these deletions as introducing new tells. Worth re-trying alone.

EXCLUDE: do NOT touch anything else.
