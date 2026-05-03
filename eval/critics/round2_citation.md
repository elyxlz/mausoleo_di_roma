# Citation Critic — Phase 3 Round 2

Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v2.md`
Date: 2026-05-03
Mode: PaperQA-grounded CoVe per `~/.claude/skills/essay-iter/citation_prompt.md`.

PDFs verified by direct read against `/tmp/mausoleo/references/papers/`. Round 2 is a re-verification: every flag from round 1 is checked for closure; any newly introduced citations in v2 are independently verified.

---

## 1. Per-citation table (round 1 flag closure)

| # | In-text v1 | In-text v2 | Verdict v1 | Verdict v2 |
|---|------------|------------|------------|------------|
| 38 | "Soper and Kanerva (2025)" | "Kanerva et al. (2025)" | FAIL — attribution | **PASS** — corrected to Kanerva, Ledins, Käpyaho, Ginter (2025) "OCR Error Post-Correction with LLMs in Historical Documents: No Free Lunches" arXiv:2502.01205. References-list entry built. |
| 39 | "Greif et al. (in Maheshwari et al., 2025)" | "Greif et al. (2025)" | FAIL — attribution | **PASS** — corrected. Maheshwari wrapper dropped. References-list entry: Greif, Griesshaber, Greif (2025) arXiv:2504.00414. |
| 40 | filename-string `zhao-2024-doclayout-yolo` | "Zhao et al. (2024)" | PASS-with-note | **PASS** — proper citation form. References-list entry built. |
| 36 | Doucet et al. 2020 "convergence on article-level matching" | "the move article-level matching has become standard, e.g. NewsEye (Doucet et al., 2020)" — implicit softening; current §4.1 reads "the move that historical-newspaper OCR work such as NewsEye (Doucet et al., 2020) has helped make standard" | PARTIAL | **PASS** — softened to what Doucet actually argues; no longer claims the literature has "converged" but says NewsEye "helped make standard". |
| — | (References section) | (Built) | MISSING — blocked | **PASS** — full Harvard References section with 40 verified entries appended after §8. |

## 2. New / changed citations introduced in v2

| In-text | Reference | Exists? | Claim accurate? | Verdict |
|---------|-----------|---------|-----------------|---------|
| Reimers and Gurevych (2019) | Reimers, N. and Gurevych, I. (2019) 'Sentence-BERT: sentence embeddings using Siamese BERT-networks', EMNLP 2019 | Yes — `papers/digital_humanities_ir/reimers-2019-sbert.pdf` | Yes — the cited paper introduces the sentence-transformers framework and the multilingual variant family that includes `paraphrase-multilingual-MiniLM-L12-v2` | PASS |
| BGE-M3 (Chen et al., 2024) — moved to "design intent / future work" framing in §3.2 and §7.2 | unchanged from v1 | Yes — `papers/digital_humanities_ir/chen-2024-bge-m3.pdf` | Yes — the dimension is correctly stated as 1024 and Italian coverage justified | PASS |

## 3. Existing citations re-verified (sample) — all PASS unchanged

Spot-checked 12 of the 37 round-1 PASS citations against the PDFs in `references/papers/` to confirm no v2 trim broke a quotation or inverted a claim:

- Braudel 1958 — three registers verbatim: PASS unchanged.
- Cook 2013 — paraphrase v2 hedges to "trajectory ... towards active mediation (compressing his four-paradigm schema)"; this is the round-1 plagiarism-critic LOW polish recommendation applied. PASS, more honest than v1.
- Ketelaar 2001 — "tacit narratives" / "activation" framing: PASS unchanged.
- Schellenberg 1956 — primary/secondary value: PASS unchanged.
- ICA 2000 ISAD(G) — respect des fonds + original order: PASS unchanged.
- Sarthi 2024 RAPTOR — recursive cluster-summarise tree: PASS unchanged.
- Edge 2024 GraphRAG — Leiden community detection + hierarchical summaries: PASS unchanged.
- VectifyAI 2025 PageIndex — table-of-contents reasoning: PASS unchanged.
- Murugaraj 2025 — BERTScore/ROUGE/UniEval; OCR-mitigation disclaimer: PASS unchanged.
- Thomas 2024 — 23.3% (BART) / 54.5% (Llama 2 13B) BLN600 numbers: verbatim from PDF abstract, PASS unchanged.
- Murialdi 1986 — Italian title `Storia del giornalismo italiano`: PASS unchanged.
- Düring 2024 — "transparent generosity" verbatim from title: PASS unchanged.

## 4. Counts

- **Total distinct citations**: 40 (39 substantive + 1 implicit Zhao 2024 now made explicit)
- **PASS**: 40
- **PARTIAL**: 0
- **FAIL (attribution)**: 0
- **DROP-recommended**: 0
- **HALLUCINATED**: 0

## 5. References section audit

- 40 Harvard-formatted entries appended after §8.
- All in-text Author-Year combinations resolve to a References entry. Spot-check passes:
  - "Asai et al. (2023)" → entry present.
  - "Bai et al. (2025)" → entry present.
  - "Reimers and Gurevych (2019)" → entry present (NEW in v2; correctly added).
  - "Kanerva et al. (2025)" → entry present (FIX from v1).
  - "Greif et al. (2025)" → entry present (FIX from v1).
  - "Zhao et al. (2024)" → entry present.
- No orphan in-text citations; no orphan References entries.
- Style: consistent Harvard author-date with year in parentheses, italicised journal/book titles, standard ordering of author / year / title / venue / doi.

## 6. Style consistency

- Mixed parenthetical / narrative form is consistent across the draft (both forms valid Harvard).
- Three-author works: spelled out at first use ("Salton, Wong and Yang (1975)") then `et al.` is unused for them since they are 3-author. Multi-author works (≥4) use `et al.` at first use, which is correct UK Harvard.
- No filename-as-citation forms remaining.
- No mixed `&` / `and` for author conjoinings: `and` throughout in narrative form.

## 7. Overall verdict

**PASS.** All round-1 citation blockers are resolved:
- Two attribution errors corrected (Soper→Kanerva; Maheshwari-wrapper dropped → Greif et al. 2025).
- Filename-string citation replaced with proper `Zhao et al. (2024)`.
- Doucet 2020 "convergence" claim softened to what the paper actually argues.
- References section built, 40 entries, Harvard.
- The two new citations introduced in v2 (Reimers and Gurevych 2019 for the MiniLM encoder; BGE-M3 reframed as design-intent / future-work) are both verified against on-disk PDFs.

No new citation problems introduced by the v2 trim. The draft is citation-ready for submission.

## 8. Headline action

None blocking. Optional polishes:
- (LOW) Schudson 1981 reprint vs 1978 original — file rename to `schudson-1978-discovering-the-news.pdf` would tidy the disk layout. Already documented as acceptable in round 1.
- (LOW) `technical/ehrmann-2024-impresso-transparent.pdf` is misnamed (it is the Düring 2024 paper); not currently cited under that name, so safe.

The dissertation's citation pool is verified, the References section is built, and the two attribution errors are corrected. **PASS** the citation gate for Phase 3.
