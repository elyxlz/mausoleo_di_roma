# §6.5 Absolute-cost data

Backing numbers for the §6.5 cost subsection and the §7.2 index-build limitation.
Authoritative sources are cited inline (RUNLOG entries, file paths, ClickHouse
queries). All LLM cost figures are token-rate proxies (no API spend; calls bill
against the Claude Max OAuth subscription quota); this is flagged
explicitly throughout — see "phantom-USD caveat" below. This file reports
**absolute costs only**; the dissertation deliberately does not use a
break-even or amortisation framing because Mausoleo is an unmonetised research
project, not a commercial service.

> **Phantom-USD caveat.** Phase 1 (`eval/summaries/run_report.json` and `_logs/run.log`)
> and the first Phase 2 run (`eval/case_studies/RUNLOG.md`, lines 1-30) both report
> a `total_cost_usd` derived from list per-token rates for Haiku 4.5 and Sonnet 4.5.
> No money was spent: the OAuth subscription path was used end-to-end. The dollar
> figure is therefore a *token-rate proxy* useful for cross-system comparison
> (Mausoleo build vs. baseline per query, Anthropic-vs-Anthropic), but it is not
> a subscription bill. Token counts are the durable unit; the dollar figures are
> retained because Phase 1 did not log per-call token totals — only the
> per-call cost the harness computed from the token counts before discarding them.

## 1. OCR compute (one-time, Phase 0)

Source: `eval/autoresearch/program.md` (final-baseline section, L18-L23) for
per-issue wall times; `eval/predictions/ensemble_30min_1943-07-*.json` for the
production-run output count.

The production OCR pipeline is `configs/ocr/ensemble_30min.py` — one
`OcrPipelineConfig` running the `ParallelEnsembleOcr` operator over 8
deterministic sub-pipelines (4 per GPU, two RTX 3090 24 GB cards). Per-issue
wall-clock on the 1910 reference issue: **GPU0 30.5 min, GPU1 28.9 min**;
end-to-end wall is bounded by the slower chain at **~30.5 min/issue**, while
aggregate GPU-time is **30.5 + 28.9 = 59.4 GPU-min ≈ 0.99 GPU-hours/issue**.

| Item | Value | Source |
|---|---|---|
| Hardware | 2× RTX 3090 24 GB | `program.md` L23 |
| Sub-pipelines / issue | 8 (4 GPU0 + 4 GPU1) | `program.md` L25-37 |
| Per-issue wall-clock (max of two GPU chains) | ~30.5 min | `program.md` L23 |
| Per-issue aggregate GPU-time | 0.99 GPU-hours | derived (GPU0 30.5 + GPU1 28.9 min) |
| July 1943 issues processed | **30** (07-01 to 07-31, 07-26 absent in source) | `eval/predictions/ensemble_30min_1943-07-*.json` |
| **Production run total wall-clock** | **~15.3 hours** (30 × 30.5 min) | derived |
| **Production run total GPU-hours** | **~29.7 GPU-hours** (30 × 0.99) | derived |
| Backend | vllm preferred; transformers fallback for unsupported models | `program.md` |
| Determinism | full pipeline reproducible from raw images, zero-cache | `program.md` L21 |

**Caveat on extrapolation.** The 30.5 min/28.9 min split was measured on the
1910 reference issue (193 articles, 185 k chars). July 1943 issues vary in
page count and article density; the 30.5 min/issue figure is treated as a
conservative upper bound under the hard 30-min/issue constraint the pipeline
was tuned to. Per-issue 1943 wall times were not captured at production-run
time (no per-issue timing log was retained), so the total-GPU-hours figure
is an honest extrapolation from the eval-issue calibration, not a direct
measurement.

### 1.1 Linear-scaling extrapolation

The OCR cost scales linearly with issue count (each issue is processed
independently, no cross-issue work). For corpus scale-ups:

| Scale | Issues | Total wall (single 2-GPU host) | Total GPU-hours |
|---|---|---|---|
| One month (July 1943, measured) | 30 | ~15.3 h | **~29.7** |
| Six years (×72 months) | ~2,160 | ~46 days | ~2,140 |
| Sixty years (full *Il Messaggero* run) | ~21,600 | ~457 days | **~21,400** |

The 60-year scale-up is reported as a substantial-but-tractable cost:
21,400 GPU-hours on 2× RTX 3090 is ~14 months of single-host wall-time,
or ~14 days on a 30× parallel cluster. It is not commercial-cost prohibitive
(rented A100/H100 pricing puts the equivalent at low five figures USD), but
the dissertation does not pursue that framing; the figure is reported as
absolute compute only.

## 2. Phase 1 — LLM index build (one-time)

Source: `eval/summaries/run_report.json`, `eval/summaries/_logs/run.log`,
`eval/summaries/manifest.json`.

| Item | Value | Source |
|---|---|---|
| Articles summarised | 6,480 | `manifest.json` `levels.article` |
| Day nodes | 31 (incl. 1943-07-26 absent) | `manifest.json` `levels.day` |
| Week nodes | 5 (W26-tail … W30) | `manifest.json` `levels.week` |
| Month nodes | 1 (1943-07) | `manifest.json` `levels.month` |
| **Total summary nodes** | **6,517** | sum of above |
| Article-phase model | `claude-haiku-4-5` (OAuth) | `run_report.json` `llm_models` |
| Day/week/month model | `claude-sonnet-4-5` (OAuth) | `run_report.json` `llm_models` |
| Embedding model | `paraphrase-multilingual-MiniLM-L12-v2`, dim=384 (CPU local; BGE-M3 deferred) | `run_report.json` |
| **Article phase cost (Haiku, phantom-USD)** | **$19.212** | `_logs/run.log` line 266 |
| **Day phase cost (Sonnet, phantom-USD)** | **$9.483** | $28.695 (line 268) − $19.212 |
| **Week + Month phase cost (Sonnet, phantom-USD)** | **$0.175** | `_logs/run.log` line 329 |
| **Embedding cost (API)** | **$0.00** (local sentence-transformers, GPU/CPU only) | `run_report.json` |
| **TOTAL phantom-USD index-build** | **$28.87** | `run_report.json` `total_cost_usd` |
| Wall time, last clean run (load → embed) | 367.9 s (6.13 min) | `run_report.json` `elapsed_sec` |
| Wall time, first build (Haiku article phase only, observed steady-state ~2.4 calls/s on 6,480 articles, conc=12) | ~45 min | `_logs/run.log` lines 4-265 |
| Wall time end-to-end (article + day + week + month + embed, including the two restart cycles documented in `notes`) | ~2 h 20 min | `run_report.json` `notes`; consistent with the dreamer's Phase 1 close-out |
| LLM-call count | not logged per-call in this run; one call per node ⇒ 6,480 + 31 + 5 + 1 = 6,517 calls | derived |
| Token totals | **not captured** in Phase 1 (harness logged dollars from rate × tokens, then discarded the token counts). Phase 2 captures tokens directly. | gap, flagged below |

### 2.1 Per-summary average cost

Average over the 6,517 summary nodes:

| Level | N nodes | Phantom-USD | $/node | Notes |
|---|---|---|---|---|
| Article (Haiku 4.5) | 6,480 | $19.212 | **$0.00296 / article** | one OCR'd day-page article in, one ~150-word summary out |
| Day (Sonnet 4.5) | 31 | $9.483 | **$0.306 / day** | all article summaries for one issue concatenated as input; ~300-word summary out |
| Week (Sonnet 4.5) | 5 | ~$0.143 | **~$0.029 / week** | week+month bundled at $0.175; split linearly here |
| Month (Sonnet 4.5) | 1 | ~$0.032 | **~$0.032 / month** | one summary input; ~600 words out |
| Embedding | 6,517 | $0.00 | $0.00 / node | local model, ~10-15 ms/node CPU on the build host |

Token estimates (from list rates, reverse-engineered, approximate):
- Article-phase Haiku 4.5 at $1/M input, $5/M output ⇒ ~$0.003/article ≈
  ~2.5 k input + ~150 output tokens per article.
- Day-phase Sonnet 4.5 at $3/M input, $15/M output ⇒ ~$0.31/day ≈
  ~80 k input + ~600 output tokens per day (input dominated by the
  concatenated article summaries for one issue).

These reverse-engineered token figures are not authoritative; they are
included for §6.5 prose so the dissertation can quote a unit. The authoritative
record is `run_report.json` (cost) and `manifest.json` (node counts).

## 3. Phase 2 — case-study per-query cost (recurring at the per-query rate)

Source: `eval/case_studies/RUNLOG.md` "Rerun 2026-05-03" block (lines 112-151)
and "Final summary" (lines 154-165). Token counts are direct from the OAuth
endpoint usage stream.

| Item | Mausoleo | Baseline (BM25 + raw articles) |
|---|---|---|
| Trials run | 9 (3 cases × 3 trials) | 9 (3 cases × 3 trials) |
| Total per-trial `tok_in` (researcher + 2 judges per trial) | 2,959,497 | 2,891,470 |
| Total per-trial `tok_out` | 22,131 | 30,588 |
| **Mean per trial `tok_in`** | **328,833** | **321,274** |
| **Mean per trial `tok_out`** | **2,459** | **3,399** |
| Mean per trial wall (s) | 76.7 s | 81.6 s |
| Mean tool calls / trial | 11.0 | 28.3 |

(Per-trial totals derived from the `done … tok_in= tok_out=` deltas in
`RUNLOG.md`. Each trial-line includes the researcher call chain *and*
the two judge calls for that trial; the case-3 oracle classification of
all 6,480 July-1943 articles ran separately and is not in the per-trial
figures. The headline 5,850,967 / 52,719 in the RUNLOG matches Mausoleo
+ baseline summed: 2,959,497 + 2,891,470 = 5,850,967 in.)

### 3.1 Case-3 oracle classification (one-time, separate from per-trial cost)

Source: `eval/case_studies/case3_oracle_ratios.json` build run.

- 6,480 July-1943 articles classified WAR/DOMESTIC/OTHER at temperature 0,
  Sonnet 4.5 over OAuth, batched 10/call → **648 batched calls**.
- Tokens (approx, captured at run-time): **~1,018,170 input + ~30,266 output**.
- Combined with per-trial Phase 2 totals, this brings the full Phase 2
  rerun token usage to **~6,869,137 input + ~82,985 output**.

The oracle is a one-time cost (the WAR/DOMESTIC/OTHER labels are stored
on disk and reused across trials and reanalyses); it is reported separately
because it is a methodological artefact of the case-3 metric design, not
of either system under test.

### 3.2 Baseline-side note

Baseline embedding/BM25 indexing cost: zero LLM calls (in-process BM25 over
the 6,480 article texts). Index build is a few seconds, no API.

## 4. Storage / inference footprint

Source: live ClickHouse instance (`http://localhost:8123`, database
`default`, table `nodes`).

| Item | Value | Source |
|---|---|---|
| Total rows in `default.nodes` | 14,235 | `SELECT count() FROM default.nodes` |
| → paragraph-level | 7,128 | `GROUP BY level` |
| → article-level | 7,068 | `GROUP BY level` |
| → day-level | 32 | `GROUP BY level` |
| → month/year/decade/archive | 2 + 2 + 2 + 1 = 7 | `GROUP BY level` |
| **Note**: row counts exceed the 6,517 canonical Phase 1 nodes because the build was re-run several times (manifest is the canonical source: 6,480 article + 31 day + 5 week + 1 month = 6,517) | | manifest.json |
| Disk size on parts (compressed) | **25.21 MiB** | `system.parts` |
| Uncompressed size | 54.67 MiB | `system.tables` |
| `embedding` column compressed | 7.61 MiB | `system.columns` |
| `summary` column compressed | 4.96 MiB | `system.columns` |
| `raw_text` column compressed | 3.20 MiB | `system.columns` |
| Total embedding floats | 5,466,240 (= 14,235 × 384) | `SELECT sum(length(embedding))` |
| Theoretical raw embedding storage | 14,235 × 384 × 4 B = **20.85 MB** | derived |
| **Spec's 6,517 × 384 × 4 B = 9.93 MB** for the canonical-node count | matches the spec note "~10 MB" | derived |
| Per-query CH inference (vector + FTS at the day/week/month tier) | sub-second (the `case_studies` runs each issue ≤ 30 tool calls in ≤ 90 s wall, so per-query CH cost is negligible vs LLM cost) | `eval/case_studies/RUNLOG.md` per-trial wall times |

**Summary**: the 6,517-node July-1943 index lives in 25 MiB of ClickHouse on
disk, the embedding column is 7.6 MiB, and per-query CH inference is
effectively free at this scale. Storage is therefore not a cost factor at
the single-month or six-year scales; at sixty-year scale the disk footprint
projects linearly to ~1.5-2 GiB on disk, still trivial. Per-query
inference latency is sub-second regardless of corpus scale because vector
retrieval over HNSW and FTS over `tokenbf_v1` are both logarithmic in node
count.

## 5. Absolute-cost summary (the headline numbers for §6.5)

| Stage | Cost | Unit | Cadence |
|---|---|---|---|
| OCR build (30 July 1943 issues) | **~29.7 GPU-hours** | 2× RTX 3090 wall | one-time |
| OCR build wall-clock | **~15.3 hours** | single-host serial-issue | one-time |
| LLM index build | **$28.87 phantom-USD** | OAuth (no money charged) | one-time |
| LLM index build wall-clock | **~2 h 20 min** | end-to-end | one-time |
| Case-3 oracle classification | **~1.05 M input + 30 k output tokens** | OAuth | one-time |
| Per-query Mausoleo | **328 k input + 2.5 k output tokens, 11 tool calls, 77 s wall** | OAuth | per query |
| Per-query baseline | **321 k input + 3.4 k output tokens, 28 tool calls, 82 s wall** | OAuth | per query |
| Per-query ClickHouse inference | **sub-second** | localhost | per query |

## 6. §7.2 limitation flag (must be reflected in the limitations list)

The cost subsection in §6.5 has three load-bearing assumptions that the
dissertation must call out:

1. **Phantom-USD unit.** All "cost" figures in §6.5 and this annex are
   token-rate proxies, not subscription bills. The OAuth Claude Max
   subscription was used throughout Phase 1 and Phase 2; no API key was
   activated. The dollar figures are useful for proportional comparison
   (which phase costs how much, Mausoleo vs baseline) but are not what
   would be on an invoice. The token counts (Phase 2 only — Phase 1 did
   not capture them per call) are the more durable unit.

2. **Linearity of OCR and article-summary cost in corpus size.** The
   60-year scale-ups in §1.1 and §2 above assume the OCR pipeline and
   the article-summary phase scale linearly with article/issue count.
   This is approximately true (each issue/article is processed
   independently). Higher LLM levels (week, month, year, decade,
   archive) are sub-linear: a year-summary collapses 12 month
   summaries (not 12 × 6,480 articles), a decade-summary collapses 10
   year summaries. The article phase and OCR continue to dominate at
   archival scale.

3. **Per-query ClickHouse inference is corpus-size-independent in
   practice.** This holds because the `embedding` column is HNSW-indexed
   and the `summary`/`raw_text` columns carry `tokenbf_v1` tokens,
   both of which give sub-second retrieval over millions of nodes.
   The per-query cost reported in §3 is therefore stable across the
   one-month, six-year, and sixty-year scales; only the LLM cost per
   query changes as the agent reads more or longer summary nodes,
   and that change is bounded by the fixed-depth tree traversal.
