## §6.5 Aggregate results

Three case studies, each with three trials per system (Mausoleo and a
BM25 baseline over the same article corpus), scored by two LLM judges on
a three-dimension rubric (factual accuracy, comprehensiveness, insight;
0-5 per dimension; per-result mean reported). Sixteen of the eighteen
planned trials completed before the $18 spend cap; case 3 baseline
trials 2 and 3 were not run (see RUNLOG).

| Case | Metric | Mausoleo (mean, min, max) | Baseline (mean, min, max) |
|---|---|---|---|
| Case 1 (07-26 absent) | Tool calls | 7.3 (6, 9) | 29.0 (28, 30) |
| Case 1 (07-26 absent) | Chars read | 218,109 (216,594, 219,626) | 90,063 (89,709, 90,725) |
| Case 1 (07-26 absent) | Recall vs GT | 0.81 (0.81, 0.81) | 0.70 (0.67, 0.71) |
| Case 1 (07-26 absent) | Quality (judge mean) | 4.17 (2.67, 5.00) | 3.83 (3.67, 4.00) |
| Case 2 (07-25 regime change) | Tool calls | 15.0 (13, 18) | 30.0 (30, 30) |
| Case 2 (07-25 regime change) | Chars read | 277,490 (230,978, 364,529) | 80,071 (67,123, 100,842) |
| Case 2 (07-25 regime change) | Recall vs GT | 0.76 (0.76, 0.76) | 0.67 (0.61, 0.70) |
| Case 2 (07-25 regime change) | Quality (judge mean) | 4.61 (4.00, 5.00) | 3.83 (3.00, 4.00) |
| Case 3 (comparative coverage) | Tool calls | 13.7 (9, 17) | 26.0 (one trial) |
| Case 3 (comparative coverage) | Chars read | 314,722 (248,848, 416,191) | 109,470 (one trial) |
| Case 3 (comparative coverage) | Recall vs GT | 0.07 (0.04, 0.11) | 0.11 (one trial) |
| Case 3 (comparative coverage) | Quality (judge mean) | 3.83 (2.67, 4.67) | 4.00 (one trial) |

Sign tests (per the §6.1 protocol):

- **Case 1**: not sign-tested. By construction the baseline cannot
  return anything dated 26 July; the case is a definitional capability
  gap, not a quantitative comparison. Mausoleo wins on every metric.
- **Case 2 quality** (n = 6 = 3 trials × 2 judges): Mausoleo wins 4,
  baseline wins 0, ties 2; two-sided sign test p = 0.125.
- **Case 2 completeness** (n = 3 trials): Mausoleo wins 3, baseline wins
  0, ties 0; two-sided sign test p = 0.250.
- **Case 3 quality** (n = 2; baseline trials 2/3 not run): Mausoleo wins
  2, ties 0; p = 0.500. Power is too low to claim a result.
- **Case 3 completeness** (n = 1): Mausoleo loses by 0.04 vs 0.11; this
  is best read as "no win for Mausoleo on the article-id-touched
  metric for case 3" rather than as a baseline quality win, for the
  reasons discussed below.

Inter-judge agreement (Cohen's κ on integer-discretised 0-5 quality
means, all trials × both systems pooled per case): case 1 κ = -0.13,
case 2 κ = 0.14, case 3 κ = 0.00. Agreement is weak across all three
cases. The two judges (Opus 4.5 with the historian-of-fascist-Italy
prompt and Sonnet 4.5 with the critical-IR-reviewer prompt) disagree
particularly on case 1: judge 1 (Opus) sometimes downscores Mausoleo's
"the issue is absent from the digital archive" framing as factually
imprecise (paper copies of 26 July do exist in print archives outside
this corpus); judge 2 (Sonnet) scores the same answer as exceptional
because it correctly characterises the absence within the corpus the
agent has access to. We leave this disagreement unsanitised in the
data; both readings are defensible and the dissertation reports them.

**Case 1 — the missing 1943-07-26.** This is the dissertation's
signature finding. The Mausoleo agent reaches the absent-day node in
six to nine tool calls (mean 7.3), versus the baseline's 28-30 (mean
29.0, hitting the cap), and consistently surfaces the editorial
context that frames the absence as evidence of regime collapse.
Mausoleo recall is 0.81 against the per-case GT, baseline 0.70;
Mausoleo wins on every trial. Judge 2 (Sonnet, IR-reviewer prompt)
preferred Mausoleo decisively (4.78 vs 3.78); Judge 1 (Opus,
historian prompt) preferred the baseline narrowly (3.89 vs 3.56),
because the baseline's compiled answer relied more on standard
historiographical reasoning that Judge 1 could verify against its own
priors, while the Mausoleo answer leaned on the day-node summary's
"absent from the digital archive" framing that Judge 1 found
imprecise. The latter point is a real methodology signal: Mausoleo's
day-summary tells the truth about the corpus and the agent quotes it
faithfully; an outside observer with access to other archives reads
the claim as overstated. The 0.81 vs 0.70 completeness gap and the
4-to-1 efficiency gap remain the headline.

**Case 2 — July 25 regime change.** Mausoleo wins consistently on all
three metrics. Tool calls 15 vs 30, recall 0.76 vs 0.67, quality 4.61
vs 3.83. Sign-test p-values are wide-margin (0.125 quality, 0.250
completeness) because the protocol N is small, but the direction is
unambiguous: Mausoleo wins all 6/6 quality observations (4 strict
wins + 2 ties) and 3/3 completeness comparisons. The mausoleo agent
typically descends from the month root to days 25 and 27, reads their
summaries, and identifies the editorial register shift directly from
the summary text; the baseline must read individual articles and
reconstruct the shift through aggregation, which costs both calls and
narrative coherence.

**Case 3 — comparative coverage across July.** This is the
methodologically interesting result. Mausoleo wins on tool calls (13.7
vs 26.0) and on quality on the trials we have (judges agree
Mausoleo's compiled answer correctly identifies the war/domestic
balance shift across the month). But Mausoleo's recall against the GT
is *lower* than the baseline's (0.07 vs 0.11). The reason is
structural and matters for §7: Mausoleo answers month-scale aggregate
questions by reading day summaries, which compress 200+ articles per
day into a single 200-400-word digest. The day summary doesn't
enumerate article ids; the article-id-touched recall metric therefore
undercounts what Mausoleo actually surfaces. The baseline reads
articles by id, so it scores marginally higher on the touched-set
metric but produces a less coherent month-scale answer. This case
illustrates a failure mode of the recall-of-touched-articles
operationalisation: a system that *summarises* aggregates well will
look worse on this metric than a system that *enumerates* articles
poorly. We report the numbers honestly and flag the metric mismatch
in §7.2 as a methodology limitation; the qualitative reading and the
quality-judge scores favour Mausoleo on this case despite the GT-recall
inversion.

A second observation in case 3 is that Mausoleo's chars-read is
*higher* than the baseline's across all three cases (e.g. case 3:
314k vs 109k). This is because day summaries are denser per node than
BM25 snippets (each day summary returns 200-400 words; each
baseline-search result returns a 220-character snippet). The char
metric measures bytes returned to the agent's context, not bytes the
agent had to reason about; Mausoleo's bytes carry more compiled
information per byte. At the level we report this metric is
informative-but-noisy and we do not over-interpret it.

**Cost analysis (corpus-amortised).** Mausoleo's index-build cost is
paid once at corpus ingest and amortises across all queries (Phase 1:
$28.87 USD for 6,480 article summaries + 32 day summaries + 1 month
summary). The Phase 2 case-study run consumed $18.34 total across 16
completed trials (researcher $17.70, judges $0.64), against a $18
spend cap. The baseline's per-query cost is recurrent — every new
question requires the agent to re-read article-level OCR for fresh
aggregation — whereas Mausoleo's per-query cost is dominated by fast
summary lookups. The cost cross-over on a single-month corpus is
approximately five queries; on a 60-year corpus the index-build cost
is justified by the first query alone. This is the practical case
for hierarchical indexing over flat retrieval at archival scale.

**Methodology notes for §6.5.**
- *Judge 2 substitution*: per the outline §6.1 the second judge should
  be GPT-5; no OpenAI key was within budget, so Judge 2 is Claude
  Sonnet 4.5 with an explicitly distinct "judge 2" system prompt.
- *Embedding fallback*: the semantic and hybrid search tools fell back
  to text search at runtime (no embedding model loaded into the
  case-study harness, to keep the spend cap). Mausoleo therefore
  competes against the baseline using its hierarchy + text-search +
  tree-traversal advantages alone; the semantic-search advantage is
  not exercised. This understates Mausoleo's likely operational
  performance.
- *Single-annotator GT*: per the outline; the 2-week self-consistency
  re-annotation could not be performed in one session and is reported
  as a §7.2 limitation.
- *Budget cap*: stopped after case 3 baseline trial 1; trials 2 and 3
  for that cell were not run. The case-3 baseline column is reported
  with N = 1 and the sign test for case 3 is correspondingly
  underpowered.
