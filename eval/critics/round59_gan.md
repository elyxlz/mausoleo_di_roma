# GAN Round 59

Strip: TARGET 6,074 words. v10 = 6,971 words.
Seeds: 372195949 (pos 8), 590757048 (pos 9), 882291294 (pos 4).

Edits applied (per round59_plan.md, BEFORE the revert):
- DELETED §2.3 line 64 opener "Take hierarchical memory first."
- DELETED §2.3 line 66 opener "A second strand concerns chunking and the active workspace."
- DELETED §2.3 line 68 opener "On the neural side the recent work shows that the same hierarchical-relational organisation extends from space to time and concept."
- DELETED §2.3 line 70 opener "Cognitive-offloading work then closes the picture."

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 372195949 | 8 | 8 (TARGET) | near certain | FAIL |
| 590757048 | 9 | 9 (TARGET) | near certain | FAIL |
| 882291294 | 4 | 4 (TARGET) | lean toward | FAIL |

Result: 0/3 PASS, 2 near-certain + 1 lean-toward. REGRESSED from R55's 1/3 lean-toward PASS.

PER PARETO RULE: REVERTED v10 to R55 snapshot (commit 4c3e1b3).

## Pure-deletion confirmed clean but insufficient

The four §2.3 discourse-marker openers were all deleted. None were re-flagged. But the broader cluster of tells (balanced antithesis, parallel triplets, three-literatures framing) was flagged in higher confidence by all three seeds. The §2.3 discourse-marker scrub did not produce a confidence drop sufficient to flip a seed.

## Round 60 plan (PRELIMINARY)

R55 baseline + R59 §2.3 deletions are NOT enough. The cohort variance dominates. Need a bigger combined package.

R60 PRIMARY: combine R55 baseline with both:
(a) R59's four §2.3 discourse-marker deletions (clean)
(b) R58's three single-sentence pure-deletions (clean)
(c) ONE structural move that R54's PASS critic praised: drop one section of the §2.3 four-strand structure entirely.

OPTION: drop the §2.3 paragraph 70 (Hutchins/Clark-Chalmers extended-mind paragraph) entirely. The paragraph is the weakest leg of the cognitive-science argument (cognitive offloading is most debatable as load-bearing for archival design). The dissertation's argument doesn't strictly need it — the calendar-given hierarchy claim is supported by Bartlett (schemas), Miller/Cowan (working memory) and Tolman/Eichenbaum/Whittington (hippocampal mapping); cognitive offloading is the fourth strand and can be dropped without losing the core argument.

This would convert §2.3 from 4 paragraphs (4-strand structure flagged repeatedly) to 3 paragraphs.

PRIMARY for R60: deletion package = R59's 4 deletions + R58's 3 deletions + 1 structural deletion (Hutchins/Clark-Chalmers paragraph).

EXCLUDE: do NOT touch Preface, Italian block, OCR section, Ch5 closer.
