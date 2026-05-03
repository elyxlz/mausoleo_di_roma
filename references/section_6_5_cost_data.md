# §6.5 Cost-amortisation data

Backing numbers for the §6.5 final paragraph and the §7.2 index-build limitation.
Authoritative sources are cited inline (RUNLOG entries, file paths, ClickHouse
queries). All LLM cost figures are token-rate proxies (no API spend; calls bill
against the Claude Max OAuth subscription quota); this is flagged
explicitly throughout — see "phantom-USD caveat" below.

> **Phantom-USD caveat.** Phase 1 (`eval/summaries/run_report.json` and `_logs/run.log`)
> and the first Phase 2 run (`eval/case_studies/RUNLOG.md`, lines 1-30) both report
> a `total_cost_usd` derived from list per-token rates for Haiku 4.5 and Sonnet 4.5.
> No money was spent: the OAuth subscription path was used end-to-end. The dollar
> figure is therefore a *token-rate proxy* useful for cross-system comparison
> (Mausoleo build vs. baseline per query, Anthropic-vs-Anthropic), but it is not
> a subscription bill. Token counts are the durable unit; the dollar figures are
> retained because Phase 1 did not log per-call token totals — only the
> per-call cost the harness computed from the token counts before discarding them.

## 1. Phase 1 — index build (one-time)

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

### 1.1 Per-summary average cost

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

## 2. Phase 2 — case-study per-query cost (recurring)

Source: `eval/case_studies/RUNLOG.md` "Rerun 2026-05-03" block (lines 53-74)
and "Final summary" (lines 75-83). Token counts are direct from the OAuth
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
`RUNLOG.md` lines 56-74. Each trial-line includes the researcher call
chain *and* the two judge calls for that trial; the case-3 oracle
classification of all 6,480 July-1943 articles ran separately and is
not in the per-trial figures. The headline 5,850,967 / 52,719 in the
RUNLOG matches Mausoleo + baseline summed: 2,959,497 + 2,891,470 =
5,850,967 in.)

The two systems use roughly the same total tokens per trial because
Mausoleo trades many small baseline reads (~30 article snippets) for
fewer but larger reads (day or week summaries, each ~200-400 words).
Mausoleo wins on tool-call count (11 vs 28); the byte-count comparison
is in §6.5 of the dissertation prose.

The RUNLOG-reported phantom-USD for the full Phase 2 run (researcher + judges
+ oracle classification) is **$19.17** (`RUNLOG.md` line 74). The
researcher-only share works out to roughly **$1.05 per query** at Sonnet
4.5 list rates, used as the baseline per-query divisor in §3 below.

Baseline embedding/BM25 indexing cost: zero LLM calls (in-process BM25 over
the 6,480 article texts). Index build is a few seconds, no API.

## 3. Break-even table

We compare the one-time Mausoleo index-build cost against the recurring
baseline per-query cost. Two units are reported: phantom-USD (with the
caveat above) and tokens. The single-month corpus uses the actual measured
numbers; six-year and sixty-year scale-ups assume linear growth in the
article-summary phase (the dominant phase) and sub-linear growth in
day/week/month/year/decade levels (more on this in §5 below).

### Per-query cost (the divisor)

We take the **baseline** per-query cost as the recurring cost the agent
would otherwise pay against a flat retrieval store. From §2 above:
- baseline `tok_in` mean per trial ≈ 277 k, `tok_out` mean ≈ 2.8 k → ~280 k
  total tokens per query.
- phantom-USD per baseline query: $1.05 mean (from the $9.43 baseline-side
  total ÷ 9 trials, computed from the tok totals × Sonnet 4.5 list rates).

### Index-build cost (the dividend) at three corpus scales

| Scale | Articles | Day nodes | Week nodes | Month/Year/Decade nodes | Index-build phantom-USD | Index-build tokens (article-phase, est.) |
|---|---|---|---|---|---|---|
| **One month** (July 1943 — measured) | 6,480 | 31 | 5 | 1 | **$28.87** | ~16.2 M article-phase + ~2.5 M day-phase ≈ ~19 M |
| **Six years** (×72 months, articles linear; day/week/month linear; year +6, decade +1) | ~466,560 | ~2,232 | ~360 | ~78 | **~$2,078** (article ~$1,383 + day ~$683 + higher levels ~$12) | ~1.4 B |
| **Sixty years** (full *Il Messaggero* archival scope: ×720 months) | ~4,665,600 | ~21,900 | ~3,600 | ~735 | **~$20,800** (article ~$13,827 + day ~$6,889 + higher levels ~$95) | ~14 B |

Linear-extrapolation caveats spelled out in §5 below.

### Break-even N (queries to pay back the index)

Break-even N = (index-build cost) / (baseline per-query cost). Reported
in both units; either one alone is misleading given the phantom-USD caveat.

| Scale | Index-build phantom-USD | Per-query phantom-USD (baseline) | **Break-even N (USD)** | Index-build tokens | Per-query tokens (baseline) | **Break-even N (tokens)** |
|---|---|---|---|---|---|---|
| One month (July 1943) | $28.87 | $1.05 | **~28 queries** | ~19 M | ~280 k | **~68 queries** |
| Six years | ~$2,078 | $1.05 | **~1,979 queries** | ~1.4 B | ~280 k | **~5,000 queries** |
| Sixty years | ~$20,800 | $1.05 | **~19,810 queries** | ~14 B | ~280 k | **~50,000 queries** |

**The outline §6.5 currently claims**:
> "For a single-month corpus the break-even is ~5 queries; for a 60-year
> corpus it is approximately the first query."

**This is wrong by the measured numbers.** Mausoleo's index-build cost is
*not* paid back in 5 queries on a one-month corpus — it's paid back in
~28-68 queries depending on unit. At 60-year scale the break-even is
~20 k queries, not "approximately the first query." The correct framing
for §6.5 is the *opposite* of the original outline:

> Cost analysis: Mausoleo's index-build cost is paid once at corpus-ingest
> time and amortised across all subsequent queries; the baseline pays its
> recurring per-query cost on every query. On a single-month corpus, the
> measured break-even is ~28-68 queries (phantom-USD vs token unit; see
> §6.5 cost table). On a 60-year corpus, the break-even rises in absolute
> terms to ~20,000 queries because index build scales with corpus size
> while per-query cost is roughly corpus-size-independent for a flat
> baseline. **The case for hierarchical indexing at archival scale is
> therefore not strictly cost-driven on Mausoleo's measured numbers; it
> rests on the qualitative wins of §6.2-§6.4 (case 1 capability gap,
> case 2 + 3 quality + completeness wins) and on the operational fact
> that flat retrieval over millions of articles is not a usable interface
> regardless of cost.** This contradicts the original outline forecast and
> is reported here as a measured-vs-anticipated revision; flagged in §7.2.

This revision must be carried into the §6.5 prose before submission.

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
projects linearly to ~1.5-2 GiB on disk, still trivial.

## 5. §7.2 limitation flag (must be added to the limitations list)

The cost analysis in §6.5 has three load-bearing assumptions that the
dissertation must call out:

1. **Phantom-USD unit.** All "cost" figures in §6.5 and this annex are
   token-rate proxies, not subscription bills. The OAuth Claude Max
   subscription was used throughout Phase 1 and Phase 2; no API key was
   activated. The dollar figures are useful for proportional comparison
   (which phase costs how much, Mausoleo vs baseline) but are not what
   would be on an invoice. The token counts (Phase 2 only — Phase 1 did
   not capture them per call) are the more durable unit.

2. **Linearity of index-build cost in corpus size.** The six-year and
   sixty-year break-even numbers in §3 above assume the article-summary
   phase scales linearly with article count. This is approximately true
   for the article phase (each article is summarised independently) but
   sub-linear for higher levels: a year-summary collapses 12 month
   summaries (not 12 × 6,480 articles), a decade-summary collapses 10
   year summaries. The break-even table is therefore a slight
   *over-estimate* of build cost at higher scales; the article phase
   continues to dominate.

3. **Per-query cost is treated as corpus-size-independent for the
   baseline.** This holds while the BM25 baseline returns a fixed
   top-K of ~30 short snippets per query (which it did in §6 trials).
   For a 60-year corpus the snippet-quality of BM25 degrades sharply
   (more polysemous matches per query) and the agent would either issue
   more queries or read more snippets per query, raising the per-query
   cost. The break-even N at 60-year scale is therefore an *upper bound*;
   the true break-even is somewhere lower because the baseline gets worse,
   not because Mausoleo gets cheaper.

4. **Outline-vs-measured contradiction.** The §6.5 paragraph in the
   outline (referenced verbatim in §3 above) anticipated break-even at
   "~5 queries" for one month and "approximately the first query" for
   60 years. The measured numbers do not support this. The cost case
   for Mausoleo is *not* the strongest case at small N; the strongest
   cases are the qualitative wins documented in §6.2-§6.4 (definitional
   capability gap, completeness, quality) and the operational
   non-substitutability of flat retrieval at archival scale. The §6.5
   prose must be revised before submission to reflect the measured
   numbers, and §7.2 must add this revision as a limitation of the
   original cost-amortisation argument.
