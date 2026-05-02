# Digital Humanities + Archival Science + Information Retrieval

A literature review for the BASC0024 dissertation on Mausoleo, a hierarchical knowledge index over one month of *Il Messaggero* (1943).

---

## Why this matters for Mausoleo

Mausoleo sits at the intersection of three mature literatures that rarely speak to one another. As a *digital humanities* artefact it operates on a heritage corpus at scale, inheriting the methodological debates around "distant reading" and computational analysis. As an *archival* system it must reckon with two centuries of theory about what an archive *is* — questions of provenance, original order, fonds, and the active role archivists (and now algorithms) play in shaping what users can see. As an *information retrieval* system it stands alongside, and partly against, the dominant search paradigm: TF-IDF and BM25, dense retrieval, and the recent retrieval-augmented-generation (RAG) stack.

The dissertation's central claim — that Mausoleo offers a *navigable knowledge structure* rather than a *searchable database* — is not a vague design preference but a specific methodological position. It asks: when a user does not know what they are looking for, can a hierarchically pre-summarised, agent-mediated index serve historical inquiry better than free-text search? That question is sharpest when Mausoleo is read against existing systems: Chronicling America (LoC), Europeana Newspapers, and especially Impresso, the closest comparator in scope and ambition. Each of those systems converges on the same UX template — a search box plus faceted filters over OCR'd text — which presupposes the user already has a query in mind. Mausoleo's hierarchical/temporal organisation is closer in spirit to RAPTOR (Sarthi et al. 2024) and GraphRAG (Edge et al. 2024) than to Impresso.

Engaging all three literatures lets the dissertation argue that Mausoleo is neither a re-implementation of Impresso nor a generic RAG demo, but a methodologically distinctive intervention: it preserves *original temporal order* (an archival principle) while exposing *macroscopic patterns* (a digital-humanities goal) through *hierarchical retrieval* (a current IR technique).

---

## Section A: Digital humanities

### A.1 Distant reading and macroanalysis (foundational)

**Moretti, F. (2013).** *Distant Reading.* London: Verso. Coined the term "distant reading" (Moretti 2000); collected essays defending quantitative, large-scale literary analysis as complementary, not subordinate, to close reading. Won the National Book Critics Circle Award; remains the canonical reference for the paradigm Mausoleo extends. (https://www.versobooks.com/products/2309-distant-reading)

**Jockers, M. L. (2013).** *Macroanalysis: Digital Methods and Literary History.* University of Illinois Press. Coined "macroanalysis" — a middle ground between close reading and Moretti's distant reading, using corpus-level statistics to surface patterns across thousands of texts. Useful framing for Mausoleo: agent-mediated drill-down explicitly *bridges* macro and micro. (https://www.press.uillinois.edu/books/?id=p079078)

### A.2 Cultural analytics (foundational + recent)

**Manovich, L. (2020).** *Cultural Analytics.* MIT Press. Manovich is the founder of cultural analytics; this book consolidates a decade of arguments about using computational methods to study cultural artefacts at scale. The argument that "before we can theorise digital culture, we need to see it" is directly relevant to Mausoleo's emphasis on legibility-at-scale. (https://mitpress.mit.edu/9780262037105/cultural-analytics/)

### A.3 Existing digital newspaper archives (recent comparators)

**Ehrmann, M., Bunout, E., & Düring, M. (2020).** "Language Resources for Historical Newspapers: the Impresso Collection." *LREC 2020*. Documents the Impresso pipeline: OCR, NER, topic modelling, lexical-semantic enrichment over Swiss/Luxembourgish newspapers across ~200 years. Closest comparator to Mausoleo by far. (https://aclanthology.org/2020.lrec-1.121/)

**Düring, M., Ehrmann, M., Wieneke, L., & Clematide, S. (2024).** "Transparent generosity: Introducing the impresso interface for the exploration of semantically enriched historical newspapers." Updated treatment of the Impresso UI and how it affords exploration vs. search. (https://www.researchgate.net/publication/381413338)

**Library of Congress.** *Chronicling America* / National Digital Newspaper Program. ~23M pages, 1690–1963; faceted search + OCR'd full text. The reference point for "what a digital newspaper archive looks like in practice" in the US. (https://chroniclingamerica.loc.gov/)

**Europeana Newspapers project (2012–2015 + ongoing).** ~28M digitised pages across 40 languages, full-text search via OCR (~70–85% quality). Demonstrates the dominant model: aggregate + index + faceted search. (http://www.europeana-newspapers.eu/)

### A.4 Critiques of computational humanities (recent)

**Da, N. Z. (2019).** "The Computational Case against Computational Literary Studies." *Critical Inquiry* 45(3): 601–639. Argues computational literary studies produces results that are either obvious-and-robust or non-obvious-and-non-robust; flags a mismatch between statistical tools and literary objects. Crucial for any DH-adjacent project to engage with — Mausoleo's response is that it does not *interpret* texts statistically; it *organises* them, deferring interpretation to the agent and the user. (https://www.journals.uchicago.edu/doi/abs/10.1086/702594)

**Underwood, T. (2019).** *Distant Horizons: Digital Evidence and Literary Change.* University of Chicago Press. The strongest recent reply to Da: positions statistical models as *interpretive* strategies akin to humanistic interpretation, not replacements for it. (https://press.uchicago.edu/ucp/books/book/chicago/D/bo35853783.html)

**Mullen, L. (2018, ongoing).** Has argued in *Computers and the Humanities* and elsewhere that DH should aim for "computational humility" — using algorithms as one source of evidence among many. Useful framing but narrower than Underwood.

---

## Section B: Archival science

### B.1 Provenance and original order (foundational)

**Jenkinson, H. (1922; 2nd ed. 1937).** *A Manual of Archive Administration.* Oxford: Clarendon. The text that imported continental ideas of *respect des fonds* and *original order* into the Anglophone tradition. Jenkinson treats the archivist as a "neutral custodian" whose job is to preserve evidence of the records' creation context. Mausoleo's commitment to *temporal* hierarchy (issue → date → page → article) is a deliberate echo of original order. (https://archive.org/details/manualofarchivea00jenkuoft)

**Schellenberg, T. R. (1956).** *Modern Archives: Principles and Techniques.* Chicago: University of Chicago Press. The American counterweight to Jenkinson, distinguishing primary (evidential) from secondary (informational) value of records. Provides the conceptual vocabulary for explaining why a newspaper archive is not a simple text corpus.

### B.2 Description and access standards (foundational)

**International Council on Archives (2000).** *ISAD(G): General International Standard Archival Description, 2nd ed.* The standard for *multi-level description* — fonds → subfonds → series → file → item. Mausoleo's hierarchy maps almost cleanly onto this: newspaper title (fonds) → year/month (series) → issue (file) → article (item). Worth citing explicitly to show Mausoleo is not inventing hierarchy from scratch. (https://www.ica.org/resource/isadg-general-international-standard-archival-description-second-edition/)

**Encoded Archival Description (EAD).** XML standard maintained by the SAA / Library of Congress for archival finding aids; the machine-readable instantiation of ISAD(G).

### B.3 Postmodern archival theory (foundational + recent)

**Cook, T. (2013).** "Evidence, memory, identity, and community: four shifting archival paradigms." *Archival Science* 13(2–3): 95–120. Cook's culminating essay: archives have moved from juridical-evidentiary to memory to identity to community paradigms; archivists are no longer neutral custodians but active mediators. Critical for Mausoleo: an LLM-mediated index is undeniably an *active* mediator, and Cook's framework lets the dissertation argue this is a continuation, not a betrayal, of contemporary archival theory. (https://link.springer.com/article/10.1007/s10502-012-9180-7)

**Ketelaar, E. (2001).** "Tacit Narratives: The Meanings of Archives." *Archival Science* 1: 131–141. Each interaction with a record is an "activation" that layers further meaning on it. Mausoleo's summaries are activations in Ketelaar's sense — they do not neutrally describe articles but inscribe an interpretive layer that future users will encounter. (https://link.springer.com/article/10.1007/BF02435644)

### B.4 Algorithmic archival processing (recent)

**Jaillant, L. (ed.) (2022).** *Archives, Access and Artificial Intelligence: Working with Born-Digital and Digitized Archival Collections.* Bielefeld University Press. The most current treatment of AI-assisted archival description; directly addresses ethical and methodological tensions. Essential citation. (https://cup.columbia.edu/book/archives-access-and-artificial-intelligence/9783837655841/)

**Marciano, R., Lemieux, V., Hedges, M., Esteva, M., Underwood, W., Kurtz, M., & Conrad, M. (2018).** "Archival Records and Training in the Age of Big Data." Articulates *Computational Archival Science (CAS)* as a transdiscipline. Mausoleo can be positioned as a small-scale instance of the CAS programme. (https://ai-collaboratory.net/cas/)

### B.5 Faceted classification (foundational, bridging to IR)

**Ranganathan, S. R. (1933).** *Colon Classification.* Madras Library Association. The first faceted classification system (PMEST: Personality, Matter, Energy, Space, Time). A useful theoretical foil: Mausoleo's hierarchy is overwhelmingly *Time*-driven, where Ranganathan's PMEST is a balanced product. Discussing this lets the dissertation defend its temporal-primacy choice as appropriate for a *daily* newspaper, where time is the dominant axis of organisation. (https://en.wikipedia.org/wiki/Colon_classification)

---

## Section C: Information retrieval (with extra emphasis on RAG and hierarchical retrieval)

### C.1 Classical IR (foundational)

**Salton, G., Wong, A., & Yang, C. S. (1975).** "A Vector Space Model for Automatic Indexing." *Communications of the ACM* 18(11): 613–620. The vector space model — documents and queries as TF-IDF-weighted vectors, similarity by cosine. Foundational. (https://dl.acm.org/doi/10.1145/361219.361220)

**Robertson, S., & Zaragoza, H. (2009).** "The Probabilistic Relevance Framework: BM25 and Beyond." *Foundations and Trends in IR* 3(4): 333–389. BM25 as the apex of the probabilistic-relevance tradition; still a strong baseline against which dense retrievers are measured. (https://www.staff.city.ac.uk/~sbrp622/papers/foundations_bm25_review.pdf)

### C.2 Dense retrieval (recent)

**Reimers, N., & Gurevych, I. (2019).** "Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks." *EMNLP-IJCNLP 2019*. Made BERT-quality semantic similarity tractable for retrieval. The infrastructure for nearly every modern semantic-search system. (https://aclanthology.org/D19-1410/)

**Karpukhin, V., et al. (2020).** "Dense Passage Retrieval for Open-Domain Question Answering." *EMNLP 2020*. DPR — dual-encoder dense retrieval, 9–19% absolute gain over BM25 at top-20 accuracy. Established that dense retrieval can dominate sparse retrieval on QA workloads. (https://aclanthology.org/2020.emnlp-main.550/)

**Chen, J., Xiao, S., Zhang, P., Luo, K., Lian, D., & Liu, Z. (2024).** "M3-Embedding: Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation." *Findings of ACL 2024.* The BGE-M3 model — 100+ languages, supports dense + sparse + multi-vector retrieval, up to 8192 tokens. Directly relevant: Italian historical text needs strong multilingual embeddings, and BGE-M3 is a defensible default. (https://aclanthology.org/2024.findings-acl.137/)

### C.3 Hybrid retrieval and re-ranking (recent)

**Khattab, O., & Zaharia, M. (2020).** "ColBERT: Efficient and Effective Passage Search via Contextualized Late Interaction over BERT." *SIGIR 2020*. Late-interaction multi-vector retrieval: keeps token-level granularity at retrieval time. The reference point for "what could a more granular retriever look like." (https://dl.acm.org/doi/10.1145/3397271.3401075)

### C.4 RAG over long-form / archival corpora (recent — Mausoleo's direct neighbour)

**Lewis, P., et al. (2020).** "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks." *NeurIPS 2020.* The original RAG paper: parametric (seq2seq) + non-parametric (dense index) memory. The architectural ancestor of every modern document-grounded LLM system, including Mausoleo. (https://arxiv.org/abs/2005.11401)

**Boroș, E., et al. (2024).** "Retrieval Augmented Generation for Historical Newspapers." *JCDL 2024.* Direct prior art: RAG over historical newspaper archives, with NER-augmented retrieval and re-ranking shown to mitigate OCR noise. The single most important comparator paper for Mausoleo's IR claims. (https://dl.acm.org/doi/10.1145/3677389.3702542)

**Thomas, A., et al. (2024).** "Leveraging LLMs for Post-OCR Correction of Historical Newspapers." *LT4HALA 2024.* Llama-2 reduces character error rate by 54% over fine-tuned BART on the BLN600 corpus. Shows that LLMs are now part of the historical-newspaper preprocessing pipeline, not just the front-end. (https://aclanthology.org/2024.lt4hala-1.14/)

### C.5 Hierarchical retrieval (recent — Mausoleo's most direct neighbour)

**Sarthi, P., Abdullah, S., Tuli, A., Khanna, S., Goldie, A., & Manning, C. D. (2024).** "RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval." *ICLR 2024.* Recursively clusters and summarises chunks bottom-up into a tree; retrieves at multiple abstraction levels. The conceptual closest sibling to Mausoleo, though Mausoleo's tree is *given* by archival/temporal structure rather than *induced* by clustering. (https://arxiv.org/abs/2401.18059)

**Edge, D., Trinh, H., Cheng, N., et al. (2024).** "From Local to Global: A Graph RAG Approach to Query-Focused Summarization." Microsoft Research / arXiv 2404.16130. GraphRAG: builds a knowledge graph + hierarchical community summaries (Leiden clustering), retrieves at chosen abstraction level. Outperforms naive RAG ~70–80% on comprehensiveness/diversity. The strongest argument that *hierarchical* retrieval is now mainstream. (https://arxiv.org/abs/2404.16130)

---

## Comparison: existing digital newspaper archives vs. Mausoleo

| System | Scope | Access paradigm | Enrichment | What it does *not* do |
|---|---|---|---|---|
| **Chronicling America** (LoC) | ~23M pages, US, 1690–1963 | Faceted search + OCR full-text | Minimal; OCR + basic metadata | No semantic enrichment, no summarisation, no agent mediation |
| **Europeana Newspapers** | ~28M pages, 40 EU languages | IIIF + full-text search APIs | OCR, OLR, NER (limited) | No hierarchical browsing, no narrative aggregation |
| **Impresso** | Swiss/Luxembourgish, ~200 yrs, French/German/Luxembourgish | Search + faceted exploration + visual comparison | NER, topic models, lexical-semantic enrichment, text reuse | Still query-driven; no agent-mediated drill-down; not designed for users without a query in mind |
| **Mausoleo** | One month, *Il Messaggero* 1943, Italian | Hierarchical navigation + agent-mediated drill-down | LLM summaries at multiple levels of abstraction | Not optimised for ad-hoc keyword search; smaller scope |

The distinguishing claim: Chronicling America, Europeana, and Impresso all assume the user arrives with a query. Mausoleo assumes the user arrives wanting to *understand* a corpus they cannot read in full. This is a different access modality, closer to RAPTOR / GraphRAG than to traditional newspaper archives.

---

## Key arguments to deploy

1. **Mausoleo extends the distant-reading paradigm by enabling agent-mediated drill-down rather than purely aggregate analysis** (Moretti 2013; Jockers 2013; Underwood 2019). Where Moretti's distant reading produces aggregate visualisations and Jockers' macroanalysis produces statistical summaries, Mausoleo produces a *navigable* hierarchy that a user can descend interactively — recovering close reading at the leaves while preserving distant-reading legibility at the root.

2. **Mausoleo preserves archival original order while transforming description, in line with Cook's (2013) "active mediator" paradigm.** The temporal hierarchy maps cleanly onto ISAD(G)'s multi-level description; the LLM-generated summaries are activations in Ketelaar's (2001) sense — additions to, not replacements of, the original record. The dissertation can argue Mausoleo is *traditionalist about provenance* while *postmodern about description*.

3. **Mausoleo's primarily-temporal hierarchy is a defensible specialisation of Ranganathan's PMEST faceted classification for daily-newspaper material**, where Time is the dominant ordering axis and Personality/Matter/Energy/Space are accessed *through* time rather than alongside it.

4. **Mausoleo addresses the OCR-noise problem in historical-newspaper RAG identified by Boroș et al. (2024)** by performing semantic retrieval over LLM-generated summaries rather than raw OCR text. Summaries function as a noise filter, partly mitigating the brittleness of dense retrieval over OCR-degraded heritage text.

5. **Mausoleo is best understood as a special case of the hierarchical-retrieval lineage (RAPTOR, GraphRAG) where the hierarchy is given by archival structure rather than learned from data.** This is methodologically defensible because daily newspapers already have a strong native hierarchy; the choice to use it rather than re-discover it via clustering is consistent with archival respect for original order.

6. **The Da (2019) critique applies less forcefully to Mausoleo than to most computational literary studies** because Mausoleo does not produce statistical claims about the corpus — it produces *navigable affordances* over it. Da's "robust-or-non-obvious" dilemma targets inference; Mausoleo's primary deliverable is access, not inference.

7. **Mausoleo participates in Marciano et al.'s Computational Archival Science programme** but at a smaller, more accessible scale: rather than processing terabytes, it demonstrates the value of computational archival processing on a single month — an undergraduate-tractable instantiation of CAS that retains methodological seriousness.

---

*Word count: approximately 2,200.*
