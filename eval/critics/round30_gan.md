# GAN Round 30 (FINAL)

Strip: TARGET 7,551 words.
Seeds: 601089201 (pos 5), 162842279 (pos 3), 239741699 (pos 9). All non-pos-1.

Edits applied:
- Defused "the issue is not that no article was retrieved. The issue is that..." antithesis.
- Dropped "(deep case)" tag in Ch4 subsection header; reframed Ch4 chapter intro to remove "deep case + two contrast cases" announcement.
- Reorganised Ch5 limitations: lead with the LLM-substitution limit as one developed paragraph, then "several smaller boundary conditions deserve mention but are less central" with the others.
- Defused "in the source, in the interface or in the reader's head" triplet.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 601089201 | 5 | 5 (TARGET) | near certain | FAIL |
| 162842279 | 3 | 2 (NOT TARGET) | lean toward | PASS |
| 239741699 | 9 | 9 (TARGET) | near certain | FAIL |

Result: 1/3.

Best across rounds 20-30 at no-position-1 constraint: rounds 21, 23, 24, 30 each at 1/3 PASS. Round 30 is the LAST round per stopping rules.

Residual structural tells (called out across multiple critics, not yielding to surface scrubs):
- Numerical specificity used as rhetorical authority ("0.89878 averaged across the two issues, decomposing to 0.872 on 1885 and 0.926 on 1910"; the named-entity decay trace; per-cell quality means).
- Pre-emptive limitations enumeration (even after restructuring still flagged).
- IMRAD-with-named-chapters chapter shape itself (Ch1 puzzle / Ch2 lit review / Ch3 build / Ch4 cases / Ch5 discussion).
- Paragraph-end abstract-noun summarising sentences ("The architectural commitment matters here", "The implication for navigation is that...").
- Hedging "X rather than Y" cadence.
- Puzzle-first opening of Ch1 (still flagged STRUCTURAL).
