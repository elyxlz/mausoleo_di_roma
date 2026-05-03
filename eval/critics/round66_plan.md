# Round 66 plan (deep-review-and-taste)

## 1. Deep re-read (§1 closer paragraph)

R61 BEST_GAN baseline, Ch1 paragraph 4 (line 31):

> A separate but converging line of research, from Tolman's (1948) spatial cognitive-map experiments to Eichenbaum (2017) on the hippocampal integration of space, time and conceptual relation, suggests that the same neural machinery handles hierarchical structure across these domains. Whittington et al. (2020) modelled the circuit as a general-purpose relational learner. The relevance for an archival interface is direct enough: the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form. **When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search holds none.**

The bolded sentence does two things:
(a) sets up a binary "either/or" about where multi-resolution structure lives (interface vs reader),
(b) tags the keyword baseline as the "neither" case via the terminal coda "holds none".

Both R65 critics 182886936 and 76069949 named this sentence as the high-leverage tell of §1. The "either X or Y, and Z" cadence + the punchy three-word coda are the specific shapes flagged.

## 2. Synthesis of R63–R65 universal tells

UNIVERSAL across R63, R64, R65 (cited by every seed):
- Balanced-antithesis-with-semicolon (e.g. para 1 sentence 4 of abstract; this §1 closer)
- Aphoristic single-sentence closers / short-clause terminal coda
- Self-referential meta-commentary ("the substantive cognitive-science claim the dissertation rests on")
- Parallel-triplet scaffolding ("paragraph in article in issue in day in week in month")

COHORT-VARIANCE (cited by 1–2 seeds, not all):
- Specific numeric pile (11.3 vs 28.3, κ values)
- Italian summary block
- Asymmetric chapter-4 case weighting

PRESERVE LIST (R61 PASS critics praised):
- Asymmetric case weighting (one deep + two shorter contrasts)
- Technical-detail texture in Ch1 thesis sentence
- Preface OCR struggle paragraph
- Italian summary

## 3. Cohort exemplar reference (taste)

2018SKYS9 §1: "Even though art appreciation has been broadly understood as a complex multi-modal experience, recent decades have seen the rise of digital documentation of art..." — long compound sentences without "either X or Y, and Z" coda construction.
2019YPGT5 §1: "Even though Spanish films are a key element in Spanish culture, they have not yet been studied in depth in their entirety..." — same pattern, no balanced coda.

Real cohort prose builds clauses additively, not in parallel-with-terminal-punch.

## 4. Candidate moves with prose-quality assessment

### Candidate A — pure deletion of closer coda

REPLACE:
> When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search holds none.
WITH:
> When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them.

**Prose-as-prose:** acceptable but the "either X or Y" clause is itself flagged by 182886936 as a balanced tic ("X either A or, failing that, B" register). Removing only the coda leaves the binary still in place.
**Argument integrity:** preserved (the keyword-baseline implication is recoverable from the next paragraph).
**Reads-human preserves:** OK.
**Downstream:** none.
**Risk of same-class tell:** medium — the surviving "either X or Y" is itself a flagged shape.

### Candidate B — defuse to flat declarative (recommended)

REPLACE the same sentence WITH:
> A researcher reading an archive at several resolutions therefore needs to hold those resolutions somewhere; the interface can do it, or the reader is left to do it mentally on top of a flat list.

**Prose-as-prose:** somewhat improved — uses an additive "therefore needs… somewhere" structure rather than a balanced binary. The semicolon clause is still parallel-ish but no longer has the punchy three-word coda; it ends on a long descriptive clause.
**Argument integrity:** preserved.
**Reads-human:** uses "therefore" as a connective which is more academic-essay register than rhetorical-balanced.
**Downstream:** none.
**Risk of same-class tell:** the semicolon-balanced shape is still flagged elsewhere ("Questions about… return tens; questions about… return hundreds"). Risk medium-high.

### Candidate C — pure deletion of the entire sentence

REPLACE the same sentence WITH:
> *(deleted)*

The paragraph then ends on "the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form."

**Prose-as-prose:** the natural follow-on is now the next paragraph "This dissertation builds and tests an interface that does hold them." — the "them" referent ("multi-resolution hierarchical structure") is preserved by the prior sentence. Reads cleanly.
**Argument integrity:** preserved. The next paragraph's first sentence ("This dissertation builds and tests an interface that does hold them.") carries the implied contrast.
**Reads-human:** very clean. No same-class tell can be introduced because nothing replaces the deleted sentence.
**Downstream:** the next paragraph's opening "This dissertation builds and tests an interface that does hold them." was previously preceded by the deleted sentence's "either holds those resolutions or asks the researcher to hold them" — so "does hold them" still has clear referent (multi-resolution hierarchical structure from the prior sentence).
**Risk of same-class tell:** none. R56–R59 lesson confirms pure-deletion is the safest.

### Candidate D — fold both Ch1 paragraph 4 and 5 closer into one

This is a multi-edit move that violates "single primary move per round". Skipping.

## 5. Decision

**Pick Candidate C — pure deletion of the §1 paragraph 4 closer sentence.**

Scoring:
- prose-as-prose: best (no replacement risk, paragraph cadence preserved)
- argument integrity: preserved (next paragraph carries the contrast)
- preserves: untouched (asymmetric case weighting, Ch1 thesis texture, Preface, OCR, Italian, Ch5 closer)
- no same-class tell introduced (R57 lesson)
- targets the EXACT high-leverage tell flagged by 2 of 3 R65 critics

## 6. Predicted downstream effect

Para 4 of §1 ends:
> The relevance for an archival interface is direct enough: the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form.

Para 5 begins:
> This dissertation builds and tests an interface that does hold them.

The "them" referent is "multi-resolution hierarchical structure" from the preceding sentence — coherent. The cohort-mirror "puzzle-first" signal that R61 PASS critics liked is preserved (the missing-26-July hook remains the dominant Ch1 motif).

## 7. Fallback (R67)

If R66 ties at 2/3 (matches R61): try defusing the next universal aphoristic closer "the gap is already inside the index" (§4 closer) by folding into preceding sentence.

If R66 regresses: revert to R61 (420027e), try Candidate B in R67.
