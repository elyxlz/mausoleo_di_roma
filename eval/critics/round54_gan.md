# GAN Round 54

Strip: TARGET 6,140 words. v10 = 7,036 words.
Seeds: 716465544 (pos 9), 691789533 (pos 8), 500150007 (pos 2).

Edits applied (per round54_plan.md):
- Defused Ch4 opener "The case studies in this chapter ask whether the architectural argument of chapter three makes a measurable difference for a researcher trying to answer real questions about July 1943." -> dropped meta-claim; chapter now opens with "The comparison in all three cases is to a BM25 baseline...".
- Defused Ch2 opener "The literatures the system needs to be read against are several." -> dropped sentence; chapter now opens with the factual second sentence "The dominant access mode in the long line of digital newspaper archives remains the keyword query against an OCR'd full text."
- Replaced Ch5 final closer "An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it." -> "At month level the summariser had compressed the regime-change to *l'arresto di Mussolini (25 luglio)*, and that compression too is part of what the index records about July 1943." (concrete factual closer citing the §3 month-level summariser detail; not a hedge.)

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 716465544 | 9 | 1 (2018SKYS9 — Ghent Altarpiece felt-pastness) | lean toward | PASS |
| 691789533 | 8 | 8 (TARGET) | near certain | FAIL |
| 500150007 | 2 | 2 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at pos 9 (lean toward). TIES BEST_GAN at 1/3 (rounds 21/23/24/30/32/33/37/38/45/47/48/49/51/54).

## PASS-critic explicitly cited TARGET as positive structural exemplar

Seed 716465544 verdict: "*If after that the essay still reads templated, then consider restructuring: lead with the visit to St. Bavo's (the puzzle of the absent panels) rather than with definitional throat-clearing, the way Essay 9 leads with the missing 26 July issue.*"

Essay 9 = TARGET. The R54 chapter-opening defusion (in-medias-res lead) directly produced this positive cohort-mirror signal: TARGET is now the structural exemplar the critic recommends OTHERS adopt. Same mechanism as R47/R48/R49/R51 PASSes.

The PASS critic also picked Essay 1 (real, 2018SKYS9 — Ghent Altarpiece) at lean-toward. Notably, the R54 closer change ("At month level the summariser had compressed the regime-change to *l'arresto di Mussolini (25 luglio)*") was NOT flagged by either FAIL critic, and the new in-medias-res Ch4 opener was NOT flagged by either FAIL critic. The R51 closer (which R52/R53 were trying to fix) is gone, with no new tell introduced.

## High-leverage tells flagged (FAIL seeds)

Seed 691789533 (pos 8, near certain):
- "**em-dash-substitute revelatory cadence with parenthetical gloss-then-extension**" — *"The 26 July does not appear in the digitised fund because there was no 26 July to digitise"*; *"The calendar-shaped hierarchy makes both workarounds unnecessary, since the gap is already inside the index"*. Pervasive surface tic.
- "**antithetical 'X is Y; Z is W' parallel paragraph closers**" — *"In Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge of the regime change"*; *"Article-touching cannot score a question whose answer is an issue that does not exist, so the recall tie does not separate the systems on this case"* — STILL flagged despite R54 closer change at the end of Ch5 (this is the §4 closer, not the Ch5 closer — different one).
- "**suspiciously clean numeric symmetry**" — "preferred by both judges in every case" + "11.3 vs 28.3" still flagged.
- "**'whether or not... while...' hedged-bidirectional construction**" recurs heavily.
- "**meta-commentary about its own argument structure**" — *"There is an interdisciplinary argument running underneath this"*; *"A wider point sits behind this"*; *"The substantive lesson is that..."* (the R53 §2.3 "substantive lesson" was never removed.)
- "**Preface that performs humility-via-specificity in an implausibly neat arc**" — three named pivots mapping to chapter structure.
- "**Italian summary block reads as LLM pastiche**" + "the self-aware confession that the model made up a prolepsis is itself a tell".
- "**Compressed citation-stacking in single sentences**" in §2.3.

Seed 500150007 (pos 2, near certain):
- "**stylized terse-aphoristic closer pattern**" — *"A flat keyword search holds none"*; *"A flat retriever has no equivalent slot"* (paragraph closers in §1 + §4).
- "**'X is Y, and Z' tricolon with abstracted nominalization**" — *"the navigation surface stays predictable to a working historian without depending on extraction quality or a clustering choice"*; *"with its absences"* parenthetical.
- "**puzzle-as-anomaly opening**" cited as canonical LLM "humanities dissertation" register — but this is the SAME structural choice the PASS critic praised. This is the recurring split in the cohort.
- "**hedge-as-throwaway closers and meta-asides**" — *"of course, because the issue does not exist"*.
- "**suspicious vocabulary cluster**" — *"prolepsis", "transparent generosity", "ethos of modesty", "respect des fonds"* sprinkled name-drops.
- "**balanced-pair rhythm at sentence level**" in abstract.
- "**Preface AI tell par excellence — fabricated personal-research narrative with suspiciously clean numbers**" — same tell as seed 691789533.
- "**parenthetical citation-string inserts**" in §4 methodology paragraph.

READS-HUMAN signals confirmed:
- OCR composite ugliness (multiple critics)
- Specific 0.872/0.926/leave-one-out granularity (multiple critics)
- ClickHouse schema specificity (one critic)

## Round 55 plan (PRELIMINARY)

R54 ties BEST_GAN at 1/3 with no new tells introduced (clean tie, unlike R52). The Ch4 + Ch2 chapter-opener defusion landed (no negative signal). The Ch5 closer change landed (no negative signal). The PASS critic explicitly cited TARGET as positive exemplar — same mechanism that produced the R47/R48/R49/R51 PASSes.

The two FAILs converge on:
- Aphoristic single-sentence paragraph closers (§1 "A flat keyword search holds none", §4 paragraph closers)
- Balanced antithesis cadence (saturating)
- Preface "implausibly neat arc" (R49 addition)
- Meta-commentary "There is an interdisciplinary argument running underneath this" / "A wider point sits behind this" / "The substantive lesson is that..."
- Italian summary block (deeply integrated; can't really remove)
- Numeric symmetry "11.3 vs 28.3" + "in every case"

PRIMARY for R55: defuse the §1 aphoristic closer "A flat keyword search holds none." (paragraph 31 closer) by folding into preceding sentence or replacing with a less rhetorically-shaped sentence.

SECONDARY: defuse the abstract paragraph 2 meta-claim "There is an interdisciplinary argument running underneath this." (start of paragraph) — this opens the second abstract paragraph with self-narrating signposting.

TERTIARY: defuse the §4 missing-26-July closer "A flat retriever has no equivalent slot." (mid-§4 paragraph) by folding into a longer sentence.

EXCLUDE: do NOT touch Preface (R50 backfired); do NOT touch Italian block (deeply integrated, removal risks readability); do NOT change "in every case" (factually load-bearing; would be fabrication to remove).
