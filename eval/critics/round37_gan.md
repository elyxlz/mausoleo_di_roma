# GAN Round 37

Strip: TARGET 6,743 words.
Seeds: 235861423 (pos 3), 348924107 (pos 2), 315134906 (pos 8). All non-pos-1, distinct.

Edits applied:
- Asymmetric case weighting: collapsed §4 cases 2 and 3 into a single "two shorter cases" paragraph; lifted case 1 with a sustained close-reading paragraph on the 27 July reappearance issue.
- Defused "matters here" closer.
- Varied §3 definitional sentence openings ("Inputs to the OCR stage are...", "All index storage lives in...", "Retrieval is exposed through...").

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 235861423 | 3 | 3 (TARGET) | near certain | FAIL |
| 348924107 | 2 | 6 (NOT TARGET) | near certain | PASS |
| 315134906 | 8 | 8 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at pos 2.

## Key residual tells

From seed 315134906 (FAIL):
- "Aphoristic paragraph-closer codas — appears 15+ times; varying paragraph endings would substantially humanize."
- "Em-dash-substitute parenthetical-citation triplets — pervasive."
- "The tidy enumerated limitations paragraph in Chapter 5 — single most diagnostic structural tell; rewrite as a discursive caveat woven into the discussion rather than a checklist."
- "End Chapter 5 with reflection rather than the limitations + future-work pairing."
- '"matters" / "is the move that" / "is what" emphatic constructions': "This matters most for the absent-day case"; "This is the move that historical-newspaper OCR work in NewsEye... helped make standard"; "this is the architectural precondition for the lead case study"

From seed 235861423 (FAIL): unread.

## Round 38 plan

1. Remove §5 explicit limitations paragraph + future-work pointers; replace with reflective close.
2. Defuse "is the move that", "is what" emphatic constructions.
3. Defuse remaining "matters" usages.
