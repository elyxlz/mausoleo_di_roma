# GAN Round 62

Strip: TARGET 5,815 words. v10 = 6,691 words.
Seeds: 603836521 (pos 7), 516034338 (pos 6), 296887689 (pos 9).

Edits applied (per round62_plan.md, BEFORE the revert):
- Collapsed Ch1 thesis sentence "at five hierarchical levels, with the leaf level holding paragraphs..." to "with paragraphs at the leaf level and the full month at the root".
- Deleted §2.2 parenthetical "(paragraph in article in issue in day in week in month)".
- Reshaped §4 chiastic closer "in Mausoleo's case the answer is grounded in the index, in the baseline's it leans on..." to "Mausoleo's compiled answer comes from the index, while the baseline's relies on the agent's prior knowledge of the regime change".

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 603836521 | 7 | 7 (TARGET) | near certain | FAIL |
| 516034338 | 6 | 6 (TARGET) | near certain | FAIL |
| 296887689 | 9 | 9 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near certain. REGRESSED HARD from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Why R62 regressed: collapse-by-shortening removed cohort-mirror content

The R61 PASS critics keyed on Ch1's thesis sentence ("at five hierarchical levels...") being read as a substantive technical detail providing texture. The R62 collapse to "with paragraphs at the leaf level and the full month at the root" stripped the texture and left the abstract noun phrasing more prominent. Result: cohort-mirroring weakened.

The triplet "paragraph in article in issue in day in week in month" was flagged by ONE earlier critic but in R62 the FAILs cited DIFFERENT triplets ("a date-bound episode to a few-day narrative to a month-scale schema" — Ch5; "Named individuals... Place names... Generic organisational acronyms" — §3 calendar-tree section; "OCR pipeline / recursive summariser / CLI" — Ch3 opener). Removing one triplet did not flip seeds because other triplets remained.

The chiastic closer rewrite did not introduce a new tell but also did not flip seeds.

The fundamental insight: R62's edits removed mass without redirecting the cohort-mirror signal. The PASS critics from R60+R61 cited Mausoleo's TECHNICAL TEXTURE (specific node IDs, the OCR composite, the Italian summary) as positive — touching the technical-detail layer reduces that signal.

## Round 63 plan (PRELIMINARY) — back to R61 baseline

R61 baseline at 2/3. Round 63 will preserve all R61 content and target the §4 OCR/numeric tells flagged by all three R62 FAILs:

CANDIDATE moves for R63 (no content stripping):
1. Defuse the §4 "Article-touching cannot score a question whose answer is an issue that does not exist" clause — flagged repeatedly. Replace with shorter version that does NOT use "X cannot score Y" form.
2. Defuse the §4 "A direct head-to-head on Impresso is the obvious experiment but is gated on language" pre-emptive hedge — flagged in R55 + R60 + R61 + R62. Either delete or rephrase to a flatter language note.

PRIMARY for R63: pure-delete of the §4 Impresso pre-emptive hedge sentence (one sentence, paragraph 56 §2.2). The previous sentence about a topic-restricted pipeline being asymmetric carries the argument; the Impresso head-to-head note can be relegated to a footnote-style aside elsewhere or simply dropped.

This is a pure-deletion, no risk of same-class tell. R61 baseline preserved.
