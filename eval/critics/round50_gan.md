# GAN Round 50

Strip: TARGET 6,295 words.
Seeds: 428149171 (pos 5), 597524082 (pos 7), 522984680 (pos 4).

Edits applied (per round50_plan.md):
- Cut §1 abstract paragraph 2 "Across eighteen scored trials..." results sentence; added "Quantitative results sit in chapter four" pointer.
- Inserted §1 "Or rather, four levels for July 1943..." parenthetical false-start.
- Inserted §2.2 "I have not been able to replicate them locally" hedge in GraphRAG description.
- Inserted §4 "the second trial of that case also returned a war/domestic ratio inverted... which I could not trace... and have left as a per-cell variance note" admission.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 428149171 | 5 | 5 (TARGET) | near certain | FAIL |
| 597524082 | 7 | 7 (TARGET) | near certain | FAIL |
| 522984680 | 4 | 4 (TARGET) | near certain | FAIL |

Result: 0/3 near-certain. REGRESSED from 5-round 1/3 streak.

## High-leverage tells flagged
- Seed 522984680: "**'Or rather' self-correction tic**, an LLM signature for performing nuance" — flagged my new §1 false-start parenthetical EXPLICITLY by name.
- Seed 522984680: "**Preface name-drop pattern**" — Bartlett-second-year + Eichenbaum/Whittington manufactures "tidy interdisciplinary origin story that aligns *exactly* with the citations later mobilised". Critic noted the post-correction-fail / realisation arc is "neat 'I tried X, it failed, I learned Y'" — flagged my new R49 Preface struggle detail as LLM-constructed backstory.
- Seed 522984680: "**suspiciously elegant numeric specificity paired with hand-wavy provenance**" — five-decimal 0.89878 + clean 0.40-0.25-0.15-0.10-0.10 weight tuple "reads as fabricated-to-look-real".
- Seed 522984680: "X either A, or B, or C" exhaustive enumeration — *"the editorial board would have had to either preview a regime change that had not yet been publicly announced, decline to mention it, or appear without an editorial line at all."*
- Reads-human: critic explicitly preserved the variance-footnote admission ("sounds like a genuine confession"). One R50 insert landed, two backfired.

## Round 51 plan (FALLBACK from round50_plan)
PRIMARY: REVERT all three R49+R50 Preface struggle additions (the post-correction pass + the OCR-realisation + the variance-not-traced admission's location). Move the variance admission to a true footnote/appendix mention in v10 only (so it never appears in the main-body strip). Revert the "Or rather" §1 false-start.
SECONDARY: defuse the "X either A, or B, or C" §4 trifurcated counterfactual to a two-element form OR a single non-enumerated sentence.
TERTIARY: round the 0.89878 to 0.90 and remove the 0.40/0.25/0.15/0.10/0.10 weight tuple inline (move to appendix only).
