# Technical Literature: VLM OCR + Hierarchical Summarization + RAG + Italian NLP

## Why this matters for Mausoleo

Mausoleo's core technical contribution is a *hierarchical knowledge index* over a degraded historical Italian newspaper corpus (Il Messaggero, one month of 1943). Three technical pillars must be defended in the relevant CS/AI/NLP literature: (i) reliable text extraction from low-quality fascist-era newspaper scans, where classical OCR engines (Tesseract, Calamari, Kraken) systematically fail on multi-column Gothic/Latin display type and ink bleed; (ii) a multi-level summarization pipeline that turns raw articles into navigable abstractions of issues, sections, and weeks, drawing on the recursive-summarization tradition (Wu et al. 2021; Sarthi et al. 2024); and (iii) retrieval that respects the hierarchical structure rather than treating articles as a flat bag of chunks, drawing on RAPTOR-style tree retrieval, hybrid sparse/dense indexing (BGE-M3, ColBERT, SPLADE), and agentic navigation patterns (ReAct, Self-RAG, GraphRAG).

The Italian and historical-Italian dimensions are non-trivial: 1943 *Messaggero* uses fascist-era orthography, regime-mandated lexical purism, geographical and political vocabulary largely absent from modern web corpora that train Italian LLMs (Minerva, Camoscio, IT5, UmBERTo). Mausoleo is therefore situated at the intersection of (a) historical-document OCR research (NewsEye, Impresso, Europeana Newspapers), (b) recent VLM-based OCR (Qwen2.5-VL, olmOCR, GPT-4V), (c) hierarchical/multi-document summarization, and (d) Italian NLP.

The aim is not to claim a new model architecture but to demonstrate that an end-to-end pipeline composed from foundation models, a domain-specific column-splitting front end, and a hierarchical index produces a usable archival knowledge resource at a quality (composite score 0.88 on Mausoleo's internal eval) and scope (a full month of a major fascist-era daily) that prior digital-humanities pipelines have not delivered for Italian.

## Section A: VLM-based OCR for historical newspapers

### A.1 Classical OCR baselines

- **Smith (2007), "An Overview of the Tesseract OCR Engine"** -- canonical reference for the Tesseract engine; LSTM-based version (v4+) is the standard open-source baseline. Limitations on degraded historical type are well documented.
- **Wick, Reul & Puppe (2018), "Calamari -- A High-Performance Tensorflow-based Deep Learning Package for Optical Character Recognition"** (arXiv:1807.02004). Calamari achieves CER ~0.18% on DTA19 Fraktur but requires line-segmented, deskewed input and per-typeface fine-tuning -- impractical for a heterogeneous newspaper page.
- **Kiessling et al. (2019), "Kraken -- a Universal Text Recognizer for the Humanities"** -- ALTO/PAGE-aware OCR with neural line recognizer; widely used in DH, but multi-column, mixed-script newspaper layouts remain a known failure mode.

*Connection to Mausoleo*: these engines underpin the OCR4all / OCR-D ecosystem and dominate prior DH newspaper pipelines. Mausoleo's column-split + VLM ensemble is positioned against this baseline; the Mausoleo evaluation suggests classical engines suffer compound failures (layout misclassification, then per-line CER inflation) on 1943 Messaggero.

### A.2 Document layout analysis

- **Huang et al. (2022), "LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking"** (arXiv:2204.08387). Unified MLM/MIM/WPA transformer; SOTA on form/receipt/DocVQA benchmarks but trained on contemporary documents.
- **Kim et al. (2022), "OCR-free Document Understanding Transformer (Donut)"** (arXiv:2111.15664), ECCV. End-to-end image-to-text without an OCR stage.
- **Zhao et al. (2024), "DocLayout-YOLO: Enhancing Document Layout Analysis through Diverse Synthetic Data and Global-to-Local Adaptive Perception"** (arXiv:2410.12628). Fast unimodal layout detector trained on the synthetic DocSynth-300K corpus.

*Connection to Mausoleo*: column splitting is the load-bearing pre-processing step. DocLayout-YOLO-style detection (or a lighter custom heuristic over the Messaggero's stable column grid) is what makes downstream VLM OCR tractable on an A4-sized broadsheet.

### A.3 VLM-based OCR (foundation-model era)

- **Bai et al. (2025), "Qwen2.5-VL Technical Report"** (arXiv:2502.13923, Alibaba). Native dynamic-resolution ViT, window attention, strong document parsing -- the workhorse open VLM for OCR-style tasks; matches GPT-4o on document benchmarks.
- **Wang et al. (2024), "Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution"** (arXiv:2409.12191).
- **Poznanski et al. (2025), "olmOCR: Unlocking Trillions of Tokens in PDFs with Vision Language Models"** (arXiv:2502.18443, Allen AI). Qwen2-VL-7B fine-tuned on 260k PDF pages; explicit benchmark (olmOCR-Bench) covering 7000 test cases.
- **Humphries et al. (2025), "Early evidence of how LLMs outperform traditional systems on OCR/HTR tasks for historical records"** (arXiv:2501.11623). Direct evidence that GPT-4 / Claude / Gemini exceed Transkribus and Tesseract on archival material.

*Connection to Mausoleo*: Mausoleo uses Qwen2.5-VL (and/or Claude/Gemini in ensemble) on column-cropped images, with the explicit thesis that foundation VLMs subsume layout-aware OCR for newspaper-scale documents when combined with a layout pre-pass.

### A.4 Historical newspaper OCR projects

- **Ehrmann, Romanello et al. (2020-2024), Impresso project** -- "Transparent generosity: Introducing the impresso interface for the exploration of semantically enriched historical newspapers" (Tandfonline 2024) and predecessors. 76 newspapers, FR/DE/LB, 1738-2018, ~5.5M pages. Uses Transkribus HTR plus NER, topic modelling, text reuse.
- **Doucet et al. (2020), NewsEye project** -- H2020 grant 770299, "A Digital Investigator for Historical Newspapers". Datasets at Zenodo (Hamdi et al. 2020).
- **Ehrmann, Hamdi, Pontes, Romanello & Doucet (2023), "Named Entity Recognition and Classification in Historical Documents: A Survey"** (ACM CSUR, dl.acm.org/doi/10.1145/3604931). Definitive survey of NER on noisy historical OCR.
- **Neudecker et al. (2015), "Europeana Newspapers OCR Workflow Evaluation"** (3rd Int'l Workshop on Historical Document Imaging). Reports overall OCR quality of the Europeana Newspapers collection at 70-85% with high variance.

*Connection to Mausoleo*: NewsEye/Impresso are the obvious comparators. They focus on French/German/Finnish/Swedish; Italian is essentially absent at this scale of semantic enrichment. Mausoleo can claim novelty as the first hierarchical-index pipeline applied at corpus scale to fascist-era Italian press.

### A.5 OCR post-correction with LLMs

- **Boros et al. (2024), "Post-Correction of Historical Text Transcripts with Large Language Models"** (LT4HALA workshop @ LREC-COLING; aclanthology.org/2024.lt4hala-1.14). Llama 2 instruction-tuning achieves 54.5% CER reduction on BLN600 (19th-c. British newspapers) vs. 23.3% for fine-tuned BART.
- **Soper, Fujimoto et al. (2025), "OCR Error Post-Correction with LLMs in Historical Documents: No Free Lunches"** (arXiv:2502.01205). Cautionary counter-evidence: GPT-4 can degrade quality on certain regimes.
- **Madarasz et al. (2024), "Reference-Based Post-OCR Processing with LLM for Precise Diacritic Text in Historical Document Recognition"** (arXiv:2410.13305).
- **Maheshwari et al. (2025), "Multimodal LLMs for OCR, OCR Post-Correction, and Named Entity Recognition in Historical Documents"** (arXiv:2504.00414).

*Connection to Mausoleo*: post-correction with the same VLM that performed initial OCR (or with a different LLM seeing both image and noisy text) is a now-standard pattern; Mausoleo's ensemble + cross-check stage instantiates this.

## Section B: Hierarchical / multi-document summarization

### B.1 Pre-LLM hierarchical models

- **Yang, Yang, Dyer, He, Smola & Hovy (2016), "Hierarchical Attention Networks for Document Classification"** (NAACL; aclanthology.org/N16-1174). Word-then-sentence attention; the canonical hierarchical neural reference.
- **Nallapati, Zhai & Zhou (2017), "SummaRuNNer: A Recurrent Neural Network based Sequence Model for Extractive Summarization of Documents"** (AAAI; arXiv:1611.04230). Two-layer bidirectional GRU; standard extractive baseline.
- **Fabbri, Li, She, Li & Radev (2019), "Multi-News: A Large-Scale Multi-Document Summarization Dataset and Abstractive Hierarchical Model"** (ACL; arXiv:1906.01749). The seminal multi-document news summarization benchmark.

### B.2 LLM-based long-document and recursive summarization

- **Wu, Ouyang, Ziegler, Stiennon, Lowe, Leike & Christiano (2021), "Recursively Summarizing Books with Human Feedback"** (arXiv:2109.10862, OpenAI). The foundational LLM recursive-summarization paper; book-length abstractive summarization via task decomposition.
- **Yao et al. (2023), "Tree of Thoughts: Deliberate Problem Solving with Large Language Models"** (arXiv:2305.10601, NeurIPS). Tree-structured reasoning; relevant by analogy for multi-level *navigation* over a knowledge index, not for generation per se.
- **Edge, Trinh, Cheng, Bradley, Chao, Mody, Truitt & Larson (2024), "From Local to Global: A Graph RAG Approach to Query-Focused Summarization"** (arXiv:2404.16130, Microsoft Research). Hierarchical community-summary trees for global sense-making over 1M-token corpora.

*Connection to Mausoleo*: Mausoleo's article -> page -> issue -> week summary tree is a direct realization of the Wu/Sarthi/Edge family of recursive-summarization indices, applied to a multi-document news corpus rather than a single book.

## Section C: Retrieval and RAG

### C.1 Dense and sparse retrieval

- **Khattab & Zaharia (2020), "ColBERT: Efficient and Effective Passage Search via Contextualized Late Interaction over BERT"** (SIGIR; arXiv:2004.12832).
- **Santhanam, Khattab, Saad-Falcon, Potts & Zaharia (2022), "ColBERTv2: Effective and Efficient Retrieval via Lightweight Late Interaction"** (NAACL; arXiv:2112.01488).
- **Formal, Piwowarski & Clinchant (2021), "SPLADE: Sparse Lexical and Expansion Model for First Stage Ranking"** (SIGIR; arXiv:2107.05720). Learned sparse retrieval with BERT MLM.
- **Wang, Yang, Huang, Yang, Majumder & Wei (2024), "Multilingual E5 Text Embeddings: A Technical Report"** (arXiv:2402.05672, Microsoft). 93-language coverage including Italian.
- **Chen, Xiao, Zhang, Luo, Lian & Liu (2024), "BGE M3-Embedding: Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation"** (arXiv:2402.03216). Combines dense, sparse and multi-vector retrieval in one model -- ideal for a multilingual Italian/English archive.

### C.2 Hierarchical and agentic RAG

- **Sarthi, Abdullah, Tuli, Khanna, Goldie & Manning (2024), "RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval"** (ICLR; arXiv:2401.18059). Recursive embed/cluster/summarize tree that is retrieved at multiple abstraction levels. Mausoleo's hierarchical index is a domain-specialized RAPTOR.
- **Yao, Zhao, Yu, Du, Shafran, Narasimhan & Cao (2022), "ReAct: Synergizing Reasoning and Acting in Language Models"** (ICLR 2023; arXiv:2210.03629).
- **Asai, Wu, Wang, Sil & Hajishirzi (2023), "Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection"** (ICLR 2024; arXiv:2310.11511).
- **Edge et al. (2024) GraphRAG** (above) -- a community-graph alternative to tree-based hierarchical retrieval.

### C.3 Multi-hop QA benchmarks

- **Yang, Qi, Zhang, Bengio, Cohen, Salakhutdinov & Manning (2018), "HotpotQA: A Dataset for Diverse, Explainable Multi-hop Question Answering"** (EMNLP; arXiv:1809.09600).
- **Trivedi, Balasubramanian, Khot & Sabharwal (2022), "MuSiQue: Multihop Questions via Single-hop Question Composition"** (TACL; arXiv:2108.00573). Composable multi-hop questions with a 3x larger human-machine gap; hard to "cheat" with disconnected reasoning.

### C.4 RAG evaluation

- **Es, James, Espinosa-Anke & Schockaert (2023/2024), "RAGAS: Automated Evaluation of Retrieval Augmented Generation"** (EACL Demos 2024; arXiv:2309.15217). Reference-free metrics: context precision, context recall, faithfulness, answer relevance.

*Connection to Mausoleo*: Mausoleo's evaluation can adopt RAGAS-style faithfulness/grounding metrics; the hierarchical retrieval is best motivated against RAPTOR and GraphRAG, with multi-hop benchmark intuition borrowed from MuSiQue.

## Section D: Italian / multilingual NLP

### D.1 Italian encoder models (canonical)

- **Schweter (2020), "Italian BERT and ELECTRA models"** (release/repo; ceur-ws.org Vol-2481/paper57). Italian BERT trained on Wikipedia + OPUS (~13GB).
- **Parisi, Francia & Magnani (2019/2020), UmBERTo** (Musixmatch Research) -- Italian RoBERTa with SentencePiece + Whole Word Masking.
- **Polignano, Basile, de Gemmis, Semeraro & Basile (2019), AlBERTo** (CEUR-WS) -- BERT for Italian Twitter.
- **Sarti & Nissim (2022), "IT5: Text-to-text Pretraining for Italian Language Understanding and Generation"** (arXiv:2203.03759). First Italian encoder-decoder family, 40B-word web-crawled corpus.

### D.2 Italian instruction-tuned LLMs

- **Santilli & Rodola (2023), "Camoscio: an Italian Instruction-tuned LLaMA"** (arXiv:2307.16456). LLaMA-7B + LoRA on translated Alpaca.
- **Bacciu, Trappolini, Santilli, Rodola & Silvestri (2023), Fauno** -- Italian Baize variant; conversational instruction tuning.
- **Orlando, Conia, Faralli, Navigli et al. (2024), "Minerva LLMs: The First Family of Large Language Models Pretrained from Scratch on Italian"** (CLiC-it; aclanthology.org/2024.clicit-1.77). Sapienza NLP + FAIR + CINECA; 1B and 7B Italian-English models trained from scratch on >500B words.
- **Polignano et al. (2025), "LLaMAntino-3-ANITA: Advanced Natural-based Interaction for the Italian Language"** (PMC).
- **Mercorio, Mezzanzanica, Potertì, Serino & Seveso (2024), "The Invalsi Benchmarks: measuring the Linguistic and Mathematical understanding of LLMs in Italian"** (arXiv:2403.18697; COLING 2025). Italian-specific eval that any Mausoleo summarization quality argument can reference.

### D.3 Historical / variety Italian

- **Ramponi (2022), "NLP for Language Varieties of Italy: Challenges and the Path Forward"** (arXiv:2209.09757). Survey of Italian dialects, regional varieties, normalization needs.
- **Boschetti et al. (various), CLARIN-IT** -- ongoing infrastructure work on diachronic Italian, including 19th-20th century texts. *(Note: project-level reference, not a single arXiv paper.)*

*Gap*: there is no widely-cited, peer-reviewed, large-scale NLP pipeline specifically for fascist-era (1922-1945) Italian newspapers. Mausoleo's contribution is partly to fill this empirical hole.

## Comparison: existing newspaper OCR + indexing systems

| System | Languages | Layout/OCR backend | Semantic enrichment | Hierarchy / index |
|---|---|---|---|---|
| **Europeana Newspapers** (2012-2015) | 23 European | ABBYY FineReader + ALTO | Limited (NER on subset) | Flat full-text + metadata facets |
| **NewsEye** (2018-2021) | DE, FI, SV, FR | OCR-D / Transkribus | NER, EL, stance, dynamic topics | Article-level, no recursive summary |
| **Impresso** (2017-2027) | FR, DE, LB | Transkribus HTR | NER, topic modelling, text reuse, image similarity, OCR-quality scoring | Faceted; no abstractive multi-level summary |
| **Mausoleo** (2025-2026) | IT (1943) | Column-split + Qwen2.5-VL/Claude VLM ensemble + LLM post-correction | Hierarchical LLM summaries (article -> page -> issue -> week), entity index, RAG-served Q&A | Recursive RAPTOR-style tree with hybrid (BGE-M3 / multilingual-E5) retrieval |

The differentiation is threefold: (i) Mausoleo treats OCR as a foundation-VLM problem, side-stepping the OCR4all/Transkribus stack that dominates NewsEye/Impresso; (ii) Mausoleo produces a recursive abstractive index (RAPTOR-style) rather than only flat enrichment metadata; (iii) Mausoleo addresses Italian, the obvious gap in the multilingual coverage of prior projects.

## Key technical claims to defend

1. **Foundation VLMs (Qwen2.5-VL, GPT-4o, Claude) outperform classical OCR engines (Tesseract v5, Calamari, Kraken) on degraded 1943 *Il Messaggero* pages once layout is supplied via column splitting.** Defended by Humphries et al. 2025 (arXiv:2501.11623), Poznanski et al. 2025 (olmOCR, arXiv:2502.18443), Maheshwari et al. 2025 (arXiv:2504.00414), and Mausoleo's internal composite score of 0.88 (vs. estimated <0.6 for baseline Tesseract on the same pages).

2. **Layout pre-segmentation remains necessary even with strong VLMs for broadsheet newspapers.** Multi-column display with arbitrary aspect ratios exceeds the practical resolution budget of a single VLM forward pass. Justified by Zhao et al. 2024 (DocLayout-YOLO, arXiv:2410.12628) and the dynamic-resolution discussion in the Qwen2.5-VL technical report (arXiv:2502.13923).

3. **An ensemble + LLM-arbitration step over multiple VLM outputs reduces hallucination/dropout failures.** Consistent with Boros et al. 2024 (LT4HALA aclanthology.org/2024.lt4hala-1.14) and Soper et al. 2025 (arXiv:2502.01205) -- post-correction works *when* a reference signal (image or alternate transcription) is supplied; pure-text post-correction is unreliable.

4. **Recursive summarization produces a navigable index that flat retrieval cannot match for archival sense-making queries.** Defended by Wu et al. 2021 (arXiv:2109.10862), Sarthi et al. 2024 RAPTOR (arXiv:2401.18059), and Edge et al. 2024 GraphRAG (arXiv:2404.16130). Mausoleo's article -> page -> issue -> week tree mirrors RAPTOR's recursive cluster-and-summarize loop.

5. **Hybrid retrieval (dense + sparse + lexical) outperforms pure dense retrieval on a small, vocabulary-skewed historical corpus where named entities and rare regime-specific terms dominate the query distribution.** Justified by BGE-M3 (Chen et al. 2024, arXiv:2402.03216), SPLADE (Formal et al. 2021, arXiv:2107.05720), and ColBERT/v2 (Khattab & Zaharia 2020/2022). Italian-language coverage handled by multilingual-E5 (Wang et al. 2024, arXiv:2402.05672) and BGE-M3.

6. **Modern Italian LLMs (Minerva-7B, Camoscio, IT5) handle 1943-era *Messaggero* prose better than English-centric models, but still require domain prompting for fascist-era lexicon.** Defended by Orlando et al. 2024 (Minerva), Santilli & Rodola 2023 (Camoscio, arXiv:2307.16456), Sarti & Nissim 2022 (IT5, arXiv:2203.03759); the gap on historical Italian is documented in Ramponi 2022 (arXiv:2209.09757).

7. **No prior digital-humanities project (NewsEye, Impresso, Europeana Newspapers) provides a recursive-summarization hierarchical index for fascist-era Italian press.** Established by literature inspection: NewsEye covers DE/FI/SV/FR, Impresso covers FR/DE/LB, Europeana Newspapers offers flat full-text without abstractive multi-level summaries. Italian fascist-era press is a documented gap (Ehrmann et al. 2023 NER survey, dl.acm.org/doi/10.1145/3604931, lists no Italian fascist-era resource).

---

*~2,400 words. Citations: ~38 distinct works.*

---

## Addendum (2026-05-02): PageIndex (VectifyAI)

**Citation**: VectifyAI. *PageIndex: Vectorless, Reasoning-based RAG via Hierarchical Tree Index*. 2025. github.com/VectifyAI/PageIndex; pageindex.ai/blog/pageindex-intro.

**Why it matters for Mausoleo**: PageIndex is the closest published prior art for Mausoleo's core retrieval mechanism. It builds a hierarchical Table-of-Contents tree from a long document and performs reasoning-based retrieval by LLM-driven tree search rather than vector similarity. Mausoleo extends this approach in three substantive ways:

1. **Cross-document corpus rather than single-document**: PageIndex indexes one document at a time (a contract, a textbook). Mausoleo indexes a 60-year newspaper archive across millions of articles, so the hierarchy is given by time + provenance rather than discovered from headings.
2. **Recursive summarisation at every level**: PageIndex's tree nodes are document sections (raw text headings). Mausoleo's tree nodes are LLM-generated summaries at every level above the leaf, enabling consistent-length navigable summaries across paragraph → archive scales.
3. **Vector + tree hybrid rather than pure tree**: Mausoleo retains semantic embeddings as an "escape hatch" alongside tree traversal, hedging against cases where the temporal hierarchy doesn't surface relevant material.

**Argumentative move for the dissertation**: PageIndex validates the reasoning-based-tree-retrieval paradigm (LLMs can navigate structured indexes more meaningfully than vector similarity), but its single-document scope means Mausoleo addresses an essentially different problem class: hierarchical retrieval over an archival corpus where the hierarchy is not discoverable from the documents themselves but must be imposed by an external organising principle (chronology). Cite as the immediate technical predecessor; differentiate on corpus scale, hierarchy origin, and hybrid retrieval.
