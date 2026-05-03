# GAN Round 52

Strip: TARGET 6,177 words (after edits, before revert). Stripped from a v10 with 7,077 words.
Seeds: 451976793 (pos 3), 270693846 (pos 2), 142987776 (pos 4).

Edits applied (per round52_plan.md, BEFORE the revert):
- Renamed Ch2 heading "Three literatures and a corpus" -> "The literatures and the corpus".
- Reworded §2.1 opener "Three systems define the field" -> "The major systems in the field at the time of writing are *Chronicling America*, *Europeana Newspapers* and *Impresso*".
- Reworded abstract "Three questions are put to *Il Messaggero*" -> "The case studies put a series of questions to *Il Messaggero*".
- Reworded Ch1 closer "Three case studies on the July 1943 material" -> "Case studies on the July 1943 material".
- Restructured Ch3 opener "Three loosely coupled stages of Mausoleo connect through..." -> "Mausoleo runs as a loosely coupled pipeline. An OCR stage..., a recursive summariser..., and a small JSON-emitting command-line interface...".
- Replaced §4 missing-26-July aphoristic closer "Article-touching cannot score a question whose answer is an issue that does not exist, so the recall tie does not separate the systems on this case" with "The recall tie does not separate the systems on a question whose answer is an absent issue".
- Replaced Ch5 final aphoristic closer "An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it" with "What this design does not test is how a human reader engages with such an interface; that question would need a separate study with human subjects, and is left for follow-up work".

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 451976793 | 3 | 3 (TARGET) | lean toward | FAIL |
| 270693846 | 2 | 2 (TARGET) | lean toward | FAIL |
| 142987776 | 4 | 4 (TARGET) | near certain | FAIL |

Result: 0/3 PASS. REGRESSED from R51's 1/3.

PER PARETO RULE: REVERTED v10 to R51 snapshot (commit 967807f). Round 53 will branch from R51 baseline with a DIFFERENT move (excluding the Ch5 closer rewrite that introduced the duplicate-hedge tell).

## Mixed signal: confidence dropped on two seeds

Although the PASS count regressed, two of three FAIL critics dropped confidence from near-certain to lean toward — softening that R51 did not produce. The tripartite-enumeration scrubs may have helped at the surface level, but the new Ch5 closer "What this design does not test is how a human reader engages..." was IDENTICAL TO an existing Ch5 mid-paragraph hedge "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested" — flagged by all three critics as a duplicate-statement tell.

This is a clear unforced error. The new closer must be replaced with something that does NOT echo the existing mid-paragraph hedge.

## High-leverage tells flagged (all three FAIL seeds)

ALL THREE seeds independently flagged the duplicate "human reader" hedge:
- Seed 451976793: "*The same hedge appears twice in different phrasings — a tell of LLM revision passes.*"
- Seed 270693846: "*The double-statement of the same limitation in two registers is a giveaway — and the pre-emptive hedging is characteristic.*"
- Seed 142987776: "*These appear twice in near-identical form within the same chapter — a redundancy a human editor would catch.*"

Other high-leverage tells (in common with R51):
- Semicolon-balanced antithesis (still flagged)
- "not X, Y" / "not X but Y" antithesis tic (still flagged)
- Aphoristic single-sentence paragraph closers — *"A flat keyword search holds none"*; *"The reasoning sits in the agent"*. (Note: the closer-defusion in §4 and Ch5 did not catch the §1/Ch3 closers.)
- Suspiciously clean numerical specificity in rhetorical packets (still flagged)
- "Take X first / A second strand / On the neural side / Cognitive-offloading work then closes the picture" — four-beat structural enumeration with discourse markers (NEW high-leverage flag from seed 270693846)

NEW STRUCTURAL TELL FROM SEED 270693846: lack of front-matter clutter — *"Every other essay has a TOC, list of abbreviations, glossary, or visible bibliography fragments. Essay 2 has none of this scaffolding despite being a 'BASC0024 Final Year Dissertation.'"* This is a cohort-mismatch tell. NOTE FOR FUTURE: the strip script removes the references section; v10 has a real reference list but the strip drops it. Could try preserving a fragment of references in the stripped version, or adding a TOC fragment to v10.

READS-HUMAN signals confirmed across all three FAIL critics:
- OCR composite ugliness (post-corrector "modernises good articles into paraphrases" + 0.6-1.1 composite cost)
- Specific numbers like 0.872 vs 0.926, 0.013, 0.016 (lab-notes texture)
- Italian summary block (one critic explicitly cited this as positive)
- R49 Preface struggle paragraph (one critic explicitly cited this as positive)

## Round 53 plan (PRELIMINARY)

R52 surfaced one big mistake (duplicate Ch5 closer hedge) and a NEW STRUCTURAL TELL (lack of front-matter cohort scaffolding).

PRIMARY: starting from R51 baseline, REMOVE the existing Ch5 mid-paragraph "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested" hedge entirely (rather than echoing it) — let the design's silence on human-subjects studies speak for itself.

SECONDARY: defuse the four-beat "Take X first / A second strand / On the neural side / Cognitive-offloading work then closes the picture" enumeration in §2.3 (Memory, hierarchy and external structure). The discourse-marker chain is a textbook LLM organisational tic. Rewrite to flatten the discourse markers — drop "Take... first", "A second strand", "Cognitive-offloading work then closes the picture".

TERTIARY: re-attempt the tripartite-enumeration scrubs from R52 (these were neutral on confidence and may help at the margin, just without the Ch5 closer error).

EXCLUDE: the new Ch5 closer rewrite from R52 (caused the duplicate-hedge tell).
