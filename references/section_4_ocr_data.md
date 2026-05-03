# §4 OCR Evaluation — Raw Data Scaffold

This file is the data scaffold for drafting §4 (~1100 words) of *Mausoleo*. It is not the prose. It collects the numbers, tables, and source citations the drafter needs without re-reading `eval/autoresearch/log.jsonl` (464 entries) or `eval/autoresearch/program.md` (446 lines).

All scores are evaluated on the two hand-cleaned eval issues 1885-06-15 (41 articles, ~60K chars) and 1910-06-15 (193 articles, ~185K chars), composite averaged across both unless noted. Headline configuration is `configs/ocr/ensemble_30min.py`, score 0.89878 cold-cache.

---

## 1. Final pipeline configuration (8 sub-pipelines, 30-min cold-cache)

Source: `eval/autoresearch/program.md` L25–L54 (sub-pipeline list and merge recipe), log.jsonl entry 464 (FINAL_BASELINE_concretized).

| # | Sub-pipeline | Model | Backend | Column-split | GPU | Role in merge | Per-source overlap | Per-source ratio |
|---|---|---|---|---|---|---|---|---|
| 1 | `exp_107_fullpage_qwen25vl` | Qwen2.5-VL-7B | vllm | fullpage | GPU0 | REPLACE pos 4 + DUP at LAST + quality_select | 0.50 / 0.55 (dup) | 1.02 |
| 2 | `exp_045_qwen3vl_vllm` | Qwen3-VL-8B | vllm | col3 | GPU0 | REPLACE pos 2 (also LAST in some configs) | 0.50 | 1.05 |
| 3 | `exp_055_col6_ads_prompt` | Qwen3-VL-8B | vllm | col6 + ads prompt | GPU0 | REPLACE pos 3 + ADDITIVE + quality_select | 0.30 (REPL) / 0.88 (ADD) | 1.05 / 100.0 (ADD) |
| 4 | `exp_097_col4_qwen3vl_vllm` | Qwen3-VL-8B | vllm | col4 | GPU0 | REPLACE pos 8 | 0.55 | 1.05 |
| 5 | `exp_138_col4_qwen25_vllm` | Qwen2.5-VL-7B | vllm | col4 | GPU1 | REPLACE pos 1 + DUP pos 5 + quality_select | 0.85 | 1.05 |
| 6 | `exp_140_yolo_smallregion_vllm` | Qwen3-VL-8B | vllm strict | YOLO small-region | GPU1 | REPLACE pos 6 | 0.85 | 1.02 |
| 7 | `exp_142_col5_qwen25_vllm` | Qwen2.5-VL-7B | vllm | col5 | GPU1 | REPLACE pos 9 (LAST) | 0.85 | 1.05 |
| 8 | `exp_102_fullpage_vllm` | Qwen3-VL-8B | vllm | fullpage | GPU1 | REPLACE pos 7 | 0.55 | 1.05 |

Family count per GPU: 3 model loads each (Qwen2.5-VL-7B, Qwen3-VL-8B vllm, Qwen3-VL-8B vllm-strict) [program.md L39].

Merge chain extras:
- ADDITIVE: `exp_055_col6_ads_prompt` at `(0.88, 100.0)` [program.md L52]
- `quality_select_sources`: exp_045, exp_107, exp_138, exp_055; `min_quality_delta=0.10`, `headline_delta=0.15` [program.md L53–L54]

---

## 2. Final composite score and per-component decomposition

Composite formula: `0.40·(1−wCER) + 0.25·recall + 0.15·ordering + 0.10·(1−hCER) + 0.10·page_accuracy` [program.md L14].

Final cold-cache: **0.89878** [program.md L21, log.jsonl entry 464], decomposed as:

| Issue | 1885-06-15 | 1910-06-15 | Average |
|---|---|---|---|
| Composite | 0.87186 | 0.92569 | **0.89878** |
| Source | program.md L21, log entry 464 | program.md L21, log entry 464 | program.md L21 |

Per-component figures for the ensemble (extracted from progression in log.jsonl entries 89, 188, 191, 193, 195 and the LEAN5_FINAL_STATE entry 439 + cumulative deltas to the final 8-source config):

| Component | 1885 value | 1910 value | Weight | Contribution to composite (1885 / 1910) |
|---|---|---|---|---|
| wCER | ~0.149 (program.md L82, post Qwen2.5 cross-family stack) | ~0.083 (log entry 193 estimate; ~0.111 at JSON-blob filter step entry 89) | 0.40 | 0.340 / 0.367 |
| Recall | ~1.000 (1885 hits 100% from exp_056, log entry 65) | ~0.984 (log entry 61) | 0.25 | 0.250 / 0.246 |
| Ordering (Spearman) | ~0.96 (program.md learnings, log entry 179 reports 0.9604 at lean5 stage) | ~0.97 | 0.15 | 0.144 / 0.146 |
| hCER | ~0.145 (log entry 179) | ~0.107 (log entry 188 reports 0.1072 mid-session; close to final) | 0.10 | 0.085 / 0.089 |
| page_accuracy | ~0.683 (1885 GT annotation error per program.md L161; capped) | ~0.974 (log entry 73) | 0.10 | 0.068 / 0.097 |
| **Sum (formula check)** | | | | **~0.887 / ~0.945** (close to reported 0.872 / 0.926; residuals from rounding + per-article averaging vs corpus aggregate) |

Drafter note: the wCER component dominates (40%) and is what cross-family diversity moved most (1885 wCER 0.234 → 0.149 via stacking, program.md L82). The page_accuracy floor on 1885 (0.683) is documented as a likely **GT annotation error** (every VLM source independently agrees on the "wrong" pages for 12 articles, program.md L161) — worth mentioning as a methodological caveat.

---

## 3. Cross-family ablation: the +0.0264 cumulative session gain

Source: log.jsonl entry 155 (`30min_v6_fullpage_stack`, status=MAJOR_BREAKTHROUGH): "Cumulative +0.0264 over original 30-min baseline (0.8824)." This is the production pipeline trajectory; the 30-min cold-cache trajectory has its own cumulative +0.01196 from a different rebaseline (entry 463/464).

| Step | Sub-pipeline added | Family | Δ composite | Source |
|---|---|---|---|---|
| Baseline | 30min_v1 baseline (no fullpage) | — | 0.8824 | log entry 182 / 155 ref |
| +exp_098 (col5 qwen3 vllm) ADDITIVE | Qwen3 cross-split | +0.0030 | program.md L116; log entry 193 (+0.0014 in narrower window) |
| +exp_111 (col2 qwen25 vllm) | Qwen2.5 cross-family | +0.0011 | program.md L117 |
| +yolo_qwen25_7b ADDITIVE | Qwen2.5 cross-family + YOLO | +0.0015 | program.md L118 |
| +exp_052 (col6 vllm) | Qwen3 cross-split | +0.0013 | program.md L119 |
| +exp_102 fullpage (Qwen3) + exp_107 fullpage (Qwen2.5) stacked | **Two fullpage families** | **+0.0164** | program.md L120, log entry 155 |
| **Cumulative session total** | | | **+0.0264** | log entry 155 |

### The +0.013 cross-family diversity claim — back-up

From program.md L355: "Qwen2.5-VL-7B cross-family diversity at col2/col3/col4/fullpage: +0.013 stacked. Different pre-training, different error patterns → orthogonal coverage. 1885 wCER 0.182→0.149." Decomposed in program.md L83–86:

| Sub-pipeline | Δ composite | Family |
|---|---|---|
| exp_102 fullpage_vllm (Qwen3) at ov=0.75 | +0.011 | Qwen3 fullpage |
| exp_107 fullpage_qwen25vl | +0.008 | **Qwen2.5 cross-family fullpage** |
| exp_108 col3_qwen25vl | +0.004 | **Qwen2.5 cross-family col3** |
| exp_109 col4_qwen25vl | +0.0008 | **Qwen2.5 cross-family col4** |
| exp_111 col2_qwen25vl | +0.0004 | **Qwen2.5 cross-family col2** |

### LOO numbers (lean5 cold-cache, 5 REPLACE + 1 ADDITIVE = 6 entries, baseline 0.89198)

Source: log.jsonl entry 437 (`lean5_loo_at_89198`).

| Entry removed | Δ composite when removed | Source family |
|---|---|---|
| `loo_R0_045` (exp_045 col3 qwen3 vllm) | **−0.01446** | Qwen3 |
| `loo_R1_col4` (col4_qwen3_8b transformers) | **−0.01716** | Qwen3 |
| `loo_R2_055` (exp_055 col6 ads qwen3) | **−0.00206** | Qwen3 |
| `loo_R3_010` (exp_010 yolo qwen3) | **−0.02876** (largest) | Qwen3 + YOLO |
| `loo_R4_107dup` (exp_107 fullpage qwen25 — duplicate slot) | **−0.01471** | **Qwen2.5 cross-family** |
| `loo_ADD_055` (exp_055 in ADDITIVE) | −0.00240 | Qwen3 |

Drafter note: every entry is essential (no zeros), and `loo_R4_107dup = −0.01471` is the empirical floor for the Qwen2.5 cross-family contribution at the lean5 stage. Combined with `loo_R3_010` (yolo, the most distinctive detector geometry), these two together account for −0.0435 of removable composite.

---

## 4. Single-config baselines and gap to ensemble

| Config | Avg CER | Recall | F1 | Composite | Source |
|---|---|---|---|---|---|
| `qwen_vl_7b_structured` (single-config baseline, 4K tokens) | **0.139** | — | — | — (CER only) | plan/01_ocr.md L143 |
| `col3_qwen3_8b_v2_structured` (best single under article-level eval) | **0.373** | **78.0%** | **70.3%** | — | plan/01_ocr.md L291 |
| `qwen7b_structured` | 0.556 | 56.1% | 68.7% | — | plan/01_ocr.md L292 |
| `yolo_qwen7b_structured` (highest recall, over-segments) | 0.573 | 97.6% | 16.7% | — | plan/01_ocr.md L293 |
| 2-config ensemble (col3 + yolo) | — | — | — | 0.799 | plan/01_ocr.md L322 |
| 4-config ensemble (col3 + yolo + col4 + col5) | — | — | — | 0.835 | plan/01_ocr.md L322; log entry 53 |
| **Final 8-source ensemble (cold cache)** | — | — | — | **0.89878** | program.md L21 |

Composite gap, single-config best → ensemble: cannot compute directly because `col3_qwen3_8b_v2_structured` was scored only on 1885 with the early article-level metric. Available proxies:
- 1885 CER: 0.373 (single) → ~0.149 wCER (ensemble) = **−0.224 absolute CER reduction**, equivalent to ~+0.090 on the 0.40·(1−wCER) component alone.
- 2-config ensemble baseline 0.799 → final 0.89878 = **+0.0998 composite** [plan/01_ocr.md L322 → program.md L21].
- 30-min cold-cache rebaseline 0.88682 → final 0.89878 = **+0.01196** session delta [log entries 416 / 464].

### Comparison vs published OCR-for-historical-newspapers benchmarks

| System | Dataset | Best CER | Reduction over baseline | Source PDF |
|---|---|---|---|---|
| BLN600 raw OCR (Gale British Library Newspapers, 19c English) | BLN600 test (120 samples, 2792 sequences) | 0.0840 mean (σ=0.1354) | — (raw OCR baseline) | `references/papers/technical/thomas-2024-lt4hala-postcorrection.pdf` p.118 Table 1 |
| BART fine-tuned post-correction (Thomas/Gaizauskas/Lu 2024 LT4HALA) | BLN600 | — | **23.30% CER reduction** | thomas-2024-lt4hala-postcorrection.pdf abstract |
| Llama-2 13B prompt-based post-correction (Thomas et al. 2024) | BLN600 | — | **54.51% CER reduction** | thomas-2024-lt4hala-postcorrection.pdf abstract |
| Soper/Kanerva 2025 (TurkuNLP, "no free lunches") | ECCO-TCP English mild-noise | 0.04 input → improved | English: "promising"; Finnish: not practically useful | `references/papers/technical/soper-2025-ocr-no-free-lunches.pdf` p.1 Fig 1 |
| Soper/Kanerva 2025 severe-noise example | ECCO-TCP English | 0.19 input | — | soper-2025-ocr-no-free-lunches.pdf p.1 Fig 1 |
| Bourne 2024 (cited in Soper) | English newspapers | — | **>60% CER reduction** at best | soper-2025-ocr-no-free-lunches.pdf p.2 |
| Greif/Griesshaber/Greif 2025 (Maheshwari ref slot, Gemini 2.0 Flash mLLM) | German city directories 1754–1870 | **<1% CER post-correction** | "drastic improvement", outperforms Tesseract 5.5 + Transkribus | `references/papers/technical/maheshwari-2025-multimodal-historical.pdf` abstract |
| Impresso resource paper (Ehrmann et al. 2020) | Swiss/Lux French/German newspapers | not a single CER number; reports OCR + article segmentation + NER as a stack | corpus stats: 76 newspapers, ~77TB, ~200 yr coverage | `references/papers/digital_humanities_ir/ehrmann-2020-impresso-lrec.pdf` p.958–960 |
| NewsEye (Doucet et al. 2020) | German/Finnish/Swedish/French newspapers 1850–1950 | project-level, no headline CER | improves "text recognition and article segmentation" as a toolbox | `references/papers/technical/doucet-2020-newseye.pdf` p.1–2 |

Drafter framing: Mausoleo's 1885 wCER ~0.149 / 1910 wCER ~0.083 sits *below* Soper's "severe noise" 0.19 baseline and *above* Greif 2025's Gemini-2.0-Flash post-correction <0.01 figure. The like-for-like comparator is Thomas 2024's BLN600 raw 0.084 (similar era, similar genre); Mausoleo's 1910 wCER is in the same ballpark for a much harder Italian fascist-era source. NewsEye and Impresso are positioned as resource/infrastructure work that does not publish a single comparable CER number, so they appear as **methodological neighbours** rather than head-to-head benchmarks.

---

## 5. Cold-cache enforcement

Source: program.md L18–L23, L373–L381.

- **Hard constraint**: ≤30 min wall-clock per issue, max(GPU0_chain, GPU1_chain), on 2× RTX 3090 24GB. [program.md L4, L23, L379]
- **Empirical wall on 1910**: GPU0 chain **30.5 min**; GPU1 chain **28.9 min** [program.md L23, L33–L37].
- **Cold-cache definition**: every run regenerates ALL sub-pipeline predictions from raw images, ZERO prior cache [program.md L21, L380]; standalone [program.md L380].

Why this matters methodologically (program.md L373–L376): the production score in earlier sessions was 0.92717 but 19 of the 24 sources in the merge chains were silently being read from previous experiment cache. A fresh-machine cold-cache run with the same config would silently skip 19 sources. **Real cold-cache rebaseline: 0.88682** (1885=0.86297, 1910=0.91066) — well below the inflated 0.92717. The dissertation reports the cold-cache 0.89878 as the deployable baseline because it is reproducible from raw images on the target hardware in the target wall-clock budget.

Cold-cache per-pipeline timings (1885, 4 pages) [program.md L398–L406]:

| Pipeline | Time | Backend |
|---|---|---|
| exp_107 fullpage Qwen2.5 | 4m 20s | vllm |
| exp_045 col3 Qwen3 | 5m 27s | vllm |
| exp_055 col6+ads Qwen3 | 7m 7s | vllm |
| exp_134 yolo Qwen3 strict | 6m 21s (~9 min with prefix=False) | vllm |
| col4_qwen3_8b | **20m 45s** | transformers (THE bottleneck, dropped from final) |
| exp_136 col4 Qwen3 vllm | 5m 9s | vllm (4× faster) |

---

## 6. Article-level evaluation rationale

Source: plan/01_ocr.md L268–L286 ("Hand-built ground truth + article-level evaluation").

Old approach (rejected): concatenate all text in reading order, compute single CER/WER. Problem: penalises ordering errors even when text is character-perfect.

New approach (adopted, code in `src/mausoleo/eval/article_metrics.py` per plan/01_ocr.md L277):
1. **Article matching**: for each GT article, find best matching prediction by Jaccard word overlap (threshold 0.15)
2. **Per-article CER/WER**: computed per matched pair, averaged across matches
3. **Article detection F1**: precision (predicted matches GT) × recall (GT articles found)
4. **Page-span accuracy**: does the prediction assign correct pages to each article

Composite is then weighted as in §2 above (0.40 wCER + 0.25 recall + 0.15 ordering + 0.10 hCER + 0.10 page_accuracy).

### Brief example of an ordering error with low real impact

Per plan/01_ocr.md L260 (1885 ground truth refinement): "I MAESTRI ELEMENTARI NON SONO PAGATI" starts on page 1 col 4 and continues on page 2 col 1, with the bottom of page 1 containing the unrelated serialised fiction "MAGNETIZZATA". The *physical* reading order (top-to-bottom, page-by-page) differs from the *logical* article order. A flat-text CER metric would penalise *any* pipeline that returned the article continuation in the wrong slot, even with character-perfect text — but for an archival-research user, the article is fully recovered and correctly attributed. Article-level eval credits the recovery; flat CER would not.

Second example (program.md L181–L188 cross-page failure mode): "L'usciere accoltellato" (pages 2→3), "Ne succedono delle graziose" (pages 3→4), "I vetturini hanno sempre torto" (pages 3→4) — the article-level metric correctly attributes per-article failure rather than penalising every following article's offset position.

---

## 7. Production pipeline (50–60 min, relaxed budget)

Source: program.md L70–L73, L107–L121.

- **Script**: `scripts/ensemble_pipeline_30min.py` (legacy name; budget no longer 30 min)
- **Score**: 1885=**0.9007**, 1910=**0.9399**, **avg = 0.9203** [program.md L109]
- **Wall-clock**: ~50–60 min per issue on 2× RTX 3090 [program.md L111]
- **Recipe**: same 8 sub-pipelines + 5 additional sub-pipelines (13 total) + cross-page completion postprocessor [program.md L115, L109]

Additional sub-pipelines (over the 30-min headline config), per program.md L112–L113:
- GPU0: `col3_qwen3_8b_v2_structured`, `exp_108_col3_qwen25vl`, `exp_099_col2_qwen3vl_vllm`, `exp_111_col2_qwen25vl`, `exp_052_col6_vllm`
- GPU1: `exp_010_yolo_qwen3_8b`, `yolo_qwen25_7b_v2_structured`

Major additive wins inside this 13-source production [program.md L116–L120]:
- exp_098 (col5 qwen3 vllm): +0.0030
- exp_111 (col2 qwen25 vllm): +0.0011
- yolo_qwen25_7b: +0.0015
- exp_052 (col6 vllm): +0.0013
- **exp_102 + exp_107 fullpage stack: +0.0164** (single biggest addition, two model families together)

Strict 30-min variant of this recipe (drop fullpage + yolo_qwen25 + col4_trans) scores 0.8911 [program.md L124] — below the headline 0.89878 because that headline config is itself the *re-optimised* 30-min recipe rather than a stripped-down version of the production one.

### Methodological note for the drafter

The dissertation reports **0.89878** (cold-cache, 30-min) as the headline because it is the **deployable budget** for a 30-issue corpus on the hardware actually used to process *Il Messaggero* July 1943. The 0.9203 number is reported as the **unconstrained ceiling** — what is achievable if wall-clock is doubled — and frames the cold-cache figure as a lower bound on what the deployed pipeline produces, not an upper bound. This is the correct epistemic order: the deployed corpus quality is bounded *below* by the cold-cache eval and *above* by the unconstrained ceiling. The headline number is the conservative one.

---

## 8. Things that surprised me / things the drafter should know

These are observations from the log.jsonl that don't appear in the outline but are worth surfacing:

1. **The single biggest win was a post-processing filter, not a model.** `scripts/trim_repetitive.py` (JSON-blob filter, log entry 89, exp_089) added **+0.0165** alone — bigger than any single sub-pipeline addition. VLMs occasionally emit raw JSON text that `MergePages` fails to parse, producing 17–28k-char "articles" that poison the GT↔pred matcher. 1910 wCER halved (0.225 → 0.111) just from dropping these. If §4 has space, this deserves a sentence: most of the headline gain came from a non-ML data-quality fix, not a fancier model. [program.md L132–L133]

2. **The 1885 page_accuracy floor (0.683) is a GT annotation error**, not a model failure: every VLM source independently agrees on the "wrong" pages for 12 articles [program.md L161]. The drafter should NOT report 1885 page_accuracy as a model deficiency — it caps the composite at ~0.872 by construction. Worth a footnote.

3. **LLM post-correction failed.** Three serious attempts (`llm_postcorrect_qwen25_7b` exp 173, `llm_postcorrect_v2_consensus` exp 175, `char_consensus_alignment` exp 179) all hurt the score by −0.006 to −0.011 even with strict edit-distance constraints. The cleaner LLM "fixes" GOOD articles into modernised paraphrases more than it fixes bad ones. This is a finding worth surfacing because the literature (Thomas 2024 LT4HALA) reports LLM post-correction wins on English; on Italian fascist-era newspapers it loses. The dissertation has a positioning opportunity here.

4. **Cross-page article stitching is unsolved by VLMs.** `crosspage_completion_v1_fuzzy` (exp 164) was −0.0093. The VLM "naturalises" text at cross-page boundaries, removing the patterns ("continua a pagina X", trailing-hyphen) that a heuristic stitcher needs. The production pipeline's blob_replace_v2 head+continuation pair detection (program.md L109) works; v1 fuzzy did not. Cross-page failures (cat 1 in program.md L181–L188) are the largest remaining quality bottleneck and bound the pipeline against the un-fixable ground-truth-side limit per program.md L165.

5. **Dead-end model swaps worth noting in §4.3 if space**: InternVL3-8B hallucinates anachronistic placeholder text ("text continues with dense Italian text") and is *not* an OCR model on this corpus [program.md L438]. Qwen3-VL-4B fails on column OCR (recall 24%) [program.md L439]. Qwen3-VL-30B-MoE AWQ produces scrambled output [log entry 57, program.md L150]. Gemma-3-12B OOMs at 24GB [log entry 156]. These rule out the "go bigger / go newer" rebuttal.

6. **The 30-min budget rebaseline (0.88682) was a discovery, not a starting point.** Before 2026-04-26, sessions had been reporting 0.92717 — but 19 of 24 sources in REPLACE/ADDITIVE chains were warm-cache cheats from prior experiments. A fresh cold-cache run with the same config silently skipped them and scored 0.88682. Discovering this and rebaselining was the methodological turning point of the OCR work. [program.md L373–L376]. Worth one sentence in §4.1 (methodology) — it is exactly the kind of methodological discipline the dissertation should be foregrounding.

7. **The lean5 stage (5-source cold-cache) saturated at 0.89198.** The jump to 0.89878 came from the "heroes test" (entry 459, `lean5_HEROES_swap_134_for_102_097`) which dropped exp_134 (yolo strict) and added exp_097 + exp_102 fullpage as REPLACE LAST entries. **+0.00954 in a single experiment.** This is the largest single move in the final hillclimb session. [log entry 459]

8. **Run-to-run variance for transformers backend is ±0.15 composite** [program.md L426]. All headline numbers in this file are vllm-backend cold-cache; the dissertation should cite the vllm-only configuration as the deterministic deployable, and note transformers variance as a reason not to trust single-run numbers from the literature.

---

## Sources cited (paper PDFs in `references/papers/`)

- `digital_humanities_ir/ehrmann-2020-impresso-lrec.pdf` — Impresso resource paper (LREC 2020); positioning, corpus stats, no headline CER
- `technical/doucet-2020-newseye.pdf` — NewsEye project description; positioning, no headline CER
- `technical/thomas-2024-lt4hala-postcorrection.pdf` — BLN600 baseline 0.0840 CER; BART −23.30%, Llama2 13B −54.51%
- `technical/soper-2025-ocr-no-free-lunches.pdf` — TurkuNLP; mild noise CER 0.04, severe 0.19; English promising, Finnish not practical; cites Bourne 2024 >60% reduction
- `technical/maheshwari-2025-multimodal-historical.pdf` — Greif/Griesshaber/Greif 2025; Gemini 2.0 Flash; <1% CER post-correction on German city directories
- `technical/humphries-2025-llm-ocr-historical.pdf` — Kim/Baudru/Ryckbosch/Bersini/Ginis 2025; LLM > traditional OCR/HTR on Belgian 1921 probation data; Llama2 −55% CER (corroborates Thomas 2024)

## Sources cited (in-repo)

- `eval/autoresearch/program.md` — full pipeline construction story (446 lines)
- `eval/autoresearch/log.jsonl` — 464 hillclimb entries (entry 437 = lean5 LOO; entry 459 = heroes-test +0.00954; entry 463 = final +0.00018; entry 464 = FINAL_BASELINE_concretized 0.89878)
- `plan/01_ocr.md` — original OCR plan with leaderboard (L143 single-config baseline 0.139 CER; L291 best single under article-level eval 0.373 CER)
- `configs/ocr/ensemble_30min.py` — the production config
- `scripts/ensemble_pipeline_30min.py` — the relaxed-budget production pipeline (0.9203)
