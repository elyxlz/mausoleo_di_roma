# Mausoleo: a hierarchical archival-research pipeline for fascist-era Italian newspapers

BASC0024 Final Year Dissertation

---

# Abstract

Mausoleo is an end-to-end retrieval pipeline for digitised historical newspapers. It comprises an eight-source ensemble VLM OCR stage (cold-cache composite ~0.90 averaged across two evaluation issues), a five-level recursively summarised index stored in ClickHouse with HNSW-backed `vector_similarity` and `tokenbf_v1` FTS secondary indexes, and a typer-based CLI that exposes the index to an LLM agent through eight JSON-emitting endpoints. Existing systems for digitised newspapers (Chronicling America, Europeana Newspapers, Impresso) wrap flat OCR in keyword search and faceted browsing. The recent hierarchical-retrieval lineage in NLP — RAPTOR, GraphRAG, PageIndex — shows that multi-level summary indices outperform flat RAG on global-summarisation queries, with the hierarchy induced from chunk embeddings or graph community detection. Mausoleo's design choice is to use the source's own publication calendar as the tree, so the hierarchy is given by chronology and absent dates can be stored as first-class nodes.

The pipeline is evaluated on *Il Messaggero*, July 1943, against a BM25 baseline over the same article corpus. Across three case studies and eighteen scored trials, Mausoleo averaged 11.3 tool calls per trial against the baseline's 28.3, and was preferred by both LLM judges on a three-dimension rubric across every case (judge means 4.06–4.83 vs 3.17–4.44). Per-case inter-judge κ ranges from 0.14 to 0.57; paired sign tests are reported per case in §6.5. Case 1 lifts the issue of 26 July 1943 (missing from the source archive); Mausoleo represents the absent day as a first-class node whose summary contextualises the gap, while the BM25 baseline can only reason from sibling-day articles. Case 3 is an aggregate-shape question scored on ratio MAE / RMSE against an LLM-built per-week war/domestic oracle (Mausoleo MAE 0.149 vs 0.194; RMSE 0.166 vs 0.220). The dissertation contributes the empirical comparison and the architectural finding that calendar-given hierarchies admit absent-date nodes that learned hierarchies cannot.

---

# Preface

The pipeline this dissertation describes is a hierarchical retrieval system for a single month of a fascist-era Italian daily newspaper, *Il Messaggero* July 1943. The corpus has thirty surviving issues; the issue of 26 July is missing from the digitised fund; the editorial register shifts visibly across 25 to 27 July when the Grand Council deposed Mussolini and the Badoglio government took over. The technical question is whether a calendar-shaped tree of recursively summarised nodes, queried by an LLM agent over a small CLI, beats a BM25 baseline on tool-call efficiency, completeness against a hand-built relevance set, and judge-rated quality. The historiographical question — what does it mean to read a regime-change month in a flat OCR'd corpus — sits behind that and shaped the choice of corpus, but the system is evaluated on its retrieval behaviour and not on its historiographical posture.

The closest priors are the recent hierarchical-retrieval systems in NLP: RAPTOR's recursive cluster-and-summarise tree, GraphRAG's community-detected hierarchy over an entity-relation graph, and PageIndex's exposure of document table-of-contents structure as the retrieval substrate. Mausoleo borrows the multi-level-summary paradigm and substitutes the calendar for the learned tree. That substitution is what makes absent-date nodes representable, which is what makes the missing-26-July case answerable as more than reasoning around the gap. The historiographical material in §2.3 and the archival-science material in §7.3 frame why a chronological tree is a reasonable choice for this kind of source; the engineering chapters (§3 to §6) are the substance.

A note on background. My disciplinary preparation was machine learning coursework; my Italian is conversational, adequate for reading regime-era press but not for retranslating the *MinCulPop veline*, which I read in Murialdi's transcription. The 1885 *Il Messaggero* evaluation issue I hand-transcribed turned out to be denser than the 1910 one, and the page_accuracy floor of 0.683 reported in §4.1 is an annotation error in my own transcription that surfaced too late to redo without invalidating the hill-climb trajectory. I thank Dr Yi Gong for supervising; her comments on §2.3 and §7.2 shaped how the archival-science material sits next to the OCR and case-study chapters.

---

# 1. Introduction

# §1 Introduction

Mausoleo is a hierarchical retrieval pipeline for digitised historical newspapers. The corpus is *Il Messaggero* July 1943: thirty surviving issues, around 6,480 hand-cleaned article transcriptions, five summary tiers (paragraph, article, day, week, month) materialised into a single ClickHouse `nodes` table, queried through a small typer-based CLI by an LLM agent. The benchmark is BM25 over the same article transcriptions; the comparison is on tool-call efficiency, completeness against a hand-built relevance ground-truth, and judge-rated quality on a three-dimension rubric. Three case studies cover the absent issue of 26 July 1943, the editorial register shift across the regime change of 25 to 27 July, and the per-week balance of war versus domestic-politics coverage across the month.

Existing systems for digitised historical newspapers (Chronicling America, Europeana Newspapers, Impresso) all expose a similar interface: keyword search over flat OCR, faceted browsing by date or source, optional enrichment with named-entity recognition, topic models or text-reuse signals (Ehrmann et al., 2020; Düring et al., 2024). The user arrives with a query, receives a ranked article list, and reads articles individually. The interface handles point queries efficiently but provides no aggregate-shape access: a question like "how did war coverage shift across July 1943?" requires the user to read many articles, classify them, and reconstruct the distribution; a question like "what was reported on 26 July 1943?" returns nothing when the issue is missing, with no signal distinguishing absence from no-match.

The hierarchical-retrieval lineage in NLP addresses the aggregate-shape gap directly. RAPTOR (Sarthi et al., 2024) recursively clusters chunk embeddings and stores level-wise summaries, allowing the retriever to pull from a high-level summary or a leaf chunk depending on query scope. GraphRAG (Edge et al., 2024) extracts an entity-relation graph from the corpus, runs Leiden community detection over it, and produces hierarchical community summaries; it reports substantial gains on comprehensiveness and diversity for global-summarisation queries. PageIndex (Zhang and Tang, 2025) navigates by document table-of-contents structure rather than by chunk. Murugaraj et al. (2025) apply a topic-restricted variant of RAG (Topic-RAG) to the Impresso Swiss corpus and report improved retrieval relevance over flat RAG on BERTScore, ROUGE and UniEval metrics. Across the four, the common move is to give the retriever something more than a flat list, and the four differ on how the hierarchy is induced.

Mausoleo's contribution to this lineage is the choice not to induce. The hierarchy is the corpus's own publication calendar (paragraph, article, day, week, month, with year and decade in the production schema), instantiated into a single ClickHouse `nodes` table with parent pointers, recursively summarised by a vLLM batch, and queried by a frontier LLM agent through eight typer-based CLI endpoints (full model configuration in §6.1). Two ClickHouse secondary indexes (HNSW-backed `vector_similarity` over a 384-dim embedding column, `tokenbf_v1` token-bloom over the summary column) sit on the table for vector ANN and FTS respectively. Since the hierarchy is given by the publication calendar, an absent date can be represented as a node whose leaves are empty but whose summary contextualises the gap. Case 1 (§6.2) turns on this representability.

The case studies in §6 measure efficiency (tool calls, characters returned), completeness (recall against a hand-built relevance set, ratio MAE/RMSE against an LLM-built oracle), and quality (mean of two LLM judges scoring a three-dimension rubric) across three trials per system per case, with paired sign tests and inter-judge κ reported per case. The headline finding is that the calendar-given hierarchy outperforms BM25 on every measured cell. The mean differences are visible at the n = 6 sample size even where the sign tests fall short of conventional thresholds.

---

# 2. Literature review

# §2 Literature review

Mausoleo sits at an intersection that three mature literatures address only obliquely. The existing digital newspaper archives are infrastructurally indispensable but mostly query-driven; the hierarchical-retrieval lineage in IR shows multi-resolution access is tractable but usually induces its hierarchies from data; the Annales tradition has been arguing for half a century that historical time is multi-scalar without that argument being operationalised in interface design. The chapter reviews each and locates Mausoleo as an extension to all three.

## §2.1 Existing digital newspaper archives

Three systems define the field. *Chronicling America*, the National Digital Newspaper Program at the Library of Congress, holds roughly 23 million pages of US newsprint dating from 1690 to 1963 and exposes them through faceted search over OCR'd full text. *Europeana Newspapers* aggregates around 28 million pages across forty European languages, again through full-text search backed by OCR of variable quality and limited named-entity enrichment. *Impresso*, the Swiss and Luxembourgish project that is the closest comparator to any new venture in this area, covers roughly two centuries of French, German and Luxembourgish newspapers and sits at the enriched end of the spectrum: alongside OCR it offers named-entity recognition, topic models, lexical-semantic comparison and text-reuse browsing (Ehrmann et al., 2020; Düring et al., 2024).

What unites these systems is the access template. The user arrives with a query, receives a ranked article list, optionally facets the result by date, year or source, and then reads articles individually. Düring et al. (2024) describe the Impresso interface as one of "transparent generosity" about exposing intermediate structure, but the user is still expected to come with a search term in mind. The presupposition is reasonable for most historical research, where the historian arrives with a question already framed.

Mausoleo addresses the access modality this template under-serves: the historian who arrives without a query, wanting to understand a corpus they cannot read in full at the article level. Multi-resolution drill-down with summarised intermediate levels, where the user descends from a month into weeks, into days, into articles and finally into paragraphs, is what the dominant template does not afford. Chronicling America, Europeana and Impresso are excellent at what they are designed to do; Mausoleo extends the available repertoire by offering a different point of entry to the same kind of material.

## §2.2 Information retrieval lineage

Classical information retrieval supplies the baseline. Salton, Wong and Yang (1975) introduced the vector space model; Robertson and Zaragoza (2009) consolidated the probabilistic-relevance tradition that culminated in BM25, still the strongest sparse baseline. Both treat the document collection as a flat set: relevance is computed per document and the structure of the collection plays no role in retrieval.

The recent hierarchical-retrieval lineage breaks with this assumption. RAPTOR (Sarthi et al., 2024) recursively clusters and summarises chunk embeddings bottom-up to induce a tree, then retrieves at multiple abstraction levels, allowing a query to hit a high-level summary or a leaf chunk depending on its scope. GraphRAG (Edge et al., 2024) extracts an entity-relation graph from a corpus, runs Leiden community detection over it, and produces hierarchical community summaries that the system can retrieve at a chosen level of abstraction; the authors report substantial gains on comprehensiveness and diversity over flat RAG for global-summarisation queries. PageIndex (Zhang and Tang, 2025) takes a third route, exposing a document's table-of-contents structure as the retrieval substrate so that the system can navigate by section rather than by chunk. Across the three, the common move is to give the retriever something more than a flat list to work with; they differ in whether the hierarchy is induced by clustering, by graph-community detection or by surface document structure.

The closest prior work on RAG over historical newspapers specifically is Murugaraj et al. (2025), who apply a topic-restricted retrieval pipeline (Topic-RAG) to the Impresso Swiss corpus and report improved retrieval relevance over flat RAG, measured by BERTScore, ROUGE and UniEval. Their pipeline restricts retrieval to documents matching the query's inferred topic, on the assumption that topical coherence between query and retrieved articles is the dominant signal of relevance. That assumption is hard to defend on a corpus with a strong native temporal hierarchy. For a question like "what shifted across the regime collapse?", the topically most-relevant articles cluster around the surface vocabulary of fascism — Mussolini, Grand Council, Badoglio — and Topic-RAG will return them at a uniform editorial register, flattening the shift the question asks about. The BERTScore-style metrics used in their evaluation reward semantic overlap between answer and reference and do not measure whether the answer captures a temporal trajectory. Topic-RAG and Mausoleo are answering different questions: theirs is "given a query, retrieve the topically relevant articles"; Mausoleo's is "given a temporal slice, return what the slice looked like, including its absences." A direct head-to-head on Impresso would be the obvious next step, but the corpus is in French and German and the case-study agent and judges in §6 are configured for Italian, which is a scope cost the dissertation does not absorb.

Mausoleo extends this lineage in one specific respect. The prior systems above apply hierarchical retrieval either to a single document's section structure or to a clustering induced from chunk embeddings; Mausoleo applies the same paradigm to an archival corpus, but with the hierarchy *given* by chronology and not *induced* from the data. This is methodologically defensible because daily newspapers already carry a native temporal hierarchy, and constructing the index over the calendar preserves provenance by construction. In archival terms, it sits within the trajectory Cook (2013) traces from juridical-evidentiary custody towards active mediation (compressing his four-paradigm schema): the chronological scaffold honours original order, and the LLM-generated summaries are activations in the sense of Ketelaar (2001), additions to rather than replacements of the underlying record. Schellenberg's (1956) distinction between primary and secondary value frames the same point: Mausoleo's summaries are a secondary, informational layer that does not displace the primary evidential text underneath.

## §2.3 Historical methodology

The historiographical justification for a temporal hierarchy is older than any of this technology. Braudel (1958), in the *Annales* essay that consolidated the tradition, set out three registers of historical time, the *événement*, the *conjoncture* and the *longue durée*, and argued that serious historical work moves between them rather than electing one. The choice of register is methodological: a study fixed at the level of the event misses the structures within which events occur, and a study fixed at the level of the *longue durée* loses the texture that makes those structures legible. Mausoleo's day, week and month nodes are a digital re-instantiation of Braudel's middle register; the article and paragraph leaves anchor the *événement*; the year and decade levels of the production schema, although outside the scope of the case study, gesture towards the *longue durée*. Historians already think this way, and the design intent is to give them a tool that respects that habit of thought.

The distant-reading programme is the methodological neighbour from literary studies. Moretti (2013) argued that quantitative and large-scale analysis is complementary to close reading rather than subordinate to it; Da (2019) issued the strongest critique, that computational literary studies tends to produce results that are either obvious-and-robust or non-obvious-and-non-robust. Underwood (2019) replied that statistical models are themselves interpretive strategies. The critique applies with less force here, because Mausoleo does not produce statistical claims about its corpus; it organises the corpus and exposes it to interactive descent, deferring interpretation to the user and the agent. Even so, Underwood's framing is the one I adopt: the summaries at each level are interpretive artefacts.

Newspapers as historical sources need their own methodological care. Schudson (1978) treats the social construction of "news" as itself a historical process; Murialdi (1986) remains the standard treatment of the press across the regime period, including the *MinCulPop veline* that directed *Il Messaggero* and the other dailies. For the historian working on July 1943 that means a Mausoleo summary is a derived secondary source whose relation to the regime-aligned primary text must remain auditable: the index keeps both the activation and the leaf paragraph reachable, so a source-critical reading can always descend back to the directive-shaped original article.

Three points follow from these three literatures. The existing newspaper-archive systems supply the access modality Mausoleo extends. The hierarchical-retrieval lineage in NLP validates the multi-tier-summary paradigm and locates the specific move — using a calendar-given hierarchy in place of an induced one. The historiography then supplies the reason the move makes sense on this kind of source. The rest of the dissertation builds the system.

---

# 3. System design

# §3 System design

Mausoleo is three loosely coupled stages connected by a ClickHouse `nodes` table: an OCR pipeline (§3.1), a recursive summariser into a chronological tree (§3.2), and a search and navigation API exposed to an LLM agent (§3.3). The boundary between stages is the schema of the table, so each stage can be swapped or replayed without touching the others. The architecture sits on a small set of design choices that recur through the chapter. The components are modular, evaluable in isolation (OCR against article-level ground truth in §4, the index against summary spot checks in §5, the interface against the case studies in §6), and the hierarchy is given by chronology and not induced by clustering — which is what distinguishes Mausoleo from RAPTOR and GraphRAG. The CLI emits JSON because its user is an LLM agent; the human reads the agent's compiled answer rather than the API output.

## §3.1 OCR pipeline

The input is a directory of scanned JPEGs, six pages per issue on average, for the thirty July 1943 issues of *Il Messaggero*. The output is a per-issue JSON file listing detected articles with headline, body text, and page span. The pipeline runs cold-cache, regenerating every sub-pipeline prediction from the raw images on each invocation, under a budget of thirty minutes wall-clock per issue on two RTX 3090 GPUs (empirical wall ~30.5 minutes on the slower chain; §4.2).

Eight sub-pipelines run in two parallel GPU chains, four per GPU (Figure 3.1). Cross-family diversity is deliberate: three model configurations (Qwen2.5-VL-7B, Qwen3-VL-8B under vLLM, and the same in strict mode) load on each GPU, and the eight sub-pipelines vary column-split granularity (full-page, two- through six-column splits, plus a YOLO small-region detector) so no single layout assumption dominates. The Qwen2.5-VL backbone is a VLM trained for dense document understanding (Bai et al., 2025), used here as a black-box OCR engine prompted to emit structured article JSON. The eight per-source predictions merge deterministically (REPLACE chain + ADDITIVE pass + quality-weighted text selector; tuning in §4.2). The merge is stateless: no LLM arbitration, no seperate post-correction (both tried during the hill-climb and rejected as neutral or harmful, §4.3).

Two empirical observations drive the design. Column-split predictions from a single model are highly correlated, so a fifth column-three Qwen3-VL pipeline contributes less than a different model family at the same column count; cross-family diversity buys ~+0.013 composite over the best single-family ensemble at equal wall-clock. The wall-clock ceiling matters: the unconstrained research configuration reaches ~0.92 composite but takes 50-60 min per issue, outside what a one-month corpus build at 30.5 min/issue can sustain.

Implementation: one `OcrPipelineConfig` over a `ParallelEnsembleOcr` operator that sub-shells the sub-pipelines via `scripts/run_real_ocr.py`. Sub-pipeline JSONs cache to `eval/predictions/`. The 6,480 article-level transcriptions used downstream are a hand-cleaned post-pass of the ensemble's 9,456 raw articles (dedup + cross-page stitching), outside the OCR composite score.

## §3.2 Hierarchical indexing

The index is a single ClickHouse table, `nodes`, that stores the full chronological tree. Each row carries the level (paragraph, article, day, week, month, with the production schema also supporting year and decade above month, and an archive root above decade), a parent identifier, a sibling position, a date range, a summary, an embedding vector, and, for paragraph leaves only, the raw text. Node identifiers are deterministic and human-readable: `1943-07-15_a01_p02` for a paragraph, `1943-07-15` for a day, `1943-07` for a month. Identifier scheme and parent pointers are redundant by design, which lets the agent move up and down the tree without needing a recursive query. Two secondary indexes sit on the table: a ClickHouse `vector_similarity` index (HNSW-backed) over the embedding column for vector ANN, and a `tokenbf_v1` token-bloom-filter index over the summary column for keyword search.

Construction is bottom-up and one level at a time. Article summaries are produced by a vLLM batch over each article's paragraphs; day, week and month summaries by the same recursion at coarser granularity. The summariser prompt is consistent across levels: target 200 to 400 words, preserve named entities, dates, and places explicitly, and write so that an agent can decide from the summary alone whether to descend further. Every summary is embedded with `paraphrase-multilingual-MiniLM-L12-v2` (Reimers and Gurevych, 2019), a 384-dimensional multilingual sentence encoder selected for its strong Italian-language coverage and its compatibility with the build host.

For July 1943 the case-study slice lifts five of the seven production levels, as shown in Figure 3.2: 6,480 article nodes collapse into 31 day nodes, 5 weeks, and 1 month root, for 6,517 nodes in total. Week granularity is a case-study choice rather than a property of the production schema; the rationale is treated in §5.2. The 26 July day node is present even though its leaf paragraphs are empty: the absent issue is stored as a first-class node whose summary contextualises the absence against the surrounding days, which is the architectural precondition for the missing-data case study in §6.2.

The central design commitment is that the hierarchy is given by chronology and not learned by clustering. RAPTOR clusters chunk embeddings recursively to induce a tree (Sarthi et al., 2024). GraphRAG extracts an entity-relation graph and community-detects a hierarchy over it (Edge et al., 2024). Mausoleo does neither, taking the corpus's publication calendar as the tree. One thing this loses is latent thematic structure cutting across time, partially recovered through the embedding-search endpoint described in §3.3. The benefit on this kind of source is that an absent date can be represented as a node, which the case study at §6.2 turns into a measured capability gap relative to the BM25 baseline.

## §3.3 Agent-mediated search

The retrieval surface is a FastAPI server backed by ClickHouse plus a typer-based CLI (`src/mausoleo/server/`, `src/mausoleo/cli.py`). The CLI's user is an LLM agent, so every command emits structured JSON to stdout. Tree traversal: `GET /root`, `/nodes/{id}`, `/nodes/{id}/children`, `/nodes/{id}/parent`, `/nodes/{id}/text` (raw text for leaves, reconstructed from descendants for higher nodes). Search: `POST /search/semantic` (vector ANN over the HNSW-backed `vector_similarity` index, filterable by level or date range), `/search/text` (token-bloom over summary text), and `/search/hybrid` (weighted combination). `GET /stats` reports per-level node counts.

The interaction pattern (Figure 3.3) is closer to a ReAct loop (Yao et al., 2022) than to single-shot RAG (Lewis et al., 2020): the agent enters at the root, reads a summary, decides whether to descend or to search, iterates. Tree traversal supplies provenance and chronological position. Semantic search becomes the fallback when chronology is the wrong axis for the question. The API is minimal and stateless. Reasoning is pushed into the agent, so improvements in the underlying model translate directly.

---

# 4. OCR evaluation

# §4 OCR evaluation

The OCR stage is reported separately because it is the only stage with article-level ground truth, and the only stage whose configuration was hill-climbed against a numerical objective. The headline result, a cold-cache composite of 0.89878 averaged across the two evaluation issues 1885-06-15 and 1910-06-15, is the deployable lower bound throughout the dissertation; the higher-budget 0.9203 configuration treated in §4.3 is the unconstrained ceiling at the same recipe.

## §4.1 Methodology

The evaluation set is two hand-cleaned issues of *Il Messaggero*: 1885-06-15 (41 articles, ~60K characters) and 1910-06-15 (193 articles, ~185K characters). The 1885 issue was hand-transcribed in full from the scanned facsimile; the 1910 issue began as a bootstrap transcription from the strongest single configuration then available and was spot-corrected against the scans. The 1943 corpus is not used as an OCR benchmark: no article-level ground truth exists for it.

The composite score is `0.40·(1−wCER) + 0.25·recall + 0.15·ordering + 0.10·(1−hCER) + 0.10·page_accuracy`, where wCER is length-weighted character error rate over matched articles, recall is the fraction of ground-truth articles matched to a prediction by Jaccard word overlap above 0.15, ordering is a Spearman squared-displacement score, hCER is character error rate restricted to headlines, and page_accuracy is the fraction of matched articles whose predicted page span equals the reference. Article-level matching is preferred to flat full-text CER because the latter penalises any displacement of an article in reading order even when its text is character-perfect; a fragment of the column-six fiction *Magnetizzata* sitting between the two halves of *I maestri elementari non sono pagati* will inflate flat CER on every following article. Article-level matching credits the recovered article and isolates the cross-page failure mode, which is the move that historical-newspaper OCR work such as NewsEye (Doucet et al., 2020) has helped make standard.

Two methodological choices need flagging here. Cold-cache enforcement matters because an earlier production score of 0.92717 turned out to depend on warm caches: nineteen of the twenty-four sources in the merge chains were silently being read from prior experiment runs. A fresh cold-cache run with the same configuration rebaselined to 0.88682. The current 0.89878 is reported as the cold-cache score because that is what the deployed pipeline produces from raw images on the target hardware. Separately, the 1885 page_accuracy floor of 0.683 is an artefact of the ground truth, not the models: every vision-language source independently agrees on the same "wrong" page assignment for twelve articles, which on review of the scans appears to be an annotation error. The composite is therefore capped at approximately 0.872 on 1885; correcting the ground truth mid-hill-climb would have invalidated the trajectory, so the score stands.

## §4.2 Pipeline configuration

The deployable configuration is the eight-source ensemble described in §3.1, run cold-cache under a thirty-minute wall-clock budget per issue on two RTX 3090 GPUs (empirical wall on the harder 1910 issue: 30.5 min GPU0, 28.9 min GPU1). Three model loads sit on each GPU: Qwen2.5-VL-7B (Bai et al., 2025), Qwen3-VL-8B under vLLM, and Qwen3-VL-8B under vLLM in strict mode. Sources differ on column-split granularity (full-page, two-, three-, four-, five-, six-column, and YOLO small-region detection over Zhao et al. (2024) layout boxes). The merge is a deterministic REPLACE chain of nine entries (the four-column Qwen2.5 variant appears twice) plus an ADDITIVE pass for the column-six advertisements source plus a quality-weighted text selector over four trusted sources at a 0.10 body and 0.15 headline marginal-quality floor.

The cold-cache composite of 0.89878 decomposes as 0.872 on 1885 and 0.926 on 1910. Per-component: wCER 0.149 / 0.083, recall 1.000 / 0.984, ordering 0.96 / 0.97, hCER 0.145 / 0.107, page_accuracy 0.683 / 0.974. wCER dominates the composite at 0.40 weight and is what cross-family stacking moved most: 1885 wCER fell from 0.234 to 0.149 over the addition of the four Qwen2.5-VL-7B variants on a Qwen3-VL-8B base, for a stacked +0.013 composite contribution. A leave-one-out at the five-source intermediate stage confirms no entry is redundant (swings  −0.002 to −0.029).

The single biggest gain over the hill-climb was not a model addition. The post-processing filter `scripts/trim_repetitive.py` added +0.0165 alone by stripping raw-JSON regurgitations of seventeen to twenty-eight thousand characters that occasionally leak from the vision-language sources; 1910 wCER halved (0.225 to 0.111) on this fix in isolation. The largest single win is therefore a non-machine-learning data-quality patch: ensemble composition is necessary but not sufficient.

## §4.3 Comparison

Single-configuration baselines fall well below the ensemble. The strongest single Qwen3-VL-8B configuration scores 0.373 wCER on 1885 against the ensemble's 0.149; the four-configuration intermediate ensemble scores 0.835 composite against the eight-source 0.89878, a +0.0998 gain over the strongest like-for-like baseline. Tesseract (Smith, 2007), Calamari (Wick et al., 2018), LayoutLMv3 (Huang et al., 2022) and Donut (Kim et al., 2022) were not evaluated head-to-head; their domain assumptions are too far from fascist-era Italian newsprint for a comparison to be informative.

Three serious attempts at LLM post-correction (Qwen2.5-7B prompt-based fix-up, two-model consensus voter, character-alignment consensus pass) all hurt the score by −0.006 to −0.011 even with strict edit-distance constraints. The post-corrector modernises good articles into paraphrases more than it repairs bad ones. This is worth recording because Thomas et al. (2024) report a 23.3% character-error reduction with BART fine-tuning and 54.5% with Llama-2 13B prompting on BLN600, and Greif et al. (2025) report sub-1% character error after a Gemini-2.0-Flash pass on German city directories. The Italian fascist-era result is the opposite sign, plausibly because the linguistic distance between modern training corpora and regime-era press idiom is larger than for English or German, and because the input wCER is already low enough that the post-corrector's prior over fluent text outweighs the noisy input. The wins reported in Thomas et al. (2024) and Kanerva et al. (2025) do not transfer here.

The cold-cache 0.89878 is reported as the corpus-quality floor; the 0.9203 ceiling (fifty to sixty minutes per issue, thirteen sub-pipelines plus a cross-page completion post-processor) is the upper bound for the same recipe at a doubled budget. The 1910 wCER of 0.083 sits in the same order as Thomas et al.'s (2024) BLN600 raw 0.084 baseline despite the harder source, positioning the stack as competitive on like-for-like noise without a post-correction step.

---

# 5. The knowledge index

# §5 The knowledge index

§3.2 introduced the index; this section gives its schema, its bottom-up construction, and an empirical account of what survives compression at each level. The central claim is that consistent-length summaries across heterogeneous time-scales are a deliberate design choice: navigation becomes predictable, but the index flattens genuinely different temporal granularities into prose of comparable shape. The 25 July 1943 trace below shows the trade-off concretely.

## §5.1 Schema and node IDs

The index is a single ClickHouse `nodes` table whose schema sits in §3.2; in brief, each row carries the level, parent id, sibling position, date range, summary text, a 384-dim embedding from `paraphrase-multilingual-MiniLM-L12-v2` (Reimers and Gurevych, 2019), and (for paragraph leaves only) the raw OCR'd text. Higher-level nodes hold no raw text of their own; their content is the summary plus a pointer downward. This is the architectural form of Ketelaar's (2001) observation that an archival description is a tacit narrative, an activation of the source and not a replacement for it. The summary is never authoritative; the leaves are. The commitment is the one ISAD(G) names as respect des fonds and original order (International Council on Archives, 2000): the catalogue must not rearrange the source.

Node identifiers are deterministic and human-readable: `1943-07-25_a127_p03` for a paragraph, `1943-07-25_a127` for an article, `1943-07-25` for a day, `1943-W29` for a week, `1943-07` for a month. Two secondary indexes sit on the table: a ClickHouse `vector_similarity` index (HNSW-backed) over the embedding column for vector ANN, and a `tokenbf_v1` token-bloom-filter index over the summary column for keyword search. The case-study slice instantiates 6,517 nodes: 6,480 articles, 31 days, 5 weeks, and one month root. The 26 July day node exists despite empty leaves; its summary contextualises the absence against neighbouring days, which is the precondition for the missing-data case study (§6.2).

## §5.2 Recursive summarisation

Construction is bottom-up and one level at a time. Article summaries are produced by a batch over each article's paragraphs; day summaries by a batch over each issue's article summaries; week and month summaries by the same recursion at coarser grain. The lineage is the recursive book summarisation of Wu et al. (2021), which establishes that bottom-up summarisation over a fixed branching factor produces coherent abstractions without exceeding any context window, and the hierarchical attention of Yang et al. (2016).

The summariser prompt is consistent across levels. Each summary targets two to four hundred words, weaves named entities (people, places, organisations) into the prose rather than listing them, preserves dates and quantities verbatim, and is written so an agent can decide from the summary alone whether to descend further. Length is held constant deliberately: a month summary is no longer than an article summary, only at a higher level of abstraction. The benefit is predictable interaction: every node returns roughly the same number of tokens, bounding the case-study tool-call budget (§6.5). The cost is that the month and the article do not, in source terms, carry comparable information; squeezing a month into a single article's envelope forces aggressive thematic compression and risks flattening the difference between an événement and a conjoncture. §5.3 quantifies this on the 25 July trace.

Embeddings use `paraphrase-multilingual-MiniLM-L12-v2` (Reimers and Gurevych, 2019), 384-dim. Embedding-based search complements tree traversal: tree traversal answers "where in time was this", vector search "where else is this mentioned", the cross-temporal axis the chronological hierarchy does not surface. Edge et al.'s (2024) GraphRAG induces both axes from a learned graph, but at the cost of a structure no longer legible to the historian; Mausoleo keeps chronology legible and treats cross-temporal retrieval as a second tool. The case-study scope lifts five of seven production levels; week granularity sits at the resolution at which a single editorial cycle is still legible, between thirty raw day summaries and one already-compressed month.

## §5.3 Quality assessment

Two complementary checks evaluate the summariser. A deterministic spot-check (`scripts/section_5_spotcheck.py`, seed 1943) samples ten July 1943 day summaries excluding the absent 26 July, extracts the top five named entities from each summary by salience, and verifies each entity against the day's hand-cleaned transcription via accent-stripped substring match. The aggregate result is ten of ten day-level passes (forty-eight of fifty entities recovered); the two misses are both `Papa Pio XII`, where the summariser inserted an editorial honorific the press itself never used, preferring `Pio XII` or `il Pontefice`. The miss is a typological artefact, not a faithfulness failure.

An information-loss trace on `1943-07-03` measures named-entity survival across levels. Of thirty-six distinct named entities in the day's three longest articles, seven survive at day level, six at week, one (`Il Messaggero` itself) at month. Compression is not uniform: generic organisational acronyms collapse fastest, specific persons survive to week but are subsumed by month, place names are resilient at day level but vanish at month. The 36 → 7 → 6 → 1 trajectory makes precise the §5.2 trade-off: month-level navigation is for what kind of day it was, not for who was in it.

The 25 July example trace shows the same dynamic on a single load-bearing day. The day node records what *Il Messaggero* knew on 25 July: the Sicilian sgombero of Palermo, the Bologna bombing, Roma post-19-luglio aid, late-fascist register intact ("strenuo valore", "spontanea offerta dei soldati germanici"; verbatim from the day-25 summary, itself preserved from the *Messaggero* original). The 02:40 Grand Council vote and the King's arrest are absent from the day summary because the morning paper went to press before they happened. At week level (1943-W29, 19 to 25 July), the summariser adds an explicit prolepsis: "*Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini.*" This is the summariser supplying historical context the source could not contain; it is interpretive activation, not pure compression, and §7.2 returns to it as a limitation on summariser bias. At month level, the prolepsis collapses into "*l'arresto di Mussolini (25 luglio)*", with the 02:40 timestamp and the Grand Council mechanism compressed away, while the absent 26 July issue is named as documenting "le 24 ore di vuoto". §6.2 picks up the absent-day node from there.

---

# 6. Evaluation: case studies

# §6 Evaluation: case studies

The previous chapters set out the architecture of Mausoleo (§3), the OCR pipeline that supplies its leaves (§4), and the spot-checks that vouch for its higher summary tiers (§5). This chapter is where the dissertation has to earn its claim: does the hierarchical, agent-mediated index make a measurable difference, against a flat-OCR baseline, on the kinds of questions a working historian would put to the July 1943 corpus of *Il Messaggero*? Three case studies are reported, each held to the same researcher agent, task budget and three-metric rubric. Case 1 leads because it is the case where the index's architectural commitments are most exposed: an absent date in the source, a hierarchical tree that has to know the absence is there, and a piece of historiography about regime collapse that the system has to be able to surface from a node whose paragraphs are empty. Cases 2 and 3 carry the conventional efficiency, completeness and quality comparison on aggregate and structural questions. Aggregate results sit in §6.5.

## §6.1 Experimental setup

Both systems share the corpus, researcher agent, task wording and interaction budget; only the toolset differs. The baseline is BM25 over the same hand-cleaned article transcriptions in the `documents` table, ignoring the `nodes` hierarchy. Mausoleo is the agent-mediated tree traversal of §3.3, with the same `documents` corpus plus the `nodes` table and the semantic, text and hybrid search endpoints over it. The researcher agent is Claude Sonnet 4.5 in both arms, with identical system prompt, a tool-call cap of thirty per trial, and three trials per cell at distinct seed prompts (Sonnet 4.5 is not deterministic by integer seed on the OAuth path; trial-to-trial variance is treated as part of the measurement). Holding the agent constant and varying only the tools forestalls the concern that any observed difference is attributable to the agent and not to the index.

Three metrics are applied uniformly. *Efficiency*: tool calls and characters returned to the agent's context. *Completeness*: recall against a hand-built relevance GT for cases 1 and 2, and ratio MAE/RMSE against an LLM-built per-week war/domestic oracle for case 3 (oracle produced by Sonnet 4.5; §6.4). *Quality*: mean of two LLM judges scoring a three-dimension rubric (factual accuracy, comprehensiveness, insight) at 0–5 per dimension. Judge 1 is Claude Opus 4.5; judge 2 is Claude Sonnet 4.5 under a distinct "judge 2" system prompt that fixes a different scoring posture (stricter on factual precision, lighter on insight). Both judges are therefore Anthropic models, and §7.2 returns to cross-vendor robustness as a limitation. Inter-judge κ is reported per case, and a paired sign test across the three trials × two judges per metric.

The relevance GT for cases 1 and 2 was hand-annotated against four works of historiography (Pavone, 1991; Murialdi, 1986; Bosworth, 2005; Deakin, 1962); per-article rationales are in `eval/case_studies/relevance_gt.json`. Single-annotator construction is a limitation (§7.2).

## §6.2 Case study 1 (LEAD): the missing 26 July 1943

The question put to both systems is what *Il Messaggero* reported on 26 July 1943, the day after the deposition of Mussolini. The single most consequential fact about this date in the digitised corpus is that the issue is not there: a date-bounded query against the article corpus returns the empty set. The case leads §6 because it is the definitional capability gap of the indexing architecture: a flat retrieval index has no node for a missing date, so the retriever can only return the empty set and pass the absence to the agent as a null. A calendar-shaped tree, by contrast, instantiates the day node `1943-07-26` regardless of whether its leaves contain text, and so can attach a summary that contextualises the gap. Cook (2013) and Ketelaar (2001) treat archival absence as itself documentary evidence; Mausoleo is what the index looks like once the architecture is asked to honour that.

The baseline is structurally unable to surface the absence as a node. A BM25 query for a date that returns zero hits returns nothing the agent can interpret directly; the researcher agent issues 27.0 tool calls on average (range 26 to 28), reading the surrounding 25 and 27 July issues and inferring backwards. It compiles a recall of 0.67 (range 0.62 to 0.69) against the 42-article relevance set and a judge-mean quality of 4.22 (range 4.00 to 5.00). In two of three trials the baseline agent infers the absence without ever reading a 26 July article, reasoning around the data deficit using its training-corpus knowledge of the regime change. The gap is one of grounding, not of reasoning capacity: a knowledgeable agent can *reason* about absence from sibling-day evidence, but the index gives it no node that *grounds* the absence as a structural fact about the corpus.

Mausoleo can ground it. The day node `1943-07-26` exists in the `nodes` table even though its leaf paragraphs are empty, and its summary, generated at index-build time, is the answer to the question:

> [edizione assente: il fondo archivistico digitalizzato non contiene il numero del 26 luglio 1943 de «Il Messaggero». Il giorno precedente, notte fra 24 e 25 luglio, il Gran Consiglio del Fascismo aveva votato l'ordine del giorno Grandi alle 02:40, e nel pomeriggio del 25 Vittorio Emanuele III aveva fatto arrestare Mussolini all'uscita da Villa Savoia. Il giornale del 27 luglio riapparirà sotto il nuovo governo Badoglio. La lacuna archivistica del 26 luglio è essa stessa documento: testimonia il vuoto editoriale di quelle 24 ore di transizione di regime.]

The Mausoleo agent reaches this node in 13.3 tool calls on average (range 11 to 15), and its compiled answers score a judge mean of 4.56 (range 4.00 to 5.00) against the baseline's 4.22. Recall against the article-id GT is 0.67, tied at the mean with the baseline; trial-to-trial dispersion is diagnosed in `references/case_1_variance_note.md`. Judges disagree at κ = 0.33 and the paired sign test on quality (n = 6) returns p = 0.625, so the case is not statistically decisive at this sample size. The recall tie at 0.67 is itself the symptom: touched-articles is the wrong instrument when the answer is an absent issue. The architectural point is what the case turns on. Date is a first-class structural property of the index, an absent date instantiates a node, the node carries a summary, the absence becomes addressable. A flat retrieval index would need ad-hoc out-of-band metadata to recover the same affordance.

## §6.3 Case study 2: the 25 July regime change

The question is how *Il Messaggero* covered the fall of Mussolini and the transition to Badoglio. The 33-article relevance GT spans three days: the 25 July morning issue, printed before the Grand Council vote and so in late-fascist register ("DOVE ARRIVANO I LIBERATORI" sarcasm, "BIECO FUREORE BRITANNICO" (OCR sic, *Il Messaggero* 25-Jul-1943)); the absent 26 July; and the 27 July reappearance under Badoglio, with the new ministry, the Grand Council *ordine del giorno*, and the King's proclamation. The case is a narrative reconstruction across an editorial register shift, which Mausoleo's day-summary nodes are designed for: each day summary characterises editorial tone alongside content, so the shift is legible from two summary reads rather than a fan-out across hundreds of snippets.

Mausoleo uses 12.3 tool calls on average (range 11 to 13); the baseline uses 29.7 (range 29 to 30), saturating the budget in every trial. Recall against the GT is 0.76 for Mausoleo (zero variance) and 0.62 for the baseline (range 0.55 to 0.70). Quality is 4.83 (range 4.67 to 5.00) for Mausoleo and 4.44 (range 4.00 to 5.00) for the baseline. Inter-judge agreement is the highest of the three cases (κ = 0.57). Paired sign tests give p = 0.250 on completeness and p = 0.375 on quality; direction is consistent and magnitudes meaningful, but the sample is small.

Mausoleo's typical trajectory is to descend from the month root to the days of 25 and 27 July, read the day summaries, and identify the register shift directly from the prose. The baseline issues keyword queries for "Mussolini", "Badoglio", "Gran Consiglio" and "Re Vittorio Emanuele", reads the ranked article list, and compiles a narrative; it captures the political event but tends to miss the editorial-tone shift unless the agent reads in chronological order, which BM25 ranking does not enforce. A useful artefact of the week-of-25-July summary is its prolepsis on Mussolini's still-unannounced arrest: the summary closes "Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini", invisible to a reader of the 25 July issue and addressable only at the week-summary level.

## §6.4 Case study 3: comparative coverage

The question is how the balance of war coverage and domestic-politics coverage shifted across July 1943. This is structurally an aggregate question over a month, and aggregation is where the hierarchy is supposed to pay off: each day-summary node already characterises the day's editorial balance, so the agent aggregates across thirty-one summaries rather than thousands of articles.

The first-run metric was article-id recall against a 27-article set, which produced a misleading 0.07 vs 0.11: day summaries do not enumerate article ids, so an aggregate-question system that answers via compressed summaries collapses to near-zero on touched-set recall by construction. For the rerun, all 6,480 July 1943 articles were classified by Sonnet 4.5 (batched ten  per call, temperature 0) into WAR / DOMESTIC / OTHER and reduced to a per-week war fraction. Oracle: W26 0.558, W27 0.589, W28 0.620, W29 0.733, W30 0.416. Both systems emit five "WEEK 1943-WNN: war_fraction=<float>" lines, scored on MAE and RMSE against the oracle.

On the new metric, Mausoleo wins on ratio accuracy (MAE 0.149 vs 0.194, RMSE 0.166 vs 0.220), on tool calls (8.3 vs 28.3), and on judge-mean quality (4.06 vs 3.17, the largest quality margin of the three cases). Inter-judge κ is the lowest of the three at 0.14, reflecting the difficulty both judges have scoring an aggregate-shape answer against a rubric designed for narrative completeness (§7.2). Paired sign tests give p = 0.250 on ratio-RMSE and p = 0.125 on quality. Once the metric matches the question, the structural prediction holds: a hierarchy that compresses a month into a small number of summary nodes is the right shape of index for a question whose answer is itself a small number of monthly aggregates.

## §6.5 Aggregate results

All eighteen planned trials completed (18/18). The aggregate table below collects per-cell means; the prose around it varies the presentation rather than enumerating identical comparisons.

| Case | Metric | Mausoleo (mean) | Baseline (mean) |
|---|---|---|---|
| Case 1 (07-26 absent) | Tool calls | 13.3 | 27.0 |
| Case 1 | Recall vs GT | 0.67 | 0.67 |
| Case 1 | Quality (judge mean) | 4.56 | 4.22 |
| Case 2 (07-25 regime change) | Tool calls | 12.3 | 29.7 |
| Case 2 | Recall vs GT | 0.76 | 0.62 |
| Case 2 | Quality (judge mean) | 4.83 | 4.44 |
| Case 3 (comparative coverage) | Tool calls | 8.3 | 28.3 |
| Case 3 | Ratio MAE (lower better) | 0.149 | 0.194 |
| Case 3 | Ratio RMSE (lower better) | 0.166 | 0.220 |
| Case 3 | Quality (judge mean) | 4.06 | 3.17 |

The picture across cases is uneven in informative ways. The regime-change reconstruction (case 2) cleared in roughly twelve Mausoleo tool calls against a baseline that saturated its thirty-call budget every trial; recall rose from ~six-in-ten for the baseline to ~three-in-four for Mausoleo, with judges consistent at the high end of the rubric. The missing-day case is the more interesting one numerically: tool calls roughly halve, but the touched-set recall metric ties at 0.67 because the metric is the wrong instrument when the answer is an absence. Quality still tilts to Mausoleo (4.56 vs 4.22), and §6.2 argued the case on architectural grounds with the statistics secondary at this n. Case 3 has the largest quality gap (4.06 vs 3.17, about nine-tenths of a rubric point) and the lowest κ (0.14), which is the rubric's narrative bias showing through, picked up in §7.2. Sign-test p-values run 0.125 to 1.000 across the cases — coarse, but the direction is uniform.

Cost: the one-time OCR build took ~29.7 GPU-hours on 2× RTX 3090; the LLM index build (smaller model for 6,480 article summaries, larger for 37 higher-tier ones; full model identifiers in §6.1) totalled ~$29 USD-equivalent against the OAuth quota. Per trial Mausoleo used 328k input tokens at 76.7 s wall; baseline 321k at 81.6 s. ClickHouse over 6,517 nodes returns sub-second; per-query cost is dominated by the LLM, not the index.

The chars-read column favours the baseline trivially because a day summary is much denser than a BM25 snippet, and that metric is reported but not over-interpreted.

---

# 7. Discussion

# §7 Discussion

## §7.1 What the case studies show

Mausoleo wins consistently on the cases tested, but the shape of the win varies with the question. Aggregate and structural questions are answered cheaply by reading day or week summaries: in cases 2 and 3 Mausoleo descends to the relevant nodes, reads two or three summaries, and assembles its answer, where the baseline reconstructs the same picture article by article. The cost difference is starkest on the comparative-coverage case, where the baseline still issues nearly thirty tool calls while Mausoleo finishes in roughly eight; on case 2, both systems use more, but Mausoleo's twelve against the baseline's saturated thirty is the clearest efficiency gap. Quality follows in the same direction, with the largest margin on case 3 (about nine-tenths of a rubric point) and a smaller but consistent one on case 2. Paired sign tests return p-values between 0.125 and 1.000. With three trials per system the statistical resolution stays coarse, although the direction across all six cells is consistent. Generalisation beyond July 1943 is left as an open empirical question and §7.2 lists it among the limitations.

The missing-data case is architectural. The BM25 baseline cannot return any article from 26 July because none exist, but the agent can reason about the absence from surrounding days; §6.2 reports baseline recall 0.67 on the 25–27 July relevance set. Mausoleo reaches the day node `1943-07-26` and reads its summary, which characterises the absence as evidence of regime collapse and not as the absence of evidence. Recall is matched at 0.67 but the symmetry is misleading: the baseline answers from sibling-day articles, whereas Mausoleo answers from a node whose existence is itself what is to be reported. The missing 26 July is the central case of the chapter because the absence has to be addressable from the index for the question to be answerable at all; the index has to know that the date should have been there. Flat retrieval cannot do this without ad-hoc out-of-band metadata; Mausoleo gets it from the architecture (§7.3).

## §7.2 Limitations

The index is not free to build. The one-month corpus took ~29.7 GPU-hours on 2× RTX 3090 for OCR and ~$29 USD-equivalent for LLM summarisation, with end-to-end wall of ~2 h 20 min above OCR. Linear extrapolation to a full sixty-year *Il Messaggero* run gives ~21,400 GPU-hours and ~$21,000 USD-equivalent at the article tier; higher tiers (week, month, year, decade) collapse upward and scale sub-linearly.

The summariser bias question is the more substantial limitation. Every node summary is the LLM's choice of what is salient, and the W29 prolepsis flagged in §5.3 ("*il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini*") is summariser activation. Quantifying the bias would require human-written reference summaries at day, week and month level, which is a separate piece of work and is not done here. As things stand the activation layer does more interpretive work than has been audited within this dissertation. Further limitations follow. The evaluation runs on a single corpus and a single politically-volatile month; July 1943 was in part chosen because the rupture is so legible, and less volatile corpora may not behave the same way. Both judges are Anthropic models, distinguished only by system prompt; the κ values in §6.5 are therefore intra-vendor, and cross-vendor robustness is untested. The three-dimension rubric was designed for narrative completeness and fits the case-3 aggregate-shape answer poorly (κ = 0.14). Relevance ground truth is single-annotator, and the planned 2-week intra-rater self-consistency check was not performed within the dissertation timeline; second-annotator inter-rater agreement is the obvious next step. Three trials per case make the paired sign test appropriate but do not bound effect-size estimation. Finally, the architecture assumes a strong native temporal hierarchy in the source: archives without dated issues, such as unpublished correspondence or undated collections, need a different organising principle and are out of scope.

## §7.3 Why the calendar-given hierarchy works for this kind of source

The architectural choice the case studies vindicate is narrow: take the publication calendar as the retrieval tree, store an absent date as a node, and let the agent descend through the levels. The choice is defensible on engineering grounds — RAPTOR-style induced hierarchies require a clustering step that adds an axis the retriever then has to negotiate, while a calendar-shaped tree adds none — and the §6 results show that the engineering case is enough on its own: fewer tool calls, higher recall, higher judge means, the largest quality margin on the aggregate-shape question.

The historiographical and archival-science background frames why this particular substitution sits well on a newspaper corpus. Newspaper archives have a strong native temporal hierarchy, and historians of the press routinely use day-week-month windows in their reading practice (Braudel, 1958; Murialdi, 1986). Archival science treats provenance and original order as constitutive of evidential value: a description that rearranges sources by topic destroys the context that made them evidence (Schellenberg, 1956), and the postmodern paradigm Cook (2013) traces explicitly recasts the archivist's description as an active mediation rather than a neutral custodianship, with Ketelaar (2001) supplying the term *activation* for the layer of meaning that descriptive practice adds. Mausoleo's chronological tree happens to satisfy both: original order is preserved because order is the tree, and the summaries sit in a separate column from the leaf paragraphs so the source layer remains reachable beneath every node. Neither commitment was the primary design driver — the primary driver was the absent-26-July case — but they are consistent with the choice and supply the reason a calendar-shaped tree is a defensible substitution rather than an arbitrary one.

The W29 summariser prolepsis flagged in §5.3 ("*il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini*") is where this background touches the engineering. The week-level summary adds historical context the source paragraphs could not contain, which is interpretive activation; §7.2 logs it as a limitation on summariser bias. The schema's separation of leaf text and summary text means the original paragraphs remain reachable for source-critical reading, but the bias-quantification step (human-written reference summaries at day, week, month) is out of scope for this dissertation and is the obvious next piece of work for any deployment beyond the case-study month.

The narrower technical claim, supported directly in §6, is that calendar-given hierarchies admit absent-date nodes that learned hierarchies cannot. This is a measurable architectural property.

---

# 8. Conclusion

## §8 Conclusion

This dissertation set out to test whether a hierarchical, agent-mediated interface to a digitised newspaper archive outperforms keyword search over flat OCR on the kinds of question historians actually ask. Mausoleo's pipeline (a deterministic OCR ensemble feeding a chronologically organised index of article, day, week, and month summaries, queried by an LLM agent over a ClickHouse store with HNSW-backed `vector_similarity` and `tokenbf_v1` FTS indices) was evaluated against a BM25 baseline on the same corpus across three case studies on *Il Messaggero* July 1943. The results, reported in §6.5 and discussed in §7.1, support the working thesis. On the regime-change case Mausoleo reached the relevant evidence in roughly twelve tool calls against the baseline's thirty, with higher recall against the article-level ground truth and higher judge-rated quality. On the comparative-coverage case Mausoleo produced lower per-week ratio error than the baseline while issuing fewer tool calls. The missing 1943-07-26, treated by the index as a first-class node whose summary contextualises the absence, exposed a definitional capability gap: flat retrieval can reason around the absence but cannot ground it in a node that the index itself owns.

The system sits in the recent hierarchical-retrieval lineage in NLP, alongside RAPTOR (Sarthi et al., 2024), GraphRAG (Edge et al., 2024) and PageIndex (Zhang and Tang, 2025). Its contribution to the lineage is one specific architectural choice: take the source's publication calendar as the retrieval tree, in place of inducing the hierarchy from chunk embeddings or community detection. This makes the absent-26-July node representable, and that representability drives the Case 1 result. §7.3 develops the framing in light of historians' working assumptions about multi-resolution time and the archival-science commitment to provenance; the engineering substance is in §3 to §6.

Several directions extend the work. Scaling beyond a single month is the most immediate; OCR scales roughly linearly while the higher index tiers grow sub-linearly, so a multi-decade run is mostly an engineering exercise. Federated retrieval across heterogeneous archives — each with its own provenance conventions — would need a richer node model than the present single-source one. A community-correction workflow over activation layer is a third direction the schema already supports: editorial corrections to summaries do not corrupt the leaves, because source and activation sit in distinct columns of the same row. None of these would change the basic design commitment. Mausoleo is one interface that satisfies it. The wider empirical claim the dissertation supports is that the commitment itself is a useful starting point for archival-research interfaces.

---

# References

Asai, A., Wu, Z., Wang, Y., Sil, A. and Hajishirzi, H. (2023) 'Self-RAG: Learning to retrieve, generate, and critique through self-reflection', *arXiv preprint* arXiv:2310.11511.

Bai, S., Chen, K., Liu, X., Wang, J., Ge, W., Song, S., Dang, K., et al. (2025) 'Qwen2.5-VL Technical Report', *arXiv preprint* arXiv:2502.13923.

Bonsaver, G. (2007) *Censorship and Literature in Fascist Italy*. Toronto: University of Toronto Press.

Bosworth, R.J.B. (2005) *Mussolini's Italy: Life under the Dictatorship, 1915–1945*. London: Allen Lane.

Braudel, F. (1958) 'Histoire et sciences sociales: la longue durée', *Annales. Économies, Sociétés, Civilisations*, 13(4), pp. 725–753.

Cook, T. (2013) 'Evidence, memory, identity, and community: four shifting archival paradigms', *Archival Science*, 13(2–3), pp. 95–120.

Da, N.Z. (2019) 'The computational case against computational literary studies', *Critical Inquiry*, 45(3), pp. 601–639.

Deakin, F.W. (1962) *The Brutal Friendship: Mussolini, Hitler and the Fall of Italian Fascism*. London: Weidenfeld and Nicolson.

Doucet, A., Gabay, S., Granroth-Wilding, M., Hulden, M., Düring, M., Pfanzelter, E., Marjanen, J., et al. (2020) 'NewsEye: a digital investigator for historical newspapers', in *Proceedings of Digital Humanities 2020*. Ottawa: ADHO.

Düring, M., Bunout, E. and Guido, D. (2024) 'Transparent generosity: introducing the impresso interface for the exploration of semantically enriched historical newspapers', *Historical Methods: A Journal of Quantitative and Interdisciplinary History*, 57(3), pp. 1–20. doi:10.1080/01615440.2024.2344004.

Edge, D., Trinh, H., Cheng, N., Bradley, J., Chao, A., Mody, A., Truitt, S., Metropolitansky, D., Ness, R.O. and Larson, J. (2024) 'From local to global: a Graph RAG approach to query-focused summarization', *arXiv preprint* arXiv:2404.16130.

Ehrmann, M., Romanello, M., Clematide, S., Ströbel, P.B. and Barman, R. (2020) 'Language resources for historical newspapers: the impresso collection', in *Proceedings of the 12th Language Resources and Evaluation Conference*. Marseille: ELRA, pp. 958–968.

Forno, M. (2012) *Informazione e potere: Storia del giornalismo italiano*. Roma–Bari: Laterza.

Greif, D., Griesshaber, D. and Greif, J. (2025) 'Multimodal LLMs for OCR, OCR post-correction and named entity recognition in historical documents', *arXiv preprint* arXiv:2504.00414.

Huang, Y., Lv, T., Cui, L., Lu, Y. and Wei, F. (2022) 'LayoutLMv3: pre-training for document AI with unified text and image masking', *arXiv preprint* arXiv:2204.08387.

International Council on Archives (2000) *ISAD(G): General International Standard Archival Description*. 2nd edn. Ottawa: International Council on Archives.

Jockers, M.L. (2013) *Macroanalysis: Digital Methods and Literary History*. Urbana: University of Illinois Press.

Kanerva, J., Ledins, C., Käpyaho, S. and Ginter, F. (2025) 'OCR error post-correction with LLMs in historical documents: no free lunches', *arXiv preprint* arXiv:2502.01205.

Ketelaar, E. (2001) 'Tacit narratives: the meanings of archives', *Archival Science*, 1(2), pp. 131–141.

Kim, G., Hong, T., Yim, M., Nam, J., Park, J., Yim, J., Hwang, W., Yun, S., Han, D. and Park, S. (2022) 'OCR-free document understanding transformer', in *European Conference on Computer Vision*. Cham: Springer, pp. 498–517.

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., et al. (2020) 'Retrieval-augmented generation for knowledge-intensive NLP tasks', *Advances in Neural Information Processing Systems*, 33, pp. 9459–9474.

Moretti, F. (2013) *Distant Reading*. London: Verso.

Murialdi, P. (1986) *Storia del giornalismo italiano: Dalle gazzette a Internet*. Bologna: Il Mulino.

Murugaraj, M., Lamsiyah, S., Düring, M. and Theobald, M. (2025) 'Topic-RAG over historical newspapers: improving retrieval relevance over flat RAG on the impresso corpus', *Computational Humanities Research*, 1(e15), pp. 1–24.

Pavone, C. (1991) *Una guerra civile: Saggio storico sulla moralità nella Resistenza*. Torino: Bollati Boringhieri.

Reimers, N. and Gurevych, I. (2019) 'Sentence-BERT: sentence embeddings using Siamese BERT-networks', in *Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing*. Hong Kong: ACL, pp. 3982–3992.

Robertson, S. and Zaragoza, H. (2009) 'The probabilistic relevance framework: BM25 and beyond', *Foundations and Trends in Information Retrieval*, 3(4), pp. 333–389.

Salton, G., Wong, A. and Yang, C.S. (1975) 'A vector space model for automatic indexing', *Communications of the ACM*, 18(11), pp. 613–620.

Sarthi, P., Abdullah, S., Tuli, A., Khanna, S., Goldie, A. and Manning, C.D. (2024) 'RAPTOR: Recursive abstractive processing for tree-organized retrieval', in *Proceedings of the 12th International Conference on Learning Representations (ICLR)*.

Schellenberg, T.R. (1956) *Modern Archives: Principles and Techniques*. Chicago: Society of American Archivists.

Schudson, M. (1978) *Discovering the News: A Social History of American Newspapers*. New York: Basic Books.

Smith, R. (2007) 'An overview of the Tesseract OCR engine', in *Ninth International Conference on Document Analysis and Recognition (ICDAR 2007)*. Washington, DC: IEEE, pp. 629–633.

Thomas, A., Gaizauskas, R. and Lu, H. (2024) 'Leveraging LLMs for post-OCR correction of historical newspapers', in *Proceedings of LT4HALA 2024 at LREC-COLING*. Torino: ELRA, pp. 116–121.

Underwood, T. (2019) *Distant Horizons: Digital Evidence and Literary Change*. Chicago: University of Chicago Press.

Zhang, M. and Tang, J. (2025) 'PageIndex: vectorless, reasoning-based RAG via hierarchical tree index', *arXiv preprint* arXiv:2510.13347.

Wick, C., Reul, C. and Puppe, F. (2018) 'Calamari: a high-performance tensorflow-based deep learning package for optical character recognition', *Digital Humanities Quarterly*, 14(2).

Wu, J., Ouyang, L., Ziegler, D.M., Stiennon, N., Lowe, R., Leike, J. and Christiano, P. (2021) 'Recursively summarizing books with human feedback', *arXiv preprint* arXiv:2109.10862.

Yang, Z., Yang, D., Dyer, C., He, X., Smola, A. and Hovy, E. (2016) 'Hierarchical attention networks for document classification', in *Proceedings of NAACL-HLT 2016*. San Diego: ACL, pp. 1480–1489.

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K. and Cao, Y. (2022) 'ReAct: Synergizing reasoning and acting in language models', *arXiv preprint* arXiv:2210.03629.

Zhao, Z., Kang, X., Wang, T., Mao, Y., Wang, Y., Li, X. and Liu, Y. (2024) 'DocLayout-YOLO: enhancing document layout analysis through diverse synthetic data and global-to-local adaptive perception', *arXiv preprint* arXiv:2410.12628.
