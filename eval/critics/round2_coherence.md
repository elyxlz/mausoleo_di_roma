# Round 2 Coherence Review — MAUSOLEO_FULL_DRAFT_v2

**Reviewer**: COHERENCE critic, Phase 3 round 2
**Date**: 2026-05-03
**Target**: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v2.md` (9,894 words main body / 12,242 total inc. abstract+preface+references)
**Outline**: `/tmp/mausoleo/references/outline.md`
**Verdict**: **PASS** (0 CRITICAL, 0 HIGH, 2 MED, 4 LOW)

---

## 1. Round 1 issue closure table

| # | Issue | Round-1 severity | v2 status |
|---|-------|------------------|-----------|
| C1 | Embedding-model contradiction (BGE-M3 1024-dim vs MiniLM 384-dim) | CRITICAL | **CLOSED** — §3.2 and §5.1 / §5.2 now say `paraphrase-multilingual-MiniLM-L12-v2` 384-dim. BGE-M3 reframed as design-intent forced to fallback by CUDA-version mismatch; named in §3.2 and §7.2 limitations as future work. |
| C2 | Word count over 10,000 hard cap (11,940w) | CRITICAL | **CLOSED** — main body now 9,894w (106w under hard cap, 6w under 9,900 buffer). |
| C3 | §1 cross-ref to §3.3 should point to §3.2 | HIGH | **CLOSED** — §1 now reads "the design that makes this possible is described in §3.2". |
| C4 | §7.2 fails to deliver promised limitations (judge-2, rubric-fit) | HIGH | **CLOSED** — §7.2 expanded to include both: judge-2 substitution from GPT-5 to Sonnet 4.5 with cross-vendor caveat; case-3 rubric-fit limitation explicitly tied to the κ=0.14. Also adds the BGE-M3 / MiniLM future-work limitation. |
| C5 | §7.3 "seven-level schema (... 8 names)" | HIGH | **CLOSED** — §7.3 reads "7-level production schema (paragraph, article, day, week, month, year, decade; archive is the conceptual root for full-corpus deployment)". The level count now matches the enumeration. |
| C6 | usearch vs HNSW vector-index naming drift | HIGH | **CLOSED** — All occurrences harmonised to "ClickHouse `vector_similarity` index (HNSW-backed)" across §3.2, §3.3, §5.1, §6.5, §8. |
| C7 | Abstract overstates judge unanimity ("in every case") | HIGH | **CLOSED** — abstract now reads "preferred by both LLM judges on a three-dimension rubric on the judge-mean score in every case tested ... with judge agreement varying across cases (Cohen's κ = 0.33 / 0.57 / 0.14)". The κ values are reported alongside the win claim. |
| C8 | "Capability gap" overclaim (BM25 cannot return; flat retrieval cannot close at all) | HIGH | **CLOSED** — Abstract: "the BM25 baseline can only reason about the absence from sibling-day articles, with no node in the index that grounds the missing day." §7.1: "the BM25 baseline cannot return any article from 26 July because none exist in the corpus, but the agent can still reason about the absence using context from surrounding days; §6.2 reports baseline recall 0.67 on the broader 25–27 July relevance set." §8: "exposed a definitional capability gap: flat retrieval can reason around the absence but cannot ground it in a node that the index itself owns." |
| C9 | §6.5 redundant per-case mini-narratives | HIGH | **CLOSED** — All four per-case "Case N — ..." subsections deleted. §6.5 trimmed from 1,765w to 472w. Headline table, sign tests, κ list, cost paragraph, methodology notes carry the new material. |
| C10 | Outline-vs-draft sub-pipeline drift (6 outline / 8 draft) | MED | NOTED — draft remains internally consistent on 8; outline is stale. Not a v2 blocker. |
| C11 | Column-split granularity inconsistency (column-two missing in §4.2 list) | MED | **CLOSED** — §4.2 now lists "full-page, two-, three-, four-, five-, six-column" matching §3.1. |
| C12 | Self-consistency vs second-annotator conflation in §7.2 | MED | **CLOSED** — §7.2 now distinguishes: "the planned 2-week intra-rater self-consistency check (§6.1) was not performed within the dissertation timeline; a second-annotator inter-rater agreement check is the obvious next step." |
| C13 | §3.1 cross-ref to wrong subsection for ablation (§4.2 → should be §4.3) | MED | **CLOSED** — §3.1 now reads "§4.3 reports the ablation". |
| C14 | "Definitional vs quantitative" framing at war with §6.2 content | MED | **CLOSED** — §1 now reads "reported in §6.2 with full quantitative comparison alongside a definitional reading". §6.2 closing reads "definitional alongside the quantitative comparison". §7.1 alignment: "Recall is matched at 0.67, but the symmetry is misleading: the baseline answers from sibling-day articles, while Mausoleo answers from a node whose existence is itself the finding." All three locations now agree. |
| C15 | Case-3 oracle self-reference loop unflagged | MED | **CLOSED** — §6.1 now reads "ratio MAE/RMSE against an LLM-built per-week war/domestic oracle for case 3 (the oracle is itself produced by Sonnet 4.5; see §6.4 for the construction and its limitations)". |
| C16 | "Distinct random seeds" overclaim on Sonnet 4.5 | MED | **CLOSED** — §6.1 now reads "three trials per cell at distinct seed prompts (Sonnet 4.5 is not deterministic by integer seed on the OAuth path; trial-to-trial variance is treated as part of the measurement)". |
| C17 | 30 vs 30.5 min OCR budget reconciliation | MED | **CLOSED** — §3.1 now reads "The 30-minute target is the design budget; the empirical wall on the harder issue runs ~30.5 minutes on the slower GPU chain (§4.2)." |
| C18 | Preface 505w vs ≤500 brief | LOW | **CLOSED** — Preface 501w (within tolerance). |
| C19 | Per-section overshoots | LOW | **CLOSED** — addressed by C2. |
| C20 | "BIECO FUREORE BRITANNICO" typo gloss | LOW | **CLOSED** — §6.3 now reads "(OCR sic, *Il Messaggero* 25-Jul-1943)". |
| C21 | REPLACE-chain count | LOW | (passed) — no change needed. |
| C22 | *Magnetizzata* example orphan | LOW | (stylistic) — preserved unchanged. |
| C23 | §5.3 spot-check denominators | LOW | **CLOSED** — §5.3 reads "ten of ten day-level passes (forty-eight of fifty entities recovered)" — denominator distinction explicit. |

**Closure summary**: 3 CRITICAL closed; 6 HIGH closed; 7 of 8 MED closed (1 MED carried as outline-stale, not a draft issue); 5 of 5 LOW addressed.

---

## 2. v2 self-consistency audit (new round-2 checks)

### Number-consistency table (re-verified)

All numerical claims spot-checked against the table in §6.5; all match across the draft.

| Number | Where it appears | Verdict |
|---|---|---|
| OCR composite cold-cache | §4 intro / §4.2 / §4.3 — all 0.89878 | CONSISTENT |
| 1885 wCER stack delta | §3.1 (+0.013) / §4.2 (+0.013, 0.234→0.149) | CONSISTENT |
| Eight sub-pipelines | §3.1 / §4.2 / §6.5 — all 8 | CONSISTENT |
| 6,480 article nodes | §3.1 / §3.2 / §5.1 / §6.4 / §6.5 — all 6,480 | CONSISTENT |
| 6,517 total nodes | §3.2 / §5.1 / §6.5 — all 6,517 | CONSISTENT |
| Day/week/month/root counts | §3.2 / §5.1 / §6.5 — all 31 / 5 / 1 / 1 | CONSISTENT |
| 30.5 min OCR per issue | §3.1 / §4.2 / §6.5 — consistent with the new "30 design / 30.5 observed" framing | CONSISTENT |
| Case 1 tool calls M / B | §6.2 / §6.5 — 13.3 / 27.0 | CONSISTENT |
| Case 1 quality M / B | §6.2 / §6.5 / abstract — 4.56 / 4.22 | CONSISTENT |
| Case 2 / Case 3 tool calls, recall, quality, ratio MAE/RMSE | §6.3 / §6.4 / §6.5 / §7.1 / abstract — all match | CONSISTENT |
| Inter-judge κ | §6.2 / §6.3 / §6.4 / §6.5 / abstract — 0.33 / 0.57 / 0.14 across all | CONSISTENT |
| Sign-test p-values | §6.2 / §6.3 / §6.4 / §6.5 — all match | CONSISTENT |
| **Embedding dim** | §3.2 / §5.1 / §5.2 / §6.5 / §7.2 — all **384-dim, MiniLM** consistently | **CONSISTENT** (the v1 contradiction is gone) |
| Vector index name | §3.2 / §3.3 / §5.1 / §6.5 / §8 — all "HNSW-backed `vector_similarity`" | CONSISTENT |
| Production-schema level count | §3.2 / §5.2 / §7.3 — all 7 production levels with archive as conceptual root | CONSISTENT |
| Word count vs cap | 9,894 ≤ 9,900 buffer ≤ 10,000 hard cap | WITHIN CAP |

### Cross-reference audit

All cross-references verified to point at content that delivers what the cross-reference promises:
- §1 → §3.2 (architecture) ✓ — corrected from v1's §3.3
- §1 → §6.2 (case 1 detail) ✓
- §1 → §7.1 (signature finding) ✓
- §3.1 → §4.3 (LLM-post-correction ablation) ✓ — corrected from v1's §4.2
- §3.2 → §6.2 (absent-day case) ✓
- §3.2 → §3.3 (embedding-search escape hatch) ✓
- §5.1 → §3.2 (schema back-reference) ✓
- §5.1 → §6.2 ✓
- §5.2 → §5.3 (compression trade-off) ✓
- §5.3 → §6.2 (absent day pickup) ✓
- §5.3 → §7.2 (summariser-bias limitation) ✓
- §6.1 → §6.4 (case-3 oracle) ✓ — now flagged as self-reference
- §6.1 → §7.2 (single-annotator + judge-2 limitations) ✓ — both now delivered
- §6.4 → §7.2 (rubric-fit limitation) ✓ — now delivered
- §6.5 → §7.2 (cost figures and limitations) ✓
- §7.1 → §6.2 + §7.3 ✓
- §7.2 → §3.2 (BGE-M3 future work) ✓
- §7.3 → §5.3 (W29 prolepsis) ✓
- §7.3 → §6 (synthesis tested) ✓
- §8 → §6.5 + §7.1 + §7.3 ✓

No broken cross-references. No promised-but-undelivered limitations. No forward-references that point at content that does not exist.

---

## 3. Residual issues (round 2)

### MED (2 — neither a blocker)

**M1 — §6.5 case-3 oracle classification briefer than §6.4 covers it.** §6.5 reports the case-3 oracle classification stats ("$1,018,170 input + 30,266 output tokens across 648 batched Sonnet 4.5 calls") inside the cost paragraph; §6.4 carries the construction. This is a clean separation but the reader may want the §6.4 → §6.5 cross-reference signposted ("(oracle construction in §6.4)"). Minor. No action required.

**M2 — Outline outline.md L91 still says 6 sub-pipelines while draft consistently says 8.** Round 1 noted this; the draft is internally clean. The outline is stale. Not a v2 blocker; flagged for whoever maintains the outline.

### LOW (4)

**L1 — §6.5 cost paragraph absorbs the cost reporting that §7.2 also references ("~29.7 GPU-hours" / "~$29 phantom-USD"). The duplication is intentional (§7.2 references the cost in the limitations frame) but a reader on a careful pass will notice.** No action.

**L2 — §7.2 BGE-M3 future-work mention overlaps with the §3.2 mention.** Intentional (one is design-rationale, the other is limitations-reframing) but mildly repetitive. No action required; helpful repetition for the marker who reads §3 then jumps to §7.

**L3 — Magnetizzata still an orphan example in §4.1.** Carried over from v1; stylistic, not load-bearing.

**L4 — Sample case-3 prediction parsed line was deleted from §6.5 with the trim.** The example "1943-W26: 0.780, 1943-W27: 0.730, ..." that was in v1 §6.5 is gone in v2. The structural claim ("both systems emit five lines verbatim") still lands without the example, but the reader who wants to see the format has to infer it from the oracle vector. Not a blocker; consider re-adding 1 line as an inline example if word budget permits in the next round (~12w).

---

## 4. Intro–conclusion fit verdict

**STRONG** (up from MEDIUM in round 1).

§1 promises four things: (a) a five-level chronological tree, (b) three case studies vs BM25 baseline measuring efficiency / completeness / quality, (c) the missing 26 July as the lead and definitional capability gap, (d) the synthetic claim that multi-resolution time + provenance is the right scaffold.

§8 lands all four:
- (a) "deterministic OCR ensemble feeding a chronologically organised index of article, day, week, and month summaries" — covered.
- (b) "evaluated against a BM25 baseline on the same corpus across three case studies" — covered.
- (c) "The missing 1943-07-26, treated by the index as a first-class node ... exposed a definitional capability gap: flat retrieval can reason around the absence but cannot ground it in a node that the index itself owns." — covered, and with the v2 calibration.
- (d) "The synthesis defended in §7.3 is that these two literatures converge on the same prescription. An interface to a historical archive is well-designed only insofar as it honours both commitments." — covered.

The round-1 fit-pulldowns (broken cross-ref, definitional-vs-quantitative framing, capability-gap overclaim) are all resolved.

---

## 5. Submission readiness

**Yes.** No blocking issues. Two MED issues are carried as non-blockers (one is an outline-vs-draft drift external to the dissertation; the other is a navigation polish). Four LOW issues are stylistic.

The draft is structurally sound, the §6 evidence lands the §7.3 synthetic claim, the abstract and §8 mirror each other and §1 without overclaim, all cross-references resolve, all numbers agree, the embedding-model contradiction is gone, the level-count enumeration matches its quantifier, and the word count is under the cap with a 106w buffer.

**PASS the coherence gate for Phase 3.**
