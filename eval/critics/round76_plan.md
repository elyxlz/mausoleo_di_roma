# Round 76 plan — STRATEGY 4 SICO HARDER

## Strategy

Continue Strategy 4 SICO but tighten the constraint surface. R75 failed because Haiku 4.5 with style anchors still produced aphoristic single-sentence paragraph closers despite the system prompt forbidding them in general terms. R76 enforces a length floor on every paragraph closer, scope-extends to the abstract opening (universal R20+ tell) and §4 prose around the table, and replaces the example exemplars with paragraphs that are LESS aphoristic in their closes.

## Specific changes from R75

1. **System prompt amendment**: explicit numerical rule — "Every paragraph must end with a sentence at least 18 words long. The final sentence may not be shorter than its preceding sentence by more than 6 words. The final sentence may not be a single declarative statement that restates the paragraph's thesis."
2. **Forbid the "X. Y." truncated-pair pattern**: "If two consecutive sentences in the rewrite end with the same number of clauses (1 each) and total fewer than 25 words combined, you must merge or expand."
3. **Replace one PHIL0046 anchor**: drop the McCoy slope-not-step paragraph (which itself ends on "What varies is the scaffold" — 4 words; possibly the source of the aphoristic-closer leakage); replace with the PHIL0046 functionalism paragraph (lines 67-69) which ends on a longer hedge.
4. **Add Abstract to scope**: the abstract opening "that template handles questions for which articles exist and is awkward for the others the corpus invites" is the universal R20+ "X handles Y and is awkward for Z" tell. Mask its specific construction and force a rewrite.
5. **Add §4 prose around table to scope**: the §4 paragraphs around lines 134-136 ("The other two cases ran on the same configuration and broke the same way") and §4 line 155 ("The regime-change case cleared in...") are the "two shorter cases" structural tell. Mask the table cells and the Italian quotation, paraphrase the surrounding prose only.

Skip §3 (technical methodology, no register pay-off), skip §2.3 (cog-sci spine), skip §2.4 (corpus context, short and citation-dense). Skip the Italian block in §4.

## Sections to apply SICO to

- Abstract (lines 7-11): ~200w
- §1 Chapter 1 (lines 23-35): ~720w
- §2.1 Existing digitised newspaper archives: ~253w
- §2.2 The hierarchical-retrieval lineage: ~511w
- §4 Chapter 4 prose around the table: ~350w (the missing-26-July paragraphs + two-shorter-cases paragraph + aggregate-numbers paragraph; preserve table verbatim, preserve Italian quotation block verbatim)
- §5 Chapter 5 Discussion: ~375w

Total ≈ 2,409w (~36% of body), wider than R75 (28%) and R72 (9%), narrower than R74 (80%).

## Pareto rule

If R76 < R61 (2/3), revert v10 to R61 baseline 420027e. R76 paraphrased version stored at /tmp/gan_round76/v10_sico_v2.md.

## Word count target

v10 currently 6,724w. R76 ±15% on ~2,409 affected words allows ±361 net swing; total stays under 7,100w.

## Prose-quality assessment per candidate

Pre-run: stricter constraints + replaced exemplar should reduce aphoristic-closer leakage. Failure modes:
- Haiku may compensate for the closer-length floor by producing artificially-padded closers that read as filler. Mitigation: the rewrite_with_retry runs sanity-check on word count drift and re-prompts if drift exceeds bounds.
- The mask-and-restore pipeline is more brittle on §4 because of the table; mask all numeric cells.
- Abstract masking risks losing the cohort-mirror pos-of-evidence ("Across eighteen scored trials...") that R47-R49 critics cited as positive cohort exemplar. Keep this sentence verbatim; rewrite only the opening.
