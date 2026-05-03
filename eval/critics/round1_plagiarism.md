# Phase 3 Round 1 — Plagiarism critic verdict

**Target.** `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v1.md` (483 lines, 8 chapters).
**Date.** 2026-05-03.
**Method.** PAN-2025 / PlagBench discourse-feature pattern per `~/.claude/skills/essay-iter/plagiarism_prompt.md`. Sampled paragraph-by-paragraph; spot-checked verbatim residue against the cited PDFs in `/tmp/mausoleo/references/papers/` (149 files across 5 disciplines); cross-checked the four Italian-language quoted spans against the system's own generated summaries in `/tmp/mausoleo/eval/summaries/`. Author's own scaffolds (`lit_review/`, `eval/case_studies/RUNLOG.md`, `eval/autoresearch/program.md`, `references/section_*.md`) treated as self-overlap, not plagiarism.

---

## 1. Per-flag table

| # | Span | Issue type | Severity |
|---|------|------------|----------|
| 1 | §2.2 L75 — "the move from juridical-evidentiary custody to active mediation" attributed to Cook (2013) | Compression of source: Cook's actual schema is FOUR paradigms ("juridical legacy → cultural memory → societal engagement → community archiving") with archivist roles "passive curator → active appraiser → societal mediator → community facilitator". Draft collapses to 2-stage move. Captures direction faithfully but elides the intermediate paradigms. Voice/discourse: writer's own. No verbatim residue. | LOW |
| 2 | §6.3 L217 — "BIECO FUREORE BRITANNICO" Italian quote (typo: FUREORE for FURORE) | Quotation taken from corpus headline; not present in any cited secondary source. Likely OCR-preserved verbatim from *Il Messaggero* 25-Jul-1943; author should add a parenthetical "(OCR sic; corpus headline, 25-Jul-1943)" so the reader doesn't read it as a writer typo. Not plagiarism, but a discourse-feature smell-test. | LOW |
| 3 | §4.3 L153 — "Thomas et al. (2024) report a 23.3% character-error reduction with BART fine-tuning and a 54.5% reduction with Llama-2 13B prompting on the BLN600 nineteenth-century English-newspaper benchmark" | Source verified: Thomas 2024 Table 1 µ-CER = 0.0840 (test split); reductions exactly 23.30% (BART) and 54.51% (Llama 2 13B). Numbers grounded; paraphrase faithful. | (verified, no flag) |
| 4 | §4.3 L155 — "1910 wCER of 0.083 sits in the same order as Thomas et al.'s (2024) BLN600 raw 0.084 baseline" | Verified against Thomas 2024 Table 1 (test µ-CER 0.0840). Comparison legitimate. | (verified, no flag) |
| 5 | §6.2 L211 — Italian block quote (~80 words) "[edizione assente: il fondo archivistico digitalizzato non contiene il numero del 26 luglio 1943 ..." | Verbatim match against `/tmp/mausoleo/eval/summaries/day/1943-07-26.json` `summary` field. Framed in draft as "its summary, generated at index-build time, is the answer to the question:" → SELF-AUTHORED system output, properly attributed by framing. Indented as block quote. Compliant. | (verified, no flag) |
| 6 | §5.3 L185 + §6.3 L221 — W29 prolepsis quote "Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini" | Verbatim match against `/tmp/mausoleo/eval/summaries/week/1943-W29.json`. §5.3 attribution: "the summariser adds an explicit prolepsis: ..." — clean. §6.3 attribution: "the week-of-25-July summary ... the summary closes ..." — clean. Both framings identify the system's own summariser as source. Compliant. | (verified, no flag) |
| 7 | §5.3 L185 — "strenuo valore", "spontanea offerta dei soldati germanici" | Verbatim match against day-25-Jul summary (which itself preserves the source paper's regime register). Framed parenthetically as register samples ("late-fascist register intact (...)") — discourse role is illustrative quotation of source register. Author should add a one-line footnote noting these are corpus quotations of *Il Messaggero* preserved through the summariser; current framing is sufficient but borderline. | LOW |
| 8 | §6.5 L201 — Pavone (1991), Murialdi (1986), Bosworth (2005), Deakin (1962) named as historiographical works against which the relevance GT was hand-annotated | Citations are reference-set declarations only; no claims paraphrased from any of the four works. PDFs verified present in `/tmp/mausoleo/references/papers/historiography/`. No paraphrase plagiarism risk because no paraphrase exists. Citation legitimately frames the GT-annotation methodology. | (verified, no flag) |
| 9 | §2.2 L71 — RAPTOR / GraphRAG / PageIndex paraphrases | Cross-checked against Sarthi 2024 abstract and §3 ("recursively clusters chunks of text based on their vector embeddings and generates text summaries"); Edge 2024 §2.1 (Leiden community detection, hierarchical community summaries). Draft's paraphrases ("recursively clusters and summarises chunk embeddings bottom-up to induce a tree"; "extracts an entity-relation graph from a corpus, runs Leiden community detection over it, and produces hierarchical community summaries") are faithful, original phrasing, no verbatim residue. | (verified, no flag) |
| 10 | §2.1 L63 — "transparent generosity" attributed to Düring et al. (2024) | Verified: Düring et al. 2024 article title is "Transparent generosity. Introducing the impresso interface...". Quote marks + author + year present. | (verified, no flag) |
| 11 | §4.2 L145 — "+0.013 composite contribution attributable to cross-family diversity"; §3.1 L103 — "cross-family diversity buys roughly +0.013 of composite score" | Grounded in author's own `references/section_4_ocr_data.md` and `eval/autoresearch/program.md` L355 ("+0.013 stacked. Different pre-training, different error patterns → orthogonal coverage. 1885 wCER 0.182→0.149"). Self-overlap, fine. | (verified, no flag) |
| 12 | Voice consistency across draft | Single coherent voice throughout: long em-dashed sentences, lower-case §/sub-§ refs, qualified hedging ("the modest one", "not statistically decisive at this sample"), repeated rhetorical move of (claim → counterclaim → resolution). No paragraph reads in a noticeably different register. No paraphrase-tool seams (no awkward synonym swaps, no broken collocations, no register breaks). | (verified, no flag) |

## 2. Total flags by severity

- CRITICAL: 0
- HIGH: 0
- MED: 0
- LOW: 3 (Cook compression; FUREORE OCR-sic; corpus-quotation footnote for §5.3 register samples)

## 3. Overall verdict

**PASS.** No MED or higher flags. All four Italian quoted spans are properly framed as system-generated summary output and attributed to the index-build-time summariser. All technical-numerical claims spot-checked (BLN600 0.084, Thomas 23.3%/54.5%, RAPTOR/GraphRAG paraphrases, +0.013 cross-family stack) are grounded in their cited sources or in the author's own scaffolds. Historiography citations (Pavone, Murialdi, Bosworth, Deakin) make no paraphrase claims, so no misattribution risk. No verbatim residue ≥10 contiguous content words from any cited PDF. Voice is uniformly the author's.

## 4. Specific edits

The three LOW flags do not block submission. Optional polishes if the author wants the draft to be airtight under a strict reviewer:

1. **Cook 2013 paraphrase tightening (§2.2 L75).** Either expand to name all four paradigms, or hedge: replace "what Cook (2013) describes as the move from juridical-evidentiary custody to active mediation" with "the trajectory Cook (2013) traces from juridical-evidentiary custody towards active mediation (compressing his four-paradigm schema)". One-clause fix.

2. **OCR sic on FUREORE (§6.3 L217).** Replace `"BIECO FUREORE BRITANNICO"` with `"BIECO FUREORE BRITANNICO" (OCR sic, *Il Messaggero* 25-Jul-1943)`. Prevents a reviewer from reading it as a writer typo.

3. **Corpus-register footnote (§5.3 L185).** After "(\"strenuo valore\", \"spontanea offerta dei soldati germanici\")" add a parenthetical "(verbatim from the day-25 summary, itself preserved from the *Messaggero* original)". Two-second edit; nothing material at stake.

Submission-ready: yes.
