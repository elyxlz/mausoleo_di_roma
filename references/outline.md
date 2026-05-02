# Mausoleo dissertation outline (BASC0024)

**Working thesis (E)**: Mausoleo's OCR + hierarchical indexing + agent-mediated search pipeline outperforms keyword-search-over-flat-OCR on archival research tasks, demonstrated through case studies on *Il Messaggero* July 1943.

**Discipline pair (cat 2 grounding)**: History + Computer Science. The system is a CS contribution; the case studies are historical research questions; the interdisciplinary move is applied CS for humanities. Cognitive science / philosophy / media studies appear only in the Discussion as related framings.

**Word budget**: 9000 words main body. Abstract ≤300, Preface ≤500 (excluded). Hard cap 10000.

**Submission spec**: BASC0024, anonymous candidate code, A4, 20mm margins, Arial/Calibri/TNR ≥10pt, 1.5 line spacing, candidate code in footer.

**Corpus**: *Il Messaggero* July 1943, 30 daily issues (07-01 to 07-31, 07-26 missing). OCR via Mausoleo's ensemble pipeline (composite score 0.89878 on the 1943-07 issues per commit `dfcbab2`). Hand-cleaned transcriptions in `eval/transcriptions/`.

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

**Sub-claims**:
1. Digital newspaper archives at scale (millions of pages) are practically inaccessible to historians: keyword search over OCR'd text returns either too much (broad terms) or too little (rare terms), and ignores the structure of how a newspaper aggregates information across time.
2. The dominant access paradigm (Chronicling America, Europeana Newspapers, Impresso) assumes the user arrives with a query. Many genuinely historical questions ("how did the paper cover X across a month") are not point queries; they are aggregate, multi-resolution questions that flat retrieval cannot serve.
3. Mausoleo proposes an alternative: build a hierarchical knowledge index (paragraph → article → day → week → month → archive) over OCR'd output, then expose it via an agent-mediated drill-down API. The dissertation's contribution is the system + an empirical demonstration that it outperforms flat retrieval on archival research tasks.

**Evidence type**: Position paper framing. Cite Chronicling America, Europeana Newspapers, Impresso as comparators. Cite Moretti distant-reading and Boroș/Murugaraj historical-newspaper RAG as the methodological neighbours.

**Citation pool**: Moretti 2013, Ehrmann/Düring 2024 (Impresso), Murugaraj 2025 (Topic-RAG historical newspapers), Edge 2024 (GraphRAG), Sarthi 2024 (RAPTOR), VectifyAI 2025 (PageIndex).

---

## §2 Literature review (1500 words)

Three sub-sections. Tight, position-defining.

### §2.1 Existing digital newspaper archives (~400 words)
- Chronicling America (LoC): scale + UX template
- Europeana Newspapers: multi-language IIIF + OCR
- Impresso: NER, topic models, lexical-semantic enrichment, faceted search
- **Gap**: all three assume query-driven access. None offers hierarchical drill-down or LLM-mediated narrative aggregation.

### §2.2 Information retrieval lineage (~500 words)
- Classical IR: BM25, TF-IDF (Salton, Robertson)
- Dense retrieval: BGE-M3, ColBERT (mention briefly, will not be primary baseline)
- Hierarchical retrieval: RAPTOR (Sarthi 2024), GraphRAG (Edge 2024), PageIndex (VectifyAI 2025)
- RAG over historical newspapers: Murugaraj 2025 (Topic-RAG, the immediate prior art)
- **Gap that Mausoleo fills**: hierarchical retrieval where the hierarchy is *given* by archival structure (chronology) rather than *induced* by clustering. Provenance-respecting (Cook 2013, archival science).

### §2.3 Historical methodology (~600 words)
- Annales school multi-scale time (Braudel: longue durée / conjoncture / événement)
- Distant reading (Moretti, Jockers); critique (Da 2019, Underwood 2019)
- Newspapers as historical sources: editorial bias, agenda-setting, methodology of using press as evidence (Schudson, Murialdi for Italian press)
- Italian fascist press: Murialdi 1986, Forno 2012, Bonsaver 2007 for the regime context

**Sub-claims**:
1. Existing newspaper archives prioritise full-text search over multi-resolution access; Mausoleo addresses a different access modality.
2. The hierarchical-retrieval lineage (RAPTOR, GraphRAG, PageIndex) validates the paradigm but applies it to single documents or learned hierarchies; Mausoleo applies it to archival corpora with chronologically given hierarchies.
3. Annales-school multi-scale time provides the historiographical justification for a temporal hierarchy: historians already think this way; Mausoleo gives them a tool that respects it.

**Citation pool**: Moretti 2013, Jockers 2013, Da 2019, Underwood 2019, Salton 1975, Sarthi 2024, Edge 2024, VectifyAI 2025, Murugaraj 2025, Cook 2013, Schellenberg 1956, Braudel 1958, Murialdi 1986, Forno 2012, Bonsaver 2007. Approx 15 sources, all on disk.

---

## §3 System design (1500 words)

Three sub-sections describing the architecture.

### §3.1 OCR pipeline (~600 words)
- Input: scanned JPEGs of *Il Messaggero* daily issues (~6 pages each, July 1943).
- Pipeline: VLM-based OCR (Qwen2.5-VL-7B), column-split + ensemble across 6 sub-pipelines, post-correction not used in final config.
- 30-min/issue cold-cache constraint on 2× RTX 3090.
- Reference: existing `plan/01_ocr.md`.

### §3.2 Hierarchical indexing (~500 words)
- 7-level tree: paragraph → article → day → month → year → decade → archive (collapsed to month-as-root for the July 1943 case).
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
- Bootstrap GT + hand-cleaned GT for 1885-06-15, 1910-06-15, 1943-07-{01..31}.
- Composite score: weighted CER + WER + article F1 + page-span accuracy.
- Cold-cache constraint: ≤30 min wall-clock per issue from raw images, no warm-cache cheating.

### §4.2 Pipeline configuration (~400 words)
- Final config: 6 sub-pipelines, 2 GPU chains, ensemble + LLM arbitration step.
- Composite score on 1943 July: ~0.898 (per commit `dfcbab2`).
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

The heart of the dissertation. Three case studies, each comparing Mausoleo vs a flat-OCR keyword baseline.

### §6.1 Experimental setup (~400 words)
- **Baseline**: keyword search over the same OCR'd text (no hierarchy, no summaries). BM25 over articles. Returns ranked article list to a human reader, who must compile findings.
- **Mausoleo**: agent-mediated drill-down via the CLI tools. Same underlying OCR.
- **Same LLM** (Claude or GPT-4o) used as the "researcher" agent for both systems, controlled for capability.
- **Metrics**: completeness (recall of relevant articles vs human-annotated GT), efficiency (steps to answer, total text read), quality (LLM-as-judge on the final compiled answer), serendipity (did the system surface relevant info the agent didn't explicitly query for).
- LLM-as-judge protocol: blind evaluation, multi-dimension rubric, multiple judge runs.

### §6.2 Case study 1: the July 25 regime change (~700 words)
**Question**: How did *Il Messaggero* cover the fall of Mussolini and the transition to the Badoglio government?

**Baseline run**: keyword queries for "Mussolini", "Badoglio", "Gran Consiglio", "Re Vittorio Emanuele". Returns a list of articles; agent compiles a narrative.

**Mausoleo run**: agent starts at month root, drills to week-of-25-July, then to day 1943-07-25, 1943-07-27 (07-26 missing), reads day summaries, descends to article level for specific evidence.

**Expected findings**:
- 1943-07-25 morning issue: pure late-fascist register (battle bulletins, "DOVE ARRIVANO I LIBERATORI", "BIECO FURORE BRITANNICO"). 273 articles.
- 1943-07-26: missing from corpus, the rupture day.
- 1943-07-27 onward: Badoglio-government register; tonal shift in editorial voice.
- Mausoleo's day-level summary surfaces this discontinuity directly; the baseline produces a list of "Mussolini" articles that the agent must read fully to discover the same shift.

**Quantitative claim**: Mausoleo gets to the regime-change finding in ~5 tool calls; baseline requires reading ~30 articles fully.

### §6.3 Case study 2: comparative coverage (~600 words)
**Question**: How does the balance of war coverage vs domestic-politics coverage shift over July 1943?

**Baseline**: cannot answer without manual aggregation across all 30 days. Agent reads several articles per day, classifies each, computes the ratio.

**Mausoleo**: queries day-level summaries directly, which already characterise the day's editorial balance.

**Expected findings**: war coverage dominates 07-01 to 07-25 (Sicily campaign), drops sharply 07-27 to 07-31 (Badoglio government, transitional editorial line). Domestic politics rise correspondingly.

**Quantitative claim**: Mausoleo answers in ~10 tool calls; baseline requires ~150+ article reads or surface-level keyword counts that miss editorial framing.

### §6.4 Case study 3: the missing 1943-07-26 (~500 words)
**Question**: What was reported on 26 July 1943, the day after Mussolini's arrest?

**Baseline**: returns zero results (no articles for that date). Agent has no way to surface why.

**Mausoleo**: day-level summary explicitly notes the gap, contextualised against the political event. Agent can compose: "the 26 July issue is missing from this archive; the fall of Mussolini occurred at 02:40 on 25 July; the gap likely reflects either the paper not being printed or its survival rate in the archive."

**Quantitative claim**: Mausoleo provides explanatory context for the gap; baseline produces null. (This is a small but methodologically significant case: handling missing data is itself an archival capability.)

### §6.5 Aggregate results (~~no allocation, summary~)
- Across three case studies: Mausoleo wins on efficiency, completeness, and serendipity. Baseline ties or wins on a fourth dimension (TBD by experimental run).
- Cost: Mausoleo's index-build cost is paid once; baseline's per-query cost is recurrent.

**Citation pool**: Moretti 2013, Da 2019 (for the methodological critique we have to address), Murialdi 1986, Forno 2012, Pavone 1991, Bosworth 2005, Deakin 1962. 7 sources, all on disk.

---

## §7 Discussion (900 words)

### §7.1 What the case studies show (~300 words)
The pipeline is better than flat retrieval on multi-resolution archival research tasks. Specifically: aggregate questions ("how did coverage change"), structural questions ("what discontinuity is observable"), and missing-data questions ("what was reported on date X") are where the hierarchical index pays off.

### §7.2 Limitations (~300 words)
- Index-build cost: not free, scales with corpus size.
- LLM bias: every summary is the LLM's choice of what's salient; this is a form of second-order agenda-setting.
- Single-corpus, single-month evaluation: results may not generalise to less politically-volatile corpora.
- The OCR ensemble's composite score is on three eval issues; ground-truth at the article level for July 1943 is bootstrap-only.

### §7.3 Related framings (~300 words)
Brief mentions, not full engagement, since the core thesis is engineering not philosophy:
- The architecture happens to mirror cognitive-scientific models of hierarchical knowledge (Friston predictive processing, Miller chunking) but the dissertation does not depend on that connection.
- The summarisation operation is a form of computational hermeneutic circle (Gadamer) but the empirical claim does not require this framing.
- Mausoleo participates in the Annales-school multi-scale time tradition by giving it a computational instantiation, but this is methodological, not theoretical.

**Citation pool**: Friston 2010, Miller 1956, Gadamer 1960, Braudel 1958. 4 sources, mentioned briefly.

---

## §8 Conclusion (500 words)

Restate: pipeline outperforms flat baseline on archival research tasks (case studies showed it on three dimensions). Discussion: this result is interdisciplinary because archival research is a humanities task and the system is a CS contribution.

Future work: scaling beyond a single month; multi-archive support; community-contributed OCR/summary corrections; generic-corpus extension (any unstructured time-stamped data).

---

## Citation pool (consolidated)

Approx 35 distinct citations across the dissertation, all currently on disk in `references/papers/`. Distribution:
- §1 Introduction: 6 sources (Moretti, Ehrmann/Düring, Murugaraj, Edge, Sarthi, VectifyAI)
- §2 Literature review: 15 sources (above + Salton, Cook, Schellenberg, Da, Underwood, Jockers, Braudel, Murialdi, Forno, Bonsaver, Schudson)
- §3 System design: 7 sources (Qwen2.5-VL, BGE-M3, RAPTOR, GraphRAG, Lewis 2020, ReAct, Self-RAG)
- §4 OCR evaluation: 11 sources (the OCR cluster: Smith, Calamari, LayoutLMv3, Donut, DocLayout-YOLO, Qwen2.5-VL, Soper, Maheshwari, NewsEye, Impresso, Thomas)
- §5 Knowledge index: 6 sources (BGE-M3, Wu, Yang HAN, GraphRAG, Ketelaar, ICA ISAD)
- §6 Evaluation: 7 sources (Moretti, Da, Murialdi, Forno, Pavone, Bosworth, Deakin)
- §7 Discussion: 4 sources (Friston, Miller, Gadamer, Braudel)
- §8 Conclusion: 0 new

Total unique: ~35 sources. Per the essay-iter rule (8-15 per major section), this is well within range. All on disk, ready for the citation critic.

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
