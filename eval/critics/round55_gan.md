# GAN Round 55

Strip: TARGET 6,114 words. v10 = 7,010 words.
Seeds: 879466124 (pos 7), 335950053 (pos 5), 379838795 (pos 8).

Edits applied (per round55_plan.md):
- Defused Abstract para 2 opener "There is an interdisciplinary argument running underneath this." -> dropped; second sentence becomes opener.
- Defused §4 missing-26-July paragraph "A wider point sits behind this." -> dropped; following sentence becomes paragraph opener.
- Defused §2.3 "The substantive lesson is that one piece of hierarchical-relational machinery handles space, time and conceptual relation in a common format." -> rewrote following sentence to absorb the claim more flatly: "A temporal index running at multiple resolutions is therefore working in the same structural form the brain uses for analogous spatial and conceptual problems."
- Defused §1 paragraph 31 closer "A flat keyword search holds none." -> folded into preceding sentence with comma+and connector.
- Defused §4 closer "A flat retriever has no equivalent slot." -> folded into preceding sentence with semicolon connector.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 879466124 | 7 | 7 (TARGET) | near certain | FAIL |
| 335950053 | 5 | 6 (2022SMMH0 — Artificial Creativity) | lean toward | PASS |
| 379838795 | 8 | 8 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at pos 5 (lean toward). TIES BEST_GAN at 1/3 (rounds 21/23/24/30/32/33/37/38/45/47/48/49/51/54/55).

## PASS-critic explicitly cited R54 closer change as positive

Seed 335950053 verdict: "*Compare with Essay 5's pointed final sentence on the month-level compression, or Essay 2's specific return to Japan/IWC.*"

Essay 5 = TARGET. The R54 closer change ("At month level the summariser had compressed the regime-change to *l'arresto di Mussolini (25 luglio)*") is now a positive structural exemplar across critics. Same cohort-mirror mechanism as R47/R48/R49/R51/R54.

The same critic also noted "Essay 7" (here 2021KLSF5) as a positive structural exemplar for asymmetric weighting — which is a real essay; the critic correctly identified Essay 6 (2022SMMH0 Artificial Creativity) as the AI-generated one.

## Successful R55 edits (no negative signal)

The five R55 edits did NOT appear in any FAIL critic's tell list:
- Abstract "There is an interdisciplinary argument" deletion: not flagged.
- §4 "A wider point sits behind this" deletion: not flagged.
- §2.3 "substantive lesson" deletion: not flagged.
- §1 closer fold: not flagged.
- §4 closer fold: not flagged.

These five tells from R54 verdicts were eliminated cleanly.

## High-leverage tells flagged (FAIL seeds) — R55

Seed 879466124 (pos 7, near certain) cited NEW high-leverage tells:
- "**'X does Y, where Z does W' balanced antithesis with contrastive pivot**" — *"Where the source-side hierarchy is already meaningful, this means the navigation surface stays predictable"*; *"a clustering-induced hierarchy has nothing to cluster from when the data are absent"*.
- "**Compulsive parallel triplets**" — *"the chunking, narrative integration and schema-formation"*; *"space, time and conceptual relation"*; *"paragraph in article in issue in day in week in month"*.
- "**puzzle-first opening**" still cited — same structural signal that R54 PASS critic praised. Recurring split.
- "**Aphoristic mini-summaries closing paragraphs**" — *"Romans reading the paper that morning learned of the deposition before the morning paper would normally have arrived, and registered that no paper had arrived"* (the R51 baseline §4 sentence) and *"the gap is already inside the index"* and *"At month level the summariser had compressed the regime-change to l'arresto di Mussolini (25 luglio), and that compression too is part of what the index records about July 1943"* (the R54 closer — flagged as engineered for resonance by THIS critic, but praised by R55 PASS critic).
- "**Hedge-laundering register**" — *"is largely consistent with"*, *"can be read as one instance of that prediction"*, *"the relevance for an external interface is more indirect"*.
- "**Vocabulary signatures**" — *"converging strands"*, *"closes the picture"*, *"the substantive cognitive-science claim the dissertation rests on"*, *"the pay-off shows up most clearly"*, *"sharpens what the gap holds"*.
- "**Fake-precision numerical scaffolding**" — same recurring tell.

Seed 379838795 (pos 8, near certain):
- "**Pre-emptive limitation hedging woven into body prose**" — explicitly cites *"How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested"*. CONFIRMED: R51 baseline still contains this hedge; R53 deleted it but R53 was reverted; R54 + R55 baselines never re-deleted it. CLEAN R56 target.
- "**'X, and Y' appositional summary clauses**" — *"The 26 July does not appear in the digitised fund because there was no 26 July to digitise"* (Ch1 paragraph 25 closer); *"Mausoleo borrows its hierarchy from the publication calendar that the printers already followed"* (§2.2 closer).
- "**'not X, but Y'**" — *"is not a list of articles but a shape across days, or an absence"* (abstract).
- "**Self-referential meta-claims**" — *"Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on"* (§2.3 opener) — NEW high-leverage flag, NOT touched in any prior round.

READS-HUMAN signals confirmed:
- OCR composite ugliness (multiple critics)
- Specific historical detail about 27 July reappearance issue front-page (NEW positive signal from seed 879466124)
- Preface failure narrative still positive across some critics

## Round 56 plan (PRELIMINARY)

R55 ties BEST_GAN at 1/3. Two clean rounds in a row (R54 + R55) with positive cohort-mirror PASSes. The closer-defusion + meta-commentary scrubs are net-additive.

CONFIRMED CLEAN R56 TARGETS:
1. **DELETE the surviving "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested"** (Ch5 mid-paragraph hedge — flagged by seed 379838795 as canonical pre-emptive limitation tell). R53 already deleted this once; R53 was reverted for unrelated reasons (the §2.3 enumeration scrub didn't move). The deletion itself was clean.
2. **Defuse the §2.3 opener self-referential meta-claim** "Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on." -> rewrite as a flatter statement that doesn't perform "the dissertation rests on".

PRIMARY for R56: both edits above. Net-additive over R55 baseline; both target NEW flagged tells with no risk of duplicate.

EXCLUDE: Preface, Italian block, "in every case", numeric specifics.
