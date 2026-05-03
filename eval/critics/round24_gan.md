# GAN Round 24

Strip: TARGET 7,476 words. Strip script `/tmp/gan_round24/strip_uniform.py` (FRAMEWORK_PATTERNS now collapse RAPTOR/GraphRAG/PageIndex to a uniform "a recent method", removing the "one such / another such / a third" tell).
Seeds: 129202849 (pos 8), 691493481 (pos 6), 636441639 (pos 5). All non-pos-1.

Edits applied:
- Restructured Ch5 paragraphs to avoid eight-in-a-row "The X is Y" anaphoric openers. Mixed in "Across the three cases", "These results", "That story", "To begin with", "There is also more going on", "Several boundary conditions", "Of these limits", "Two other directions", "There is a wider point".
- Rewrote "Scope conditions on the evaluation." fragment opener.
- Removed "the absent issue is one of the most articulate documents the corpus contains" chiasmus from preface.
- Varied 3 occurrences of "paragraph, article, day, week, month".

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 129202849 | 8 | 8 (TARGET) | near certain | FAIL |
| 691493481 | 6 | 5 (NOT TARGET) | lean toward | PASS |
| 636441639 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 1/3.

Residual tells:
- "What changed across the literature reading... was that I started to see..." preface conversion arc still flagged.
- Cleft constructions: "What the schema's leaf-summary separation does is preserve...", "What the default ranked list of articles is doing, by contrast, is making..."
- Tricolons-with-semicolons: "Date sits as a first-class structural property of the index, an absent date instantiates a first-class node, that node carries a summary, and the absence becomes addressable from within the index rather than from outside it."
- "their question and Mausoleo's are different: theirs is, given a query, retrieve the topically relevant articles; Mausoleo's is, given a temporal slice, return what the slice looked like, including its absences."
- Bare definite-NP topic-comment openers throughout chapter 3 setup.
- Limitations enumeration even after restructuring.

Edits for round 25:
- Rewrite preface so the "X then Y conversion arc" goes; lead with concrete operational anecdote instead.
- Break the tricolon "Date sits... an absent date instantiates... that node carries..."
- Defuse cleft "What the schema's leaf-summary separation does is preserve..." and similar.
- Vary chapter 3 openers.
- Replace the Murugaraj differentiation passage entirely (the "their question and Mausoleo's are different" antithesis).
