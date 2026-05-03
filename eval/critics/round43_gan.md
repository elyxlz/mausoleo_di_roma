# GAN Round 43

Strip: TARGET 6,503 words.
Seeds: 780718832 (pos 2), 886658090 (pos 5), 419721153 (pos 3).

Edits applied:
- Distributed §5 omnibus limitations across §4 setup and §5 (3-trials, single-annotator, vendor, one-month, politically volatile).
- Defused vocab signatures: "instantiates", "substrate", "affordance", "provenance" → behaviour, target, slot, etc.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 780718832 | 2 | 2 (TARGET) | lean toward | FAIL |
| 886658090 | 5 | 5 (TARGET) | near certain | FAIL |
| 419721153 | 3 | 3 (TARGET) | near certain | FAIL |

Result: 0/3, one lean-toward.

## Key signal: another strip-script artifact

Critic seed 780718832 flagged: "Awkward artifact: 'the an open-weight vision-language model backbone is a vision-language model trained for dense document understanding.' This phrasing in Chapter 3 reads like a placeholder substitution gone wrong."

This is the strip-script substituting Qwen2.5-VL → "an open-weight vision-language model" without preceding article rewrite, so "The Qwen2.5-VL" → "The an open-weight". Patched the script.

## Round 44 plan

1. Re-run with patched strip script.
2. Compress §4 cases 2/3 yet further into a single one-paragraph block.
3. Defuse "X is Y" definitional openings in §3 ("Mausoleo is three loosely coupled stages"; "The interaction pattern is closer to a ReAct loop").
4. Drop the abstract/§1/§3 parenthetical-inventory repeat ("(thirty surviving issues, around 6,480 hand-cleaned article transcriptions)" appears in abstract, ch1, ch3).
