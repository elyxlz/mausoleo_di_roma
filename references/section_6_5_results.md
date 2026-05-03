## §6.5 Aggregate results

All eighteen planned trials completed in the rerun (18/18; rerun date 2026-05-03).

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

Paired sign tests (n=6 for quality, n=3 for completeness/RMSE) return p-values between 0.125 and 1.000; the direction is uniform in Mausoleo's favour but with three trials per system the statistical resolution is coarse. Inter-judge κ on integer-discretised quality means is 0.33 (Case 1), 0.57 (Case 2), 0.14 (Case 3).

Cost is reported in absolute terms; no money was charged because all Anthropic calls bill against the Claude Max OAuth subscription quota. The one-time OCR build totalled ~15.3 wall-hours and ~29.7 GPU-hours on 2× RTX 3090. The one-time LLM index build (Haiku 4.5 for 6,480 article summaries plus Sonnet 4.5 for the 37 higher-tier summaries) carried a harness-reported phantom-USD figure of $28.87. Per trial across the rerun, mean per-query cost was Mausoleo 328k input + 2.5k output tokens at 76.7 s wall; baseline 321k input + 3.4k output tokens at 81.6 s wall. The case-3 oracle classification of all 6,480 articles cost ~1,018,170 input + 30,266 output tokens across 648 batched Sonnet 4.5 calls. ClickHouse retrieval over the 6,517 nodes (HNSW-backed `vector_similarity` index plus `tokenbf_v1` FTS index) returns sub-second on the build host; per-query inference cost is dominated by LLM tokens, not by index lookup.

Two methodology notes carry over from the rerun. Judge 2 was substituted as discussed in §6.1, and the §7.2 limitation accordingly notes that cross-vendor robustness is untested. The embedding model used to build the stored ClickHouse `embedding` column is `paraphrase-multilingual-MiniLM-L12-v2` (384-dim); the Phase 1 silent text-search fallback was fixed for this rerun, and a smoke test confirmed the encoder load (the nearest day node to the query "Mussolini" by L2 distance is `1943-07-26`, the regime-change day, which is the right answer). Mausoleo's chars-read is higher than the baseline's across all three cases because a day summary is denser per node than a 220-character BM25 snippet; the chars-read metric measures bytes returned to the agent, not bytes the agent reasoned about, and is reported but not over-interpreted.

---
