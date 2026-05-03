# Round 72 plan — STRATEGY 3 (cross-model rewrite via Sonnet 4.5)

## 1. R71 result + diagnosis

R71: 0/3 PASS, all near certain. Hard regression from R61's 2/3 BEST.

R71 critic explicitly named AuthorMist garble: "Garbled/agrammatical sentences
that suggest generation drift. ... this sentence loses its subject."

**Strategy 1 (AuthorMist) is exhausted at this draft length / register.** AuthorMist
Qwen2.5-3B produces sentence-fragment / awkward-phrasing artefacts that the
critic flags as MORE diagnostic of LLM-generation than the polished R61 tells.

## 2. Strategy pivot: Strategy 3 (cross-model rewrite)

Per Phase 3 Stage B 70+ directive:
> §7.3 synthesis: regenerate with Sonnet 4.5 + radically different system prompt
> Abstract: regenerate with Haiku 4.5 (different model class entirely)
> §8 conclusion: regenerate with Sonnet 4.5 + different prompt

For Mausoleo (no §7.3, no §8), the equivalents are:
- §3 system design (technical methodology) — regenerate via Sonnet 4.5
- §5 Discussion — regenerate via Sonnet 4.5

The hypothesis: even though Sonnet 4.5 and Opus 4.7 are both Anthropic models,
the DIFFERENT MODEL + RADICALLY DIFFERENT SYSTEM PROMPT will shift surface
distribution measurably without grammatical drift.

## 3. Implementation

For each target section (§3 + §5):

1. **Extract source section** verbatim from `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v10.md`.

2. **Build a rewrite prompt** that:
   - Specifies UK-academic register, third-person expository voice
   - Mandates: keep all citations, numerics, technical terms, file paths, Italian
     phrases verbatim
   - Mandates: no em-dashes, no " - " separator
   - Forbids the universal Opus tells flagged across R61–R71:
     * NO balanced antithesis with semicolon pivot
     * NO aphoristic closers ("the gap is already inside the index" pattern)
     * NO "X handles Y and is awkward for Z" triadic framing
     * NO "Inputs are X. Outputs are Y." parallel-construction openers
     * NO three-case symmetric experimental framing in §4 (preserve §4 from baseline)
   - Mandates a different voice register: short declarative sentences, occasional
     mid-paragraph qualification, varied paragraph lengths

3. **Use a radically different system prompt** for Sonnet 4.5: NOT
   "You are Claude Code" but a research-engineer persona that defaults to
   plain technical prose.

4. **Sanity-check**: word count within ±10% of original section, all numerics
   preserved, all citations preserved. If sanity-check fails, retry up to 2
   times. If still fails, fall back to original.

5. **Splice into v10** to produce `v10_cross_model.md`.

## 4. R72 target sections

(a) **§3 Chapter 3: How Mausoleo is built** — full chapter, ~1,321 words.
(b) **§5 Chapter 5: Discussion** — paragraphs 1-3 (preserve para 4 closer).

These are the same sections AuthorMist was trying to paraphrase + reverted.
Cross-model rewrite avoids the AuthorMist garble problem because Sonnet 4.5
produces fluent English at sentence-level.

## 5. Decision logic

If R72 lands 3/3: STOP, mission complete.
If R72 lands 2/3: COMMIT as new BEST_GAN.
If R72 lands 1/3: extend cross-model scope to §1 + Abstract for R73.
If R72 lands 0/3: fall back to R61 ship.

## 6. Risk

Sonnet 4.5 is also an Anthropic model. The critic Opus 4.7 may recognise
Sonnet's stylistic fingerprint as still LLM-generated. But the system-prompt
divergence (research-engineer persona, NOT default-Claude voice) should produce
prose distributionally distinct from Opus 4.7 default style.

The R47/R48/R49/R51/R55 cohort-mirror PASSes happened because critics keyed on
positive cohort exemplars. R72 prose has to PRESERVE those positives (Preface,
OCR engineering frustration, Italian quotation block, asymmetric case weighting)
while NEUTRALISING the universal Opus tells in §3 + §5.

## 7. Word-count constraint

v10 = 6,724 words. R72 target: stay within 9,950w cap (we are well under).
