# Mausoleo dissertation outline (BASC0024)

**Working thesis (E)**: Mausoleo's OCR + hierarchical indexing + agent-mediated search pipeline outperforms keyword-search-over-flat-OCR on archival research tasks, demonstrated through case studies on *Il Messaggero* July 1943. The pipeline's chronological hierarchy is the computational form of two commitments the historiographical and archival traditions already share: multi-resolution time (Annales / Braudel) and respect for provenance (Cook 2013, Ketelaar 2001, Schellenberg 1956). The dissertation's interdisciplinary contribution is an empirical demonstration that this commitment is necessary for archival research interfaces, with the missing 1943-07-26 as the signature case.

**Discipline pair (cat 2 grounding)**: History + Computer Science. History supplies the historiographical commitment to multi-resolution time (Annales) and the archival commitment to provenance (Cook, Ketelaar, Schellenberg); CS supplies the hierarchical retrieval lineage (RAPTOR, GraphRAG, PageIndex) and the system implementation. The integration is substantive, not decorative: §7.3 commits to a synthetic claim about why the chronological hierarchy is the right computational form for archival access. Cognitive science / philosophy / media studies are explicitly out of scope.

**Word budget**: 9000 words main body. Abstract ≤300, Preface ≤500 (excluded). Hard cap 10000.

**Submission spec**: BASC0024, anonymous candidate code, A4, 20mm margins, Arial/Calibri/TNR ≥10pt, 1.5 line spacing, candidate code in footer.

**Corpus**: *Il Messaggero* July 1943, 30 daily issues (07-01 to 07-31, 07-26 missing). The OCR ensemble pipeline was hillclimbed against the bootstrap-plus-hand-cleaned ground truth on 1885-06-15 + 1910-06-15 (per `plan/01_ocr.md`, composite score 0.89198 on those eval issues). The same ensemble configuration was then applied to all 30 July 1943 issues, producing 9456 raw articles which were post-hoc hand-cleaned (deduplication + cross-page stitching, `scripts/cleanup_transcriptions.py` + manual pass) into the 6480 article-level transcriptions in `eval/transcriptions/`. The dissertation distinguishes the OCR-quality score (0.892 on 1885+1910 hand-cleaned GT) from the corpus-quality of the 1943 transcriptions (hand-cleaned, not formally CER-evaluated against an article-level 1943 GT).

---

## Section allocation

| § | Section | Words | Purpose |
|---|---------|-------|---------|
| 1 | Introduction | 900 | Problem, gap, proposal, contribution |
| 2 | Literature review | 1500 | Position vs prior art, identify gap |
| 3 | System design | 1500 | OCR + index + search architecture |
| 4 | OCR evaluation | 1100 | Cold-cache eval methodology + results |
| 5 | The knowledge index | 1000 | Schema + summarisation pipeline |
| 6 | Evaluation: case studies | 2200 | Three case studies, Mausoleo vs baseline |
| 7 | Discussion | 900 | Implications, limitations, related framings |
| 8 | Conclusion | 500 | Restate, future work |
| | TOTAL | 9600 | |

Plus: Abstract (≤300), Preface (≤500, interdisciplinary rationale + BASc connections), References (excluded from count), Appendix (figures, tables, code references).

---

## §1 Introduction (900 words)

**Opening question (historiographical, not retrieval)**: how does a historian read a month of a fascist-era newspaper across the rupture of 25 to 27 July 1943? The Annales-school tradition (Braudel: longue durée, conjoncture, événement) treats history as multi-resolution: the daily event sits inside the conjuncture of the regime sits inside the longue durée of fascist Italy. Reading *Il Messaggero* July 1943 requires moving fluently between these scales. Existing digital archives (Chronicling America, Europeana Newspapers, Impresso) afford keyword search and faceted browsing over flat OCR, but they do not afford agent-mediated drill-down across summarised temporal scales; the historian's multi-resolution movement is left to the historian.

**Two task types where this matters**:
- **Aggregate questions**: how did coverage shift across the month, what is the editorial balance over a week. Answerable by flat retrieval only by manual aggregation across many article reads.
- **Missing-data questions**: what was reported on a date that is absent from the source archive; what does that absence mean. Unanswerable by flat retrieval because the absent date returns no results.

**Sub-claims**:
1. Multi-resolution reading is a historiographical commitment (Braudel; Annales) that flat keyword retrieval over OCR'd newspapers cannot serve directly. It supports point queries; aggregate and missing-data questions require either an indexed hierarchy of summaries or extensive manual aggregation by the human researcher.
2. *Il Messaggero* July 1943 is a stress test for any newspaper-archive interface because it contains a regime-change rupture in the middle of the corpus: the Grand Council voted Mussolini out at 02:40 on 25 July, the King had him arrested that afternoon, the issue of 26 July is absent from the source archive, and the editorial register shifts visibly from 27 July onward.
3. Mausoleo's hierarchical index + agent-mediated drill-down handles both task types: aggregate questions by exposing day, week, and month summary nodes; missing-data questions by treating absent dates as first-class nodes whose summaries contextualise the gap. Three case studies on *Il Messaggero* July 1943 test whether this pipeline outperforms keyword-search-over-flat-OCR on the two task types: cases 2 and 3 (efficiency + completeness + quality on aggregate and structural-aggregate questions); case 1 (the missing 1943-07-26, demonstrating the capability gap on missing-data questions).

**Evidence type**: position-paper framing for a historiographical question, with engineering as the answer. Cite Braudel + Moretti for the multi-resolution-reading commitment, then Chronicling America / Europeana / Impresso as comparators that fail to serve it, then Murugaraj 2025 / Sarthi 2024 / Edge 2024 / VectifyAI 2025 as the methodological neighbours Mausoleo extends.

**Citation pool**: Braudel 1958 (longue durée), Moretti 2013 (distant reading), Ehrmann 2020 (Impresso resource), Düring 2024 (Impresso interface), Murugaraj 2025 (Topic-RAG newspapers, retrieval-relevance not OCR-noise), Sarthi 2024 (RAPTOR), Edge 2024 (GraphRAG), VectifyAI 2025 (PageIndex).

**Cross-references to thread the missing 26 July**: §6.2 (lead case study), §7.1 (closing example), §3.3 (handled architecturally as a node-with-summary-but-no-leaves).

---

## §2 Literature review (1500 words)

Three sub-sections. Tight, position-defining.

### §2.1 Existing digital newspaper archives (~400 words)
The dominant access template across Chronicling America (LoC, ~23M pages, US 1690-1963), Europeana Newspapers (~28M pages, 40 EU languages), and Impresso (Swiss/Luxembourgish, ~200 years) is keyword + faceted search over OCR'd text, optionally enriched with NER, topic models, lexical-semantic comparison, or text-reuse browsing. Impresso is the most enriched of the three but still organises access around the query: the user arrives with a search term, receives a ranked article list, optionally facets by date/year/source, and reads articles individually.

Mausoleo addresses the access modality this template under-serves: the historian who arrives without a query, wanting to *understand* a corpus they cannot read in full at the article level. Multi-resolution drill-down with summarised intermediate levels is what these systems do not afford. This is a positioning claim, not a deficiency claim: Chronicling America, Europeana, and Impresso are excellent at what they are designed to do, and Mausoleo extends rather than displaces them.

### §2.2 Information retrieval lineage (~500 words)
- Classical IR: BM25, TF-IDF (Salton, Robertson)
- Dense retrieval: BGE-M3, ColBERT (mention briefly, will not be primary baseline)
- Hierarchical retrieval: RAPTOR (Sarthi 2024), GraphRAG (Edge 2024), PageIndex (VectifyAI 2025)
- RAG over historical newspapers: Murugaraj 2025 (Topic-RAG over Impresso Swiss newspapers; topic-restricted retrieval improves relevance over flat RAG, measured by BERTScore / ROUGE / UniEval; the immediate prior art for newspaper-corpus RAG, though it does not specifically test OCR-noise mitigation).
- **Gap that Mausoleo fills**: hierarchical retrieval where the hierarchy is *given* by archival structure (chronology) rather than *induced* by clustering. Provenance-respecting (Cook 2013, archival science).

### §2.3 Historical methodology (~600 words)
- Annales school multi-scale time (Braudel: longue durée / conjoncture / événement)
- Distant reading (Moretti, Jockers); critique (Da 2019, Underwood 2019)
- Newspapers as historical sources: editorial bias, methodology of using press as evidence (Schudson 1978; Murialdi for Italian press)
- Italian fascist press: Murialdi 1986 *Storia del giornalismo italiano* (covers the regime period), Forno 2012, Bonsaver 2007 for the regime context

**Sub-claims**:
1. Existing newspaper archives prioritise full-text search over multi-resolution access; Mausoleo addresses a different access modality.
2. The hierarchical-retrieval lineage (RAPTOR, GraphRAG, PageIndex) validates the paradigm but applies it to single documents or learned hierarchies; Mausoleo applies it to archival corpora with chronologically given hierarchies.
3. Annales-school multi-scale time provides the historiographical justification for a temporal hierarchy: historians already think this way; Mausoleo gives them a tool that respects it.

**Citation pool**: Moretti 2013, Jockers 2013, Da 2019, Underwood 2019, Salton 1975, Robertson 2009 (BM25), Sarthi 2024 (RAPTOR), Edge 2024 (GraphRAG), VectifyAI 2025 (PageIndex), Murugaraj 2025 (Topic-RAG, retrieval-relevance), Cook 2013, Ketelaar 2001, Schellenberg 1956, Ehrmann 2020 (Impresso resource paper, LREC), Düring 2024 (Impresso interface paper, Historical Methods), Braudel 1958, Murialdi 1986, Forno 2012, Bonsaver 2007, Schudson 1978. Approx 20 sources, all on disk.

---

## §3 System design (1500 words)

Three sub-sections describing the architecture.

### §3.1 OCR pipeline (~600 words)
- Input: scanned JPEGs of *Il Messaggero* daily issues (~6 pages each, July 1943).
- Pipeline: VLM-based OCR with cross-family + cross-backend diversity (Qwen2.5-VL-7B and Qwen3-8B, vLLM + transformers backends), column-split at multiple granularities (col2/col3/col4/col6/yolo/fullpage), 6 sub-pipelines arranged in two parallel GPU chains under a 30-min/issue cold-cache budget on 2× RTX 3090. The final config uses a **deterministic ensemble selection** step (REPLACE / ADDITIVE chains with per-source overlap thresholds and quality-weighted selection, per `plan/01_ocr.md` Lean5) over the 6 sub-pipelines' outputs; no LLM arbitration stage and no standalone post-correction model are used in the final config. Cross-family + cross-backend diversity contributes a documented +0.013 stack to the composite score over single-model ensembles, which is the methodologically interesting result and is foregrounded over single-pipeline numbers.
- 30-min/issue cold-cache constraint on 2× RTX 3090.
- Reference: existing `plan/01_ocr.md`.

### §3.2 Hierarchical indexing (~500 words)
- The dissertation describes a 5-level case-study schema: paragraph → article → day → week → month, with month as the root for the July 1943 corpus. The production system extends to 7 levels (year → decade → archive) for full-archive scale; the case-study scope lifts only the first 5. Week is a case-study granularity choice, not a property of the production schema; design rationale appears in §5.2.
- ClickHouse storage: nodes table with summary + embedding + raw text at leaves only.
- Recursive summarisation pipeline: bottom-up, vLLM, BGE-M3 embeddings.
- Reference: existing `plan/03_hierarchical_index.md`.

### §3.3 Agent-mediated search (~400 words)
- API server (FastAPI + ClickHouse) + CLI (typer, JSON output for LLM agents).
- Tree traversal endpoints: `/nodes/{id}`, `/nodes/{id}/children`, `/nodes/{id}/text`.
- Search endpoints: semantic (vector), text (BM25-like), hybrid.
- Tool descriptions for LLM agents.
- Reference: existing `plan/04_search_and_cli.md`.

**Sub-claims**:
1. The architecture is modular: OCR, index, and search can be evaluated independently.
2. The hierarchy is given by chronology, not induced; this is the central design commitment that distinguishes Mausoleo from RAPTOR / GraphRAG.
3. The agent interface (CLI returning JSON) treats the LLM as the user, not the human; the human reads the agent's compiled answer.

**Citation pool**: Qwen2.5-VL paper, BGE-M3 (Chen 2024), RAPTOR (Sarthi 2024), GraphRAG (Edge 2024), Lewis 2020 (RAG), ReAct (Yao 2022), Self-RAG (Asai 2023). 7 sources, all on disk.

---

## §4 OCR evaluation (1100 words)

Methodology + results from the existing autoresearch hillclimb.

### §4.1 Methodology (~400 words)
- Hand-cleaned article-level ground truth for 1885-06-15 (41 articles, full manual pass), bootstrap-plus-spot-correction ground truth for 1910-06-15. These two issues are the OCR hillclimbing eval set.
- Composite score: weighted CER + WER + article F1 + page-span accuracy. Reported on the 1885 + 1910 eval set, not on 1943 (no formal article-level GT exists for 1943; July 1943 issues are post-hoc hand-cleaned at the corpus-curation stage and used as the dissertation's primary source, not as an OCR benchmark).
- Cold-cache constraint: ≤30 min wall-clock per issue from raw images, no warm-cache cheating.

### §4.2 Pipeline configuration (~400 words)
- Final config: 6 sub-pipelines, 2 GPU chains, deterministic ensemble selection (REPLACE / ADDITIVE chains with per-source overlap and quality-weighted selection per `plan/01_ocr.md` Lean5).
- Composite score on the 1885+1910 eval set: ~0.892 (per `plan/01_ocr.md` Lean5 final, composite of weighted CER + WER + article F1 + page-span accuracy). Same ensemble config applied to 1943 July; corpus-quality of the resulting 1943 transcriptions is reported in §3.1 as 9456 raw articles → 6480 hand-cleaned, with the cleaning protocol documented in `scripts/cleanup_transcriptions.py`.
- Article-level matching, page-span accuracy.

### §4.3 Comparison (~300 words)
- Vs single-config baselines (qwen_vl_7b_structured at 0.139 CER initial)
- Vs published OCR-for-historical-newspapers benchmarks: NewsEye, Impresso, Boroș/Thomas post-correction work.

**Sub-claims**:
1. VLM-based OCR with column-split + ensemble outperforms single-VLM and classical OCR on degraded fascist-era Italian newspapers.
2. Cold-cache evaluation is methodologically necessary; warm-cache scores are inflated.
3. Article-level evaluation (CER + F1 + page span) is required because flat full-text CER penalises ordering errors that are not actually quality errors.

**Citation pool**: Qwen2.5-VL paper, Smith Tesseract, Calamari, LayoutLMv3, Donut, DocLayout-YOLO, Soper 2025, Maheshwari 2025, NewsEye, Impresso, Thomas 2024 LT4HALA. 11 sources, all on disk.

---

## §5 The knowledge index (1000 words)

Schema + summarisation pipeline; hands off concrete examples.

### §5.1 Schema and node IDs (~300 words)
- ClickHouse `nodes` table: level, parent_id, position, date_start, date_end, summary, raw_text (leaves only), embedding, child_count.
- Deterministic IDs: `1943-07-15_a01_p02` for paragraphs, `1943-07-15` for days, `1943-07` for months.
- Vector + FTS indexes.

### §5.2 Recursive summarisation (~400 words)
- Bottom-up: paragraphs → article summaries → day summaries → week summaries → month summaries.
- Prompt design: consistent length per level (~200-400 words), entities woven in, specific names/dates/places preserved.
- Embedding: BGE-M3 multilingual (chosen for Italian).
- Inference: vLLM, Ray Data orchestration.

### §5.3 Quality assessment (~300 words)
- Spot-check: pull 10 day-summaries at random from July 1943, verify named entities + key events present.
- Information loss across levels: what survives compression from day to month?
- Examples: how is July 25 represented at day vs week vs month level?

**Sub-claims**:
1. Summaries of consistent length across levels are a design choice with consequences: they make navigation predictable but risk flattening genuinely different time-scales.
2. The hierarchy preserves provenance (every node points to its source paragraphs); summaries are activations, not replacements (Ketelaar 2001).
3. Embedding-based search complements tree traversal: tree for "where in time", vector for "where else this is mentioned".

**Citation pool**: BGE-M3 (Chen 2024), Wu 2021 recursive book summarisation, Yang 2016 hierarchical attention, Edge 2024 GraphRAG, Ketelaar 2001, ICA 2000 ISAD(G). 6 sources, all on disk.

---

## §6 Evaluation: case studies (2200 words)

The heart of the dissertation. Three case studies, each comparing Mausoleo vs a flat-OCR keyword baseline. Case 1 (the missing 1943-07-26) leads because it is the dissertation's signature interdisciplinary moment, not because it is the smallest or most modest finding. Cases 2 and 3 demonstrate the efficiency + quality gap on aggregate and structural questions.

### §6.1 Experimental setup (~300 words)
- **Baseline**: BM25 over the same OCR'd text in the same `documents` table; baseline ignores the `nodes` hierarchy entirely. No summaries, no semantic embedding.
- **Mausoleo**: agent-mediated drill-down via the CLI tools, hitting `nodes` table summaries + the `text` endpoint for descent to leaves.
- **LLM (researcher agent)**: Claude Sonnet 4.5 used for both systems with identical system prompts; only the tools differ. Three trials per case study.
- **Three metrics, applied uniformly across all case studies**: (a) efficiency, reported as both tool calls and total characters read to reach the agent's compiled answer; (b) completeness, reported as recall of relevant articles against the relevance GT; (c) quality, scored by two distinct LLM judges on a three-dimension rubric (factual accuracy, comprehensiveness, insight). The earlier draft included a fourth "serendipity" metric, which was dropped because (i) its 0/1 binary signal is uninformative at N=3, (ii) it is not cleanly distinguishable from completeness, and (iii) the deep review identified it as a typology weakness.
- **Trial protocol**: 3 trials per case study, mean + min + max + a paired sign test reported across the 3 trials × 2 judges. The paired sign test is appropriate at this N and avoids over-claiming the strength of the difference.
- **Historical methodology for relevance GT**: built by reading July 1943 issues against the historiographical literature (Pavone 1991, Murialdi 1986, Bosworth 2005, Deakin 1962) and annotating ~30 articles per case study as relevant. Single annotator (the dissertation author), with a self-consistency check: the annotator re-annotates one case study after a 2-week gap; intra-rater agreement (Cohen's κ) is reported in §6.5 as a rigor floor. Acknowledged as a methodological limitation in §7.2.
- **GT provenance**: §6.1 distinguishes corpus-level transcriptions (hand-cleaned in `eval/transcriptions/`, used by both Mausoleo and the baseline as their input) from relevance GT (the annotator's relevance judgements per case, used only by the completeness metric). Completeness is non-circular because the corpus-side and the relevance-side GT are built independently.
- **Researcher agent control**: identical model (Claude Sonnet 4.5), identical system prompt, identical task wording, identical interaction budget (max 30 tool calls per case). The only thing that differs between Mausoleo and the baseline is the toolset exposed: Mausoleo gets the hierarchy + search endpoints, baseline gets BM25 over the same `documents` table. The "agent constant, tools varied" framing is foregrounded in §6.1 to forestall the reviewer concern that the win is the agent's rather than the index's.
- **LLM-as-judge protocol**: blind evaluation against the three-dimension rubric. Two distinct judges (Claude Opus 4.5 + GPT-5), each scoring once; scores averaged per dimension per trial. Inter-judge agreement (Cohen's κ on the 0-5 score discretised) reported as a secondary observation.

### §6.2 Case study 1 (LEAD): the missing 1943-07-26 (~550 words)
**Question**: What was reported on 26 July 1943, the day after Mussolini's arrest?

This case leads §6 because it is the dissertation's signature interdisciplinary moment. The 26 July issue is absent from the source archive. Reading this absence requires three simultaneous moves: (a) a CS retrieval problem (null result handling), (b) an archival-science question (provenance of absence per Cook 2013, Ketelaar 2001), and (c) a historical event (the Grand Council deposition at 02:40 on 25 July, arrest that afternoon, regime instability that day).

**Baseline**: returns zero results for date = 1943-07-26. The researcher agent has no way to surface what the silence means.

**Mausoleo**: the day node `1943-07-26` exists in the index even though its leaf paragraphs are empty; its summary contextualises the absence against the surrounding days (07-25 fascist register, 07-27 Badoglio register) and against the historical event. The researcher agent composes an answer that reads the absence as evidence.

**Expected findings**: Mausoleo produces an answer of the form "the 26 July issue is absent; the surrounding context places it on the rupture day; this absence is itself archival evidence of the regime collapse." Baseline produces null. Completeness: Mausoleo recovers the full historical context, baseline recovers nothing. Quality (LLM-as-judge): Mausoleo's answer scores high on all three axes; baseline scores zero.

**Quantitative reporting**: efficiency (tool calls + characters read), completeness (against relevance GT, defined for this case as the set of articles in 25 and 27 July that contextualise the rupture; baseline recovers zero of this set because it cannot surface the absent day), quality (LLM-judge mean across 3 trials × 2 judges, with min/max + paired sign test as per §6.1).

This case is a definitional capability gap, not a fine-grained efficiency comparison; the §7.1 framing names "missing-data archival capability" as a third category alongside aggregate and structural questions.

### §6.3 Case study 2: the July 25 regime change (~550 words)
**Question**: How did *Il Messaggero* cover the fall of Mussolini and the transition to the Badoglio government?

**Baseline run**: keyword queries for "Mussolini", "Badoglio", "Gran Consiglio", "Re Vittorio Emanuele". Returns a ranked article list; the researcher agent reads articles in order, compiles a narrative.

**Mausoleo run**: agent starts at month root, drills to week-of-25-July, reads the day summaries for 07-25 and 07-27 (07-26 already named in §6.2), descends to article level for specific evidence.

**Expected findings**:
- 1943-07-25 morning issue: pure late-fascist register (Sicilian battle bulletins, "DOVE ARRIVANO I LIBERATORI" sarcasm, "BIECO FURORE BRITANNICO"). 273 articles.
- 1943-07-26 absent (already analysed in §6.2).
- 1943-07-27 onward: Badoglio-government register; tonal shift visible in editorial voice.

**Quantitative reporting**: 3 metrics × 3 trials × 2 judges, mean + min + max + paired sign test per §6.1. Anticipated direction: Mausoleo wins on efficiency (one tool call to a day-summary vs the baseline's full-article read, with characters read as the comparable unit), Mausoleo ties or wins on completeness, Mausoleo wins on quality (the compiled narrative captures the register shift; the baseline captures the political event but tends to miss the editorial-tone shift unless the agent reads articles in chronological order).

### §6.4 Case study 3: comparative coverage (~500 words)
**Question**: How does the balance of war coverage vs domestic-politics coverage shift over July 1943?

**Baseline**: cannot answer aggregate questions in a single query. Agent reads sample articles per day, classifies each, computes the ratio across the month.

**Mausoleo**: queries day-level summaries directly; the day summaries already characterise the day's editorial balance. Agent aggregates summary content across the month.

**Expected findings**: war coverage dominates 07-01 to 07-25 (Sicily campaign), drops sharply 07-27 to 07-31 (Badoglio government, transitional editorial line). Domestic politics rise correspondingly.

**Quantitative reporting**: 3 metrics × 3 trials × 2 judges, mean + min + max + paired sign test per §6.1. Anticipated direction: Mausoleo wins decisively on efficiency (~10 tool calls vs ~150 article reads), wins on completeness (full month aggregated, baseline samples), wins on quality (the editorial balance is what day-summaries explicitly characterise; the baseline must derive it indirectly from sampled articles).

### §6.5 Aggregate results (~300 words)
Cross-case-study synthesis. Table (M = Mausoleo, B = Baseline; all values per-trial averages over 3 trials × 2 judges, anticipated values to be replaced with measured at draft time):

| Metric | Case 1 (07-26) | Case 2 (07-25) | Case 3 (comparative) |
|---|---|---|---|
| Efficiency (tool calls) | M:1, B:0 (null) | M:~5, B:~30 | M:~10, B:~150 |
| Efficiency (chars read) | M:~2k, B:0 | M:~10k, B:~120k | M:~25k, B:~600k |
| Completeness (recall vs GT) | M:1.0, B:0.0 | M:0.95, B:0.85 | M:0.90, B:0.65 |
| Quality (judge 0-5) | M:4.5, B:0.0 | M:4.0, B:3.0 | M:4.5, B:2.5 |
| Inter-judge κ | reported | reported | reported |

Case 1 is reported separately as a definitional capability gap rather than a quantitative comparison: the baseline returns null because the date is absent from the corpus, so case-1 numbers in the table are forecast as M:1.0 / B:0.0 across all metrics by construction. Cases 2 and 3 carry the genuine efficiency + completeness + quality comparison, with paired sign tests reported per metric.

Cost (absolute, not amortised — this is an unmonetised research project): one-time OCR build of the 30 July 1943 issues took ~29.7 GPU-hours on 2× RTX 3090 (8-source deterministic ensemble, ~30.5 min wall per issue). One-time LLM index build of 6,517 summary nodes (article + day + week + month) cost $28.87 in phantom-USD (Haiku 4.5 + Sonnet 4.5 over OAuth, no money charged) and ~2 h 20 min wall. Per query, Mausoleo uses ~328 k input + 2.5 k output tokens, 11 tool calls, ~77 s wall; the baseline uses ~321 k input + 3.4 k output tokens, 28 tool calls, ~82 s wall. Per-query ClickHouse inference (HNSW + tokenbf_v1) is sub-second. All numbers are reported in absolute terms; the case for hierarchical indexing rests on the qualitative wins of §6.2-§6.4 and the operational unworkability of flat retrieval at archival scale, not on a per-query cost differential.

**Citation pool**: Moretti 2013, Da 2019 (for the methodological critique we have to address), Murialdi 1986, Forno 2012, Pavone 1991, Bosworth 2005, Deakin 1962. 7 sources, all on disk.

---

## §7 Discussion (900 words)

### §7.1 What the case studies show (~350 words)
The pipeline outperforms flat retrieval on two task types established in §1:

- **Aggregate questions**: "how does coverage shift across the month" (case 3) and "how is the regime change visible in the editorial register" (case 2) are both answered cheaply by reading day or week summaries; flat retrieval requires the agent to read many articles manually. Mausoleo wins on efficiency, completeness, and quality across cases 2 and 3, with the paired sign tests in §6.5 supporting the strength of the difference.

- **Missing-data questions**: case 1 is the capability gap. The baseline cannot return anything for a date absent from the corpus; Mausoleo's day-level node `1943-07-26` carries a summary that contextualises the absence. The forecast result is not a quantitative win but a definitional one, and §6.5 reports it as such.

Closing example: the missing 1943-07-26 is the dissertation's signature finding. It is simultaneously a CS retrieval problem, an archival-science question (provenance of absence), and a historical event (Mussolini's deposition). The pipeline handles all three because the hierarchical index treats date as a first-class structural property of the corpus rather than as a metadata facet over articles; flat retrieval cannot do this without a separate "missing-data" subsystem bolted on. The architectural commitment to the chronological hierarchy is what enables the case-1 result, which is the synthesis tested empirically by §7.3.

### §7.2 Limitations (~250 words)
- **Index-build cost**: not free, scales with corpus size. The one-month corpus (July 1943) cost ~29.7 GPU-hours on 2× RTX 3090 for OCR and ~$29 phantom-USD for LLM summarisation. Scaling to a full 60-year archive is roughly linear in OCR (×720 ≈ 21,400 GPU-hours, substantial) and roughly linear in the article-summary phase (×720 ≈ $21 k phantom-USD); higher levels (week, month, year, decade, archive) collapse upward and scale sub-linearly, so the total grows slower than ×720 above the article tier. Per-query inference on the indexed corpus stays sub-second regardless of scale, since vector retrieval over HNSW and FTS over `tokenbf_v1` are both logarithmic in node count.
- **LLM bias as second-order agenda-setting**: every summary at every level is the LLM's choice of what is salient. The dissertation does not test for or correct this bias directly; it only acknowledges that what the system surfaces as "the editorial balance of July 1943" is filtered through the summariser's own salience function. The case studies do not control for this and a comparison with human-written reference summaries would be the next methodological step. (~80 words.)
- **Single-corpus, single-month evaluation**: results may not generalise to less politically-volatile corpora; July 1943 is in part chosen because the rupture is so legible.
- **Single-annotator relevance GT**: mitigated by the 2-week self-consistency re-annotation reported in §6.5 but not eliminated. A second-annotator agreement check is the obvious extension.
- **N=3 trials per case**: paired sign test is appropriate at this N but does not bound effect-size estimation. The strength of the conclusion is "Mausoleo wins consistently on the cases tested," not "the win generalises with bounded confidence."
- **Architectural assumption**: the pipeline assumes a strong native temporal hierarchy in the source; archives without dated issues (e.g. unpublished correspondence, undated collections) need a different organising principle and are out of scope.

### §7.3 The Annales hierarchy as computational form of provenance (~300 words)
Mausoleo's chronologically-given hierarchy is the computational form of the archival principle of provenance. The Annales tradition, particularly Braudel's (1958) framing of history as multi-resolution time, treats événements (events) as sitting inside conjonctures (medium-term structures) inside the longue durée (long-term). Archival science (Cook 2013; Ketelaar 2001; Schellenberg 1956) holds that records must be respected in their original order and provenance, with description as activation rather than replacement of the source.

Mausoleo brings these together. Each level of the tree is a different temporal resolution; each summary is an activation of the source paragraphs beneath it; the original order (chronology) is preserved at every level. The missing 26 July, archivally significant precisely because it is the gap in the provenance, becomes a first-class object in the computational record, addressable, summarisable, contextualisable.

This is a synthetic claim, not a borrowed framing: the dissertation argues that an interface to a historical archive is well-designed only insofar as it respects the historiographical commitment to multi-resolution time and the archival commitment to provenance. Mausoleo is one such design; flat retrieval is not. The case studies test the synthesis empirically.

**Citation pool**: Braudel 1958 (longue durée), Cook 2013 (postmodern archival paradigms), Ketelaar 2001 (tacit narratives, summary as activation), Schellenberg 1956 (provenance and original order). 4 sources, all on disk, all engaged substantively.

---

## §8 Conclusion (500 words)

Restate: pipeline outperforms flat baseline on archival research tasks (case studies showed it on three dimensions). Discussion: this result is interdisciplinary because archival research is a humanities task and the system is a CS contribution.

Future work: scaling beyond a single month; multi-archive support; community-contributed OCR/summary corrections; generic-corpus extension (any unstructured time-stamped data).

---

## Citation pool (consolidated)

Approx 36 distinct citations across the dissertation, all currently on disk in `references/papers/`. Distribution:
- §1 Introduction: 8 sources (Braudel 1958, Moretti 2013, Ehrmann 2020, Düring 2024, Murugaraj 2025, Sarthi 2024, Edge 2024, VectifyAI 2025)
- §2 Literature review: 20 sources (above + Salton 1975, Robertson 2009 BM25, Cook 2013, Ketelaar 2001, Schellenberg 1956, Da 2019, Underwood 2019, Jockers 2013, Murialdi 1986, Forno 2012, Bonsaver 2007, Schudson 1978)
- §3 System design: 7 sources (Qwen2.5-VL, BGE-M3, RAPTOR, GraphRAG, Lewis 2020, ReAct, Self-RAG)
- §4 OCR evaluation: 11 sources (the OCR cluster: Smith Tesseract, Calamari, LayoutLMv3, Donut, DocLayout-YOLO, Qwen2.5-VL, Soper 2025, Maheshwari 2025, NewsEye, Ehrmann 2020 Impresso, Thomas 2024 LT4HALA)
- §5 Knowledge index: 6 sources (BGE-M3, Wu 2021 recursive book summ, Yang 2016 HAN, Edge 2024 GraphRAG, Ketelaar 2001, ICA 2000 ISAD(G))
- §6 Evaluation: 7 sources (Moretti 2013, Da 2019, Murialdi 1986, Forno 2012, Pavone 1991, Bosworth 2005, Deakin 1962)
- §7 Discussion: 4 sources (Braudel 1958, Cook 2013, Ketelaar 2001, Schellenberg 1956), substantively engaged in §7.3 not just name-dropped
- §8 Conclusion: 0 new

Total unique: ~36 sources. Per the essay-iter rule (8-15 per major section), this is well within range for §2 / §6 and on the edge for §1 / §3 / §4 / §5 (which is fine, those sections are tighter). All on disk in `references/papers/`, citation manifest in `references/manifests/`.

Citation correctness fixes applied this revision:
- Ehrmann/Düring split into Ehrmann 2020 (LREC, resource paper) + Düring 2024 (Historical Methods, interface paper). Previously cited as a single "Ehrmann/Düring 2024" entry, which was a mis-attribution.
- Murugaraj 2025 OCR-noise claim removed. The paper measures BERTScore / ROUGE / UniEval improvements via topic-restricted retrieval; it does not specifically test OCR-noise mitigation. Outline now claims only "improves retrieval relevance over flat RAG."
- Murialdi 1986 cited as *Storia del giornalismo italiano* (the actual title of the file on disk; covers the regime period substantively).
- Boroș 2024 RAG-newspapers entry removed (unverifiable, ACM-paywalled, no preprint). Murugaraj 2025 occupies that slot.
- Thomas/Gaizauskas/Lu 2024 LT4HALA post-OCR paper attribution corrected; previously cited as Boroș et al.

---

## Reviewer-pass checklist

Before drafting:
- [ ] Phase 1 reviewers: rubric (against the 4-category rubric in `c041e51f`), citation (CoVe on the citation pool), plagiarism (not applicable to outline; deferred), coherence (cross-section consistency)
- [ ] Lock thesis to E + discipline pair to history + CS
- [ ] Confirm word allocation against the actual draft start

Phase 2 (drafting):
- Order: §3 (system design) → §4 (OCR eval) → §5 (knowledge index) → §6 (case studies, run experiments first) → §2 (lit review, last because the framing follows from what the experiments showed) → §1 (intro, last) → §7 (discussion) → §8 (conclusion).

Phase 3 (essay-iter rounds):
- Stage A reviewers (rubric + citation + plagiarism + coherence) on the full first draft.
- Stage B (GAN) once Stage A passes.
- Stage C (GAN + AI-detection paired) once GAN clears.
