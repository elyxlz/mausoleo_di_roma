# GAN Round 48

Strip: TARGET 6,171 words.
Seeds: 954870642 (pos 9), 943095667 (pos 7), 216301607 (pos 5).

Edits applied (per round48_plan.md):
- Rewrote §2.2 RAPTOR/GraphRAG/PageIndex paragraph: desymmetrised the three system descriptions, added a substantive caveat to GraphRAG (extraction cost + opacity of community hierarchy), demoted PageIndex from co-equal third entry to a related-line aside.
- Rewrote §2.3 "Mausoleo extends..." opener: killed "while X" balanced antithesis; the new version mentions concrete advantages (no clustering decisions, no quality-of-extracted-graph dependence, predictable navigation surface).
- Rewrote §4 "A flat index has no node for a missing date and can only return null. A calendar-shaped tree, by contrast..." pair as a single non-parallel sentence.
- Rewrote §5 opener "Across the three cases, Mausoleo wins on every metric reported" with hedged opener acknowledging the recall tie up front.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 954870642 | 9 | 7 (NOT target) | lean toward | PASS |
| 943095667 | 7 | 7 (TARGET) | lean toward | FAIL |
| 216301607 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at non-position-1 (seed 954870642, pos 9). Both FAILs softer than R47: one lean-toward, one near-certain (vs R47 two near-certain). Confidence trend is downward.

## High-leverage tells flagged across the 2 FAILs
- "balanced antithesis with rhetorical 'X handles Y and is awkward for Z' cadence" — quoted my own R46 abstract sentence "that template handles questions for which articles exist and is awkward for the others the corpus invites".
- The new R48 §2.3 sentence "no clustering decisions, no quality-of-extracted-graph dependence, and a navigation surface a working historian can predict" is itself a triadic negation list — flagged.
- "is the test the design was built around" / "is the case the design was built around" near-verbatim repetition (§1 end + §4) flagged.
- "Bare nominal sentence fragments used as topic openers" — "Chunking and the active workspace come in next."; "Lastly there is the cognitive-offloading literature."; "The first is hierarchical memory."
- "the X is the Y" definitional flourish — "The schema permits days with no underlying articles."; "The pay-off shows up most clearly on the absent-day case."

## Round 49 plan
PRIMARY: kill the §2.3 "no clustering decisions, no quality-of-extracted-graph dependence, and a navigation surface a working historian can predict" triadic-negation list (just-introduced R48 tell). Replace with single non-list sentence about the predictability of calendar navigation.
SECONDARY: collapse the "is the case/test the design was built around" two-instance verbatim echo to one instance (cut at §1 end).
TERTIARY: defuse the bare-nominal openers in §2.3 ("The first is hierarchical memory."; "Chunking and the active workspace come in next."; "Lastly there is the cognitive-offloading literature.") to full sentences with verbs.
