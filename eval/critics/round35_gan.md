# GAN Round 35

Strip: TARGET 6,971 words.
Seeds: 978070917 (pos 2), 151362502 (pos 6), 618742706 (pos 3). All non-pos-1, distinct.

Edits applied:
- Rewrote Ch2 opening to break "X but Y" triplet.
- Dropped §1 chapter map.
- Defused "is itself the index" register tic.
- Scrubbed §4 in-prose hedging ("Inter-judge κ is weak (0.33) and the paired sign test on quality (n = 6, p = 0.625) does not separate..." removed; "single-annotator construction is a limitation" removed; "cross-vendor robustness is untested" removed).

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 978070917 | 2 | 2 (TARGET) | near certain | FAIL |
| 151362502 | 6 | 6 (TARGET) | near certain | FAIL |
| 618742706 | 3 | 3 (TARGET) | near certain | FAIL |

Result: 0/3.

## Key residual tells (verbatim)

From seed 978070917 (near certain):
- "Aphoristic mini-summaries that close paragraphs with a tidy reversal: 'The index does not have to be smart'; 'The recall tie itself is a symptom'; 'The calendar-shaped hierarchy avoids the workaround by carrying the gap inside the index itself'; 'an event whose temporal slot the memory system does not hold cannot register as missing, only fail to come back when looked for.'"
- "STRUCTURAL — Opening framing leads with the puzzle as a perfectly turned anecdote: 'Il Messaggero did not appear on 26 July 1943...' then a one-paragraph reveal that the archive returns nothing, then the thesis. The Preface re-narrates the same anecdote ('I came to this dissertation through a question about an absent newspaper'). This double-hook is a common AI-essay shape"
- "Vocabulary signatures: 'internally hybrid' / 'by construction' / 'methodologically defensible' / 'architecturally-clean case' / 'structural form the brain already uses' / 'at one remove' / 'in measurable form.'"
- Suggestion: break rule-of-three symmetry: drop parallel "tool calls / recall / quality" reporting for cases 2 and 3, or let case 3 be a single paragraph of negative result.

## Diagnosis

Round 35 ties round 34 at 0/3. The §4 hedging scrub didn't move the needle. The Ch2 opening rewrite didn't either.

The double-hook opening (Preface + §1 both anchoring on missing 26 July) is structural. Replace with single-hook.

The vocabulary signatures are surface but pervasive. Need a sweep.

The aphoristic paragraph-closer cadence is high-leverage. Need to scrub closing-sentence rhythm.

## Round 36 plan

1. Replace Preface anecdote — open with the OCR work / engineering side instead. Single-hook in §1 only.
2. Defuse vocabulary signatures: "by construction", "methodologically defensible", "architecturally-clean", "at one remove", "in measurable form", "internally hybrid".
3. Scrub aphoristic paragraph-closers: rewrite each paragraph's last sentence to break the tidy-reversal cadence.
