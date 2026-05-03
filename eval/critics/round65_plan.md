# Round 65 plan (rewritten under deep-review-and-taste directive)

## 1. Deep re-read of affected section (Abstract paragraph 1)

R61 BEST_GAN baseline currently has, in para 1 of the Abstract:

> A digitised newspaper corpus normally allows a historian to retrieve articles by keyword, with date as a facet on the side. **For the July 1943 *Il Messaggero* corpus this dissertation works with, that template handles questions for which articles exist and is awkward for the others the corpus invites.** The morning paper for 26 July 1943 was not printed (the Grand Council had deposed Mussolini overnight and an editorial line could not be drawn in time); a flat article index returns nothing for the date. Questions about the regime-change days of 25 to 27 July return tens of articles that the reader has to assemble; questions about the war-and-domestic balance across the month return hundreds. The dissertation argues that a digital archive ought to respond to questions of these shapes with the structural information available to it, and builds a system, Mausoleo, that does so by storing the corpus as a calendar-shaped tree of recursively summarised nodes over which a researcher agent navigates.

The bolded sentence is the universal R61–R64 tell ("X handles Y and is awkward for Z"). What it does argumentatively: it announces, at the level of an abstract claim, the asymmetry between "questions for which articles exist" and "the others the corpus invites". The next three sentences then enact that asymmetry in concrete terms (one missing morning, the 25–27 July tens, the month-long hundreds). The bolded sentence is therefore an abstract pre-summary of work the next three sentences already do.

## 2. Synthesis of prior 2–3 round verdicts

**Universal tells (flagged in R61, R62, R63 AND R64 verdicts):**
- The "X handles Y and is awkward for Z" antithesis frame in para 1 sentence 2 (target of this round)
- Balanced antithesis throughout the abstract more generally
- Aphoristic single-sentence closers
- "Three questions are put to *Il Messaggero*" tripartite framing in para 2

**Cohort-variance tells (flagged by some critics, not consistently):**
- Specific triplets: "paragraph in article in issue in day in week in month"; "date-bound episode to a few-day narrative to a month-scale schema"
- Particular numeric claims (11.3 vs 28.3); the sign-test references
- Italian-summary block in §4

**Reads-human signals to PRESERVE (cited as positive cohort-mirror):**
- The asymmetric case weighting (deep 26 July case + two shorter contrasts) — Essay 2/9 cohort cite from R61 PASS critic
- The technical-detail texture in Ch1 thesis sentence ("at five hierarchical levels...")
- The Preface OCR struggle paragraph
- The Italian summary block as authentic

**Critical caution (Elio's directive):** The previous agent's candidate
"...returns nothing on dates with no surviving issue, several hundred articles to be classified by hand on aggregate-shape questions, and tens of articles to be assembled by hand on the regime-change days"
swaps an antithesis tell for a triadic-listing tell. R56–R64 verdicts have repeatedly flagged exactly this kind of asyndetic three-clause list as a same-class LLM cadence (R52 "three X" tripartite enumeration; R57 ladder-list-without-Oxford-comma flagged). Refusing the triadic replacement.

## 3. Cohort exemplar abstracts (taste calibration)

- **2019YPGT5** (Spanish Cinema, real, cited as positive cohort by R61 PASS critic): opens with bare topic statement "This paper examines the representation of society in six films released during the Spanish transition to democracy from 1975 to 1982. It does so firstly by examining Spain's historical and political context, then by analysing..." Then enumerates its three film-pairs. **No antithesis frame, no rhetorical setup — direct topic statement and then methodology.**
- **2018SKYS9** (Ghent Altarpiece, real, cited positively by R54 PASS critic): "The Ghent Altarpiece is unique for its important place in art history and for the website Closer to Van Eyck, which documents the process of the 2010-2016 restoration with high-resolution images. Its accessibility as well as their potential to surpass the original artefact in some ways call for a better understanding of the relationship between the digital and the physical." **Direct factual statement about the object, then a "call for" sentence stating the gap.**
- **2020FSXD0** (Kant on Whaling, real): opens with a direct research question: "Can Kant provide an account of universal environmental duties? This question will be tackled in two parts..."

What real cohort abstracts do NOT do: open with "X normally Y. For Z however, X handles A and is awkward for B." That frame is the universal tell.

## 4. Candidate moves with prose-quality assessment

### Candidate A — pure deletion of the antithesis sentence

REPLACE the first two sentences:
> A digitised newspaper corpus normally allows a historian to retrieve articles by keyword, with date as a facet on the side. For the July 1943 *Il Messaggero* corpus this dissertation works with, that template handles questions for which articles exist and is awkward for the others the corpus invites.

WITH just:
> A digitised newspaper corpus normally allows a historian to retrieve articles by keyword, with date as a facet on the side.

Then the paragraph runs straight into "The morning paper for 26 July 1943 was not printed..."

**Prose-as-prose:** improves — removes an abstract pre-summary that the following three sentences already concretise. The opening sentence is a flat descriptive proposition; the next sentence drops the reader directly into a concrete historical fact. Reads like the "direct topic statement, then concrete instance" rhythm of 2018SKYS9 and 2019YPGT5.
**Argument integrity:** preserved. The case-study sentences that follow already establish what the keyword template returns on each question type; the deleted sentence was a redundant high-level pre-summary.
**Reads-human preserves:** the asymmetric-case-weighting structure (one deep case + two shorter contrasts) is preserved untouched in the next three sentences. The technical-texture sentence at the end of para 1 is preserved.
**Downstream effect:** none — single-sentence pure-deletion, no cascade.

### Candidate B — replace with a direct topic-statement opener (2019YPGT5 mirror)

REPLACE the same two sentences with:
> This dissertation builds and tests a hierarchical interface to a digitised Italian-newspaper corpus, the *Il Messaggero* run for July 1943, and asks whether exposing the temporal structure in the index changes how a researcher reads it.

**Prose-as-prose:** competent but slightly conventional. Reads as a direct topic statement, in the 2019YPGT5 register.
**Argument integrity:** preserved.
**Reads-human preserves:** loses the puzzle-first opening that R61/R47 PASS critics liked ("the way Essay 9 leads with the missing 26 July issue").
**Downstream effect:** the specific date-and-question content from para 1 is duplicated in para 2 (where the same questions are listed). Risk: redundancy.

### Candidate C — replace with a research question (2020FSXD0 mirror)

REPLACE the antithesis sentence with:
> Can a hierarchical, calendar-given index improve on a flat keyword index for archival questions whose answers do not sit inside a single article?

**Prose-as-prose:** acceptable but interrogative-opening is rare in the cohort (only 2020FSXD0 does it).
**Argument integrity:** preserved.
**Reads-human preserves:** loses concreteness of the puzzle-first reading.
**Downstream effect:** awkward — the paragraph then pivots from a question to a series of declarative facts about the missing 26 July.

## 5. Decision

**Pick Candidate A — pure deletion.** It scores best on:
- prose-as-prose (removes a redundancy that pre-summarises the concrete next three sentences)
- argument integrity (the deleted sentence is replaceable by what follows)
- preserve list (untouched: asymmetric case weighting, puzzle-first 26 July hook, technical-detail texture, Italian block, Preface, OCR, Ch5 closer, R54 closer)
- no same-class tell introduced (Candidate A is pure-deletion; R57 lesson: replacement scrubs introduce same-class tells)

The replacement-text candidates (B and C) all swap one rhetorical move for another and risk same-class tells. The cohort rule from R56–R59: pure deletion is the safer move when an antithesis sentence is also a redundant pre-summary.

## 6. Predicted downstream effect

The opening pair becomes:
> A digitised newspaper corpus normally allows a historian to retrieve articles by keyword, with date as a facet on the side. The morning paper for 26 July 1943 was not printed (the Grand Council had deposed Mussolini overnight and an editorial line could not be drawn in time); a flat article index returns nothing for the date.

This drops the reader from a flat statement of how the field standardly works into the historical anomaly. The "puzzle-first" cohort signal R61's PASS critic praised is sharpened (not weakened), because the puzzle now arrives in sentence 2 rather than sentence 3. The asymmetric-case-weighting structure is preserved.

Risk (low): a critic might read the bare topic statement + immediate puzzle as "missing thesis statement". Mitigation: the existing thesis-and-system sentence at the end of para 1 ("The dissertation argues that a digital archive ought to respond to questions of these shapes...") is unchanged and supplies the thesis.

## 7. Fallback (R66)

If R65 ties at 2/3 (matches R61): continue with another single pure-deletion of an aphoristic closer (e.g. §1 closer "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed.").

If R65 regresses below 2/3: revert to R61 snapshot (420027e) and try Candidate B in R66.
