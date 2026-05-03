# GAN Round 33

Strip: TARGET 7,347 words.
Seeds: 778076712 (pos 9), 767859265 (pos 5), 996705218 (pos 2). All non-pos-1, distinct.

Edits applied:
- Restored exact numbers in §4 case-study prose (round 32 range conversion was flagged as fabrication).
- Restored aggregate-numbers table.
- Replaced Preface retrospective-coherence paragraph (Bartlett/Hutchins/Eichenbaum) with a single concrete OCR-frustration anecdote about the 1885 column-six fiction header.
- Fixed "(material at every level (material at every level...)" stutter.
- Collapsed §5 limitations cascade from 6 paragraphs to 3 paragraphs.
- Broke "X, not Y" antithesis cadence at sentence level (7 instances).
- Restructured "what fails is not... what fails is" negation pivot in §4.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 778076712 | 9 | 9 (TARGET) | near certain | FAIL |
| 767859265 | 5 | 5 (TARGET) | near certain | FAIL |
| 996705218 | 2 | 5 (NOT TARGET) | lean toward | PASS |

Result: 1/3 PASS at pos 2.

## Key residual tells (verbatim)

From seed 778076712:
- (verdict short, mainly cited the structural shape of chapters and the cohort comparison)

From seed 767859265 (pos 5):
- "Triple-nested parentheticals doing balanced work: 'as a calendar-shaped tree of recursively summarised nodes (running from paragraph at the bottom up through article, day, week and month) over which a researcher agent navigates'"
- "Balanced antithesis as a structural tic. 'The missing day has no articles. The indexer has no representation for the day in itself.'"
- "STRUCTURAL — Pre-emptive limitations dump in a single cluster paragraph. 'A second cluster of caveats sits around the evaluation. There were three trials per cell, with sign tests in place of power-bounded effect sizes; both LLM judges came from the same vendor; relevance ground truth is single-annotator...' This is the classic LLM 'cover all bases' limitations enumeration, semicolon-chained, executed with suspicious symmetry."
- "STRUCTURAL — Anecdote-as-authentication inserted in the Preface. 'The 1885 evaluation issue had a column-six fiction header in a font my pipeline kept misreading...' This reads as an LLM doing 'human texture'"
- "Genre-fiction phrasing of empirical claims. 'The publication calendar, which the printers already followed, supplies it for free.' And 'the absent issue is stored as a first-class node'"

## Diagnosis

- Limitations cascade collapse FAILED — re-flagged as semicolon-chained "cover all bases" enumeration. Need to actually shorten or restructure.
- The OCR-frustration Preface replacement was also flagged as performed authenticity. Fix in round 34: drop the entire reading-shaping paragraph and merge the surrounding paragraphs.
- "First-class node" / "for free" / "supplies it for free" — register tics from CS-blog prose.
- "The missing day has no articles" / "The indexer has no representation" — the tightest aphoristic-clincher chiasmus in §1 is now a high-leverage tell.

## Round 34 plan

1. Drop the reading-shaping paragraph in Preface entirely; merge into surrounding paragraphs.
2. Defuse "supplies it for free" / "first-class node" CS-blog register tics.
3. Defuse "The missing day has no articles. The indexer has no representation for the day in itself." chiasmus in §1.
4. Restructure §5 limitations: instead of bulleted-cascade or semicolon-chained, fold each into the relevant earlier discussion paragraph (cost into the OCR section in §3, rubric mismatch into §4, etc.) and leave §5 with only the LLM-substitution limit.
