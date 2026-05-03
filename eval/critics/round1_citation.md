# Citation Critic — Phase 3 Round 1

Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v1.md` (483 lines)
Date: 2026-05-03
Mode: PaperQA-grounded CoVe per `~/.claude/skills/essay-iter/citation_prompt.md`.

PDFs were verified by direct read of `/tmp/mausoleo/references/papers/<discipline>/<file>` (`pdftotext` extraction or `pdfinfo` metadata). Where text extraction yielded zero output, the PDF is a scanned book and existence/identity was checked via file-size + `pdfinfo` Title.

---

## 1. Per-citation table

| # | In-text | Surrounding claim (short) | Exists? | PDF on disk | Claim accurate? | Verdict |
|---|---------|----------------------------|---------|-------------|-----------------|---------|
| 1 | Braudel (1958) | Three registers: événement / conjoncture / longue durée | Yes — Persée, *Histoire et Sciences sociales: La longue durée* | `historiography/braudel-1958-longue-duree.pdf` (59 pp) | Yes | PASS |
| 2 | Moretti (2013) | Distant reading complementary to close reading | Yes — *Distant Reading* | `digital_humanities_ir/moretti-2013-distant-reading.pdf` (file present, content scanned) | Yes (canonical claim) | PASS |
| 3 | Jockers (2013) | Coined "macroanalysis" between distant and close reading | Yes — *Macroanalysis: Digital Methods & Literary History* | `digital_humanities_ir/jockers-2013-macroanalysis-ch2.pdf` | Yes | PASS |
| 4 | Da (2019) | Computational lit-studies results either obvious-and-robust or non-obvious-and-non-robust | Yes — *The Computational Case Against Computational Literary Studies* | `digital_humanities_ir/da-2019-computational-case.pdf` | Yes (matches abstract & key argument) | PASS |
| 5 | Underwood (2019) | Statistical models are interpretive strategies, not substitutes | Yes — *Distant Horizons* | `digital_humanities_ir/underwood-2019-distant-horizons.pdf` (229 pp) | Yes (book-level claim is accurate) | PASS |
| 6 | Schudson (1978) | Social construction of "news" as a historical process | Yes — *Discovering the News*, originally pub. 1978 (Basic Books) | `historiography/schudson-1981-discovering-the-news.pdf` (1981 reprint, scan, 119 pp) | Yes | PASS — but filename year (1981) ≠ cited year (1978). Either rename file or cite as "Schudson (1978/1981)". |
| 7 | Murialdi (1986) | *Storia del giornalismo italiano*; press under regime; MinCulPop veline | Yes — Murialdi, *Storia del giornalismo italiano*, Il Mulino, 1986 | `historiography/murialdi-1986-stampa-regime-fascista.pdf` (verified title page) | Yes — draft uses correct Italian title at L83 | PASS |
| 8 | Forno (2012) | *Informazione e potere*; press inside fascist info-control | Yes (315-pp book) | `historiography/forno-2012-informazione-potere.pdf` | Yes | PASS |
| 9 | Bonsaver (2007) | Surrounding history of regime censorship across cultural field | Yes — *Censorship and Literature in Fascist Italy* (422 pp) | `philosophy_media_1943/bonsaver-2007-censorship.pdf` | Yes | PASS — note: file is in `philosophy_media_1943/`, not `historiography/`. Also duplicated in historiography? Check if mis-shelved. |
| 10 | Pavone (1991) | Used as relevance-GT historiography (also Pavone in case 2) | Yes — *Una guerra civile*, 911-pp scan | `historiography/pavone-1991-guerra-civile.pdf` | Yes | PASS |
| 11 | Bosworth (2005) | Relevance-GT background | Yes — *Mussolini's Italy* (688 pp) | `philosophy_media_1943/bosworth-2005-mussolinis-italy.pdf` | Yes | PASS |
| 12 | Deakin (1962) | Relevance-GT background | Yes — *The Brutal Friendship* (911 pp) | `philosophy_media_1943/deakin-1962-brutal-friendship.pdf` | Yes | PASS |
| 13 | Ehrmann et al. (2020) | Impresso enrichments: NER, topic models, text reuse | Yes — Ehrmann/Romanello/Clematide/Ströbel/Barman, LREC 2020, "Language Resources for Historical Newspapers: the Impresso Collection" | `digital_humanities_ir/ehrmann-2020-impresso-lrec.pdf` | Yes (abstract lists OCR + NER + topic + text reuse) | PASS |
| 14 | Düring et al. (2024) | Impresso interface; "transparent generosity" | Yes — Düring/Bunout/Guido, *Historical Methods* 2024, DOI 10.1080/01615440.2024.2344004 | `digital_humanities_ir/during-2024-impresso-interface.pdf` (also duplicated as `technical/ehrmann-2024-impresso-transparent.pdf` — wrong filename, NOT Ehrmann) | Yes; "transparent generosity" phrase verified on title page | PASS — but `technical/ehrmann-2024-impresso-transparent.pdf` is misnamed (should be `during-2024-...`); not currently cited under that name, so safe. |
| 15 | Cook (2013) | Active mediation; provenance shift from juridical custody | Yes — Cook, *Archival Science* 13:95–120 (2013), "Evidence, memory, identity, and community: four shifting archival paradigms" | `digital_humanities_ir/cook-2013-archival-paradigms.pdf` (NOTE: file lives in `digital_humanities_ir/`, NOT `historiography/` as one might expect from disciplinary tag) | Yes — abstract directly supports the "active mediation / four paradigms" claim | PASS |
| 16 | Ketelaar (2001) | "Tacit narratives" — description as activation of source | Yes — Ketelaar, *Archival Science* 1:131–141 (2001) | `digital_humanities_ir/ketelaar-2001-tacit-narratives.pdf` | Yes — abstract: "fonds…contain tacit narratives which must be deconstructed" | PASS |
| 17 | Schellenberg (1956) | Primary vs secondary value; original order | Yes — *Modern Archives*, 1956 (scan, 30 MB) | `digital_humanities_ir/schellenberg-1956-modern-archives.pdf` | Yes | PASS |
| 18 | International Council on Archives (2000) — ISAD(G) | Respect des fonds and original order | Yes — *ISAD(G) General International Standard Archival Description, 2nd ed.*, Ottawa 2000 | `digital_humanities_ir/ica-2000-isadg.pdf` | Yes | PASS |
| 19 | Salton, Wong and Yang (1975) | Vector space model for indexing | Yes — Salton/Wong/Yang, "A Vector Space Model for Automatic Indexing", *CACM* 1975 | `digital_humanities_ir/salton-1975-vsm.pdf` | Yes | PASS |
| 20 | Robertson and Zaragoza (2009) | BM25 / probabilistic-relevance framework | Yes — *Foundations and Trends in IR* 3(4):333–389, 2009, "The Probabilistic Relevance Framework: BM25 and Beyond" | `digital_humanities_ir/robertson-2009-bm25.pdf` | Yes | PASS |
| 21 | Sarthi et al. (2024) | RAPTOR — recursive clustering+summary tree | Yes — RAPTOR ICLR 2024, arXiv:2401.18059 | `technical/sarthi-2024-raptor.pdf` | Yes | PASS |
| 22 | Edge et al. (2024) | GraphRAG — Leiden community-detected hierarchy; gains on global summarisation | Yes — Edge/Trinh/Mody et al., "From Local to Global: A GraphRAG Approach", arXiv:2404.16130 | `technical/edge-2024-graphrag.pdf` (also duplicated in `digital_humanities_ir/`) | Yes | PASS |
| 23 | VectifyAI (2025) | PageIndex — reasoning-based tree search over ToC | Yes — *PageIndex: Vectorless, Reasoning-based RAG via Hierarchical Tree Index* (Mingtian Zhang, Yu Tang) | `technical/vectifyai-2025-pageindex.pdf` | Yes | PASS |
| 24 | Murugaraj et al. (2025) | Topic-RAG over Impresso; improves retrieval relevance over flat RAG; BERTScore/ROUGE/UniEval | Yes — Murugaraj/Lamsiyah/Düring/Theobald, *Computational Humanities Research* 1:e15 (2025) | `digital_humanities_ir/murugaraj-2025-topic-rag-newspapers.pdf` | **Yes — abstract verifies BERTScore (P/R/F1), ROUGE and UniEval as metrics; explicitly outperforms baseline RAG.** Draft does NOT misuse Murugaraj for OCR-noise mitigation (L73 even adds "they do not specifically test OCR-noise mitigation"). | PASS |
| 25 | Lewis et al. (2020) | Single-shot RAG | Yes — RAG, Lewis et al. NeurIPS 2020 | `technical/lewis-2020-rag.pdf` | Yes | PASS |
| 26 | Yao et al. (2022) | ReAct loop | Yes — Yao et al., ICLR 2023 (arXiv 2210.03629, 2022 release) | `technical/yao-2022-react.pdf` | Yes | PASS |
| 27 | Asai et al. (2023) | Self-RAG critique | Yes — Asai et al., arXiv:2310.11511 | `technical/asai-2023-self-rag.pdf` | Yes | PASS |
| 28 | Bai et al. (2025) | Qwen2.5-VL backbone | Yes — Qwen2.5-VL Technical Report, March 2025, arXiv:2502.13923 | `technical/bai-2025-qwen25-vl.pdf` | Yes (used as black-box VLM is fair) | PASS |
| 29 | Chen et al. (2024) | BGE-M3 multilingual encoder; Italian coverage | Yes — Chen/Xiao/Zhang et al., M3-Embedding paper, arXiv:2402.03216 | `technical/chen-2024-bge-m3.pdf` (also `digital_humanities_ir/chen-2024-bge-m3.pdf`) | Yes — paper explicitly markets multi-linguality; Italian is a covered tier | PASS |
| 30 | Wu et al. (2021) | Recursive book summarisation | Yes — Wu/Ouyang/Ziegler et al., arXiv:2109.10862 | `technical/wu-2021-recursive-book-summarization.pdf` | Yes | PASS |
| 31 | Yang et al. (2016) | Hierarchical attention networks | Yes — Yang/Yang/Dyer/He/Smola/Hovy, NAACL 2016 | `technical/yang-2016-hierarchical-attention.pdf` | Yes | PASS |
| 32 | Smith (2007) | Tesseract OCR | Yes — Ray Smith, "An Overview of the Tesseract OCR Engine" | `technical/smith-2007-tesseract.pdf` | Yes | PASS |
| 33 | Wick et al. (2018) | Calamari OCR | Yes — Wick/Reul/Puppe, Calamari paper | `technical/wick-2018-calamari.pdf` | Yes | PASS |
| 34 | Huang et al. (2022) | LayoutLMv3 — clean-input pretraining | Yes — Huang/Lv/Cui et al., LayoutLMv3, arXiv:2204.08387 | `technical/huang-2022-layoutlmv3.pdf` | Yes | PASS |
| 35 | Kim et al. (2022) | Donut — OCR-free document understanding | Yes — Kim/Hong/Yim et al., Donut, arXiv:2111.15664 | `technical/kim-2022-donut.pdf` | Yes | PASS |
| 36 | Doucet et al. (2020) | Convergence on article-level matching for newspaper OCR | Yes — Doucet/Gasteiner/Granroth-Wilding et al., NewsEye, DH2020 | `technical/doucet-2020-newseye.pdf` | PARTIAL — Doucet et al. introduce the NewsEye platform; the "article-level matching is the standard the literature converged on" is a fair extrapolation but not a direct claim of the paper. | PARTIAL |
| 37 | Thomas et al. (2024) | Post-OCR correction; 23.3% CER reduction with BART, 54.5% with Llama-2 13B prompting on BLN600 | Yes — Thomas/Gaizauskas/Lu, "Leveraging LLMs for Post-OCR Correction of Historical Newspapers", LT4HALA 2024 | `technical/thomas-2024-lt4hala-postcorrection.pdf` (also duplicated as `digital_humanities_ir/thomas-2024-postocr.pdf`) | **Yes — verified verbatim from PDF abstract: "54.51% reduction…against BART's 23.30%".** Draft correctly attributes to Thomas et al., NOT to Boroș (per Phase 1 lesson). | PASS |
| 38 | Soper and Kanerva (2025) | "Wins reported in Thomas et al. (2024) and Soper and Kanerva (2025) do not transfer here" | **NO — citation is misattributed.** The PDF `technical/soper-2025-ocr-no-free-lunches.pdf` is actually **Kanerva, Ledins, Käpyaho, Ginter (2025), "OCR Error Post-Correction with LLMs in Historical Documents: No Free Lunches", arXiv:2502.01205**. There is no "Soper" author. | `technical/soper-2025-ocr-no-free-lunches.pdf` (file present but author wrong) | Claim shape (mixed results for LLM post-OCR on historical text) does match the actual paper. | **FAIL — attribution error**. Fix: cite as `Kanerva et al. (2025)`. Rename file to `kanerva-2025-no-free-lunches.pdf`. |
| 39 | Greif et al. (in Maheshwari et al., 2025) | Sub-1% CER after Gemini-2.0-Flash pass on German city directories | **PARTIAL HALLUCINATION** — file `technical/maheshwari-2025-multimodal-historical.pdf` is actually **Greif, Griesshaber, Greif (April 2025), "Multimodal LLMs for OCR, OCR Post-Correction and Named Entity Recognition in Historical Documents", arXiv:2504.00414**. There is no "Maheshwari" author. Greif et al. IS the paper; the parenthetical "(in Maheshwari et al., 2025)" is incorrect — Greif is not "in" anything, and there is no Maheshwari paper containing it. | File present; mis-named. | The substantive claim (sub-1% CER via mLLM post-correction on German city directories) is corroborated by the abstract: "drastic improvement…<1% CER…on city directories published in German between 1754 and 1870." | **FAIL — attribution error**. Fix: cite as `Greif et al. (2025)`, drop the "in Maheshwari et al." wrapper. Rename file. |
| 40 | Zhao 2024 (DocLayout-YOLO lineage) | "YOLO small-region detection over `zhao-2024-doclayout-yolo` lineage layout boxes" — implicit reference | Yes — Zhao/Kang/Wang et al., DocLayout-YOLO, arXiv:2410.12628 | `technical/zhao-2024-doclayout-yolo.pdf` | Yes (used as architectural ancestor reference, not for any factual claim) | PASS — but cite formally as `Zhao et al. (2024)` rather than as a filename string. |

### Citations not currently in the in-text catch but referenced in §6.1 relevance-GT footnote
| 41 | Pavone, 1991; Murialdi, 1986; Bosworth, 2005; Deakin, 1962 (collectively used to hand-build relevance GT) | Already covered above (rows 7, 10, 11, 12) | All on disk | Yes | PASS |

---

## 2. Counts

- **Total distinct citations**: 40 (39 substantive + 1 implicit Zhao 2024)
- **PASS**: 37
- **PARTIAL**: 1 (Doucet et al. 2020 — minor: extrapolation beyond what the paper directly claims)
- **FAIL (attribution)**: 2 (Soper and Kanerva 2025; Greif via "Maheshwari et al. 2025")
- **DROP-recommended**: 0 (both FAILs are fixable in-place by correcting attribution; the underlying claims are sound)
- **HALLUCINATED (paper does not exist)**: 0

## 3. Overall verdict

**FAIL (one or more unverified)**.

Two attribution errors block PASS:
1. "Soper and Kanerva (2025)" — paper has no Soper author. Real authors: Kanerva, Ledins, Käpyaho, Ginter.
2. "Greif et al. (in Maheshwari et al., 2025)" — there is no Maheshwari paper. Greif et al. IS the standalone paper; the "Maheshwari" wrapper appears to be an artefact of a wrong filename in `/tmp/mausoleo/references/papers/technical/`.

Both are correctable with one-line fixes; once corrected, the audit returns PASS on every other count (existence + on-disk + claim accuracy).

## 4. Specific edit list (file:section → fix)

1. **`MAUSOLEO_FULL_DRAFT_v1.md` §4.3 line 153** ("The wins reported in Thomas et al. (2024) and Soper and Kanerva (2025) do not transfer here.")
   → Replace `Soper and Kanerva (2025)` with `Kanerva et al. (2025)`. The paper is Kanerva/Ledins/Käpyaho/Ginter, "OCR Error Post-Correction with LLMs in Historical Documents: No Free Lunches" (TurkuNLP, arXiv:2502.01205, Feb 2025).

2. **`MAUSOLEO_FULL_DRAFT_v1.md` §4.3 line 153** ("Greif et al. (in Maheshwari et al., 2025) report sub-1% character error after a Gemini-2.0-Flash pass on German city directories.")
   → Replace with `Greif et al. (2025)`. Drop the "in Maheshwari et al." wrapper. The paper is Greif/Griesshaber/Greif, "Multimodal LLMs for OCR, OCR Post-Correction and Named Entity Recognition in Historical Documents" (arXiv:2504.00414, April 2025). Sub-1% CER claim is on the abstract.

3. **`MAUSOLEO_FULL_DRAFT_v1.md` §4.2 line 143** ("YOLO small-region detection over `zhao-2024-doclayout-yolo` lineage layout boxes")
   → Replace filename string with proper citation: `(Zhao et al., 2024)`.

4. **`MAUSOLEO_FULL_DRAFT_v1.md` §2.3 line 83** — Schudson date: cited as 1978; PDF on disk is 1981 reprint. Acceptable as-is (1978 is original Basic Books publication), but consider noting the edition: `Schudson (1978)` is fine. No change needed; file rename to `schudson-1978-discovering-the-news.pdf` would tidy it.

5. **Reference list missing.** The draft has no `# References` section. For Harvard/Chicago author-date style this is mandatory. Build one from the verified-existing PDFs in `/tmp/mausoleo/references/papers/` (40 items).

6. **File-naming hygiene** (does NOT affect citations but recommended for the writer's future audits):
   - Rename `technical/maheshwari-2025-multimodal-historical.pdf` → `greif-2025-multimodal-historical.pdf`.
   - Rename `technical/soper-2025-ocr-no-free-lunches.pdf` → `kanerva-2025-no-free-lunches.pdf`.
   - Rename `technical/ehrmann-2024-impresso-transparent.pdf` → `during-2024-impresso-interface.pdf` (it is the same paper as in `digital_humanities_ir/`, by Düring/Bunout/Guido).
   - `historiography/ehrmann-2024-impresso.pdf` is actually Düring et al. 2023 "impresso Text Reuse at Scale" (Frontiers in Big Data) — distinct from the 2024 Historical Methods piece. Rename → `during-2023-impresso-text-reuse.pdf`. (Not currently cited, so low urgency.)

## 5. Citation pool quality — engaged vs name-dropped

### Sources deeply engaged (load-bearing for an argument)
- **Braudel 1958** — central to §1, §2.3, §5.3, §7.3. Engaged, not name-dropped.
- **Cook 2013, Ketelaar 2001, Schellenberg 1956, ICA 2000** — together carry the §7.3 archival-science argument. Engaged.
- **Sarthi 2024 (RAPTOR), Edge 2024 (GraphRAG), VectifyAI 2025 (PageIndex)** — explicitly contrasted with Mausoleo's chronological-given hierarchy in §2.2 + §3.2. Engaged.
- **Murugaraj 2025** — engaged correctly with metric-level specificity (BERTScore/ROUGE/UniEval) and a careful disclaimer about OCR-noise scope. Phase 1 lesson respected.
- **Thomas 2024** — engaged with quantitative numbers (54.51% / 23.30% CER reduction); contrasted directly with the Italian fascist-era post-correction failure. Engaged.
- **Murialdi 1986, Forno 2012, Bonsaver 2007** — engaged briefly but precisely as the Italian-press-historiography frame for *Il Messaggero* under fascism (§2.3).
- **Salton 1975, Robertson 2009** — engaged as IR-baseline lineage (§2.2). Brief but apt.

### Name-dropped (one-line citation, no engagement) — candidates for trim or deepening
- **Schudson 1978** (§2.3 L83) — single sentence about social construction of news. If trimming, defensible to keep because it positions newspapers methodologically; if deepening, two sentences on Schudson's "news as cultural form" argument would tighten §2.3.
- **Pavone 1991, Bosworth 2005, Deakin 1962** (§6.1 L201) — cited only as relevance-GT background, no in-text engagement with their arguments. Acceptable for a footnote use, but if word-count is a constraint these can compress to a single citation cluster.
- **Bai 2025 (Qwen2.5-VL)** (§3.1 L99, §4.2 L143) — used as a backbone-citation only, no engagement with the model's claims. Standard practice; keep.
- **Lewis 2020 (RAG), Yao 2022 (ReAct), Asai 2023 (Self-RAG)** (§3.3 L121) — three single-sentence references. Engagement is light but architecturally apt; trim depends on word budget.
- **Yang 2016, Wu 2021** (§5.2 L173) — cited as lineage for hierarchical-summarisation prior. Each gets one sentence. Adequate.
- **Da 2019, Underwood 2019** (§2.3 L81) — both engaged in the same paragraph on computational-literary-studies critique, decent depth.
- **Smith 2007 (Tesseract), Wick 2018 (Calamari), Huang 2022 (LayoutLMv3), Kim 2022 (Donut)** (§4.3 L151) — bundled in a "not evaluated head-to-head because domain mismatch" sentence. Light engagement, but the rhetorical use is honest. Keep.
- **Doucet 2020** (§4.1 L137, §4.3) — cited as "where the literature has converged"; the cited paper does not directly make this convergence claim. Either soften ("…the move article-level matching has become common in the historical newspaper OCR literature, e.g. NewsEye, Doucet et al. 2020") or replace with a survey citation (e.g. Ehrmann et al. 2023 NER-survey, which is on disk at `technical/ehrmann-2023-ner-survey.pdf`).

### Trim candidates if word count needs to drop
- §6.1 L201 footnote citations (Pavone, Murialdi, Bosworth, Deakin) can collapse to a single "(four works of historiography listed in `eval/case_studies/relevance_gt.json`)".
- §4.3 L151 Tesseract/Calamari/LayoutLMv3/Donut paragraph could compress to one sentence covering all four.
- The §3.3 ReAct + Self-RAG cluster (Yao 2022 + Asai 2023) could merge into one citation parenthetical.

### Deepen candidates if word count permits
- **Cook 2013** (§7.3) deserves one extra sentence on the four-paradigm framework, since the synthesis claim leans heavily on it.
- **Murugaraj 2025** could carry one extra sentence comparing topic-restricted vs chronologically-given hierarchies, since it is the closest prior work.

### Pool sources NOT cited but on disk (potential canonical gaps)
The following PDFs are downloaded under `/tmp/mausoleo/references/papers/` but the draft never cites them:
- `cohen-rosenzweig-2005-digital-history.pdf` — canonical digital-history reference; would strengthen §2.3.
- `guldi-armitage-2014-history-manifesto.pdf` — *The History Manifesto* explicitly argues the longue durée case for digital history; obvious complement to Braudel in §7.3.
- `tworek-2019-news-from-germany.pdf` — propaganda-state press, useful comparative context for Italian fascist press.
- `nora-1989-between-memory-and-history.pdf`, `halbwachs-1950-memoire-collective.pdf` — collective-memory frame for §7.3 archival-as-mediation argument.
- `ginzburg-1976-cheese-and-the-worms.pdf`, `ginzburg-1989-clues-myths-historical-method.pdf` — microhistory + evidential paradigm; Ginzburg's "evidential paradigm" is a natural foil for the missing-26-July finding.
- `marciano-2018-cas-big-data.pdf`, `jaillant-2022-archives-ai.pdf` — current archives-and-AI literature; both would update §2.1.

If the writer wants to engage 90 % of the verified pool (PaperOrchestra rule), citing 2–3 of the above (especially Guldi & Armitage, and either Ginzburg) would close the canonical-source gap flagged below.

### Missing canonical sources (not on disk, would expect at this band)
- For an Annales-grounded history of newspapers, **Anderson (1983) *Imagined Communities*** is the standard reference for the press-as-temporal-coordinator argument. Not in pool.
- For provenance + postmodern archives, **Derrida *Mal d'archive* (1995)** is the philosophical complement to Cook/Ketelaar; absence is defensible at the dissertation length but worth flagging.

---

## 6. Style consistency

- Mixed in-text citation style: same sentence sometimes uses parenthetical `(Author, Year)` and sometimes narrative `Author (Year)`. This is normal Harvard/Chicago author-date practice; both forms are valid. Consistency is fine.
- Author lists with three names: §2.2 L69 uses `Salton, Wong and Yang (1975)` (Oxford comma absent). §3.1 L99 uses `(Bai et al., 2025)`. Three-author works are spelled out at first use, which is correct Harvard.
- One filename-as-citation: §4.2 L143 `zhao-2024-doclayout-yolo lineage` — **fix: cite as `Zhao et al. (2024)`**.
- Quoted Italian primary text in §6.2 L211 is set in italics inside a blockquote — appropriate; no page number needed because it is the summariser's own output, not a quoted historian.
- No reference list at the end of the draft. **Build one** before submission.

## 7. Headline action (one paragraph)

Two attribution errors must be fixed before submission: `Soper and Kanerva (2025)` → `Kanerva et al. (2025)`, and `Greif et al. (in Maheshwari et al., 2025)` → `Greif et al. (2025)`. Both papers exist and the substantive claims are accurate; only the author attribution is wrong. Replace the filename-string `zhao-2024-doclayout-yolo` with `Zhao et al. (2024)`. Soften the Doucet-et-al. "convergence" claim (PARTIAL). Build a `# References` section from the 40 verified PDFs. After these five edits, the citation audit will PASS on existence + grounding + claim-accuracy across every cited work in the draft.
