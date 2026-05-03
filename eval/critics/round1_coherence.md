# Round 1 Coherence Review — MAUSOLEO_FULL_DRAFT_v1

**Reviewer**: COHERENCE critic, Phase 3 round 1
**Date**: 2026-05-03
**Target**: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v1.md` (12,766 words total / 11,940 main body)
**Outline**: `/tmp/mausoleo/references/outline.md`
**Verdict**: **FAIL** (3 CRITICAL, 6 HIGH, 8 MED, 5 LOW)

---

## 1. Per-issue table

| # | Issue type | Location(s) | Severity |
|---|---|---|---|
| C1 | Embedding-model contradiction: §3.2 / §5.1 / §5.2 say BGE-M3, 1024-dim. §6.5 ("Embedding restoration") says `paraphrase-multilingual-MiniLM-L12-v2`, 384-dim — and explicitly says "the same model used to build the stored ClickHouse `embedding` column." These two cannot both be true. | §3.2 L111; §5.1 L167; §5.2 L177; §6.5 L361, L433 | **CRITICAL** |
| C2 | Word-budget overshoot of hard cap: 11,940 main-body words against the 10,000 hard cap (outline L7). Driven by §6.5 (1769w / 300w target = +488%) plus uniform overshoot in every other section. | All sections; §6.5 acutely | **CRITICAL** |
| C3 | Broken cross-reference: §1 L47 promises "the design that makes [the absent-day node] possible is described in §3.3." §3.3 is the agent/CLI section; the absent-day-node-as-first-class-object architecture actually lives in §3.2 (L113). | §1 L47 → §3.2 L113 | **HIGH** |
| C4 | §7.2 fails to deliver promised limitations. §6.1 L199 says judge-2 substitution "is treated as a limitation in §7.2." §6.4 L229 says the rubric-fit issue is "flagged as a rubric-fit limitation in §7.2." Neither appears in §7.2 (L459-463). | §6.1 L199, §6.4 L229 → §7.2 L459-463 | **HIGH** |
| C5 | Level-count contradiction: §7.3 L467 says "seven-level schema (paragraph, article, day, week, month, year, decade, archive)" — that enumerates EIGHT levels. Outline L96 specifies 7 production levels. §3.2 / §5.1 / §5.2 are all internally ambiguous about which 7 (production "extends to year, decade, archive" added to the case-study 5 = 8). | §7.3 L467; §3.2 L109, §5.1 L167; outline L96 | **HIGH** |
| C6 | Vector-index naming drift: §3.2 L109 + §3.3 L119 + §5.1 L169 say "**usearch L2 index**". §6.5 L414 + §8 L479 say "**HNSW vector index**". Plausibly the same thing under the hood, but the reader cannot tell. | §3.2 L109, §3.3 L119, §5.1 L169 vs §6.5 L414, §8 L479 | **HIGH** |
| C7 | Abstract overstates judge unanimity: "preferred by two LLM judges on a three-dimension rubric **in every case**" (L13) — but case 1 sign test = 3M / 1B (κ=0.33, judge 1 sometimes downscores Mausoleo, §6.2 L213). Mausoleo wins on judge **mean** in every case, not on every judge × case cell. | Abstract L13 vs §6.2 L213, §6.5 L261 | **HIGH** |
| C8 | "Capability gap" overclaim: Abstract L13 ("the BM25 baseline cannot return it"), §7.1 L457 ("BM25 baseline cannot return anything") and §8 L479 ("flat retrieval cannot close at all") all overstate, since §6.2 L207 documents that the baseline reaches recall 0.67 and quality 4.22 on case 1 by reasoning around the absence from sibling-day articles. The architectural point survives a more honest framing. | Abstract L13, §7.1 L457, §8 L479 vs §6.2 L207 | **HIGH** |
| C9 | §6.5 (1769w) crowds out §6.3 (473w) and §6.4 (440w), both of which sit BELOW their outline budget. Per-case results are duplicated between §6.3/§6.4 prose and §6.5 mini-narratives (lines 309-355). The §6.5 mini-narratives ("Case 1 — the missing 1943-07-26", "Case 2 — July 25 regime change", "Case 3 — comparative coverage") restate material already in §6.2/§6.3/§6.4 with no new information. | §6.5 L309-355 vs §6.2-§6.4 | **HIGH** |
| C10 | Sub-pipeline count drift in §3.1 / §4.2 vs outline. Draft (§3.1 L99, §4.2 L143) consistently says **8 sub-pipelines / 8 sources**. Outline L91 says **6 sub-pipelines**. The draft is internally consistent on 8; outline is stale. Not a draft-internal contradiction, but outline-vs-draft drift the reader will notice if they have the outline. (Marked MED because the draft is internally clean.) | §3.1 L99, §4.2 L143 vs outline L91 | MED |
| C11 | Column-split granularity inconsistency: §3.1 L99 lists "two-, three-, four-, five-, and six-column splits". §4.2 L143 lists "full-page, three-, four-, five-, six-column" (no column-two). §4.2 L145 then says cross-family stack added "the four Qwen2.5-VL-7B variants (column-two, column-three, column-four, full-page)". Internal inconsistency on whether the eight-source ensemble includes column-two. | §3.1 L99 vs §4.2 L143 vs §4.2 L145 | MED |
| C12 | §6.1 L201 promises "the planned 2-week self-consistency re-annotation could not be performed within the dissertation timeline" — outline L183 had explicitly required it "as a rigor floor". §7.2 L463 then says "single-annotator; a second-annotator agreement check is the obvious extension," conflating the missing intra-rater check with a separate inter-annotator extension. | §6.1 L201, §7.2 L463 | MED |
| C13 | §3.1 L101 "no LLM arbitration step and no standalone post-correction model in the production configuration. Both were tried during the hill-climb (§4.2 reports the ablation)" — but the LLM-post-correction ablation appears in §4.3 L153, not §4.2. Cross-ref to wrong subsection. | §3.1 L101 → §4.3 L153 | MED |
| C14 | §1 L49 says case 1 is "treated separately in §6.2 because its asymmetry is definitional rather than quantitative" — but §6.2 actually reports full quantitative comparison (recall, quality, tool calls, sign test). The §1 framing of "definitional rather than quantitative" is then re-asserted in §6.5 L319 and §7.1 L457, but §6.2 itself does both. The framing is at war with the content. | §1 L49 vs §6.2 L207-213 vs §6.5 L319, §7.1 L457 | MED |
| C15 | "ratio MAE/RMSE against an LLM-built per-week war/domestic oracle" (§6.1 L199) says oracle was built for case 3, but the Sonnet-4.5 oracle classification is described only in §6.4 L227 and §6.5 L287. The §6.1 forward-reference is correct in principle (it does point to §6.4) but the reader has to wait 30 lines to learn that the oracle is itself Sonnet-4.5-derived — a self-reference loop the reader should be warned about up front. | §6.1 L199 forward-ref to §6.4 L227 | MED |
| C16 | "Three trials per cell at distinct random seeds" (§6.1 L197) — but Sonnet 4.5 is not a deterministic-by-seed model on the OAuth path. The methodological commitment is stated more strongly than the implementation can support. | §6.1 L197 | MED |
| C17 | §3.1 L97 "thirty minutes wall-clock per issue" vs §3.1 L103 "30.5 minutes per issue" vs §4.2 L143 "30.5 minutes on GPU0". Three closely-related numbers, two of them slightly above the stated budget. Not an error, but the reader is owed one sentence saying "30 min budget; observed wall 30.5 min on the harder issue." | §3.1 L97, L103; §4.2 L143 | MED |
| C18 | Preface 505w against ≤500 brief; abstract 280w against ≤300 (clean). Preface is +1%, trivial. | Preface | LOW |
| C19 | Per-section overshoots above outline targets: §1 +13%, §4 +13%, §5 +18%, §7 +12%. Each is individually within Phase-3 tolerance; cumulatively they push the total well over the 9600w budget even before §6.5. | All sections | LOW |
| C20 | "BIECO FUREORE BRITANNICO" (§6.3 L217) appears to be a typo for "BIECO FURORE BRITANNICO" (consistent with outline L211). Italian spell-check failure rather than a coherence issue, but the same headline is glossed correctly in the outline. | §6.3 L217 | LOW |
| C21 | §3.1 L101 "REPLACE chain of nine entries (one source... appears twice)" — nine entries from eight sources is consistent. §4.2 L143 repeats "REPLACE chain of nine entries". Internally consistent. (No issue; recorded as a passed check.) | §3.1 L101, §4.2 L143 | LOW (passed) |
| C22 | "*Magnetizzata*" example in §4.1 L137 is well-placed but never recurs; an orphan illustration that the reader may expect to see again in §4.2 / §4.3. Stylistic, not load-bearing. | §4.1 L137 | LOW |
| C23 | §5.3 L185 reports the spot-check 48/50 entities recovered with the two misses both `Papa Pio XII`. The §5.2/§5.3 numbering "ten of ten passes (forty-eight of fifty entities)" — 10/10 day-passes, 48/50 entities — uses two different success criteria in one sentence. Internally consistent but compact to the point of being unclear. | §5.3 L181 | LOW |

---

## 2. Number-consistency table

| Number | Where it appears | Value at each location | Verdict |
|---|---|---|---|
| Final OCR cold-cache composite | §4 intro L131; §4.2 L145; §4.3 L155 | 0.89878 / 0.89878 / 0.89878 | CONSISTENT |
| OCR composite — warm-cache historical | §4.1 L139 | 0.92717 → 0.88682 (rebaseline) | CONSISTENT (single mention) |
| OCR composite — unconstrained ceiling | §3.1 L103 ("~0.92"); §4 intro L131 ("0.9203"); §4.3 L155 ("0.9203 production ceiling") | 0.92 / 0.9203 / 0.9203 | CONSISTENT (round-down OK) |
| Per-issue OCR composite | §4.2 L145: 0.872 (1885), 0.926 (1910) | single source | CONSISTENT |
| 1885 wCER stack delta | §3.1 L103 (+0.013); §4.2 L145 (+0.013, "0.234 → 0.149") | +0.013 / +0.013 | CONSISTENT |
| Sub-pipeline count | §3.1 L99 ("Eight"), §4.2 L143 ("eight-source ensemble"), §6.5 L389 ("8 sub-pipelines") | 8 / 8 / 8 | CONSISTENT internally; outline L91 says 6 (stale) |
| Articles in 1885 GT | §4.1 L135 (41 articles); abstract not mentioned | 41 | CONSISTENT |
| Articles in 1910 GT | §4.1 L135 (193 articles) | 193 | CONSISTENT |
| Raw → cleaned 1943 articles | §3.1 L105 (9456 → 6480); §3.2 L113 (6480 article nodes); §5.1 L169 (6,480 articles); §6.4 L227, §6.5 L288, L396, L409, L413 | 9456 / 6480 / 6,480 / 6,480 | CONSISTENT (mixed comma styling — minor LOW) |
| Total nodes | §3.2 L113 (6517 = 6480+31+5+1); §5.1 L169 (6,517); §6.5 L413 (6,517) | 6517 / 6,517 / 6,517 | CONSISTENT |
| Day / week / month nodes | §3.2 L113 (31 / 5 / 1); §5.1 L169 (31 / 5 / 1); §6.5 L397 (31 / 5 / 1) | identical | CONSISTENT |
| OCR build wall-time | §3.1 L103 (30.5 min/issue); §4.2 L143 (30.5 GPU0, 28.9 GPU1); §6.5 L394 (~30.5 min, ~15.3 wall-hours, ~29.7 GPU-hours); §7.2 L461 (~29.7 GPU-hours) | CONSISTENT | CONSISTENT |
| Index-build phantom-USD | §6.5 L399 ($28.87); §7.2 L461 (~$29) | CONSISTENT (rounding) | CONSISTENT |
| Per-query input tokens (M) | §6.5 L405 (328 k); abstract / §7.1 / §8 do not repeat | single source | CONSISTENT |
| Mausoleo across-cases mean tool calls | Abstract L13 (mean 11.0); §6.5 L405 (11.0); §7.1 L455 (does not give a mean, gives per-case) | 11.0 / 11.0 | CONSISTENT |
| Baseline across-cases mean tool calls | Abstract L13 (28.3); §6.5 L407 (28.3) | 28.3 / 28.3 | CONSISTENT — but **note**: 28.3 is also case-3's baseline tool-call number specifically, so reusing it as the "across-cases mean" is a numerical coincidence the reader will misread |
| Case 1 tool calls M / B | §6.2 L207 (27.0 baseline), L213 (13.3 Mausoleo); §6.5 L244 (13.3 / 27.0); §6.5 L312-314 (13.3 / 27.0); §7.1 L457 not numeric for case 1 | CONSISTENT | CONSISTENT |
| Case 1 recall M / B | §6.2 L213 (0.67 / 0.67); §6.5 L246 (0.67 / 0.67); §6.5 L317-318 (0.67 / 0.67); §7.1 L457 (0.67 matched) | CONSISTENT | CONSISTENT |
| Case 1 quality M / B | §6.2 L213 (4.56 / 4.22); §6.5 L247 (4.56 / 4.22) | CONSISTENT | CONSISTENT |
| Case 2 tool calls M / B | §6.3 L219 (12.3 / 29.7); §6.5 L248 (12.3 / 29.7); §6.5 L326-327; §7.1 L455 (12.3 / 29.7); §8 L479 ("twelve... thirty") | CONSISTENT | CONSISTENT |
| Case 2 recall M / B | §6.3 L219 (0.76 / 0.62); §6.5 L250 (0.76 / 0.62); §6.5 L328-330 | CONSISTENT | CONSISTENT |
| Case 2 quality M / B | §6.3 L219 (4.83 / 4.44); §6.5 L251; §6.5 L331-332; §7.1 L455 (4.83 / 4.44) | CONSISTENT | CONSISTENT |
| Case 3 tool calls M / B | §6.4 L229 (8.3 / 28.3); §6.5 L252 (8.3 / 28.3); §6.5 L349-350; §7.1 L455 | CONSISTENT | CONSISTENT |
| Case 3 ratio MAE M / B | §6.4 L229 (0.149 / 0.194); §6.5 L254 (0.149 / 0.194); §6.5 L344-346; §7.1 L455 | CONSISTENT | CONSISTENT |
| Case 3 ratio RMSE M / B | §6.4 L229 (0.166 / 0.220); §6.5 L255 (0.166 / 0.220); §7.1 L455 (0.166 / 0.220) | CONSISTENT | CONSISTENT |
| Case 3 quality M / B | §6.4 L229 (4.06 / 3.17); §6.5 L256 (4.06 / 3.17) | CONSISTENT | CONSISTENT |
| Inter-judge κ | §6.2 L213 (case 1: 0.33); §6.3 L219 (case 2: 0.57); §6.4 L229 (case 3: 0.14); §6.5 L271-273 | 0.33 / 0.57 / 0.14 across both | CONSISTENT |
| Sign-test p-values | §6.2 L213 (case 1 quality p=0.625); §6.3 L219 (case 2 quality p=0.375, completeness p=0.250); §6.4 L229 (case 3 RMSE p=0.250, quality p=0.125); §6.5 L261-266 | identical | CONSISTENT |
| Embedding dimension | §5.1 L167 (1024-dim, BGE-M3); §6.5 L361 (384-dim, MiniLM) | **1024 vs 384** | **INCONSISTENT — CRITICAL (C1)** |
| Vector-index name | §3.2 L109 (usearch); §3.3 L119 (usearch); §5.1 L169 (usearch); §6.5 L414 (HNSW); §8 L479 (HNSW) | usearch vs HNSW | INCONSISTENT (C6) |
| Production-schema level count | §3.2 L109 (5 + 3 = 8 names listed); §5.2 L177 ("five of seven"); §7.3 L467 ("seven-level schema (… 8 names …)") | 5+3 / 5-of-7 / 7-listed-as-8 | INCONSISTENT (C5) |
| Word counts vs outline | abstract 280 (≤300 OK), preface 505 (≤500 +1%), §1 1019 (900 +13%), §2 1550 (1500 +3%), §3 1571 (1500 +5%), §4 1247 (1100 +13%), §5 1175 (1000 +18%), §6 3864 (2200 +76%), §7 1012 (900 +12%), §8 502 (500 ≈OK). Main body 11,940 vs 9000 target / 10,000 hard cap. | OVER hard cap by 1,940w | **INCONSISTENT — CRITICAL (C2)** |

---

## 3. Overall verdict

**FAIL.** Three CRITICAL issues block submission as-is:

1. **C1** — embedding-model contradiction (BGE-M3 1024-dim vs MiniLM 384-dim). One of the two sections is wrong about what is actually in the index, and the dissertation cannot afford an unforced contradiction at this level of specificity. The §6.5 statement is more recent and explicitly empirical ("smoke test: nearest day node to 'Mussolini' is 1943-07-26"), so it is more likely the truth and §3.2 / §5 should be revised to match.
2. **C2** — main body 11,940 words against the 10,000 hard cap. Driven primarily by §6.5 at +488% over its 300w outline budget, with redundant per-case mini-narratives that duplicate §6.2-§6.4 material.
3. The remaining HIGH issues (C3-C9) are individually fixable but compound: broken cross-references, an overclaimed abstract, a vocabulary drift on the central architectural term ("usearch" vs "HNSW"), and a §7.3 level-count error in the dissertation's load-bearing synthetic claim.

---

## 4. Specific edits

### CRITICAL

**C1 — embedding model and dimension**
- Decide ground truth: which encoder is actually loaded into ClickHouse? §6.5 L361 says MiniLM-L12-v2 384-dim and ran a passing smoke test at rerun time; this should be treated as authoritative.
- §3.2 L111: replace "Every summary is then embedded with BGE-M3 (Chen et al., 2024), a multilingual dense encoder chosen for its Italian coverage." with the MiniLM model name and a brief note on why (multilingual coverage at low dimension keeping ANN throughput high).
- §5.1 L167: replace "1024-dimensional embedding vector" with "384-dimensional embedding vector".
- §5.2 L177: replace "BGE-M3 (Chen et al., 2024), a multilingual dense model whose Italian coverage is competitive with monolingual baselines" with the corresponding MiniLM justification.
- §2.2 / Citation list: drop the BGE-M3 / Chen 2024 entry from §3 and §5 citation pools if it is no longer used. Add the MiniLM/sentence-transformers reference (Reimers & Gurevych 2019, "Sentence-BERT") in its place.
- Independent risk to check: if BGE-M3 is in fact what was used and §6.5 misreports, then §6.5 L361 + L433 must be flipped; either way both sides of the contradiction must be reconciled before any further reviewer round.

**C2 — word count over 10,000 hard cap**
- §6.5: cut to ≤700w. Concretely: delete the per-case mini-narratives at L309-355 entirely (they restate §6.2-§6.4 verbatim). Keep the aggregate table (L242-256), the sign-test list (L261-266), the inter-judge κ list (L271-273), the case-3 metric-substitution paragraph (L277-307), and the cost section (L383-423). Move "Embedding restoration", "Char-budget caveat", and "Methodology notes" into a single "Methodological notes" subsection (≤200w).
- §1, §4, §5, §7: trim ~10% each via tightening; specific candidates: §1 L41 second half ("Impresso is the most enriched..." → already covered in §2.1); §4.1 L137 mid-paragraph ("a fragment of the column-six fiction *Magnetizzata*..." example can be shortened); §5.2 L173 "the lineage is the recursive book summarisation of Wu et al. (2021)... and the hierarchical attention of Yang et al. (2016)..." can drop one of the two; §7.1 L455 can compress the per-case tool-call recap (it appears 3+ times across the draft already).
- Target: bring main body to ≤9,800w (1,500w margin under the hard cap as a safety floor for layout).

### HIGH

**C3 — §1 cross-ref to §3.3 should point to §3.2**
- §1 L47: change "the design that makes this possible is described in §3.3" to "the design that makes this possible is described in §3.2".

**C4 — §7.2 must deliver the limitations §6 promised**
- §7.2 L463: add one sentence on the judge-2 substitution — "The second LLM judge was Claude Sonnet 4.5 with an explicit 'judge 2' prompt rather than the GPT-5 the design called for, because no OpenAI key was sourced for this dissertation; the inter-judge κ values reported in §6.5 are therefore measured between two Anthropic models rather than across vendors, and the cross-vendor robustness of the comparison is untested."
- §7.2 L463: add one sentence on rubric-fit — "The three-dimension judge rubric (factual accuracy, comprehensiveness, insight) was designed for narrative completeness and fits the case-3 aggregate-shape answer poorly, which is reflected in the case-3 inter-judge κ of 0.14 (§6.5)."

**C5 — §7.3 level-count error**
- §7.3 L467: replace "seven-level schema (paragraph, article, day, week, month, year, decade, archive)" with either "eight-level schema" (consistent with the enumerated names) or drop one level name to make 7. Recommend: "seven-level production schema (article, day, week, month, year, decade, archive), with paragraph as the leaf substrate beneath article". This matches outline L96 ("year → decade → archive" for full archive scale, with paragraph as substrate).
- §3.2 L109 / §5.1 L167: harmonise to the same description ("the production schema extends from article through year, decade, archive; paragraph is the leaf").

**C6 — vector-index naming**
- Decide canonical term. ClickHouse 24.x supports both `usearch` (vector-similarity index type) and `HNSW`-style ANN; the relevant index type is in the DDL, which is `usearch` in the codebase. Standardise on "usearch (HNSW-backed) vector index" at first mention (§3.2 L109), then use "vector index" thereafter.
- §6.5 L414: replace "HNSW vector index" with "usearch vector index".
- §8 L479: replace "HNSW vector and FTS indices" with "usearch vector and `tokenbf_v1` FTS indices" or simply "vector and FTS indices".

**C7 — abstract overclaim on judges**
- Abstract L13: replace "is preferred by two LLM judges on a three-dimension rubric in every case" with "is preferred by the judge-mean rubric score in every case (case 1 mean 4.56 vs 4.22, case 2 4.83 vs 4.44, case 3 4.06 vs 3.17), with judge agreement varying across cases (κ = 0.33 / 0.57 / 0.14)." Or, if compactness is the priority: "is preferred by both LLM judges on average in every case."

**C8 — capability-gap framing**
- Abstract L13: change "while the BM25 baseline cannot return it" to "while the BM25 baseline can only reason about the absence from sibling-day articles, with no node in the index that grounds the missing day."
- §7.1 L457: change "The BM25 baseline cannot return anything; there are no articles to retrieve" to "The BM25 baseline returns no 26 July article and so cannot ground the absence in the corpus, although a knowledgeable agent can still reason about it from sibling-day evidence (§6.2)."
- §8 L479: change "exposed a definitional capability gap that flat retrieval cannot close at all" to "exposed a definitional capability gap: flat retrieval can reason around the absence but cannot ground it in a node that the index itself owns."

**C9 — §6.5 redundant mini-narratives**
- Delete §6.5 L309-355 (the per-case "Case 1 / Case 2 / Case 3" mini-narratives). They duplicate §6.2 / §6.3 / §6.4. The aggregate table + sign tests + κ list + case-3 metric-substitution + cost section carry the new material.

### MED (numbered C10-C17)

**C10 — outline drift on sub-pipeline count**
- No draft change needed; mark outline L91 stale ("6 sub-pipelines" → "8 sub-pipelines") so future reviewers do not flag the draft.

**C11 — column-split granularity inconsistency**
- §4.2 L143: replace "full-page, three-, four-, five-, six-column" with "full-page, two-, three-, four-, five-, six-column", matching §3.1 L99 and the §4.2 L145 stack-decomposition that names the column-two variant explicitly.

**C12 — self-consistency vs second-annotator conflation**
- §7.2 L463: separate the two limitations. "Relevance ground truth is single-annotator, and the planned 2-week intra-rater self-consistency check (§6.1) was not performed within the dissertation timeline; a second-annotator inter-rater agreement check is the obvious next step."

**C13 — wrong subsection cross-ref**
- §3.1 L101: change "§4.2 reports the ablation" to "§4.3 reports the ablation".

**C14 — definitional-vs-quantitative framing**
- §6.2 L213 closing: add one clause distinguishing the two — e.g. "The case is reported throughout as definitional rather than quantitative (the M:0.67 / B:0.67 recall tie is precisely the symptom that a recall-of-touched-articles metric is the wrong instrument here); the case-1 numbers are reported for completeness but the load-bearing finding is architectural."

**C15 — case-3 oracle self-reference**
- §6.1 L199: add one parenthetical when introducing the case-3 ratio metric — "(the oracle is itself produced by Sonnet 4.5; see §6.4 for the construction and its limitations)".

**C16 — "distinct random seeds" overclaim on Sonnet**
- §6.1 L197: replace "three trials per cell at distinct random seeds" with "three trials per cell at distinct seed prompts (Sonnet 4.5 is not deterministic by integer seed on the OAuth path; trial-to-trial variance is treated as part of the measurement)."

**C17 — 30 vs 30.5 min budget**
- §3.1 L97 → L103 → §4.2 L143: add one transitional sentence at §3.1 L103 — "The 30-minute target is the design budget; the empirical wall on the harder issue runs ~30.5 minutes on the slower GPU chain (§4.2)." This makes the numbers cohere on first read.

### LOW (no action required, recorded for completeness)

- C18 — Preface 505w vs ≤500: trim 5 words.
- C19 — Per-section overshoots: addressed by C2.
- C20 — "BIECO FUREORE" → "BIECO FURORE": typo fix in §6.3 L217.
- C22 — *Magnetizzata* example never recurs: stylistic only.
- C23 — §5.3 spot-check denominators: no action.

---

## 5. Intro–conclusion fit verdict

**MEDIUM.** §1 promises four things: (a) a five-level chronological tree over July 1943 *Il Messaggero*, (b) three case studies against a BM25 baseline measuring efficiency / completeness / quality, (c) the missing 26 July as the lead and definitional capability gap, (d) a synthetic claim that multi-resolution time + provenance is the right scaffold and that Mausoleo is one form of it.

§8 lands all four:
- (a) "a deterministic OCR ensemble feeding a chronologically organised index of article, day, week, and month summaries" — covered.
- (b) "evaluated against a BM25 baseline on the same corpus across three case studies" — covered.
- (c) "The missing 1943-07-26, treated by the index as a first-class node whose summary contextualises the absence, exposed a definitional capability gap" — covered.
- (d) "The synthesis defended in §7.3 is that these two literatures converge on the same prescription. An interface to a historical archive is well-designed only insofar as it honours both commitments" — covered.

What pulls the fit down from STRONG to MEDIUM:
- §1 promises §6.2 to handle the missing 26 July, and §6.2 does deliver — but §1 also says (L47) "described in §3.3", which is wrong (should be §3.2). C3.
- §1 frames case 1 as "definitional rather than quantitative", §6.2 reports full quantitative comparison, and §8 inherits the §1 framing rather than the §6 evidence. The conclusion lands the synthesis but slightly mis-cites the case-1 evidence base it rests on. C14 + C8.
- §8's "future work" paragraph (L483) introduces multi-archive support, community corrections, and generic-corpus extension — none of these are in §1's promise but they do not contradict it. Net neutral.

If C3, C7, C8, C14 are fixed, intro-conclusion fit moves from MEDIUM to STRONG.

---

## 6. Submission readiness

**No, not as-is.** Named blockers, in order:
1. C1 (embedding-model contradiction) — must be reconciled before any further reviewer round.
2. C2 (word count over 10,000 hard cap) — must be cut by ~2,000 words; §6.5 is the obvious surgical site.
3. C3, C4, C5 (cross-references and level-count) — five-minute fixes that should ship together.
4. C6 (usearch / HNSW naming) — fifteen-minute fix.
5. C7, C8 (abstract / §7.1 / §8 overclaim) — wording-only edits that materially affect what a marker reads in the abstract.

Once 1-5 are addressed, the draft is structurally sound and the §6 evidence does land the §7.3 synthetic claim.
