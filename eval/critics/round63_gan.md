# GAN Round 63

Strip: TARGET 5,847 words. v10 = 6,690 words.
Seeds: 580711645 (pos 2), 713035088 (pos 3), 532139052 (pos 5).

Edits applied (per round63_plan.md, BEFORE the revert):
- DELETED §2.2 sentence "A direct head-to-head on Impresso is the obvious experiment but is gated on language: the Impresso corpus is French and German, and the case-study agent and judges in chapter four are configured for Italian." (line 56 closer)

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 580711645 | 2 | 2 (TARGET) | lean toward | FAIL |
| 713035088 | 3 | 3 (TARGET) | near certain | FAIL |
| 532139052 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, 1 lean-toward + 2 near-certain. REGRESSED from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Cohort variance dominates

The Impresso hedge deletion was clean (no re-flag in any verdict). One seed dropped to lean-toward; two remained near-certain. The R61 PASS critics drew different cohort positions than R63's seed set, and the FAIL critics here cited different specific tells than R61's FAIL critic.

NEW high-leverage tells from R63 verdicts:
- Seed 532139052 + 713035088 cite "**Why the calendar-given hierarchy should be the right shape... is the substantive cognitive-science claim the dissertation rests on**" — this is the §2.3 self-referential opener that R56 attempted to remove but R56 was reverted alongside an unrelated mistake. R55 baseline (and R60 + R61 + R63 baselines) all still have it.
- Seed 580711645 cites "**'X is the Y' deflationary closer per section**" — *"the gap is already inside the index"*; *"the reasoning sits in the agent"*; *"that compression too is part of what the index records about July 1943"* (R54 closer split-flagged again).

CONFIRMED CLEAN R64 TARGET: pure-delete the §2.3 self-referential opener "Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on." (line 62) AND "Several converging strands from cognitive science support it, and they are worth taking in turn." (the second sentence — R55 still has both).

R56 attempted both with a clean replacement "Several converging strands from cognitive science support the choice of a calendar-given hierarchy for an archival interface." That replacement form was NOT re-flagged in R56 verdicts. The only reason R56 was reverted was the unrelated Ch5 hedge deletion that didn't help.

R64 will re-attempt the R56 §2.3 opener change, isolated, in a single edit, on top of R61 baseline.
