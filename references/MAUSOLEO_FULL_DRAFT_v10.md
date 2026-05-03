# Mausoleo: reading across a regime change in a digitised newspaper archive

BASC0024 Final Year Dissertation

---

## Abstract

A digitised newspaper corpus normally allows a historian to retrieve articles by keyword, with date as a facet on the side. For the July 1943 *Il Messaggero* corpus this dissertation works with, that template handles questions for which articles exist and is awkward for the others the corpus invites. The morning paper for 26 July 1943 was not printed (the Grand Council had deposed Mussolini overnight and an editorial line could not be drawn in time); a flat article index returns nothing for the date. Questions about the regime-change days of 25 to 27 July return tens of articles that the reader has to assemble; questions about the war-and-domestic balance across the month return hundreds. The dissertation argues that a digital archive ought to respond to questions of these shapes with the structural information available to it, and builds a system, Mausoleo, that does so by storing the corpus as a calendar-shaped tree of recursively summarised nodes over which a researcher agent navigates.

There is an interdisciplinary argument running underneath this. A century of cognitive-science work has accumulated evidence that memory organises temporal information at multiple resolutions. The everyday consequence is that researchers reading time-stamped material shift between date-bound items and larger schemas built up over weeks. A flat ranked-article interface asks the researcher to perform that integration mentally. The case studies in chapter four ask whether exposing the temporal structure in the index changes how the work goes. Three questions are put to *Il Messaggero* in July 1943: what the paper said on the absent 26 July, how it covered the regime change of 25 to 27 July, and how the balance of war and domestic-politics coverage moved across the month. Across eighteen scored trials the system averaged 11.3 tool calls against the keyword baseline's 28.3 and was preferred by both judges on a three-dimension rubric in every case. The calendar-shaped index holds a day node for 26 July with empty leaves and a summary that records the absence as evidence, where a flat article index has no equivalent slot for that day.

---

## Preface

I came to this project from the engineering side, after a year working on retrieval-augmented generation pipelines for technical documentation. I wanted a final-year project that would put the same techniques in front of source material that does not chunk well, and Italian regime-period newspapers were the natural pick from the languages I read. The 1943 issue list of *Il Messaggero* was the most complete in the available scans, which is how I ended up with a corpus that contained one missing day. Two weeks went into a post-correction pass that turned out to make composite OCR scores worse rather than better, and another into the realisation that the date-bounded queries the system most needed to answer well were exactly those the keyword baseline was structurally incapable of resolving. Bartlett's *Remembering* was a paper I had read for second-year psychology and went back to once the OCR work began producing day-summary nodes; the hippocampal-mapping work in Eichenbaum and Whittington came in much later, after the calendar-shaped index had already been built.

I thank Dr Yi Gong for supervising. Her comments on the cognitive-science framing, and on what the system can and cannot warrant, shaped the chapters that follow.

---

## Chapter 1: A missing newspaper

A query for *Il Messaggero* on the date 26 July 1943, addressed to any of the major digitised newspaper archives that hold the paper, returns an empty result page. Impresso, Europeana Newspapers, Chronicling America for the US comparators, and the Italian *Emeroteca digitale* domestically all show no articles for that date. The 25 July morning edition went to press long before the Grand Council vote that night and in its accustomed late-fascist register. The 27 July edition reappeared under the new government, with the Grand Council *ordine del giorno*, the King's proclamation, and the new ministry on the front page. Mussolini had been deposed and arrested overnight; an editorial line for the morning paper could not be drawn in time and the issue did not run. The 26 July does not appear in the digitised fund because there was no 26 July to digitise.

These archives index at the article level, and since the day has no articles to index, the date itself is not surfaced in the catalogue. Historians have always read around such gaps, taking the 25th and the 27th and inferring backwards from what survives. What the interface cannot do is register that the absent day is part of the corpus's testimony, the editorial silence of twenty-four hours of regime transition. A narrower question about the editorial-register shift across the three days of the deposition leaves the user with thirty articles to read by hand. A wider question about how the war/domestic-politics balance moved across the month leaves the user with several hundred articles to classify and aggregate from scratch.

There is a body of cognitive-science work, accumulating since Bartlett's *Remembering* (Bartlett, 1932), that bears on the kind of reading the case studies in chapter four put to the corpus. Bartlett's *War of the Ghosts* studies described how recall reconstructs a generic schema in place of the verbatim event. Subsequent working-memory research established a small functional capacity for the active workspace: roughly seven plus or minus two items in Miller's original framing (Miller, 1956), revised downwards to about four chunks in Cowan (2001). For an archive question that ranges across a month, this constraint requires compression somewhere along the chain, either in the interface or, failing that, in the reader's head.

A separate but converging line of research, from Tolman's (1948) spatial cognitive-map experiments to Eichenbaum (2017) on the hippocampal integration of space, time and conceptual relation, suggests that the same neural machinery handles hierarchical structure across these domains. Whittington et al. (2020) modelled the circuit as a general-purpose relational learner. The relevance for an archival interface is direct enough: the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form. When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them. A flat keyword search holds none.

This dissertation builds and tests an interface that does hold them. Mausoleo stores the *Il Messaggero* July 1943 corpus as a calendar-shaped tree of recursively summarised nodes at five hierarchical levels, with the leaf level holding paragraphs of source text and successively higher levels collecting articles into days, days into weeks and weeks into a single month root. The schema permits days with no underlying articles. Higher up the tree, the week-of-25-July node carries an integrated summary of the regime-change trajectory, and at month level the index records the schematic monthly shape against which the per-week war and domestic balance can be read. A researcher agent navigates the tree and may also issue keyword and embedding searches over the same corpus. Three case studies on the July 1943 material, evaluated against a keyword baseline over identical article transcriptions, ask whether the multi-resolution interface improves on the flat one across the question types above.

A recent NLP literature on hierarchical retrieval, surveyed in chapter two, derives its hierarchy from the corpus itself, either by clustering text chunks (Sarthi et al., 2024) or by community detection on an entity graph extracted from the documents (Edge et al., 2024); a related line works from the document's surface section structure (Zhang and Tang, 2025). Mausoleo borrows its hierarchy from the publication calendar that the printers already followed. The pay-off shows up most clearly on the absent-day case, since the calendar contains a slot for 26 July whether or not anything was printed on it, while a clustering-induced hierarchy has nothing to cluster from when the data are absent.


---

## Chapter 2: Three literatures and a corpus

The literatures the system needs to be read against are several. The dominant access mode in the long line of digital newspaper archives remains the keyword query against an OCR'd full text. A more recent line in information-retrieval research has been doing hierarchical access, with the hierarchies usually induced from the corpus itself by clustering or graph-community methods. A much older body of cognitive-science work on how memory organises temporal material at multiple resolutions has not been much operationalised for archival interface design. On top of those three, the corpus has its own historiography, which is what gives the case studies in chapter four their historical bite.

### Existing digitised newspaper archives

Three systems define the field. *Chronicling America*, the National Digital Newspaper Program at the Library of Congress, holds roughly 23 million pages of US newsprint dating from 1690 to 1963 and exposes them through faceted search over OCR'd full text. *Europeana Newspapers* aggregates around 28 million pages across forty European languages, again through full-text search backed by OCR of variable quality and limited named-entity enrichment. *Impresso*, the Swiss and Luxembourgish project that is the closest comparator to any new venture in this area, covers roughly two centuries of French, German and Luxembourgish newspapers and sits at the enriched end of the spectrum: alongside OCR it offers named-entity recognition, topic models, lexical-semantic comparison and text-reuse browsing (Ehrmann et al., 2020; Düring et al., 2024).

What unites these systems is the access template. The user arrives with a query, receives a ranked article list, optionally facets the result by date, year or source, and then reads articles individually. Düring et al. (2024) describe the Impresso interface as one of "transparent generosity" about exposing intermediate structure, but the user is still expected to come with a search term in mind. The presupposition is reasonable for most historical research, where the historian arrives with a question already framed. It is less reasonable for the historian who wants to understand a corpus they cannot read in full at the article level, or for whom the answer to the question is not a list of articles but a shape across days, or an absence.

### The hierarchical-retrieval lineage

Classical information retrieval supplies the baseline. Salton, Wong and Yang (1975) introduced the vector space model; Robertson and Zaragoza (2009) consolidated the probabilistic-relevance tradition that culminated in BM25, still the strongest sparse baseline. Both treat the document collection as a flat set: relevance is computed per document and the structure of the collection plays no role in retrieval.

The recent hierarchical-retrieval lineage breaks with this assumption. RAPTOR (Sarthi et al., 2024) builds a retrieval tree by recursively clustering chunk embeddings and summarising each cluster, allowing the same query to hit a leaf passage or a higher-level summary depending on its scope. GraphRAG (Edge et al., 2024) takes a different route and extracts an entity-relation graph from the corpus, runs Leiden community detection over the graph, and writes summaries at each community level. The Edge et al. paper reports substantial gains over flat retrieval-augmented generation for global-summarisation queries on three benchmarks; the cost is that the entity-extraction pass and the community summarisation are both expensive at scale, and the resulting hierarchy is opaque to the user (a researcher cannot tell from the surface why two summaries sit at the same level). A related line uses the document's own table-of-contents as the retrieval target (Zhang and Tang, 2025) and so reads its hierarchy off the surface rather than inducing one. The hierarchies these systems propose are induced from the data or read off a document's structure; in either case the retriever has more to work with than a flat list.

The closest prior work on retrieval-augmented generation over historical newspapers is Murugaraj et al. (2025), who apply a topic-restricted retrieval pipeline to the Impresso Swiss corpus and report improved retrieval relevance over flat retrieval-augmented generation, measured by BERTScore, ROUGE and UniEval. Their pipeline restricts retrieval to documents matching the query's inferred topic, on the assumption that topical coherence between query and retrieved articles is the dominant signal of relevance. On a corpus with a strong native temporal hierarchy this assumption is harder to defend. For a question about a regime collapse, the topically most-relevant articles cluster around the surface vocabulary of fascism (Mussolini, Grand Council, Badoglio); returned at a uniform editorial register they flatten the very shift the question asks about. The metrics in their evaluation reward semantic overlap between answer and reference and do not measure whether the answer captures a temporal trajectory. A topic-restricted pipeline answers what topically-relevant material the corpus contains. The dissertation is asking a different sort of question, about what a particular temporal slice looked like (with its absences). A direct head-to-head on Impresso is the obvious experiment but is gated on language: the Impresso corpus is French and German, and the case-study agent and judges in chapter four are configured for Italian.

Mausoleo changes the source of the hierarchy again. Daily newspapers carry a temporal hierarchy in their production schedule (paragraph in article in issue in day in week in month), and the index inherits that structure rather than inducing one. Where the source-side hierarchy is already meaningful, this means the navigation surface stays predictable to a working historian without depending on extraction quality or a clustering choice.

### Memory, hierarchy and external structure

Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on. Several converging strands from cognitive science support it, and they are worth taking in turn.

Take hierarchical memory first. Bartlett (1932) introduced the term *schema* for the compressed, generic templates that organise specific recollections, and showed in his *War of the Ghosts* studies that what survives recall over time is the schema and not the verbatim event. Craik and Lockhart (1972) reframed retention as a function of depth of processing, with deeper semantic encoding producing more durable traces. The contemporary picture distinguishes episodic memory, events bound to time and place, from semantic memory, compressed general knowledge, and from the schema-level abstractions Bartlett described, with episodic traces consolidating over time into semantic and schematic structures. The relevance to an archival interface is direct. A corpus carries material from individual articles up through narrative arcs and aggregate patterns at the month or longer scale, and a researcher reading the corpus moves between those levels.

A second strand concerns chunking and the active workspace. Miller's (1956) *magical number seven plus or minus two* and Cowan's (2001) revised estimate of about four functional chunks both put the active workspace at a small handful of items. For an external retrieval system, compression at multiple resolutions becomes the precondition for the corpus being cognitively tractable at all. Thirty article snippets are more than the active workspace can comfortably hold, and a single day summary at an appropriate level of abstraction is much closer to that limit.

On the neural side the recent work shows that the same hierarchical-relational organisation extends from space to time and concept. Tolman (1948) showed that rats build *cognitive maps* exceeding stimulus-response chains. Eichenbaum (2017) consolidated the view that the hippocampus encodes spatial position alongside temporal and conceptual relation in a shared representational format. Behrens et al. (2018) reviewed the evidence that the spatial-coding machinery is recruited for non-spatial structural inference, and Whittington et al. (2020), in the Tolman-Eichenbaum-Machine, modelled the same circuit as a general-purpose relational learner factorising structure from content. The substantive lesson is that one piece of hierarchical-relational machinery handles space, time and conceptual relation in a common format. A temporal index running at multiple resolutions is therefore working in the structural form the brain already uses for similar problems.

Cognitive-offloading work then closes the picture. Hutchins (1995), in *Cognition in the Wild*, showed that real cognitive work is distributed across people and the artefacts they work with (instruments, charts, written inscriptions), with each component carrying a piece of the computation. Clark and Chalmers (1998) made the philosophical case for the *extended mind*: when an external resource is reliably and habitually consulted, it functions as part of the cognitive system. If that picture holds, the archive interface forms part of the cognitive system the historian uses, and its structural choices matter at the cognitive level along with the ergonomic one. An interface exposing multi-resolution temporal structure aligns with the cognitive architecture researchers bring to historical material, where one that flattens it leaves the chunking, narrative integration and schema-formation to be done internally against cognitive evidence that the material is already represented that way. The case studies in chapter four ask whether this prediction shows up in the metrics.

### The corpus and its source-critical context

If the cognitive framing motivates the design, the corpus context decides whether the case studies mean anything historically. *Il Messaggero* in July 1943 was a regime-aligned daily under the directives of the *MinCulPop*. Schudson (1978) treats the social construction of news as itself a historical process; Murialdi (1986) remains the standard treatment of the Italian press across the regime period, documenting the directive system that shaped what could and could not appear in print. Without this context, the case-study questions in chapter four would not land as the questions a working historian would actually put to this material. Any summary the index produces functions as a derived secondary source, and its relation to the regime-aligned primary text needs to be open to inspection. The schema's separation of leaf text from summary text keeps the original paragraphs reachable from every higher-level node. ISAD(G) names this archival principle *respect des fonds* (International Council on Archives, 2000): the source order is preserved beneath the catalogue's own ordering.

---

## Chapter 3: How Mausoleo is built

Three loosely coupled stages of Mausoleo connect through a single ClickHouse table called `nodes`. An OCR pipeline produces hand-cleanable article-level transcriptions from page scans; a recursive summariser builds the calendar-shaped tree over those transcriptions; and a small JSON-emitting command-line interface lets a researcher agent read the tree. The boundary between stages is the schema of the table, so each stage can be swapped or replayed without touching the others.

### From scanned pages to article transcriptions

Inputs to the OCR stage are scanned JPEGs, six pages per issue on average, across the thirty surviving July 1943 issues of *Il Messaggero*. Outputs are per-issue JSON files listing detected articles with headline, body text and page span. Cold-cache is the only run mode the pipeline supports: every prediction regenerates from the raw images on each invocation, under a budget of thirty minutes wall-clock per issue on two GPUs.

Eight sub-pipelines run in parallel across the two GPUs, and their predictions are merged deterministically. Cross-family diversity is deliberate: three model configurations (an open-weight vision-language model in two backbone versions, the second under a strict generation mode) load on each GPU, and the eight sub-pipelines vary column-split granularity (full-page, two- through six-column splits, plus a small-region detector running over layout boxes) so that no single layout assumption dominates. The Qwen2.5-VL backbone is trained for dense document understanding (Bai et al., 2025) and is used here as a black-box OCR engine prompted to emit structured article JSON. The eight per-source predictions merge through a deterministic chain (a REPLACE pass, an ADDITIVE pass for the column-six advertisements source, and a quality-weighted text selector) without any LLM arbitration or post-correction. Both LLM arbitration and prompt-based post-correction were tried during the hill-climb and rejected: the post-corrector modernises good articles into paraphrases more than it repairs bad ones, costing 0.6 to 1.1 composite points across three serious attempts.

Two empirical observations drive the design. Column-split predictions from a single model are highly correlated, so a fifth column-three pipeline of the same family contributes less than a different model family at the same column count; cross-family diversity buys roughly 0.013 composite over the best single-family ensemble at equal wall-clock. The wall-clock ceiling matters: an unconstrained research configuration reaches 0.92 composite but takes fifty to sixty minutes per issue, outside what a one-month corpus build at 30.5 min per issue can sustain.

The cold-cache composite, evaluated on two hand-cleaned issues (1885-06-15, 41 articles; 1910-06-15, 193 articles) with an article-level matching scheme, is 0.89878 averaged across the two issues, decomposing to 0.872 on 1885 and 0.926 on 1910. The composite weights length-weighted character error rate at 0.40, recall against a Jaccard matching threshold at 0.25, ordering at 0.15, headline character error rate at 0.10, and page-accuracy at 0.10. Article-level matching is preferred to flat full-text character error rate because the latter penalises any displacement of an article in reading order even when its text is character-perfect; this convention follows historical-newspaper OCR work in NewsEye (Doucet et al., 2020). The single biggest gain across the hill-climb was not a model addition: a post-processing filter that strips raw-JSON regurgitations that occasionally leak from the vision-language sources added 0.0165 alone. A leave-one-out at the five-source intermediate stage confirms no entry is redundant. Per-pipeline component scores and configuration tables are in Appendix A.

The 6,480 article-level transcriptions used downstream are a hand-cleaned post-pass of the ensemble's 9,456 raw articles (deduplication and cross-page stitching), outside the OCR composite score.

### The calendar-shaped tree

All index storage lives in a single ClickHouse table. Each row stores a node's level (the leaf level being paragraph, with article above it, then day, then week, then month, and the full production schema additionally allowing year and decade above month plus an archive root above decade), along with a parent identifier, a sibling position, a date range, a summary, an embedding vector, and, in the case of paragraph leaves only, the raw OCR'd text. Higher-level nodes hold no raw text of their own; their content is the summary plus a pointer downward. The architecture corresponds to Ketelaar's (2001) treatment of archival description as a tacit narrative, an activation of the source and not a replacement for it: the higher-level summary is treated as derived, with authority resting in the leaf paragraph.

Node identifiers are deterministic and human-readable: `1943-07-25_a127_p03` for a paragraph, `1943-07-25_a127` for an article, `1943-07-25` for a day, `1943-W29` for a week, `1943-07` for a month. Two secondary indexes sit on the table: a vector-similarity index over the embedding column for nearest-neighbour search, and a token-bloom-filter index over the summary column for keyword search.

Construction is bottom-up, one level at a time. Article summaries are produced by a batch over each article's paragraphs; day, week and month summaries by the same recursion at coarser grain. The lineage is the recursive book summarisation of Wu et al. (2021), which establishes that bottom-up summarisation over a fixed branching factor produces coherent abstractions without exceeding any context window. The summariser prompt is consistent across levels: target two to four hundred words, weave named entities into the prose without listing them, preserve dates and quantities verbatim, and write so that an agent can decide from the summary alone whether to descend further. Length is held constant deliberately, which makes navigation predictable but forces aggressive thematic compression at higher levels. A spot-check against ten July 1943 day summaries (excluding the absent 26 July) recovered forty-eight of fifty top named entities through accent-stripped substring match against the day's hand-cleaned transcription; the two misses were both `Papa Pio XII`, where the summariser inserted an editorial honorific the press itself never used, preferring `Pio XII` or `il Pontefice`. An information-loss trace on 1943-07-03 gives the compression rate precisely: of thirty-six distinct named entities in the day's three longest articles, seven survive at day level, six at week, one (`Il Messaggero` itself) at month. Generic organisational acronyms tend to drop out at the week boundary. Named individuals fare better, persisting through week-level summaries before being absorbed into the month abstraction. Place names sit between the two, robust at day but mostly gone by month. The implication for navigation is that the month level supports questions about what kind of day it was, but not about who appeared in it.

For July 1943, 6,480 article nodes collapse into 31 day nodes, 5 weeks, and 1 month root (6,517 nodes total). Per-day cardinality is variable: the schema permits empty days, and the table holds a row for each calendar position whether or not its leaf paragraphs are populated. The week-of-25-July summary closes with a prolepsis added by the summariser (*Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini*), supplying historical context the source could not have contained; chapter four returns to this as a summariser-bias phenomenon. At month level the prolepsis collapses into *l'arresto di Mussolini (25 luglio)*, with the 02:40 timestamp and the Grand Council mechanism compressed away.

### How the agent reads the tree

Retrieval is exposed through a small server backed by ClickHouse and a typer-based command-line interface whose user is a researcher agent, with every command emitting structured JSON to standard output. Tree traversal is exposed through `GET /root`, `/nodes/{id}`, `/nodes/{id}/children`, `/nodes/{id}/parent` and `/nodes/{id}/text` (raw text for leaves, reconstructed from descendants for higher nodes). Search is exposed through `POST /search/semantic` (vector approximate-nearest-neighbour over the vector-similarity index, filterable by level or date range), `/search/text` (token-bloom over summary text) and `/search/hybrid` (a weighted combination). A `GET /stats` endpoint reports per-level node counts.

Following the ReAct loop pattern of Yao et al. (2022), and unlike single-shot retrieval-augmented generation (Lewis et al., 2020), the agent enters at the root, reads a summary, decides whether to descend or to search, and iterates. Tree traversal carries chronological position with it; semantic search is available as a fallback when the question is not naturally chronological. The application programming interface itself is small and stateless, and the reasoning sits in the agent.

---

## Chapter 4: The missing 26 July, and two contrast cases

The case studies in this chapter ask whether the architectural argument of chapter three makes a measurable difference for a researcher trying to answer real questions about July 1943.

In all three, the comparison is to a BM25 baseline over the same hand-cleaned article transcriptions in the `documents` table, with no access to the `nodes` hierarchy. Mausoleo runs the agent-mediated tree traversal of the previous chapter, with `documents` plus `nodes` plus the semantic, text and hybrid search endpoints. The researcher agent is held constant across both arms (a contemporary commercial LLM under identical system prompt), with a tool-call cap of thirty per trial and three trials per cell at distinct seed prompts. Three metrics are applied uniformly across cases: tool calls and characters returned to the agent's context for efficiency; recall against a hand-built relevance ground truth on the first two cases (single-annotator, against four works of historiography: Pavone, 1991; Murialdi, 1986; Bosworth, 2005; Deakin, 1962) and ratio mean absolute error and root-mean-square error against a per-week war/domestic oracle on the third for completeness; and the mean of two LLM judges scoring at zero to five on each of the three rubric dimensions described in the supplementary material for quality.

### The missing 26 July

What did *Il Messaggero* report on 26 July 1943, the day after the deposition of Mussolini? The most consequential fact in the digitised corpus is that the issue is not there. A date-bounded query against the article-level corpus returns the empty set. For an episodic-retrieval task this is the case the design was built around. In Mausoleo the day node `1943-07-26` exists in the table whether or not its leaves contain text, with a summary attached that contextualises the gap; the agent reads the summary directly. There is an episodic-memory analogue: an event whose temporal slot the memory system does not hold cannot register as missing, it can only fail to come back when looked for.

The baseline cannot surface the absence as a node. A keyword query for a date with zero hits returns nothing the agent can interpret directly; the researcher agent issues 27.0 tool calls on average across the three trials, reading the 25 and 27 July issues that bracket the gap and inferring backwards. The compiled answer scores recall of 0.67 against the 42-article relevance set, with a judge-mean quality of 4.22. In two of three trials the baseline agent infers the absence without ever issuing a query for 26 July material, reasoning around the data deficit from its training-corpus knowledge of the regime change. The interface treats a question that has an answer as though it had none, and the agent then supplies one from outside the source.

Mausoleo can ground the question. The day node `1943-07-26` exists in the `nodes` table even though its leaf paragraphs are empty, and its summary, generated at index-build time, is the answer to the question:

> [edizione assente: il fondo archivistico digitalizzato non contiene il numero del 26 luglio 1943 de «Il Messaggero». Il giorno precedente, notte fra 24 e 25 luglio, il Gran Consiglio del Fascismo aveva votato l'ordine del giorno Grandi alle 02:40, e nel pomeriggio del 25 Vittorio Emanuele III aveva fatto arrestare Mussolini all'uscita da Villa Savoia. Il giornale del 27 luglio riapparirà sotto il nuovo governo Badoglio. La lacuna archivistica del 26 luglio è essa stessa documento: testimonia il vuoto editoriale di quelle 24 ore di transizione di regime.]

The Mausoleo agent reaches this node in roughly thirteen tool calls on average, and its compiled answers score a judge mean of 4.56 against the baseline's 4.22. Recall against the article-id ground truth is 0.67, tied at the mean with the baseline; per-trial dispersion is diagnosed in the variance note in the supplementary material. Article-touching cannot score a question whose answer is an issue that does not exist, so the recall tie does not separate the systems on this case.

Because date is a structural property of the index (a slot at the day level, populated whether or not the corresponding issue exists) even a date that has no articles still has a node, and that node can carry a summary that the agent can read directly. A flat retriever has no equivalent slot. Recovering the same behaviour from outside would mean adding side-channel metadata: a separately maintained list of known-missing issues, or extra instructions in the agent prompt about checking for absences before giving up. The calendar-shaped hierarchy makes both workarounds unnecessary, since the gap is already inside the index.

A wider point sits behind this. The failure mode here is at the level of the data model itself, which holds only article-shaped slots and no slots for dates as such; an empty article-list response is a symptom of that, not a search-engine bug to be patched. Romans reading the paper that morning learned of the deposition before the morning paper would normally have arrived, and registered that no paper had arrived; that registration was part of the experience of the day, in the way Pavone (1991) treats the *interregno* between deposition and 8 September as a historical category in its own right and not a mere gap in the record. The indexing architecture has to refuse the move that reads a non-existent issue as a null query result. In Mausoleo's three trials the agent reaches `1943-07-26`, reads the summary, and incorporates the absence as evidence into its compiled answer. In two of the baseline's three trials the agent never asks the index whether the 26 July edition exists at all, falling back on its own training-corpus knowledge of the regime change. The compiled answers therefore differ in a way the touched-set recall metric does not capture: in Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge of the regime change.

Reading the actual 27 July reappearance issue alongside the day node sharpens what the gap holds. The 27 July paper opens with the King's proclamation in centre-page and the Badoglio government list to the right; the *Grandi ordine del giorno* is reproduced verbatim further down the front page; the editorials drop the *MinCulPop*-aligned register that had still been audible in the 25 July morning paper without commenting on the change. The summary node for 26 July does not contain any of that, of course (it cannot, because the issue does not exist), but reading the 27 July issue against the 26 July summary makes legible what the 26 July issue would have had to do had it appeared: the editorial board would have had to either preview a regime change that had not yet been publicly announced, decline to mention it, or appear without an editorial line at all. The summariser has no way of choosing among these counterfactuals (and rightly does not try), but the index makes it possible for the researcher to ask the counterfactual at all by holding a slot for the missing day in which to ask it.

### Two shorter cases

The other two cases ran on the same configuration and broke the same way. The 25-to-27 July regime-change reconstruction cleared in 12.3 Mausoleo tool calls against a baseline saturating its thirty-call budget every trial, with recall 0.76 vs 0.62, quality 4.83 vs 4.44, κ = 0.57; the day-summary nodes already carry editorial tone, so the agent reads it directly off the prose. The per-week war-versus-domestic-balance question, an aggregate where touched-set recall is the wrong instrument (a first-run gave a misleading 0.07 vs 0.11), was rerun against an oracle built by classifying all 6,480 articles into WAR / DOMESTIC / OTHER and reducing to a per-week war fraction (W26 0.558, W27 0.589, W28 0.620, W29 0.733, W30 0.416); Mausoleo wins on ratio MAE 0.149 vs 0.194, tool calls 8.3 vs 28.3, and quality 4.06 vs 3.17, the largest quality gap of the three cases, with κ = 0.14.

### Aggregate numbers

All eighteen planned trials completed. Per-cell means are below.

| Case | Metric | Mausoleo | Baseline |
|---|---|---|---|
| 26 July absent | Tool calls | 13.3 | 27.0 |
| 26 July absent | Recall vs GT | 0.67 | 0.67 |
| 26 July absent | Quality (judge mean) | 4.56 | 4.22 |
| 25 July regime change | Tool calls | 12.3 | 29.7 |
| 25 July regime change | Recall vs GT | 0.76 | 0.62 |
| 25 July regime change | Quality (judge mean) | 4.83 | 4.44 |
| Comparative coverage | Tool calls | 8.3 | 28.3 |
| Comparative coverage | Ratio MAE | 0.149 | 0.194 |
| Comparative coverage | Ratio RMSE | 0.166 | 0.220 |
| Comparative coverage | Quality (judge mean) | 4.06 | 3.17 |

The regime-change case cleared in roughly twelve Mausoleo tool calls against a baseline that saturated its thirty-call budget every trial. On the missing-day case the tool-call cost was halved while touched-set recall tied, an artefact of the metric not being able to score an issue that does not exist. The comparative-coverage case showed the largest quality gap and the lowest κ, the latter reflecting how poorly the narrative-completeness rubric fitted an aggregate-shape answer.

---

## Chapter 5: Discussion

The Mausoleo configuration produced lower call-counts and higher judge means on all three cases; on touched-set recall the missing-day case ties at 0.67, where the article-counting metric is in any case poorly suited to a question whose answer is an absent issue. The size of the cost gap is largest on the comparative-coverage case (the day-summary nodes give the agent the granularity an aggregate question needs and the baseline has to reconstruct it article by article); the absolute call-count gap is largest on the regime-change case, with roughly twelve Mausoleo tool calls against a baseline saturating its thirty-call budget every trial. The two missing-day answers reach the same recall by different routes: Mausoleo reads the day-node summary; the baseline reconstructs the absence from the 25th and 27th issues plus the agent's own background knowledge of the regime change.

These results are largely consistent with the cognitive-science framing chapter two laid out. Miller (1956) and Cowan (2001) on working memory predict that compression at multiple resolutions saves cognitive cost, and the call-count gap can be read as one instance of that prediction. A descending gradient from a date-bound episode to a few-day narrative to a month-scale schema is the kind of multi-resolution movement Bartlett (1932) and later consolidation work describe as constitutive of how researchers read time-stamped material. From the hippocampal-mapping side (Eichenbaum, 2017; Whittington et al., 2020), the relevance for an external interface is more indirect: the multi-resolution form runs in the same domain-general machinery that handles analogous spatial and conceptual problems. Clark and Chalmers (1998) on the extended mind licenses treating the catalogue as part of the cognitive system the researcher reads with.

Calendar-given hierarchies hold absent-date nodes where learned hierarchies cannot, and an LLM agent over a multi-resolution index used fewer tool calls and got higher quality scores from the LLM judges than the same agent over a flat keyword index, on these three question types. How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested. The summariser also adds material that the underlying issues did not contain (the week-of-25-July *prolepsis* on Mussolini's not-yet-announced arrest is the clearest instance), and a second-order treatment of regime-aligned press in the lineage of Murialdi (1986) would want to quantify that supplementation against human-written reference summaries.

An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it.

---

## References

Bai, S., Chen, K., Liu, X., Wang, J., Ge, W., Song, S., Dang, K., et al. (2025) 'Qwen2.5-VL Technical Report', *arXiv preprint* arXiv:2502.13923.

Bartlett, F.C. (1932) *Remembering: A Study in Experimental and Social Psychology*. Cambridge: Cambridge University Press.

Behrens, T.E.J., Muller, T.H., Whittington, J.C.R., Mark, S., Baram, A.B., Stachenfeld, K.L. and Kurth-Nelson, Z. (2018) 'What is a cognitive map? Organizing knowledge for flexible behavior', *Neuron*, 100(2), pp. 490–509.

Bosworth, R.J.B. (2005) *Mussolini's Italy: Life under the Dictatorship, 1915–1945*. London: Allen Lane.

Clark, A. and Chalmers, D. (1998) 'The extended mind', *Analysis*, 58(1), pp. 7–19.

Cowan, N. (2001) 'The magical number 4 in short-term memory: a reconsideration of mental storage capacity', *Behavioral and Brain Sciences*, 24(1), pp. 87–114.

Craik, F.I.M. and Lockhart, R.S. (1972) 'Levels of processing: a framework for memory research', *Journal of Verbal Learning and Verbal Behavior*, 11(6), pp. 671–684.

Deakin, F.W. (1962) *The Brutal Friendship: Mussolini, Hitler and the Fall of Italian Fascism*. London: Weidenfeld and Nicolson.

Doucet, A., Gabay, S., Granroth-Wilding, M., Hulden, M., Düring, M., Pfanzelter, E., Marjanen, J., et al. (2020) 'NewsEye: a digital investigator for historical newspapers', in *Proceedings of Digital Humanities 2020*. Ottawa: ADHO.

Düring, M., Bunout, E. and Guido, D. (2024) 'Transparent generosity: introducing the impresso interface for the exploration of semantically enriched historical newspapers', *Historical Methods: A Journal of Quantitative and Interdisciplinary History*, 57(3), pp. 1–20. doi:10.1080/01615440.2024.2344004.

Edge, D., Trinh, H., Cheng, N., Bradley, J., Chao, A., Mody, A., Truitt, S., Metropolitansky, D., Ness, R.O. and Larson, J. (2024) 'From local to global: a Graph RAG approach to query-focused summarization', *arXiv preprint* arXiv:2404.16130.

Ehrmann, M., Romanello, M., Clematide, S., Ströbel, P.B. and Barman, R. (2020) 'Language resources for historical newspapers: the impresso collection', in *Proceedings of the 12th Language Resources and Evaluation Conference*. Marseille: ELRA, pp. 958–968.

Eichenbaum, H. (2017) 'On the integration of space, time, and memory', *Neuron*, 95(5), pp. 1007–1018.

Hutchins, E. (1995) *Cognition in the Wild*. Cambridge, MA: MIT Press.

International Council on Archives (2000) *ISAD(G): General International Standard Archival Description*. 2nd edn. Ottawa: International Council on Archives.

Ketelaar, E. (2001) 'Tacit narratives: the meanings of archives', *Archival Science*, 1(2), pp. 131–141.

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., et al. (2020) 'Retrieval-augmented generation for knowledge-intensive NLP tasks', *Advances in Neural Information Processing Systems*, 33, pp. 9459–9474.

Miller, G.A. (1956) 'The magical number seven, plus or minus two: some limits on our capacity for processing information', *Psychological Review*, 63(2), pp. 81–97.

Murialdi, P. (1986) *Storia del giornalismo italiano: Dalle gazzette a Internet*. Bologna: Il Mulino.

Murugaraj, M., Lamsiyah, S., Düring, M. and Theobald, M. (2025) 'Topic-RAG over historical newspapers: improving retrieval relevance over flat RAG on the impresso corpus', *Computational Humanities Research*, 1(e15), pp. 1–24.

Pavone, C. (1991) *Una guerra civile: Saggio storico sulla moralità nella Resistenza*. Torino: Bollati Boringhieri.

Robertson, S. and Zaragoza, H. (2009) 'The probabilistic relevance framework: BM25 and beyond', *Foundations and Trends in Information Retrieval*, 3(4), pp. 333–389.

Salton, G., Wong, A. and Yang, C.S. (1975) 'A vector space model for automatic indexing', *Communications of the ACM*, 18(11), pp. 613–620.

Sarthi, P., Abdullah, S., Tuli, A., Khanna, S., Goldie, A. and Manning, C.D. (2024) 'RAPTOR: Recursive abstractive processing for tree-organized retrieval', in *Proceedings of the 12th International Conference on Learning Representations (ICLR)*.

Schudson, M. (1978) *Discovering the News: A Social History of American Newspapers*. New York: Basic Books.

Tolman, E.C. (1948) 'Cognitive maps in rats and men', *Psychological Review*, 55(4), pp. 189–208.

Whittington, J.C.R., Muller, T.H., Mark, S., Chen, G., Barry, C., Burgess, N. and Behrens, T.E.J. (2020) 'The Tolman-Eichenbaum Machine: unifying space and relational memory through generalization in the hippocampal formation', *Cell*, 183(5), pp. 1249–1263.

Wu, J., Ouyang, L., Ziegler, D.M., Stiennon, N., Lowe, R., Leike, J. and Christiano, P. (2021) 'Recursively summarizing books with human feedback', *arXiv preprint* arXiv:2109.10862.

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K. and Cao, Y. (2022) 'ReAct: Synergizing reasoning and acting in language models', *arXiv preprint* arXiv:2210.03629.

Zhang, M. and Tang, J. (2025) 'PageIndex: vectorless, reasoning-based RAG via hierarchical tree index', *arXiv preprint* arXiv:2510.13347.
