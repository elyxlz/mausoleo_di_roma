# Case 1 Mausoleo trial-2 variance note

Phase 2 rerun (2026-05-03). Case 1 mausoleo trials had recall 0.79 / **0.45** / 0.79.
This note diagnoses the t2 dip from the per-trial JSON artefacts in
`eval/case_studies/runs/case1_mausoleo_t{1,2,3}.json`.

## 1. Tool-call sequence per trial

All three trials open identically: enter the absent-day node `1943-07-26`,
read sibling day nodes `1943-07-25` and `1943-07-27`, then list their
articles via `children(limit=20)`. The divergence is at call #6+.

| # | t1 (seed 1233, recall 0.79) | t2 (seed 2242, recall 0.45) | t3 (seed 3251, recall 0.79) |
|---|---|---|---|
| 1 | node 07-26 | node 07-26 | node 07-26 |
| 2 | node 07-25 | node 07-25 | node 07-25 |
| 3 | node 07-27 | node 07-27 | node 07-27 |
| 4 | children 07-25 lim=20 | children 07-25 lim=20 | children 07-25 lim=20 |
| 5 | children 07-27 lim=20 | children 07-27 lim=20 | children 07-27 lim=20 |
| 6 | text 27_a006 | text 27_a006 | node 07-24 |
| 7 | node 07-24 | text 27_a000 | node 07-28 |
| 8 | search_text "Mussolini arrestato" 25-31 | search_text "Badoglio proclama..." 27-27 | text 27_a006 |
| 9 | search_text "Badoglio governo" 27-28 | node 07-28 | text 27_a007 |
| 10 | search_semantic "proclama Badoglio..." 27-28 | node 07-24 | text 27_a013 |
| 11 | **children 07-27 lim=60** | search_text "Mussolini Gran Consiglio" 24-24 | text 27_a000 |
| 12 | - | search_text "Roma manifestazioni..." 27-28 | search_text "Mussolini arresto..." 25-28 |
| 13 | - | text 07-27 (full day) | search_text "dimissioni Duce..." 25-28 |
| 14 | - | search_semantic "manifestazioni Roma..." 27-27 | search_text "Badoglio proclama..." 25-28 |
| 15 | - | - | **children 07-27 lim=60** |

Touched-article totals: t1=81, t2=40, t3=80. Touched-relevant: t1=33, t2=19, t3=33.

## 2. Diagnosis: what caused the dip

t1 and t3 both eventually issued `children(node_id="1943-07-27", limit=60)`,
which paginates beyond the default 20-article window and returns articles
`1943-07-27_a020`..`a059` (99386 chars). That second pagination is what
surfaces the bulk of the GT-relevant Badoglio-transition coverage —
specifically articles a021, a022, a024, a026, a029, a030, a032, a033,
a036, a038, a040, a048, a049 (thirteen of the missing fourteen GT items;
the fourteenth is `1943-07-28_a190`, which only t1 reached via a
`search_semantic` hit).

**t2 never paginated past the first 20 children.** Instead, after
`children 07-27 lim=20` it tried four search calls (one
`search_text` against 27-27, one `search_text` against 24-24, one
`search_text` against 27-28, one `search_semantic` against 27-27) plus
a `text(node_id="1943-07-27")` full-day pull. The four searches all
returned empty/no-hit payloads (88, 64, 79, 105 chars respectively —
confirming no article-level matches were returned). The `text(07-27)`
call returned the day-summary (12309 chars) but does not enumerate
article ids, so it did not add to `article_ids_touched`.

Net effect: t2's 14 tool calls accomplished less coverage than t1's 11
or t3's 15, because t2 spent its budget on text/semantic searches that
either returned nothing or returned a synthesised summary, rather than
on the simple `children(..., limit=60)` pagination that t1 and t3
discovered. Same answer quality (judges scored t2 at 4.0/4.0 across
both judges, vs 4.33 for t1 and 5.0 for t3 — a small but consistent
quality dip), but the recall-of-touched-articles metric penalises t2
sharply because the metric counts ids enumerated, not facts grounded.

## 3. Verdict: noise, with a small systematic flavour

**Primarily noise.** The three trials differ only in seed (1233, 2242,
3251) and they all reached the same correct conclusion (07-26 is
absent; 07-27 frames the regime change). The semantic-search fallback
in t2 returned empty because the harness's text-search (the embedder is
loaded but the article-level corpus appears not to BM25-match the
specific phrasings t2 chose: "Roma manifestazioni 26 luglio Quirinale",
"Badoglio proclama ordine pubblico manifestazioni"). This is search-
recall noise, not a Mausoleo defect: when the LLM happens to pick
search queries that miss, the metric punishes it for not having
fallen back to brute-force pagination.

There is a **mild systematic component**: the agent's planning prompt
does not strongly signal "if your searches return empty, paginate the
children list further before concluding." That is a tunable prompt
issue, not a research finding.

## 4. Recommendation for §6.5 drafter

1. **Keep t2 in the mean.** Three trials is already a small sample and
   removing the variance trial inflates the apparent stability. The
   reported case-1 mausoleo mean of 0.67 (min 0.45, max 0.79) honestly
   captures the dispersion; do not drop t2 as an outlier.
2. **Flag the variance briefly** in the §6.5 case-1 paragraph: a one-
   sentence note that recall has high variance on case 1 because the
   metric is article-id enumeration and the agent occasionally answers
   well from a day-summary without enumerating ids. Cross-reference
   §7.2 limitations.
3. **Do not rerun.** The variance is real and informative; suppressing
   it via lower temperature or seed re-rolling would be p-hacking.
4. **§7.2 addition.** Add a sub-bullet under the existing
   "recall-of-touched-articles operationalisation" limitation: "the
   metric is sensitive to whether the agent paginates exhaustively or
   answers from a compressed summary; case-1 trial 2 illustrates this
   (recall 0.45 with a qualitatively complete answer, judge mean 4.0)."
5. **Optional follow-up** (not for this dissertation): tweak the
   Mausoleo planner prompt to fall back to wider pagination when N
   consecutive search calls return empty. Note as future work in §8.
