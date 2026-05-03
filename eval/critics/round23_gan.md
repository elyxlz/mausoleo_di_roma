# GAN Round 23

Strip: TARGET 7,360 words.
Seeds: 64906983 (pos 4), 983853785 (pos 3), 845958655 (pos 6). All non-pos-1.

Structural moves applied this round:
- Collapsed Ch6 into Ch5 (single closing chapter, no two-chapter limitations split).
- Dropped "(lead case)" header tag.
- Dropped chapter-1 chapter-by-chapter forecast.
- Reworked the Sarthi/Edge/Zhang triplet so each method is in its own clause structure.
- Defused "The summary is never authoritative; the leaves are." aphoristic closer.
- Defused "Sign-test p-values run from 0.125 to 1.000; coarse, but uniform in direction." aphoristic closer.
- Defused "Thirty article snippets exceed active capacity; one day-summary at the right level of abstraction sits comfortably within it." antithesis.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 64906983 | 4 | 4 (TARGET) | near certain | FAIL |
| 983853785 | 3 | 2 (NOT TARGET) | lean toward | PASS |
| 845958655 | 6 | 6 (TARGET) | near certain | FAIL |

Result: 1/3.

Residual tells:
- Antithesis still: "the missing one has not, since there is nothing to digitise"; "Reading around the gap meant reading the 25th and the 27th and inferring; the interface treated my question as a query that returned nothing, when in fact the absent issue is one of the most articulate documents the corpus contains."
- Paradox/chiasmus: "the absent issue is one of the most articulate documents the corpus contains".
- Triplet "paragraph, article, day, week, month" repeated verbatim.
- Anaphoric definite-article paragraph openers in Ch5 (eight in a row): "The cognitive-science framing..." / "The story is not simply..." / "The build is not cheap..." / "The summariser is doing..." / "Scope conditions on the evaluation." / "The most consequential limitation..." / "The wider point I would still make..."
- "Scope conditions on the evaluation." flagged as telegraphic header-as-sentence.
- Stripped framework-name dodges still showing up ("one such method (Sarthi et al.), another such method...") — STRIP ARTEFACT but visible.

Edits for round 24:
- Vary paragraph openers in Ch5 (mix non-NP and subordinate clauses).
- Rewrite "Scope conditions on the evaluation." paragraph opener.
- Remove "the absent issue is one of the most articulate documents the corpus contains" chiasmus from preface.
- Vary "paragraph, article, day, week, month" repetitions.
- Rewrite the "Reading around the gap meant ..." sentence in preface.
- Improve strip script so RAPTOR/GraphRAG/PageIndex don't collapse to "one such method, another such method, a third method".
