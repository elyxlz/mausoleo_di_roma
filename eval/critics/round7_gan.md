# GAN critic — Phase 3 Stage B, round 7

Run date: 2026-05-03 ~15:30 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v6.md` (branched from v5; round-6 verdict edits applied: ~10 more "X rather than Y" instances varied across abstract/§3.1/§3.2/§6.2/§6.5/§7.2/§7.3/§8, abstract composite rounded to ~0.90, "phantom-USD" → "USD-equivalent", Foster Court anecdote dropped from preface, "embarrassingly" + "without invalidating the hill-climb" layered apology trimmed)
Cohort: 8 BASc 1st-class dissertations
Critic: claude-opus-4-7 via OAuth
Strip: `/tmp/gan_round7/strip_years.py`; stripped: `/tmp/gan_round7/stripped/`; runs: `/tmp/gan_round7/runs/`

## 1. Year-strip verification

42 target / 271 ref tags stripped, uniform across 9 essays. Target main-body: 9,477w.

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span |
|------|-----------------|---------------|------------|-----------|-----------------------|
| 1943 | 9 | Essay 9 | near certain | FAIL | "Pervasive 'X rather than Y' antithetical framing" + "Section-closing meta-summaries with uniform cadence" + "Constructed-authentic preface confession" |
| 1944 | 9 | Essay 9 | lean toward | FAIL | "Characteristic LLM epistemic-hedge cadence" + "Meta-structural self-commentary" + "Uncritical reference to current Anthropic model names as judges/tools" |
| 1945 | 1 | Essay 6 (= 2022RDBR1, a reference) | lean toward | PASS | "Encyclopedic, voiceless definitional prose" |

## 3. Overall verdict

**FAIL at 2 of 3 positions, PASS = 1/3.**

But: seed 1944 dropped from round 6's "near certain" to "lean toward" — partial recovery from the round 5 regression. Seed 1943 still "near certain". Net: same 1/3 PASS as rounds 2/3/4/5/6.

**TIES round 4 on FAIL-confidence aggregate** (rounds 4 and 7 both have one "lean toward" + one "near certain"; round 4 had two "lean toward"). So round 4 still best on aggregate confidence; round 7 close but not equal.

## 4. New tells flagged in round 7

- **"X rather than Y" antithesis still pervasive** despite ~10 round-6 edits: critic now cites "calendar-given hierarchy in place of induced clustering", "interpretive activation, not pure compression", "extension rather than a displacement". Round-7 cuts haven't reached every one.
- **Section-closing meta-summaries with uniform cadence**: "Read against one another, these literatures fix the position Mausoleo occupies. The newspaper archives are the access modality it extends." (§2 closer)
- **Anthropic model name density**: "Claude Sonnet 4.5, Opus 4.5, Haiku 4.5" used as judges/summarizers — flagged as "uncritical reference to current Anthropic model names" + "tools that postdate when most of these other essays appear to be written" + "consistent with AI generation referencing its own ecosystem". Structural: real models I used. Could be partly anonymised by saying "a frontier LLM" once and the model-card name once but not at every mention.
- **Preface confession still flagged** at seed 1943 as "constructed-authentic" — round-7 trim helped but not enough; the underlying structure (technical-error-as-honesty) reads as performed.
- **"Mausoleo wins on every case tested here. Whether it generalises to a different month or paper is an empirical question I cannot answer from this corpus."** (§7.1) — "characteristic LLM epistemic-hedge cadence".

## 5. Round 8 plan

Per stopping rule, round 8 = final regardless of verdict. Edits should target:

1. **Anonymise model name density** — replace ~half the "Claude Sonnet 4.5" / "Opus 4.5" / "Haiku 4.5" mentions with "a frontier LLM" / "the judge model" / "the summariser" while keeping the methodology section's full disclosure.
2. **Soften §2 closing meta-summary** — drop "Read against one another, these literatures fix the position Mausoleo occupies."
3. **Soften §7.1 hedged-confidence pair** — "Mausoleo wins on every case tested here. Whether it generalises..."
4. **Final pass on remaining "rather than" antithesis** — at this point getting diminishing returns, but worth one more sweep.

## 6. Trajectory

| Round | Seed 1943 | Seed 1944 | Seed 1945 | PASS |
|-------|-----------|-----------|-----------|------|
| 4 | lean toward | lean toward | PASS | 1/3 |
| 5 | near certain | near certain | PASS | 1/3 |
| 6 | near certain | near certain | PASS | 1/3 |
| 7 | near certain | lean toward | PASS | 1/3 |

BEST_GAN candidate: round 4 still has the best FAIL-confidence aggregate; round 7 is second.
