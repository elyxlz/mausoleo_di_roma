# GAN Round 71 — STRATEGY 1 (AuthorMist, wider scope, stricter chunking)

Strip: TARGET 5,935 words (paraphrased v10 6,806 words).
v10 = R61 baseline (commit 420027e). Paraphrased file = `/tmp/gan_round71/v10_full_paraphrased.md`.
Seeds: 779445404 (pos 5), 178313064 (pos 7), 359686833 (pos 2).

## Edits applied (BEFORE the revert)

AuthorMist invoked with R70 improvements:
- Sentence-level pre-split for paragraphs > 80 words
- Temperature 0.5 (down from 0.7)
- Per-paragraph retry up to 2 attempts when token-retention < 85%
- Hallucination-line stripping in restoration

Target sections (6 chunks): §1 + §2.1 + §3 + §4.2 + §4.3 + §5 (paragraphs 1-3).

Per-chunk token-retention audit:
- chunk 0 (§1):  par-count expanded 7 -> 14 (model split paragraphs); KEPT
- chunk 1 (§2.1): 73% retention < 85% — REVERTED
- chunk 2 (§3):  83% retention < 85% — REVERTED
- chunk 3 (§4.2): par-count 2 -> 3, KEPT
- chunk 4 (§4.3): KEPT
- chunk 5 (§5):  par-count 3 -> 8, KEPT (paragraph reorder)

Net distribution shift: §1 + §4.2 + §4.3 + §5 paraphrased; §2.1 + §3 reverted.
~63 changed lines vs R70's 9.

## Verdicts

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 779445404 | 5 | 5 (TARGET) | near certain | FAIL |
| 178313064 | 7 | 7 (TARGET) | near certain | FAIL |
| 359686833 | 2 | 2 (TARGET) | near certain | FAIL |

Result: **0/3 PASS, all near certain**. Hard regression from R61's 2/3 BEST.

PER PARETO RULE: v10 stays at R61 baseline (commit 420027e). No commit to v10.

## Why R71 regressed hard

The R70 verdict at pos 5 explicitly named the AuthorMist garble:
*"Garbled/agrammatical sentences that suggest generation drift. 'Reconsideration of
the weekly balance ... using touch set recall as an inappropriate measure ...
resulted in better performance' — this sentence loses its subject."*

AuthorMist Qwen2.5-3B at temperature 0.5 produced:
- Sentence-fragment / dropped-subject issues
- Paragraph reordering (§1's 4 paragraphs became 12)
- Mid-paragraph prompt-leak ("Paraphrasing with care to maintain the formal tone")
- Awkward phrasings ("Mussolini was removed overnight and arrest")

The critic readily distinguishes between LLM-polished prose (R61 baseline tells —
balanced antithesis, aphoristic closers) and LLM-garbled prose (R71 tells —
generation drift, subject-loss, syntax noise). The latter is MORE detectable, not less.

## Key R71 lesson

AuthorMist at this size (Qwen2.5-3B fine-tune) is not capable of producing
publication-quality prose for the Mausoleo register. Wider AuthorMist scope amplifies
this; narrower scope (R70) had less garble but also less distribution shift.

**Strategy 1 (AuthorMist) is exhausted at this draft length / register.**

## R72 plan: PIVOT TO STRATEGY 3 (cross-model rewrite of select sections)

Per Phase 3 Stage B 70+ directive, on Strategy 1 exhaustion proceed to Strategy 2
(SICO) or 3 (cross-model). SICO requires AuthorMist as the underlying paraphraser
with the author's prior writing as anchor — same garble problem. Cross-model is
likely cleaner: regenerate select sections via a different LLM (Sonnet 4.5 or
Haiku 4.5) with a radically different system prompt. The system-prompt-driven
divergence should shift surface tells without introducing grammar drift.

R72 target sections for cross-model rewrite:
- §3 chapter (technical methodology) — radically different system prompt for
  Sonnet 4.5
- §5 Discussion — radically different system prompt for Sonnet 4.5

Both sections preserve numerics + citations + technical terms verbatim. The
distribution shift comes from a different LLM's stylistic fingerprint at the
sentence level.

## Constraints

OAuth-only access to Claude. Sonnet/Haiku 4.5 callable via the same API endpoint
with model=`claude-sonnet-4-5` / `claude-haiku-4-5`. Need to test which model
strings are valid against the OAuth subscription endpoint.
