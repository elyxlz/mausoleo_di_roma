# GAN Round 51

REVERTED v10 to round 49 snapshot (commit 57adb34) before applying R51 edits, per Pareto branching rule (R50 regressed 1/3 -> 0/3).

Strip: TARGET 6,177 words.
Seeds: 884245850 (pos 6), 695192394 (pos 2), 298874268 (pos 3).

Edits applied (per round51_plan.md):
- Defused §4 "X either A, or B, or C" trifurcated counterfactual to a two-clause sober statement ("No editorial line on the deposition was available in time, and an issue without one would have had no plausible front page").
- Rounded 0.89878 -> 0.90 inline; replaced explicit weight tuple "0.40 / 0.25 / 0.15 / 0.10 / 0.10" with "the exact weight breakdown sits in Appendix A".
- Rounded 0.0165 -> "roughly 0.016" inline.
- Added Appendix A (after References) containing: explicit weight tuple, leave-one-out pointer, and the per-cell variance note (moved from main body, with concrete W29 attribution and seed-pinned re-run failure phrased as engineer's confession).
- Kept R49 Preface struggle paragraph and R49 §2.3 changes (these are the R49 1/3 PASS baseline).

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 884245850 | 6 | 6 (TARGET) | near certain | FAIL |
| 695192394 | 2 | 9 (2022SMMH0 — Artificial Creativity) | lean toward | PASS |
| 298874268 | 3 | 3 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at non-pos-1 (PASS at pos 2). TIES BEST_GAN at 1/3 (rounds 21/23/24/30/32/33/37/38/45/47/48/49/51).

## High-leverage tells flagged (FAIL seeds)

Seed 884245850 (pos 6, near certain):
- "**signature parallel-triplet/balanced-antithesis cadence**" — *"questions for which articles exist and is awkward for the others the corpus invites"*; *"holds those resolutions or asks the researcher to hold them"*; *"the gap is already inside the index"*.
- "**'with X' appositive tic**" at sentence tails — *"with the leaf level holding paragraphs..."*; *"with date as a facet on the side"*; *"with the structural information available to it"*.
- "**pre-emptive concession-and-recovery framing**" — *"How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested"*; *"A direct head-to-head on Impresso is the obvious experiment but is gated on language"*; *"the recall tie does not separate the systems on this case"*.
- "**suspiciously clean numerical results with no messiness**" — *"Across eighteen scored trials the system averaged 11.3 tool calls against the keyword baseline's 28.3"*; *"a composite of 0.90"*; *"recovered forty-eight of fifty top named entities"*. Round-to-0.90 did NOT defuse this; the composite-of-numbers gestalt remains the tell.
- "**Italian summary insertion as ornament**" — block-quoted Italian summary read as fabricated.
- "**Preface that is too on-thesis**" — autobiographical arc maps perfectly onto dissertation moves; Bartlett-second-year + Eichenbaum-later flagged again.
- READS-HUMAN: "OCR composite-score discussion has welcome ugliness — the failed post-correction pass... and the admission that a single post-processing filter outperformed model additions feel like real engineering memory rather than generated narrative".

Seed 298874268 (pos 3, near certain):
- "**balanced antithesis with semicolon hinges**" — *"In Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge of the regime change"*; *"That template handles questions for which articles exist and is awkward for the others the corpus invites"*.
- "**'not X, Y' / 'less X, more Y' antithesis tic**" — *"What the interface cannot do is register that the absent day is part of the corpus's testimony"*; *"the failure mode here is at the level of the data model itself, which holds only article-shaped slots and no slots for dates as such"*.
- "**puzzle-as-cute-paradox abstract opening**" — absence-as-evidence hook flagged as canonical LLM essay-arc move.
- "**aphoristic closers ending sections**" — *"Article-touching cannot score a question whose answer is an issue that does not exist"*.
- "**hedged meta-commentary**" — same as seed 884 critic, pre-emptive limitations-hedging mid-argument flagged.
- "**vocabulary signature: 'lineage,' 'the picture,' 'the substantive lesson,' 'the pay-off'**" — cohort-uncommon abstraction nouns clustered.
- "**suspiciously clean tripartite enumeration framing**" — *"Three literatures and a corpus"*; *"Three systems define the field"*; *"Three case studies"*; *"Three loosely coupled stages"*. The "three X" framing recurs at every structural level.
- "**'X or Y. Z none'** terse three-beat pattern" — *"the interface either holds those resolutions or asks the researcher to hold them. A flat keyword search holds none."*
- READS-HUMAN: "The OCR-pipeline section's specific failure honesty... has the texture of someone who actually ran the experiment and got burned. Keep that grain."

Seed 695192394 (pos 2, **PASS** at lean-toward — picked Essay 9, real "Artificial Creativity" 2022SMMH0):
- The critic CITED Essay 2's preface (TARGET) approvingly: *"Compare Essay 2's preface ('Two weeks went into a post-correction pass that turned out to make composite OCR scores worse rather than better') with Essay 9's 'Having studied various related subjects including Computer Science, Psychology, and Philosophy throughout my degree...' The latter is genericized résumé prose."* The R49 Preface struggle detail that R50's PASS critic flagged as LLM-constructed is now LANDING AS HUMAN under this seed. Cohort-mirroring works for some critics, fails for others.
- The critic also approvingly used Essay 2 as a positive structural exemplar: *"Essay 2's 'missing 26 July' deep case + two shorter cases is the exemplar — one primary investigation carries the argument; secondary cases ratify it."*

## Round 52 plan (PRELIMINARY — to be detailed in round52_plan.md)

R51 ties BEST_GAN. Two of three critics still flag near-certain; the dominant tells span SURFACE (parallel-triplet/balanced antithesis with semicolon hinges, "with X" tail, "not X, Y" antithesis, "three X" enumeration) and STRUCTURAL (pre-emptive concession-and-recovery, aphoristic section closers).

PRIMARY (highest leverage across both FAIL seeds): defuse the "three X" tripartite enumeration framing at its FOUR structural occurrences (chapter 2 opener "Three literatures and a corpus", §2.1 "Three systems define the field", chapter 4 "Three questions are put", chapter 3 opener "Three loosely coupled stages"). Both critics flagged this independently, and the cluster is unique to TARGET in the cohort.

SECONDARY: scrub the most-flagged surface tics — the semicolon-hinged balanced antithesis at three explicit instances (abstract sentence 2; chapter 4 missing-26-July paragraph; missing-26-July closer "in Mausoleo's case the answer is grounded..., in the baseline's it leans...").

TERTIARY: kill ONE pre-emptive concession in chapter 5 ("How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested") — leave the limitation as an open question rather than a defused-and-recovered move.

QUATERNARY (only if word-budget permits): defuse the "with X" appositive at the chapter 1 thesis sentence and the abstract closer.

EXCLUDE: do NOT touch the OCR composite-score "ugliness" or the Preface struggle paragraph — both flagged as positive READS-HUMAN signal across multiple critics.
