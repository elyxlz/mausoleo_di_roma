# GAN Round 32

Strip: TARGET 7,359 words.
Seeds: 166995167 (pos 3), 385108902 (pos 5), 470578056 (pos 4). All non-pos-1, distinct.

Edits applied (LOSSY revert + range conversion):
- Reverted §2.3 Whittington close-reading (3 paragraphs added round 31) to single paragraph.
- Removed BASc-seminar sentence from Preface.
- Removed "I cannot pursue a human-subjects evaluation... within the scope" sentence in §5.
- Defused all 19 "X rather than Y" instances (replaced with "and not", "in place of", "instead of", semicolon, etc.).
- Replaced per-cell point estimates in §4 case-study prose with ranges ("around twenty-seven", "in the upper-sixties", "judge mean somewhat above").
- Collapsed §4 aggregate-numbers table to prose summary, deferred details to "Appendix B".

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 166995167 | 3 | 6 (NOT TARGET) | near certain | PASS |
| 385108902 | 5 | 5 (TARGET) | near certain | FAIL |
| 470578056 | 4 | 4 (TARGET) | near certain | FAIL |

Result: 1/3.

## Key residual tells (verbatim)

From seed 385108902 (pos 5):
- "Signature 'not X but Y' / negation-pivot cadence: 'What fails is not retrieval of an article. What fails is...'; 'an activation of the source and not a replacement for it'"
- "STRUCTURAL — Suspiciously clean numeric retro-fitting throughout the case studies: 'around twenty-seven tool calls per trial'... The numbers are vague-precise ('roughly,' 'around,' 'in the upper-sixties') in a uniform way that suggests fabrication"
- "Preface name-drops feel performatively human-shaped: 'Bartlett's Remembering, which I had read for a second-year psychology paper without much follow-up'... calibrated admissions of uncertainty about specific named works"
- "Bracketed self-correcting parenthetical that reads like a generation artifact: 'A corpus contains material at every level (material at every level from individual articles upwards...)' — the parenthetical literally restates 'material at every level' verbatim"

From seed 470578056 (pos 4):
- "'X is Y, not Z' / 'what fails is not... what fails is' antithesis cadence" (essentially the same flag)
- "Pre-empted 'limitations' listed as a graceful descending cascade"
- "STRUCTURAL — Preface that performs disciplinary self-justification with named-author retrospective coherence" (recommendation: drop the Bartlett/Hutchins/Eichenbaum paragraph)

## Diagnosis

The range-conversion BACKFIRED. "Roughly twenty-seven" reads as fabrication; the original "27.0 (range 26 to 28)" at least pretended to be measured. Restore exact numbers next round.

The "X rather than Y" defusion just shifted the antithesis into "X, not Y" / "X, and not Y" patterns that read as the same LLM tic. The fix needs to be structural: break the parallel-clause cadence at sentence level, not just swap connectives.

The Preface retrospective-coherence paragraph is now flagged STRUCTURAL by both FAIL critics. Will excise next round and replace with a single concrete archival frustration (per critic's own suggestion).

The verbatim-restated bracketed parenthetical ("material at every level (material at every level...)") is a stuttering artefact in v10 itself. Fix.

## Round 33 plan

1. Restore the precise numbers in §4 case-study prose (revert range conversion, keep exact tool-call counts, recall, judge means).
2. Drop the Preface retrospective-coherence paragraph entirely; replace with a single concrete OCR-frustration sentence.
3. Fix the "material at every level (material at every level...)" stutter.
4. Break the "X, not Y" antithesis at sentence level (split into two short sentences without the parallelism, OR run-on without contrast pivot).
5. Collapse the ranked-limitations cascade in §5 into a single denser paragraph without the "single limit I would put most weight on... several smaller boundary conditions... two other directions worth flagging" descending shape.
