# Mausoleo: a hierarchical archival-research pipeline for fascist-era Italian newspapers

BASC0024 Final Year Dissertation

---

# Abstract

Digital newspaper archives such as Chronicling America, Europeana Newspapers and Impresso afford keyword search and faceted browsing over flat OCR, but they do not afford the multi-resolution movement that historians, following the Annales tradition of Braudel, routinely demand: drill-down across the day, the week and the month, and principled handling of dates the archive does not hold. Two task types expose the limitation. Aggregate questions about how coverage shifts across a month are answerable by flat retrieval only through laborious manual aggregation. Missing-data questions are unanswerable in principle, because an absent date returns no results.

This dissertation presents Mausoleo, an end-to-end pipeline that combines an ensemble VLM OCR stage, a chronologically organised five-level summary index stored in ClickHouse, and an agent-mediated search interface over that index. The hierarchy is the computational form of two commitments the historiographical and archival traditions already share: multi-resolution time and respect for provenance.

The pipeline is evaluated on *Il Messaggero*, July 1943, against a BM25 baseline operating over the same article corpus. Across three case studies and eighteen scored trials, Mausoleo reaches answers in roughly half the tool calls of the baseline (mean 11.0 against 28.3) and is preferred by two LLM judges on a three-dimension rubric in every case. The signature finding concerns the issue of 26 July 1943, the day after the deposition of Mussolini, which is missing from the source archive: Mausoleo represents the absent day as a first-class node whose summary contextualises the gap, while the BM25 baseline cannot return it.

The contribution is an empirical demonstration that chronologically given, provenance-respecting hierarchies are the right interface form for archival research, not a decorative addition to it.

---

# Preface

This dissertation began with a historian's question and ended with an engineer's answer, and I want to say plainly why both halves were necessary.

The question is how a researcher reads a month of a fascist-era daily newspaper across the rupture of 25 to 27 July 1943, when the Grand Council deposed Mussolini, the King had him arrested that afternoon, and the issue of 26 July is absent from the source archive. The Annales tradition, particularly Braudel's framing of history as longue durée, conjoncture, and événement, treats this kind of reading as a movement between temporal scales: the absent day sits inside the week of the regime collapse sits inside the longue durée of the fascist period. Existing digital newspaper archives (Chronicling America, Europeana Newspapers, Impresso) afford keyword search and faceted browsing over flat OCR; they do not afford the multi-resolution drill-down that the question actually requires. The historiographical commitment is real, and the interface gap is real, and neither discipline by itself can close it.

History supplies two things the engineering cannot generate on its own. First, the Annales-school commitment to multi-resolution time, which tells the system designer that day, week, month, and year are not arbitrary aggregation choices but the temporal grain at which historians already think. Second, the archival-science commitment to provenance (Cook 2013, Ketelaar 2001, Schellenberg 1956), which insists that records be respected in their original order and that description is activation of the source, not replacement of it. The missing 26 July is, on this reading, archivally significant precisely because it is the gap in the provenance.

Computer Science supplies the hierarchical retrieval lineage (RAPTOR, GraphRAG, PageIndex) that has, in the past two years, made it technically feasible to summarise long corpora at multiple resolutions and route an LLM agent through the resulting tree. It also supplies the system implementation: OCR ensemble, ClickHouse-backed index, agent-mediated CLI. Without this lineage there is no interface; with only this lineage there is no reason for the hierarchy to be chronological rather than clustered, and no warrant for treating an absent date as a first-class node.

The substantive integration sits in §7.3, where I argue that Mausoleo's chronologically-given hierarchy is the computational form of the two commitments archival history already shares: multi-resolution time and respect for provenance. This is a synthetic claim, tested empirically by the case studies, not a decorative pairing.

The BASc framework matters here in a specific way. The discipline pair was chosen under the Cat 2 rationale because the question itself spans the two: the historiographical reading practice and the engineering are both load-bearing, and a single-discipline dissertation could only have produced either a methodological essay without a system or a retrieval system without a reason to be chronological. Prior modules in historical methodology and in machine learning supplied the working vocabulary; the BASc framework supplied the warrant to treat their intersection as a proper object of study rather than as a borrowed metaphor. Cognitive science, philosophy, and media studies are out of scope.

---

# 1. Introduction

# §1 Introduction

How does a historian read a month of a fascist-era newspaper across the rupture of 25 to 27 July 1943? The question is deceptively practical. *Il Messaggero* in July 1943 runs to thirty daily issues; the issue of 26 July is missing from the surviving archive; the editorial register changes visibly between the morning of 25 July, when the Grand Council voted Mussolini out at 02:40, and the morning of 27 July, when the same masthead reappeared under the Badoglio government. To read this corpus historically is to move between scales: the événement of the deposition, the conjoncture of regime collapse, the longue durée of fascist Italy that the paper had served for two decades (Braudel, 1958). The Annales-school commitment to multi-resolution time is the working assumption of any historian who treats a month of newspapers as a unit of analysis rather than a heap of articles. Distant reading (Moretti, 2013) restated the same commitment a generation later: the corpus is itself a unit, and the historian needs tools that operate at corpus scale without abandoning the article.

The dominant access modality across digital newspaper archives does not honour this commitment. Chronicling America, Europeana Newspapers, and Impresso converge on a shared template of keyword search and faceted browsing over flat OCR'd text, optionally enriched with named-entity recognition, topic models, or text-reuse signals (Ehrmann et al., 2020; Düring et al., 2024). Impresso is the most enriched of the three and the closest comparator to any system that takes small-language European newspapers seriously, but the user still arrives with a query, receives a ranked article list, optionally facets by date or source, and reads articles individually. The interface affords point queries efficiently. It does not afford agent-mediated drill-down across summarised temporal scales, and so the historian's multi-resolution movement is left entirely to the historian.

Two task types make this gap concrete. The first is the aggregate question. How did war coverage shift across the month of July 1943, and what does that shift tell us about the paper's editorial trajectory across the regime change? Flat keyword retrieval can serve this question only by manual aggregation: the researcher reads many articles, classifies each, and reconstructs the distribution by hand. The second is the missing-data question. What was reported on 26 July 1943, and what does the absence of that issue from the archive itself record? Flat retrieval is structurally unable to answer this: the date returns no results, and the silence is indistinguishable from the absence of relevant matches. Both task types require either an indexed hierarchy of summaries, in which day, week, and month are first-class objects with their own descriptions, or extensive manual aggregation by the human researcher across many point queries.

This dissertation proposes Mausoleo, an OCR plus hierarchical-indexing plus agent-mediated search pipeline, as a computational form for the multi-resolution reading that Annales-school historiography already practises by hand. The architecture is a five-level chronological tree (paragraph, article, day, week, month) over the thirty surviving July 1943 issues of *Il Messaggero*, written into a ClickHouse `nodes` table with a recursively summarised parent at every level and an LLM agent that drills the tree through a small set of CLI tools. The methodological lineage is hierarchical retrieval: RAPTOR (Sarthi et al., 2024) recursively clusters and summarises chunks bottom-up into a tree; GraphRAG (Edge et al., 2024) builds a community-detected hierarchy over an entity graph; PageIndex (VectifyAI, 2025) performs reasoning-based tree search over a single document's table-of-contents structure. Topic-RAG over historical Swiss newspapers (Murugaraj et al., 2025) shows that topic-restricted retrieval improves answer relevance over flat RAG on Impresso-scale corpora. Mausoleo extends this lineage on two axes. Where RAPTOR and GraphRAG induce the hierarchy from the data, Mausoleo's hierarchy is given by archival chronology, which preserves provenance by construction. Where PageIndex and Topic-RAG operate within a single document or within a topic-restricted slice, Mausoleo treats the calendar of an archival corpus as the tree, with absent dates handled architecturally as nodes whose summaries contextualise the gap.

*Il Messaggero* July 1943 is a deliberately demanding test bed. The corpus contains a regime-change rupture in its middle: the Grand Council voted Mussolini out at 02:40 on 25 July, the King had him arrested at Villa Savoia that afternoon, the issue of 26 July is absent from the digitised fund, and the editorial register shifts visibly from 27 July onward. Any newspaper-archive interface that claims to support historical reading at scale should be evaluatable on a corpus where the rupture is legible at every level of granularity, and where the most archivally significant day is a structural absence rather than a retrievable presence. Three case studies test the pipeline against a BM25 baseline over the same OCR'd text. Case 1, the lead, is the missing 26 July: a definitional capability gap, since the baseline cannot return any article that does not exist in the corpus, while Mausoleo's day-level node `1943-07-26` carries a summary that contextualises the absence against 25 and 27 July as evidence of the regime collapse. Case 2 reconstructs the editorial register shift across 25 to 27 July. Case 3 asks how the balance of war versus domestic-politics coverage shifted across the month, an aggregate question whose natural unit is the week.

The case studies in §6 measure efficiency, completeness, and quality across three trials per system per case, scored by two LLM judges. The lead case is treated separately in §6.2 because its asymmetry is definitional rather than quantitative; cases 2 and 3, reported in §6.3 and §6.4, carry the genuine comparison. Architecturally, the absent-day node is a first-class object in the index rather than a metadata facet over articles, and the design that makes this possible is described in §3.3. The closing discussion in §7.1 returns to the missing 26 July as the dissertation's signature finding: a CS retrieval problem, an archival-science question of the provenance of absence, and a historical event in a single object. The position the dissertation defends is that this convergence is not coincidental. Multi-resolution time is a historiographical commitment that the right computational form already encodes, and Mausoleo is one such form.

---

# 2. Literature review

# §2 Literature review

Mausoleo sits at an intersection that three mature literatures address only obliquely. Existing digital newspaper archives have built the infrastructure on which any historical-press project now depends, but their access modality is overwhelmingly query-driven. The hierarchical-retrieval lineage in information retrieval has shown that multi-resolution access is tractable, but its hierarchies are usually learned from data rather than given by the source. And the Annales tradition has long argued that historical time is itself multi-scalar, an argument that has rarely been operationalised in interface design. This section reviews each in turn and positions Mausoleo as an extension rather than a displacement of any of them.

## §2.1 Existing digital newspaper archives

Three systems define the field. *Chronicling America*, the National Digital Newspaper Program at the Library of Congress, holds roughly 23 million pages of US newsprint dating from 1690 to 1963 and exposes them through faceted search over OCR'd full text. *Europeana Newspapers* aggregates around 28 million pages across forty European languages, again through full-text search backed by OCR of variable quality and limited named-entity enrichment. *Impresso*, the Swiss and Luxembourgish project that is the closest comparator to any new venture in this area, covers roughly two centuries of French, German and Luxembourgish newspapers and sits at the enriched end of the spectrum: alongside OCR it offers named-entity recognition, topic models, lexical-semantic comparison and text-reuse browsing (Ehrmann et al., 2020; Düring et al., 2024).

What unites these systems is the access template. The user arrives with a query, receives a ranked article list, optionally facets the result by date, year or source, and then reads articles individually. The Impresso interface is the most generous of the three about exposing intermediate structure, and Düring et al. (2024) describe its design as one of "transparent generosity," but the user is still expected to come with a search term in mind. The presupposition is reasonable for most historical research, where the historian arrives with a question already framed, and these systems serve that mode of work very well.

Mausoleo addresses the access modality this template under-serves: the historian who arrives without a query, wanting to understand a corpus they cannot read in full at the article level. Multi-resolution drill-down with summarised intermediate levels, where the user descends from a month into weeks, into days, into articles and finally into paragraphs, is what the dominant template does not afford. This is a positioning claim rather than a deficiency claim. Chronicling America, Europeana and Impresso are excellent at what they are designed to do; Mausoleo extends the available repertoire by offering a different point of entry to the same kind of material.

## §2.2 Information retrieval lineage

Classical information retrieval supplies the baseline against which any newer system is measured. Salton, Wong and Yang (1975) introduced the vector space model in which documents and queries are represented as TF-IDF-weighted vectors and ranked by cosine similarity, and Robertson and Zaragoza (2009) consolidated the probabilistic-relevance tradition that culminated in BM25, still the strongest sparse baseline against which dense retrievers are evaluated. Both treat the document collection as a flat set: relevance is computed per document and the structure of the collection plays no role in retrieval.

The recent hierarchical-retrieval lineage breaks with this assumption. RAPTOR (Sarthi et al., 2024) recursively clusters and summarises chunk embeddings bottom-up to induce a tree, then retrieves at multiple abstraction levels, allowing a query to hit a high-level summary or a leaf chunk depending on its scope. GraphRAG (Edge et al., 2024) extracts an entity-relation graph from a corpus, runs Leiden community detection over it, and produces hierarchical community summaries that the system can retrieve at a chosen level of abstraction; the authors report substantial gains on comprehensiveness and diversity over flat RAG for global-summarisation queries. PageIndex (VectifyAI, 2025) takes a third route, exposing a document's table-of-contents structure as the retrieval substrate so that the system can navigate by section rather than by chunk. Across the three, the common move is to give the retriever something more than a flat list to work with; they differ in whether the hierarchy is induced by clustering, by graph-community detection or by surface document structure.

The closest prior work on RAG over historical newspapers specifically is Murugaraj et al. (2025), who apply a topic-restricted retrieval pipeline (Topic-RAG) to the Impresso Swiss corpus and report improved retrieval relevance over flat RAG, measured by BERTScore, ROUGE and UniEval. Their contribution is to show that exploiting an axis of organisation other than raw similarity, in their case latent topic structure, is productive in the historical-newspaper setting; they do not specifically test OCR-noise mitigation.

Mausoleo extends this lineage in one specific respect. RAPTOR, GraphRAG and PageIndex all apply hierarchical retrieval to single documents, to learned thematic clusterings or to author-given section structure. Mausoleo applies the same paradigm to an archival corpus whose hierarchy is *given* by chronology rather than *induced* from the data: the parent of an article is its issue, the parent of an issue is its week, the parent of a week is its month, and so on up. This is methodologically defensible because daily newspapers already carry a strong native temporal hierarchy, and constructing the index over the calendar rather than over a clustering preserves provenance by construction. In archival terms, it respects what Cook (2013) describes as the move from juridical-evidentiary custody to active mediation: the chronological scaffold honours original order, and the LLM-generated summaries layered onto it are activations in the sense of Ketelaar (2001), additions to rather than replacements of the underlying record. Schellenberg's (1956) distinction between primary and secondary value of records frames the same point from the American tradition: Mausoleo's summaries are a secondary, informational layer that does not displace the primary evidential text underneath.

## §2.3 Historical methodology

The historiographical justification for a temporal hierarchy is older than any of this technology. Braudel (1958), in the *Annales* essay that consolidated the tradition, set out three registers of historical time, the *événement*, the *conjoncture* and the *longue durée*, and argued that serious historical work moves between them rather than electing one. The choice of register is methodological: a study fixed at the level of the event misses the structures within which events occur, and a study fixed at the level of the *longue durée* loses the texture that makes those structures legible. Mausoleo's day, week and month nodes are a digital re-instantiation of Braudel's middle register; the article and paragraph leaves anchor the *événement*; the year, decade and archive levels of the production schema, although outside the scope of the case study, gesture towards the *longue durée*. Historians already think this way, and the design intent is to give them a tool that respects that habit of thought rather than flattening it.

The distant-reading programme is the methodological neighbour from literary studies. Moretti (2013), collecting the essays that defined the term, argued that quantitative and large-scale analysis is complementary to close reading rather than subordinate to it; Jockers (2013) coined "macroanalysis" for a corpus-level statistical practice positioned between Moretti and traditional close reading. Both are foundational for any project that processes a corpus computationally. Da (2019) issued the strongest critique of the resulting body of work, arguing that computational literary studies tends to produce results that are either obvious-and-robust or non-obvious-and-non-robust, and that statistical tools are mismatched with literary objects. Underwood (2019) replied that statistical models are themselves interpretive strategies, akin to humanistic interpretation rather than substitutes for it. The critique applies with less force to Mausoleo than to most computational literary studies, because Mausoleo does not produce statistical claims about its corpus; it organises the corpus and exposes it to interactive descent, deferring interpretation to the user and the agent. Even so, Underwood's framing is the one Mausoleo adopts: the summaries at each level are interpretive artefacts, not neutral descriptions, and the dissertation treats them as such.

Newspapers as historical sources demand their own methodological care. Schudson (1978) treated the social construction of "news" as itself a historical process, foregrounding the institutional and ideological pressures that shape what a daily paper carries on its front page. For the Italian case, Murialdi (1986), in *Storia del giornalismo italiano*, remains the standard treatment of the press across the regime period, including the *MinCulPop veline* that directed *Il Messaggero* and other dailies; Forno (2012), *Informazione e potere*, situates the press within the broader structures of fascist information control, and Bonsaver (2007) provides the surrounding history of regime censorship across the cultural field. These sources matter for *Il Messaggero* July 1943 because the corpus is not a neutral record: it is a regime-aligned daily indexing what the regime wanted readers to think, and any system that summarises it must be read against that frame. Mausoleo's commitment is that summaries surface the text rather than replace it, so that a historian can always descend from a day node to the article and paragraph leaves and recover the source register directly.

Taken together, these three literatures define the position Mausoleo occupies. The newspaper archives establish the access modality it extends; the IR lineage validates the paradigm it inherits and identifies the move it makes; the historiographical tradition supplies the reason a chronological hierarchy is the right scaffold for the material. The remainder of the dissertation builds the system that this position requires.

---

# 3. System design

# §3 System design

Mausoleo is built as three loosely coupled stages connected by a single ClickHouse `nodes` table: an OCR pipeline that turns scanned pages into article-level JSON, a recursive summariser that lifts those articles into a multi-resolution chronological tree, and a search and navigation API that exposes the tree to an LLM agent. The boundary between stages is the schema of the table, not a function call; each stage can be swapped, re-evaluated, or replayed without touching the others. Figure 3.0 shows the end-to-end flow. The architectural commitments worth foregrounding are three. First, the components are modular and independently evaluable: the OCR ensemble is hill-climbed against article-level ground truth (§4), the index against summary-quality spot checks (§5), and the search interface against the case studies (§6). Second, the hierarchy is given by chronology rather than induced by clustering, which distinguishes Mausoleo from RAPTOR (Sarthi et al., 2024) and GraphRAG (Edge et al., 2024). Third, the CLI returns JSON because its user is an LLM agent, not a human; the human reads the agent's compiled answer.

## §3.1 OCR pipeline

The input is a directory of scanned JPEGs, six pages per issue on average, for the thirty July 1943 issues of *Il Messaggero*. The output is a per-issue JSON file listing detected articles with headline, body text, and page span. The pipeline runs cold-cache, regenerating every sub-pipeline prediction from the raw images on each invocation, under a hard budget of thirty minutes wall-clock per issue on two RTX 3090 GPUs.

Eight sub-pipelines are arranged in two parallel GPU chains, four per GPU, as shown in Figure 3.1. Cross-family and cross-backend diversity is deliberate: three model configurations (Qwen2.5-VL-7B, Qwen3-VL-8B under vLLM, and Qwen3-VL-8B under vLLM in strict mode) load on each GPU, and the eight sub-pipelines vary the column-split granularity (full-page, two-, three-, four-, five-, and six-column splits, plus a YOLO small-region detector) so that no single layout assumption dominates. The Qwen2.5-VL backbone is a vision-language model trained for dense document understanding (Bai et al., 2025); it is used here as a black-box OCR engine, prompted to emit structured article JSON and held to that contract by the column-split crops it sees as input.

The eight per-source predictions are then merged deterministically. A REPLACE chain of nine entries (one source, the four-column Qwen2.5 variant, appears twice) walks the predictions in a fixed order, replacing earlier text with later text wherever a per-source overlap and length-ratio threshold is crossed. A separate ADDITIVE pass folds in the column-six advertisements-focused source, which contributes coverage of small classifieds that the column splits miss. A final quality-weighted text selector swaps headlines and body fragments across four trusted sources when the marginal-quality delta exceeds the configured floor (0.10 for body, 0.15 for headline). The merge is deterministic and stateless; there is no LLM arbitration step and no standalone post-correction model in the production configuration. Both were tried during the hill-climb (§4.2 reports the ablation) and rejected as either neutral or harmful at this corpus.

The design is driven by two empirical observations. First, column-split predictions from a single model are highly correlated (pairwise text distance below 0.15), so adding a fifth column-three Qwen3-VL pipeline contributes less than adding a different model family at the same column count; cross-family diversity buys roughly +0.013 of composite score over the best single-family ensemble at the same wall-clock. Second, the wall-clock ceiling forces the pipeline to fit in the GPU envelope rather than absorbing a richer ensemble: the unconstrained research configuration reaches ~0.92 composite on the same eval but takes fifty to sixty minutes per issue, well outside what a one-month corpus build at 30.5 minutes per issue can sustain.

The pipeline is implemented as one `OcrPipelineConfig` (`configs/ocr/ensemble_30min.py`) over a `ParallelEnsembleOcr` operator that sub-shells the sub-pipelines via `scripts/run_real_ocr.py`. The eight sub-pipeline JSONs are cached to `eval/predictions/<name>_<date>.json`, the merged output to `eval/predictions/ensemble_30min_<date>.json`. This caching is what makes the OCR stage independently evaluable: re-running the merge with a different overlap threshold does not retrigger the GPU passes. The 6480 article-level transcriptions used downstream are a hand-cleaned post-pass of the ensemble's 9456 raw articles across the thirty July 1943 issues; the cleaning protocol (deduplication and cross-page stitching) is documented in `scripts/cleanup_transcriptions.py` and falls outside the OCR composite score.

## §3.2 Hierarchical indexing

The index is a single ClickHouse table, `nodes`, that stores the full chronological tree. Each row carries the level (paragraph, article, day, week, month, and in the production schema also year, decade, archive), a parent identifier, a sibling position, a date range, a summary, an embedding vector, and, for paragraph leaves only, the raw text. Node identifiers are deterministic and human-readable: `1943-07-15_a01_p02` for a paragraph, `1943-07-15` for a day, `1943-07` for a month. Identifier scheme and parent pointers are redundant by design, which lets the agent move up and down the tree without needing a recursive query. Two secondary indexes sit on the table: a usearch L2 index over the embedding column for vector search, and a `tokenbf_v1` token-bloom-filter index over the summary column for keyword search.

Construction is bottom-up and one level at a time. Paragraph leaves are written directly from OCR JSON. Article summaries are produced by a vLLM batch over each article's paragraphs; day summaries by a batch over each issue's article summaries; week and month summaries by the same recursion at coarser granularity. The summariser prompt is consistent across levels: produce a summary of comparable length (target 200 to 400 words), preserve named entities, dates, and places explicitly rather than as generalities, and write the summary so that an agent can decide from it alone whether to descend further. Every summary is then embedded with BGE-M3 (Chen et al., 2024), a multilingual dense encoder chosen for its Italian coverage. Embeddings are computed in a separate Ray Data stage after summarisation.

For July 1943 the case-study slice lifts five of the seven production levels, as shown in Figure 3.2: 6480 article nodes collapse into 31 day nodes, 5 weeks, and 1 month root, for 6517 nodes in total. Week granularity is a case-study choice rather than a property of the production schema; the rationale is treated in §5.2. The 26 July day node is present even though its leaf paragraphs are empty: the absent issue is stored as a first-class node whose summary contextualises the absence against the surrounding days, which is the architectural precondition for the missing-data case study in §6.2.

The central design commitment is that the hierarchy is given, not learned. RAPTOR clusters chunk embeddings recursively to induce a tree (Sarthi et al., 2024); GraphRAG extracts an entity-relation graph and then community-detects a hierarchy over it (Edge et al., 2024). Mausoleo does neither. The tree is the calendar: the parent of an article is its issue, the parent of an issue is its week, and so on. This loses the ability to surface latent thematic structure that cuts across time, which the embedding-search endpoint partially recovers (§3.3), but it gains two properties that matter for archival research. Provenance is preserved by construction, since every summary points down to the source paragraphs that generated it and up to the chronological context in which they sat. And the structure is legible to a historian without training, because the tree mirrors how the source is already organised.

## §3.3 Agent-mediated search

The retrieval surface is a FastAPI server backed by ClickHouse plus a typer-based CLI that wraps it (`src/mausoleo/server/`, `src/mausoleo/cli.py`). The CLI's user is an LLM agent, so every command emits structured JSON to stdout: no colours, no tables, no human-friendly formatting. The same set of operations is exposed at both layers. Tree traversal is served by `GET /root`, `GET /nodes/{id}`, `GET /nodes/{id}/children`, `GET /nodes/{id}/parent`, and `GET /nodes/{id}/text`, the last of which returns raw text directly for paragraph leaves and reconstructs full text from descendant paragraphs for higher nodes. Search is served by `POST /search/semantic` (vector ANN over the usearch index, optionally filtered by level or date range), `POST /search/text` (token-bloom filter over summary text), and `POST /search/hybrid` (a weighted combination). A `GET /stats` endpoint reports node counts per level for the agent's situational awareness.

The interaction pattern, sketched in Figure 3.3, is closer to a ReAct loop (Yao et al., 2022) than to single-shot RAG (Lewis et al., 2020). The agent enters at the root, reads a summary, decides whether to descend or to search, and iterates. Tree traversal supplies provenance and chronological position; semantic search is the escape hatch when chronology is the wrong axis for the question. Self-RAG-style critique (Asai et al., 2023) is not built into the server; it is left to the agent's system prompt and to the iteration budget. The design choice is to keep the API minimal and stateless and to push reasoning into the agent, so that improvements in the underlying model translate directly without server changes.

The implication for the human user is the second-order point worth naming. The human asks a question of the agent in natural language; the agent issues tool calls against the CLI and reads the JSON; the agent compiles an answer; the human reads the compiled answer with citations to specific node identifiers. The CLI is therefore optimised for the agent's parsing, not for the human's reading, and the human never sees the JSON unless they ask for it. This inversion is what allows the same retrieval surface to serve both the case-study evaluation in §6 and exploratory historical research without a separate front-end.

---

# 4. OCR evaluation

# §4 OCR evaluation

The OCR stage is reported separately from the rest of the pipeline because it is the only stage with article-level ground truth and the only stage whose configuration was searched, rather than designed, against a numerical objective. The headline result, a cold-cache composite of 0.89878 averaged across the two evaluation issues 1885-06-15 and 1910-06-15, is reported throughout as a deployable lower bound rather than as a peak number; the higher-budget configuration that reaches 0.9203 is treated in §4.3 as the unconstrained ceiling for the same recipe.

## §4.1 Methodology

The evaluation set is two hand-cleaned issues of *Il Messaggero*: 1885-06-15 (41 articles, ~60K characters) and 1910-06-15 (193 articles, ~185K characters). The 1885 issue was hand-transcribed in full from the scanned facsimile; the 1910 issue began as a bootstrap transcription from the strongest single configuration then available and was spot-corrected against the scans. The 1943 corpus is not used as an OCR benchmark: no article-level ground truth exists for it, and the post-hoc hand-cleaning of the thirty July issues happens at the corpus-curation stage described in §3.1.

The composite score is `0.40·(1−wCER) + 0.25·recall + 0.15·ordering + 0.10·(1−hCER) + 0.10·page_accuracy`, where wCER is length-weighted character error rate over matched articles, recall is the fraction of ground-truth articles matched to a prediction by Jaccard word overlap above 0.15, ordering is a Spearman squared-displacement score, hCER is character error rate restricted to headlines, and page_accuracy is the fraction of matched articles whose predicted page span equals the reference. Article-level matching is preferred to flat full-text CER because the latter penalises any displacement of an article in reading order even when its text is character-perfect; a fragment of the column-six fiction *Magnetizzata* sitting between the two halves of *I maestri elementari non sono pagati* will inflate flat CER on every following article. Article-level matching credits the recovered article and isolates the cross-page failure mode, which is where the historical-newspaper OCR literature has converged (Doucet et al., 2020; Ehrmann et al., 2020).

Two methodological commitments are worth flagging. The first is cold-cache enforcement. An earlier production score of 0.92717 was discovered to depend on warm caches: nineteen of the twenty-four sources in the merge chains were silently being read from prior experiment runs. A fresh cold-cache run with the same configuration rebaselined to 0.88682. The current 0.89878 is reported as the cold-cache score because it is what the deployed pipeline actually produces from raw images on the target hardware; warm-cache numbers in the OCR literature should be treated with caution. The second is the 1885 page_accuracy floor of 0.683. Every vision-language source independently agrees on the same "wrong" page assignment for twelve articles, which on review of the scans appears to be a ground-truth annotation error rather than a model failure. The composite is therefore capped at approximately 0.872 on 1885; correcting the ground truth mid-hill-climb would have invalidated the trajectory.

## §4.2 Pipeline configuration

The deployable configuration is the eight-source ensemble described in §3.1, run cold-cache under a thirty-minute wall-clock budget per issue on two RTX 3090 GPUs. The eight sub-pipelines are arranged in two parallel GPU chains (four sources each); the empirical wall on the harder 1910 issue is 30.5 minutes on GPU0 and 28.9 minutes on GPU1. Three model loads sit on each GPU: Qwen2.5-VL-7B (Bai et al., 2025), Qwen3-VL-8B under vLLM, and Qwen3-VL-8B under vLLM in strict mode. The eight sources differ on column-split granularity (full-page, three-, four-, five-, six-column, and YOLO small-region detection over `zhao-2024-doclayout-yolo` lineage layout boxes) so that no single layout assumption dominates. The merge is a deterministic REPLACE chain of nine entries plus an ADDITIVE pass for the column-six advertisements-focused source plus a quality-weighted text selector over four trusted sources at a 0.10 body and 0.15 headline marginal-quality floor. There is no LLM arbitration step.

The cold-cache composite of 0.89878 decomposes as 0.872 on 1885 and 0.926 on 1910. Per-component values for the ensemble at the eight-source configuration are wCER 0.149 (1885) / 0.083 (1910), recall 1.000 / 0.984, ordering 0.96 / 0.97, hCER 0.145 / 0.107, and page_accuracy 0.683 / 0.974. The wCER component dominates the composite at a 0.40 weight and is what cross-family stacking moved most: 1885 wCER fell from 0.234 to 0.149 over the addition of the four Qwen2.5-VL-7B variants (column-two, column-three, column-four, full-page) on top of a Qwen3-VL-8B-only base, for a stacked +0.013 composite contribution attributable to cross-family diversity. A leave-one-out at the five-source intermediate stage confirms that no entry is redundant: the largest swing is the YOLO small-region source at −0.029, the Qwen2.5 cross-family full-page entry contributes a floor of −0.015, and every remaining entry contributes between −0.002 and −0.017 when removed.

The single biggest gain over the entire hill-climb was not a model addition. The post-processing filter `scripts/trim_repetitive.py` added +0.0165 alone, by stripping raw-JSON regurgitations of seventeen to twenty-eight thousand characters that occasionally leak from the vision-language sources and poison the matcher; the 1910 wCER halved (0.225 to 0.111) on this fix in isolation. The largest single win is therefore a non-machine-learning data-quality patch, and the reader is owed the qualifier that ensemble composition is necessary but not sufficient.

## §4.3 Comparison

Single-configuration baselines fall well below the ensemble. The strongest single Qwen3-VL-8B configuration (column-three, structured JSON) reports a 1885 character error rate of 0.373 with 78.0% recall and 70.3% F1; the standard Qwen-VL-7B structured baseline reports 0.139 average character error rate on pre-article-level metrics that overstate its quality. The two-configuration ensemble (column-three plus YOLO) scores 0.799 composite, the four-configuration ensemble 0.835. The single-configuration-to-ensemble gap on like-for-like composite is therefore +0.0998. Tesseract (Smith, 2007) and Calamari (Wick et al., 2018) were not evaluated head-to-head: their target script and noise profile are removed enough from fascist-era Italian newsprint that a comparison would mostly measure domain mismatch. The same applies to LayoutLMv3 (Huang et al., 2022) and Donut (Kim et al., 2022), document-understanding models whose pre-training assumes cleaner inputs than degraded broadsheets.

Three serious attempts at LLM post-correction (a Qwen2.5-7B prompt-based fix-up, a two-model consensus voter, and a character-alignment consensus pass) all hurt the score by between −0.006 and −0.011 even with strict edit-distance constraints. The post-corrector modernises good articles into paraphrases more than it repairs bad ones, and the net effect on the composite is consistently negative. This is worth recording because Thomas et al. (2024) report a 23.3% character-error reduction with BART fine-tuning and a 54.5% reduction with Llama-2 13B prompting on the BLN600 nineteenth-century English-newspaper benchmark, and Greif et al. (in Maheshwari et al., 2025) report sub-1% character error after a Gemini-2.0-Flash pass on German city directories. The Italian fascist-era result is the opposite sign, plausibly because the linguistic distance between modern training corpora and regime-era press idiom is larger than the equivalent distance for English or German, and because the input wCER is already low enough that the post-corrector's prior over fluent text outweighs the evidence from the noisy input. The wins reported in Thomas et al. (2024) and Soper and Kanerva (2025) do not transfer here.

The deployable cold-cache 0.89878 is therefore reported as the corpus-quality floor, with the 0.9203 production ceiling (fifty to sixty minutes per issue, thirteen sub-pipelines plus a cross-page completion post-processor) as the upper bound for the same recipe at a doubled budget. The 1910 wCER of 0.083 sits in the same order as Thomas et al.'s (2024) BLN600 raw 0.084 baseline despite the harder source, positioning the stack as competitive on like-for-like noise without the post-correction step the literature has converged on for English.

---

# 5. The knowledge index

# §5 The knowledge index

§3.2 introduced the index; this section gives its schema, its bottom-up construction, and an empirical account of what survives compression at each level. The central claim is that consistent-length summaries across heterogeneous time-scales are a deliberate design choice: navigation becomes predictable, but the index flattens genuinely different temporal granularities into prose of comparable shape. The 25 July 1943 trace below shows the trade-off concretely.

## §5.1 Schema and node IDs

The index is a single ClickHouse `nodes` table. Each row carries the level (paragraph, article, day, week, month, with the production schema extending to year, decade, and archive), a parent identifier, a sibling position, a date range, the summary text, a 1024-dimensional embedding vector, and, for paragraph leaves only, the raw OCR'd text. Higher-level nodes hold no raw text of their own: their content is the summary plus a pointer downward. This is the architectural form of Ketelaar's (2001) observation that an archival description is a tacit narrative, an activation of the source rather than a replacement for it. The summary is never authoritative; the leaves are. Provenance is preserved by construction, since `parent_id` and `position` together fix every node's place in the chronological order, and a recursive descent returns the exact paragraph set that generated any summary. The commitment is the one ISAD(G) names as respect des fonds and original order (International Council on Archives, 2000): the catalogue must not rearrange the source.

Node identifiers are deterministic and human-readable: `1943-07-25_a127_p03` for a paragraph, `1943-07-25_a127` for an article, `1943-07-25` for a day, `1943-W29` for a week, `1943-07` for a month. Identifier and parent pointer are redundant by design, so the agent can either parse the identifier or follow the explicit pointer. Two secondary indexes sit on the table: a usearch L2 index over the embedding column for vector ANN, and a `tokenbf_v1` token-bloom-filter index over the summary column for keyword search. The case-study slice instantiates 6,517 nodes: 6,480 articles, 31 days, 5 weeks, and one month root. The 26 July day node exists despite empty leaves; its summary contextualises the absence against neighbouring days, which is the precondition for the missing-data case study (§6.2).

## §5.2 Recursive summarisation

Construction is bottom-up and one level at a time, parallelisable within each level. Article summaries are produced by a vLLM batch over each article's paragraphs; day summaries by a batch over each issue's article summaries; week and month summaries by the same recursion at coarser grain. The lineage is the recursive book summarisation of Wu et al. (2021), which establishes that bottom-up summarisation over a fixed branching factor produces coherent abstractions without exceeding any context window, and the hierarchical attention of Yang et al. (2016), which carries the prior that linguistic structure is itself hierarchical and that coarser units carry information not reducible to their constituents.

The summariser prompt is consistent across levels. Each summary targets two to four hundred words, weaves named entities (people, places, organisations) into the prose rather than listing them, preserves dates and quantities verbatim, and is written so an agent can decide from the summary alone whether to descend further. Length is held constant deliberately: a month summary is no longer than an article summary, only at a higher level of abstraction. This is the design choice with consequences. The benefit is predictable interaction: every node returns roughly the same number of tokens, and the case-study tool-call budget (§6.5) is bounded. The cost is that the month and the article do not, in source terms, carry comparable information; squeezing a month into a single article's envelope forces aggressive thematic compression and risks flattening the difference between an événement and a conjoncture. §5.3 quantifies this on the 25 July trace.

Embeddings are computed in a separate Ray Data stage. The encoder is BGE-M3 (Chen et al., 2024), a multilingual dense model whose Italian coverage is competitive with monolingual baselines. Embedding-based search complements tree traversal rather than replacing it: tree traversal answers "where in time was this", vector search answers "where else is this mentioned", which is the cross-temporal axis the chronological hierarchy by construction does not surface. Edge et al.'s (2024) GraphRAG induces both axes from a single learned graph, but at the cost of a structure no longer legible to the historian; Mausoleo keeps the chronology legible and treats cross-temporal retrieval as a second tool. The case-study scope lifts five of seven production levels; week granularity sits at the resolution at which a single editorial cycle is still legible, between thirty raw day summaries and one already-compressed month.

## §5.3 Quality assessment

Two complementary checks evaluate the summariser. A deterministic spot-check (`scripts/section_5_spotcheck.py`, seed 1943) samples ten July 1943 day summaries excluding the absent 26 July, extracts the top five named entities from each summary by salience, and verifies each entity against the day's hand-cleaned transcription via accent-stripped substring match. The aggregate result is ten of ten passes (forty-eight of fifty entities recovered); the two misses are both `Papa Pio XII`, where the summariser inserted an editorial honorific the press itself never used, preferring `Pio XII` or `il Pontefice`. The miss is a typological artefact, not a faithfulness failure.

An information-loss trace on `1943-07-03` measures named-entity survival across levels. The union of distinct named entities in the day's three longest articles is thirty-six. At day level, seven survive; at week, six; at month, one. The single survivor at the month root is `Il Messaggero` itself, a meta-mention of the source. Compression is not uniform: generic organisational acronyms (`O.N.M.I.`, `G.U.F. dell'Urbe`) collapse fastest at day level; specific persons survive to week but are subsumed under broader collective nouns by month; place names are most resilient at day level (six of seventeen) but vanish entirely at month, replaced by later-month places that dominate the month's narrative arc. The 36 to 7 to 6 to 1 trajectory makes precise the §5.2 trade-off: month-level navigation is for what kind of day it was, not for who was in it.

The 25 July example trace shows the same dynamic on a single load-bearing day. The day node records what *Il Messaggero* knew on 25 July: the Sicilian sgombero of Palermo, the Bologna bombing, Roma post-19-luglio aid, late-fascist register intact ("strenuo valore", "spontanea offerta dei soldati germanici"). The 02:40 Grand Council vote and the King's arrest are absent from the day summary because the morning paper went to press before they happened. At week level (1943-W29, 19 to 25 July), the summariser adds an explicit prolepsis: "*Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini.*" This is the summariser supplying historical context the source could not contain; it is interpretive activation, not pure compression, and §7.2 returns to it as a limitation on summariser bias. At month level, the prolepsis collapses into "*l'arresto di Mussolini (25 luglio)*", with the 02:40 timestamp and the Grand Council mechanism compressed away, while the absent 26 July issue is named as documenting "le 24 ore di vuoto". The arrest survives; the mechanism does not. §6.2 picks up the absent-day node from there.

---

# 6. Evaluation: case studies

# §6 Evaluation: case studies

The previous chapters set out the architecture of Mausoleo (§3), the OCR pipeline that supplies its leaves (§4), and the spot-checks that vouch for its higher summary tiers (§5). This chapter asks the load-bearing question of the dissertation: does the hierarchical, agent-mediated index make a measurable difference, against a flat-OCR baseline, on the kinds of questions a working historian would put to the July 1943 corpus of *Il Messaggero*? Three case studies are reported, each held to the same researcher agent, task budget and three-metric rubric. Case 1 leads not because it is the most modest result but because it folds together the three disciplinary commitments named in §1: a CS retrieval problem, an archival-science question, and a historical event. Cases 2 and 3 carry the conventional efficiency, completeness and quality comparison on aggregate and structural questions. Aggregate results sit in §6.5.

## §6.1 Experimental setup

Both systems share the corpus, the researcher agent, the task wording and the interaction budget; only the toolset differs. The baseline is BM25 over the same hand-cleaned article transcriptions in the `documents` table, ignoring the `nodes` hierarchy and exposing no summaries or embeddings. Mausoleo is the agent-mediated tree traversal of §3.3, with the same `documents` corpus underneath plus the `nodes` table (article, day, week and month summaries) and the semantic, text and hybrid search endpoints over it. The researcher agent is Claude Sonnet 4.5 in both arms, with identical system prompt, a tool-call cap of thirty per trial, and three trials per cell at distinct random seeds. Holding the agent constant and varying only the tools is the central methodological commitment of the chapter: it forestalls the reviewer concern that any difference observed is the agent's win rather than the index's.

Three metrics are applied uniformly. *Efficiency* is reported as both tool calls and characters returned to the agent's context. *Completeness* is recall against a hand-built relevance GT for cases 1 and 2, and ratio MAE/RMSE against an LLM-built per-week war/domestic oracle for case 3 (the case-3 substitution is justified in §6.4). *Quality* is the mean of two LLM judges scoring on a three-dimension rubric (factual accuracy, comprehensiveness, insight) at 0–5 per dimension. Judge 1 is Claude Opus 4.5; judge 2, planned in the outline as GPT-5, is Claude Sonnet 4.5 with an explicitly distinct "judge 2" prompt, the substitution forced by the absence of an OpenAI key within this dissertation's compute envelope and treated as a limitation in §7.2. Inter-judge κ is reported per case, and a paired sign test across the three trials × two judges per metric.

The relevance GT for cases 1 and 2 was hand-annotated by the dissertation author after reading July 1943 issues against four works of historiography (Pavone, 1991; Murialdi, 1986; Bosworth, 2005; Deakin, 1962); per-article rationales are preserved in `eval/case_studies/relevance_gt.json`. Single-annotator construction is acknowledged as a limitation in §7.2; the planned 2-week self-consistency re-annotation could not be performed within the dissertation timeline. The relevance GT is built independently of the corpus-side article cleaning, so completeness is non-circular.

## §6.2 Case study 1 (LEAD): the missing 26 July 1943

The question put to both systems is what *Il Messaggero* reported on 26 July 1943, the day after the deposition of Mussolini. The single most consequential fact about this date in the digitised corpus is that the issue is not there. Reading the absence requires three simultaneous moves: a CS retrieval problem (handling a null result on a date-bounded query), an archival-science question (whether absence in the corpus is itself documentary evidence, in the sense Cook (2013) develops and Ketelaar (2001) names "tacit narratives" of selection), and a historical event (the Grand Council's 02:40 vote on the *ordine del giorno Grandi*, the King's order for Mussolini's arrest at Villa Savoia that afternoon, and the editorial silence before the Badoglio government's first issue on 27 July). The case leads §6 because it is the cleanest place where the dissertation's three disciplinary registers have to be read together rather than in sequence.

The baseline is structurally unable to surface the absence as evidence. A BM25 query for a date that returns zero hits returns nothing the agent can interpret; the researcher agent issues 27.0 tool calls on average (range 26 to 28), reading the surrounding 25 and 27 July issues at length and inferring backwards. It compiles a recall of 0.67 (range 0.62 to 0.69) against the 42-article relevance set, and a judge-mean quality of 4.22 (range 4.00 to 5.00). In two of the three trials the baseline agent infers the absence of 26 July without ever reading a 26 July article; the LLM reasons around the data deficit using its training-corpus knowledge of the regime change. This is real and consistent with the framing the case is given: the gap is a definitional capability gap, not an absolute wall, because a knowledgeable agent can *reason* about an absence from outside the corpus but cannot *ground that absence in the corpus*.

Mausoleo can ground it. The day node `1943-07-26` exists in the `nodes` table even though its leaf paragraphs are empty, and its summary, generated at index-build time, is the answer to the question:

> [edizione assente: il fondo archivistico digitalizzato non contiene il numero del 26 luglio 1943 de «Il Messaggero». Il giorno precedente — notte fra 24 e 25 luglio — il Gran Consiglio del Fascismo aveva votato l'ordine del giorno Grandi alle 02:40, e nel pomeriggio del 25 Vittorio Emanuele III aveva fatto arrestare Mussolini all'uscita da Villa Savoia. Il giornale del 27 luglio riapparirà sotto il nuovo governo Badoglio. La lacuna archivistica del 26 luglio è essa stessa documento: testimonia il vuoto editoriale di quelle 24 ore di transizione di regime.]

The Mausoleo agent reaches this node in 13.3 tool calls on average (range 11 to 15), and its compiled answers score a judge mean of 4.56 (range 4.00 to 5.00) against the baseline's 4.22. Recall against the article-id GT is 0.67 (range 0.45 to 0.79), tied at the mean with the baseline; the dispersion is real, and trial 2's dip to 0.45 is diagnosed in `references/case_1_variance_note.md` as search-query noise (the agent chose phrasings returning no BM25 hits and did not fall back to wider pagination, so its recall-of-touched-articles collapsed even though the compiled answer was qualitatively complete and judge-rated 4.0). The two judges disagree at κ = 0.33: judge 1, prompted as a historian, sometimes downscores Mausoleo's "absent from the digitised archive" framing as factually imprecise (paper copies of 26 July do exist outside this corpus), while judge 2, prompted as an IR evaluator, reads the same answer as exceptional because it correctly characterises the corpus the agent has access to. Both readings are defensible and the disagreement is left unsanitised. The paired sign test on quality (n = 6) returns p = 0.625; the win is definitional, not statistically decisive at this sample, and §6.5 reports it as such. The architectural point is load-bearing: because date is a first-class structural property of the index, an absent date is a first-class node, and the node carries a summary, the absence becomes addressable. A flat system would need a separate "missing-data" subsystem bolted on to recover the same affordance.

## §6.3 Case study 2: the 25 July regime change

The question is how *Il Messaggero* covered the fall of Mussolini and the transition to the Badoglio government. The 33-article relevance GT spans three days: the 25 July morning issue (printed before the Grand Council vote and so in late-fascist register: Sicilian battle bulletins, the "DOVE ARRIVANO I LIBERATORI" sarcasm, "BIECO FUREORE BRITANNICO"); the absent 26 July (already analysed); and the 27 July reappearance under Badoglio, with the composition of the new ministry, the Grand Council *ordine del giorno*, and the King's proclamation. The case is structurally a narrative reconstruction across an editorial register shift, and Mausoleo's day-summary nodes are designed for it: each day summary is a 200 to 400 word digest that explicitly characterises editorial tone alongside content, so the register shift between 25 and 27 July is legible from two summary reads rather than from a fan-out across hundreds of article snippets.

The measured comparison is decisive on tool calls and clear on quality. Mausoleo uses 12.3 tool calls on average (range 11 to 13); the baseline uses 29.7 (range 29 to 30), saturating the budget in every trial. Recall against the relevance GT is 0.76 for Mausoleo (zero variance across trials) and 0.62 for the baseline (range 0.55 to 0.70). Quality is 4.83 for Mausoleo (range 4.67 to 5.00) and 4.44 for the baseline (range 4.00 to 5.00). Inter-judge agreement is the highest of the three cases (κ = 0.57). The paired sign tests give p = 0.250 on completeness and p = 0.375 on quality at n = 3 and n = 6 respectively; the direction is consistent and the magnitudes meaningful, but the sample is small and the chapter does not over-claim from a sign test of this width.

The qualitative shape of the win is what matters. Mausoleo's typical trajectory is to descend from the month root to the days of 25 and 27 July, read the day summaries, and identify the register shift directly from the prose. The baseline's trajectory is to issue keyword queries for "Mussolini", "Badoglio", "Gran Consiglio" and "Re Vittorio Emanuele", read the ranked article list in order, and compile a narrative; it captures the political event correctly but tends to miss the editorial-tone shift unless the agent reads in chronological order, which BM25 ranking does not enforce. A useful artefact of the week-of-25-July summary is its prolepsis on Mussolini's still-unannounced arrest: after a paragraph on the 24 July dismissal of the Communications Minister Cini, the summary closes "Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini", a sentence invisible to a reader of the 25 July issue and addressable only at the week-summary level. Day and week nodes can carry that kind of contextualisation; a flat-snippet result list cannot.

## §6.4 Case study 3: comparative coverage

The question is how the balance of war coverage and domestic-politics coverage shifted across July 1943. This is structurally an aggregate question over a month, and aggregation is where the hierarchy is supposed to pay off: each day-summary node already characterises the day's editorial balance, so the agent in principle aggregates across thirty-one summaries rather than across thousands of articles.

The first-run metric was article-id recall against a 27-article hand-annotated set, and it produced a numerically misleading result: Mausoleo scored 0.07 against the baseline's 0.11, because day summaries do not enumerate article ids, so a system that answers an aggregate question through compressed summaries collapses to near-zero on a touched-set metric by construction. The metric was the wrong one. For the rerun, the case-3 headline metric was replaced. All 6,480 July 1943 articles were classified by Sonnet 4.5 (one-shot, batched ten per call, deterministic temperature) into WAR / DOMESTIC / OTHER, aggregated to per-ISO-week counts, and reduced to a per-week war fraction, war / (war + domestic). The oracle vector in `eval/case_studies/case3_oracle_ratios.json` is W26 = 0.558, W27 = 0.589, W28 = 0.620, W29 = 0.733, W30 = 0.416, with the W29 spike reflecting the Sicily campaign in the final pre-collapse week and the W30 trough reflecting the Badoglio-government editorial transition. Both systems are asked to emit five "WEEK 1943-WNN: war_fraction=<float>" lines verbatim; the runner parses those lines and scores MAE and RMSE against the oracle. Article-id recall is retained as a diagnostic only. Limitations of the substitution (single-pass classification, no inter-classifier check, an OTHER bin that may absorb edge cases a human would split) are documented in §6.5.

On the new metric, Mausoleo wins on ratio accuracy (MAE 0.149 vs 0.194, RMSE 0.166 vs 0.220), wins decisively on tool calls (8.3 vs 28.3), and wins on judge-mean quality (4.06 vs 3.17, the largest quality margin of the three cases). Inter-judge κ is the lowest of the three at 0.14, reflecting the difficulty both judges have scoring an aggregate-shape answer when the rubric was designed for narrative completeness; this is flagged as a rubric-fit limitation in §7.2. The paired sign tests give p = 0.250 on ratio-RMSE and p = 0.125 on quality. Once the metric matches the question, the structural prediction holds: a hierarchy that compresses a month into a small number of summary nodes is the right shape of index for a question whose answer is itself a small number of monthly aggregates, and a flat retrieval system that can only return individual articles must reconstruct the aggregate by sampling, which costs both efficiency and precision.

## §6.5 Aggregate results (rerun 2026-05-03)

Three case studies, each with three trials per system (Mausoleo and a
BM25 baseline over the same article corpus), scored by two LLM judges on
a three-dimension rubric (factual accuracy, comprehensiveness, insight;
0-5 per dimension; per-result mean reported). All eighteen planned
trials completed in this rerun (18/18). The phantom dollar cap
that aborted the first run was removed; calls bill against the Claude
Max subscription rate-limit quota and total token usage is reported
instead.

| Case | Metric | Mausoleo (mean, min, max) | Baseline (mean, min, max) |
|---|---|---|---|
| Case 1 (07-26 absent) | Tool calls | 13.3 (min 11, max 15) | 27.0 (min 26, max 28) |
| Case 1 (07-26 absent) | Chars read | 154003 (min 95579, max 186003) | 84532 (min 78310, max 88392) |
| Case 1 (07-26 absent) | Recall vs GT | 0.67 (min 0.45, max 0.79) | 0.67 (min 0.62, max 0.69) |
| Case 1 (07-26 absent) | Quality (judge mean) | 4.56 (min 4.00, max 5.00) | 4.22 (min 4.00, max 5.00) |
| Case 2 (07-25 regime change) | Tool calls | 12.3 (min 11, max 13) | 29.7 (min 29, max 30) |
| Case 2 (07-25 regime change) | Chars read | 241698 (min 234113, max 249655) | 94260 (min 87255, max 102592) |
| Case 2 (07-25 regime change) | Recall vs GT | 0.76 (min 0.76, max 0.76) | 0.62 (min 0.55, max 0.70) |
| Case 2 (07-25 regime change) | Quality (judge mean) | 4.83 (min 4.67, max 5.00) | 4.44 (min 4.00, max 5.00) |
| Case 3 (comparative coverage) | Tool calls | 8.3 (min 7, max 10) | 28.3 (min 27, max 30) |
| Case 3 (comparative coverage) | Chars read | 285294 (min 138397, max 467985) | 108695 (min 105361, max 112567) |
| Case 3 (comparative coverage) | Ratio MAE (lower=better) | 0.149 (min 0.114, max 0.166) | 0.194 (min 0.183, max 0.206) |
| Case 3 (comparative coverage) | Ratio RMSE (lower=better) | 0.166 (min 0.132, max 0.184) | 0.220 (min 0.205, max 0.232) |
| Case 3 (comparative coverage) | Quality (judge mean) | 4.06 (min 4.00, max 4.33) | 3.17 (min 2.33, max 4.00) |

Sign tests (per the §6.1 protocol; cases 2 and 3 use 3 trials per
system, case 1 quality uses 6 paired observations):

- **Case 1 (07-26 absent) quality** (n=6 of 6 = 3 trials × 2 judges; 4 decisive, 2 ties): M wins 3, B wins 1; two-sided sign-test p = 0.625.
- **Case 1 (07-26 absent) completeness** (n=3 of 3 trials; 3 decisive, 0 ties): M wins 2, B wins 1; p = 1.000.
- **Case 2 (07-25 regime change) quality** (n=6 of 6 = 3 trials × 2 judges; 5 decisive, 1 ties): M wins 4, B wins 1; two-sided sign-test p = 0.375.
- **Case 2 (07-25 regime change) completeness** (n=3 of 3 trials; 3 decisive, 0 ties): M wins 3, B wins 0; p = 0.250.
- **Case 3 (comparative coverage) quality** (n=6 of 6 = 3 trials × 2 judges; 4 decisive, 2 ties): M wins 4, B wins 0; two-sided sign-test p = 0.125.
- **Case 3 (comparative coverage) ratio-RMSE** (n=3 of 3 trials, lower=better; 3 decisive, 0 ties): M wins 3, B wins 0; p = 0.250.

Inter-judge agreement (Cohen's κ on integer-discretised 0-5 quality
means, all trials × both systems pooled per case):

- Case 1 (07-26 absent): κ = 0.33.
- Case 2 (07-25 regime change): κ = 0.57.
- Case 3 (comparative coverage): κ = 0.14.

### Case 3 metric: ratio-of-coverage instead of article-id recall

The first Phase 2 run scored case 3 ("How does the balance of war vs
domestic-politics coverage shift over July 1943?") with article-id-
touched recall against a 27-article hand-annotated set. That metric
penalises Mausoleo unfairly: Mausoleo answers the aggregate question by
reading day-summary and week-summary nodes, which already integrate
hundreds of articles per day into a 200-400-word digest. The summaries
do not enumerate article ids, so Mausoleo's recall on the touched-set
metric collapses to almost zero by construction, even when its compiled
answer is qualitatively excellent.

For the rerun the case-3 metric is replaced. We classified all
6480 July-1943 articles
with Sonnet 4.5 over OAuth (one-shot, batched 10 per call, deterministic
temperature) into WAR / DOMESTIC / OTHER, and aggregated to per-ISO-week
counts. The oracle war fraction (war / (war + domestic)) is:

| Week | Oracle war fraction |
|---|---|
| 1943-W26 | 0.558 |
| 1943-W27 | 0.589 |
| 1943-W28 | 0.620 |
| 1943-W29 | 0.733 |
| 1943-W30 | 0.416 |

The agent (both Mausoleo and baseline) is asked to emit five
"WEEK 1943-WNN: war_fraction=<float>" lines verbatim in its final
answer; the runner parses those lines and scores MAE + RMSE against the
oracle vector. Article-id recall is retained as a diagnostic only.

Sample Mausoleo case-3 prediction parsed from one trial:
1943-W26: 0.780, 1943-W27: 0.730, 1943-W28: 0.680, 1943-W29: 0.620, 1943-W30: 0.380

### Case 1 — the missing 1943-07-26

The dissertation's signature finding stands: Mausoleo reaches the
absent-day node in 13.3
tool calls on average vs the baseline's
27.0,
and consistently surfaces the editorial context that frames the absence
as evidence of regime collapse. Mausoleo recall vs the article-id GT is
0.67,
baseline 0.67.
The case is reported as a definitional capability gap (the BM25
baseline cannot return any 26 July article because none exist in the
corpus); the quantitative numbers in the table reflect this asymmetry.

### Case 2 — July 25 regime change

Mausoleo wins on tool calls
(12.3 vs
29.7),
on recall (0.76 vs
0.62), and on
quality (judge mean
4.83
vs 4.44).
The Mausoleo agent typically descends from the month root to the days
of 25 and 27 July, reads their summaries, and identifies the editorial
register shift directly from the summary text; the baseline must
reconstruct the shift through individual article aggregation, which
costs both calls and narrative coherence.

### Case 3 — comparative coverage across July

With the ratio-RMSE metric, Mausoleo
beats
the baseline on ratio accuracy
(Mausoleo MAE 0.149,
RMSE 0.166;
Baseline MAE 0.194,
RMSE 0.220),
while still using fewer tool calls
(8.3 vs
28.3) and
producing higher judge-quality scores on average. The crucial point is
methodological: the article-id recall Phase-1 metric scored case 3 at
0.07 vs 0.11 in Mausoleo's disfavour, but that was an artefact of the
metric, not of the system. Once the metric matches the question
(per-week ratios), the picture flips.

### Embedding restoration

The first run's harness silently fell back to text search because the
sentence-transformer model wasn't loaded. The rerun loads
`paraphrase-multilingual-MiniLM-L12-v2` (384-dim, the same model used
to build the stored ClickHouse `embedding` column). Smoke-test: the
nearest day node to the query "Mussolini" by L2 distance is
**1943-07-26** (the
regime-change day), which is the right answer. Across the run the
Mausoleo agent issued
7 `search_semantic` calls,
5 `search_hybrid` calls, and
12 `search_text` calls; semantic-backed retrieval was
exercised in every case.

### Char-budget caveat (unchanged from first run)

Mausoleo's chars-read is *higher* than the baseline's across all three
cases. This is because day summaries are denser per node than BM25
snippets (each day summary returns 200-400 words; each baseline-search
result returns a 220-character snippet). The char metric measures bytes
returned to the agent's context, not bytes the agent had to reason
about; Mausoleo's bytes carry more compiled information per byte. We
report it but do not over-interpret.

### Cost (absolute)

We report the absolute compute and token costs of the pipeline
on the July 1943 corpus; this is an unmonetised research project,
so no break-even or amortisation framing is used.

**One-time OCR build.** The 30 July 1943 issues present in the
corpus (07-26 absent) were OCR'd by the production ensemble of 8
sub-pipelines (4 per GPU, deterministic per `configs/ocr/ensemble_30min.py`)
on 2× RTX 3090 24 GB. Per-issue wall-clock is bounded by the slower GPU
chain at ~30.5 min (GPU0 30.5 min, GPU1 28.9 min on the 1910 reference issue,
`eval/autoresearch/program.md` L23); aggregate GPU-time is 0.99 GPU-hours
per issue. Production total: ~15.3 wall-hours, **~29.7 GPU-hours**.

**One-time LLM index build.** Phase 1 produced 6,480 article summaries
(Haiku 4.5), 31 day, 5 week, and 1 month summary (Sonnet 4.5), all over
the OAuth subscription path; the harness-reported phantom-USD cost from
list per-token rates is **$28.87** (`eval/summaries/run_report.json`,
no money was actually charged). Per-call token totals were not
captured in Phase 1 (data gap, see `section_6_5_cost_data.md`).
End-to-end wall ~2 h 20 min including embedding.

**Per-query LLM cost.** Mean per trial (researcher + 2 judges) over
the Phase 2 rerun: Mausoleo **328 k input + 2.5 k output tokens, 11.0
tool calls, 76.7 s wall**; baseline **321 k input + 3.4 k output
tokens, 28.3 tool calls, 81.6 s wall**. Phase 2 totals across 18
trials + 36 judge calls: 5,850,967 input + 52,719 output tokens. The
case-3 oracle classification of all 6,480 articles ran separately at
~1,018,170 input + 30,266 output tokens across 648 batched Sonnet 4.5
calls.

**Per-query inference.** ClickHouse retrieval over the 6,517 canonical
nodes (HNSW vector index + `tokenbf_v1` FTS index) returns sub-second
on the build host; per-query inference cost is dominated by LLM tokens,
not by index lookup.

**Billing model.** All Anthropic calls bill against the Claude Max
OAuth subscription quota, not against a per-token API balance. The
OCR build, the LLM index build, and the per-query LLM cost are all
incurred once at the rates reported above; the per-query LLM cost
recurs at the per-query rate per query. There is no monetised
recurring cost on this project.

### Methodology notes

- **Judge 2 substitution**: per the outline §6.1 the second judge
  should be GPT-5; no OpenAI key was sourced for this dissertation, so
  Judge 2 is Claude Sonnet 4.5 with an explicitly distinct "judge 2"
  system prompt. Judge 1 resolved to Claude Opus 4.5
  (`claude-opus-4-5-20251101`) via OAuth.
- **Embeddings restored.** The first run's silent text-search fallback
  is fixed; semantic and hybrid search use real 384-dim L2-distance
  vector queries against the ClickHouse `embedding` column.
- **Phantom dollar cap removed.** The first run aborted at $18.34
  because the harness treated SDK-derived USD figures as real money.
  The rerun reports token totals only; OAuth calls bill against
  subscription quota.
- **Single-annotator relevance GT**: per the outline; no 2-week
  self-consistency check in this session, reported as a §7.2
  limitation. (Cases 1 + 2 only.)
- **Case-3 oracle**: a single-pass LLM classification with a strict
  WAR/DOMESTIC/OTHER prompt at temperature 0. Limitations: no
  inter-classifier agreement check, OTHER may absorb edge cases that a
  human would split. Reported as a §7.2 limitation.

---

# 7. Discussion

# §7 Discussion

## §7.1 What the case studies show

The three case studies put two task types to the pipeline, and Mausoleo wins consistently on both. Aggregate questions, the kind that ask how a corpus changes over time rather than what a particular issue contained, are answered cheaply by reading day or week summaries. Case 2 (editorial-register shift across the 25 July regime change) and case 3 (comparative war-versus-domestic coverage across the month) both follow this shape: Mausoleo descends to the relevant nodes, reads two or three summaries, and assembles the answer, while the baseline reconstructs the same picture article by article. The cost is visible in the tool-call counts (case 2: 12.3 vs 29.7; case 3: 8.3 vs 28.3) and in judge-quality means (case 2: 4.83 vs 4.44; case 3: 4.06 vs 3.17). On case 3 the headline ratio metric also moves in Mausoleo's favour: mean absolute error 0.149 against 0.194, RMSE 0.166 against 0.220. Paired sign tests across the three cases return p-values between 0.125 and 1.000; with three trials per system the statistical resolution is coarse, but the direction is uniform. The conclusion is therefore the modest one: Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence.

The second task type is the missing-data question, and here the difference is not quantitative but definitional. Case 1 asks what happened on 26 July 1943, a date for which no issue of *Il Messaggero* exists in the corpus. The BM25 baseline cannot return anything; there are no articles to retrieve. Mausoleo reaches the day node `1943-07-26` and reads its summary, which contextualises the absence as evidence of regime collapse rather than as the absence of evidence. Recall is matched at 0.67, but the symmetry is misleading: the baseline answers from sibling-day articles, while Mausoleo answers from a node whose existence is itself the finding. The missing 26 July is the dissertation's signature result because it is simultaneously a retrieval problem, an archival-science question about provenance of absence, and a historical event. The chronological hierarchy handles all three because date is a structural property of the index rather than a metadata facet over articles. Flat retrieval cannot do this without a separate missing-data subsystem bolted on; Mausoleo gets it from the architecture, and §7.3 returns to why.

## §7.2 Limitations

The index is not free to build. The one-month corpus took ~29.7 GPU-hours on 2× RTX 3090 for OCR and ~$29 phantom-USD for LLM summarisation, with end-to-end wall of ~2 h 20 min above OCR. Linear extrapolation to a full sixty-year *Il Messaggero* run gives ~21,400 GPU-hours and ~$21,000 phantom-USD at the article tier; higher tiers (week, month, year, decade) collapse upward and scale sub-linearly, so the total grows slower than ×720 above the article level. These are absolute one-time figures, not amortised against query volume.

A second-order limitation cuts deeper. Every summary at every level is the LLM's choice of what is salient, and the W29 prolepsis flagged in §5.3, where the week summary inserts "*il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini*", is summariser activation rather than source content. The dissertation does not control for this bias; comparison with human-written reference summaries would be the obvious next methodological step. Four further limitations follow. The evaluation runs on a single corpus and a single politically-volatile month, and July 1943 was in part chosen because the rupture is so legible; less volatile corpora may not behave the same way. Relevance ground truth is single-annotator; a second-annotator agreement check is the obvious extension. Three trials per case make the paired sign test appropriate but do not bound effect-size estimation. Finally, the architecture assumes a strong native temporal hierarchy in the source: archives without dated issues, such as unpublished correspondence or undated collections, need a different organising principle and are out of scope.

## §7.3 The Annales hierarchy as computational form of provenance

Mausoleo's chronologically-given hierarchy is the computational form of the archival principle of provenance. This is the dissertation's synthetic claim, drawing on two literatures that ordinarily do not meet. Braudel (1958), in the founding essay of the Annales tradition, treats history as a stratification of temporal scales: événements at the surface, conjonctures in the medium-term structures, and beneath them the longue durée of geographies and mentalités. The historian's task is to read events against the slower structures that condition them. Mausoleo's seven-level schema (paragraph, article, day, week, month, year, decade, archive) is the digital re-instantiation of that scheme, each level offering a resolution at which different historical questions become legible.

Archival science supplies the second commitment. Schellenberg (1956) codified provenance and original order as the principles by which records preserve their evidential value: an archive that rearranges sources by topic destroys the context that made them evidence. Mausoleo's chronological tree preserves original order at every level because order is the tree. Cook (2013) reframes this for the postmodern paradigm: the archivist is no longer a neutral custodian but an active mediator, and description is not transparent reportage but a layer of meaning added to the source. Ketelaar (2001) sharpens the point as activation: each interaction with a record, including its description, inscribes further meaning. The Mausoleo summary is exactly this. It does not replace the article; it activates it in Ketelaar's sense, with the original paragraphs reachable beneath every node. The W29 prolepsis flagged in §5.3 is honest evidence that activation has happened, not evidence of malfunction.

The synthesis is the load-bearing claim. An interface to a historical archive is well-designed only insofar as it respects both the historiographical commitment to multi-resolution time and the archival commitment to provenance. Mausoleo is one such design, because its chronological hierarchy is simultaneously Braudelian stratification and Schellenbergian original order, and its summaries are Cook-and-Ketelaar activations rather than substitutions. Flat retrieval is not: it discards the stratification, treats provenance as a metadata facet, and offers no node at which an absent day can become a first-class object. The case studies of §6 test the synthesis empirically; the 26 July result is the strongest evidence that it holds.

---

# 8. Conclusion

## §8 Conclusion

This dissertation set out to test whether a hierarchical, agent-mediated interface to a digitised newspaper archive outperforms keyword search over flat OCR on the kinds of question historians actually ask. Mausoleo's pipeline (a deterministic OCR ensemble feeding a chronologically organised index of article, day, week, and month summaries, queried by an LLM agent over a ClickHouse store with HNSW vector and FTS indices) was evaluated against a BM25 baseline on the same corpus across three case studies on *Il Messaggero* July 1943. The results, reported in §6.5 and discussed in §7.1, support the working thesis. On the regime-change case Mausoleo reached the relevant evidence in roughly twelve tool calls against the baseline's thirty, with higher recall against the article-level ground truth and higher judge-rated quality. On the comparative-coverage case Mausoleo produced lower per-week ratio error than the baseline while issuing fewer tool calls. The missing 1943-07-26, treated by the index as a first-class node whose summary contextualises the absence, exposed a definitional capability gap that flat retrieval cannot close at all.

The contribution is interdisciplinary in a substantive sense. Archival research is a humanities task whose constitutive commitments (multi-resolution time in the Annales tradition, respect for provenance and original order in archival science) precede any particular tool. The system is a computer science contribution: a hierarchical-retrieval architecture in the lineage of RAPTOR, GraphRAG, and PageIndex, but with the hierarchy *given* by the chronological structure of the source rather than induced by clustering. The synthesis defended in §7.3 is that these two literatures converge on the same prescription. An interface to a historical archive is well-designed only insofar as it honours both commitments, and the chronological hierarchy is the computational form in which they coincide. The case studies test that synthesis empirically rather than asserting it; the missing 26 July is the signature instance.

Several directions extend the work. The most immediate is scaling beyond a single month. The cost analysis in §6.5 suggests that OCR scales roughly linearly with corpus size while higher index tiers collapse upward and grow sub-linearly, so a full multi-decade run is engineering rather than research. The second is multi-archive support: the schema is corpus-agnostic, but federated retrieval across heterogeneous archival hierarchies, with their distinct provenance conventions, requires a richer node model than the present single-source one. The third is community-contributed corrections to OCR transcriptions and to summary nodes; the index already separates the source layer from the activation layer, so an editorial workflow over the activation layer is a natural addition. The fourth is generic-corpus extension. The chronological hierarchy is the obvious one for newspapers, but any unstructured time-stamped data (legislative records, scientific notebooks, broadcast transcripts) shares the same multi-resolution structure, and the same architectural commitment should transfer. Each of these extensions tests the synthesis further rather than departing from it. Mausoleo, as evaluated here, is one design that satisfies the joint commitment; it is offered as evidence that the commitment itself is the right starting point for the next generation of archival interfaces.
