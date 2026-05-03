# GAN Round 64

Strip: TARGET 5,820 words. v10 = 6,696 words.
Seeds: 108424452 (pos 8), 881105998 (pos 7), 614025030 (pos 9).

Edits applied (BEFORE the revert):
- DELETED §2.3 self-referential opener "Why the calendar-given hierarchy should be the right shape... is the substantive cognitive-science claim the dissertation rests on. Several converging strands from cognitive science support it, and they are worth taking in turn."
- REPLACED with R56's clean form "Several converging strands from cognitive science support the choice of a calendar-given hierarchy for an archival interface."

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 108424452 | 8 | 8 (TARGET) | near certain | FAIL |
| 881105998 | 7 | 7 (TARGET) | near certain | FAIL |
| 614025030 | 9 | 9 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near certain. REGRESSED hard from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Cohort variance noise floor reached

Rounds 61-64 show that the v10 is at the cohort-variance noise floor:
- R61 (clean §2.4 + Ch5 deletes): 2/3 PASS
- R62 (R61 + collapsed thesis sentence + chiasmus rewrite): 0/3
- R63 (R61 + Impresso hedge delete): 0/3
- R64 (R61 + §2.3 opener clean replacement): 0/3

Each non-R61 round drew different seed sets. The single-edit signal is dominated by which seeds are drawn and how each critic cohort-mirrors. R61's PASSes were two specific seeds that happened to draw cohort positions producing positive cohort-mirror.

To break out of the noise floor, edits need to address tells that EVERY critic flags — not just specific ones rotating.

UNIVERSAL TELLS across R61-R64 verdicts:
- "**X handles Y and is awkward for Z**" — abstract opening, flagged in EVERY round since R20
- "**balanced antithesis throughout**" — saturating, flagged every round
- "**aphoristic single-sentence closers**" — flagged every round
- "**'Three questions are put to Il Messaggero' tripartite framing**" — abstract para 2 (R57 attempted to remove "Three" but R57 was reverted)

## Round 65 plan (PRELIMINARY)

R65 PRIMARY: defuse the **abstract opening "X handles Y and is awkward for Z" frame**. This is the highest-leverage tell in every R61-R64 verdict. The current sentence: "For the July 1943 *Il Messaggero* corpus this dissertation works with, that template handles questions for which articles exist and is awkward for the others the corpus invites."

REPLACEMENT: "For the July 1943 *Il Messaggero* corpus this dissertation works with, that template returns nothing on dates with no surviving issue, several hundred articles to be classified by hand on aggregate-shape questions, and tens of articles to be assembled by hand on the regime-change days."

This swaps the antithesis frame for a direct factual triad of what the keyword template returns. It removes the "X handles Y and is awkward for Z" rhythm entirely. The factual triad reads as concrete reporting rather than rhetorical balance.

EXCLUDE: do NOT touch §2.3, Preface, Italian block, OCR, Ch5 closer, R54 closer.
