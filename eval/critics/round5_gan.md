# GAN critic — Phase 3 Stage B, round 5

Run date: 2026-05-03 ~14:50 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v4.md` (round-4 verdict edits applied: "X rather than Y" antithesis softened across ~8 instances, manufactured-personal Preface detail removed, "is what carries the case" / "is the architectural property that drives Case 1" / "is the place this background actually bites the engineering" cadence varied, abstract precision-then-disclaimer rhythm split, §1 declarative chain softened, §7.2 "honest position" / "worried me most" framings softened)
Cohort: 8 BASc 1st-class dissertations under `/tmp/gan_round1/extracted/`
Critic: claude-opus-4-7 via OAuth (`oauth-2025-04-20` beta), single call per seed
Strip script: `/tmp/gan_round5/strip_years.py`
Stripped inputs: `/tmp/gan_round5/stripped/`
Per-seed prompts + raw verdicts: `/tmp/gan_round5/runs/`

## 1. Year-strip verification

Stripped 42 citation-year tags from target (unchanged from round 4); 271 from references (unchanged). Strip uniform across target + 8 refs.

Target main-body word count: 9,427.

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span |
|------|-----------------|---------------|------------|-----------|-----------------------|
| 1943 | 9 | Essay 9 | near certain | FAIL | "compressed parallel clauses with em-dashes setting up tidy contrasts" + "phantom-USD coinage" + "hedged-confidence cadence about its own statistical limits" |
| 1944 | 9 | Essay 9 | near certain | FAIL | "Aphoristic balanced-pair summary sentences" + "Unnaturally dense and uniform cross-referencing" + "with effect sizes large enough to read off the means at the n = 6 sample size even when the sign tests do not clear conventional thresholds" |
| 1945 | 1 | Essay 8 (= 2020FSXD0, a reference) | lean toward | PASS | "Meta-justification of interdisciplinarity in preface" |

## 3. Overall verdict

**FAIL at 2 of 3 positions** (PASS = 1/3, same as rounds 2/3/4).

**REGRESSION on confidence**: rounds 4's "lean toward" at both FAIL seeds returned to "near certain" in round 5. The aggressive Preface cut (removing the manufactured-personal detail entirely, leaving only generic supervisor thanks) appears to have stripped what little human-anchoring the round-4 draft had — and the critic at seed 1944 explicitly cites this: "the preface lacks the personal texture of the others (compare to Essay 6's Brussels anecdote or Essay 4's internship story); it reads as a structural recap rather than personal reflection."

The "X rather than Y" softening neutralised that specific tic, but in dropping the anchoring + the precision-hedge combination's protective value, it exposed the underlying balanced-clause cadence (semicolon-bridged antithesis, dense cross-references) which the critic now reads as the dominant tell.

The PASS pick at seed 1945 also shifted — round 4 picked 2022RDBR1 (Sartre/Arendt confabulations), round 5 picks 2020FSXD0 (Kant essay) for "meta-justification of interdisciplinarity in preface". Position 1 is reading the target's now-too-bare Preface positively but only by comparison.

## 4. Tells flagged in round 5

### Seed 1943 (target = Essay 9)
- "Compressed parallel clauses with em-dashes setting up tidy contrasts" — semicolon-balanced antithesis pattern: "The cost is the loss of latent thematic structure that cuts across time; the embedding-search endpoint (§3.3) partially recovers it" / "Tree traversal supplies provenance and chronological position; semantic search is the escape hatch when chronology is the wrong axis."
- "Phantom-USD coinage" — flagged as "fabricated specificity" (this is a real artefact of the OAuth quota system but reads odd).
- "Hedged-confidence cadence about its own statistical limits" — "with effect sizes large enough to read off the means at the n = 6 sample size even when the sign tests do not clear conventional thresholds."

### Seed 1944 (target = Essay 9)
- "Unnaturally dense and uniform cross-referencing" — "§7.3 returns to the design choice", "§6.2 picks up the absent-day node from there", "§5.3 quantifies this on the 25 July trace" — far more systematic than human dissertation prose.
- "Aphoristic balanced-pair summary sentences" — "The cost is the loss of latent thematic structure that cuts across time; the embedding-search endpoint (§3.3) partially recovers it" — same pattern as seed 1943.
- "Mausoleo's contribution to this lineage is the choice not to induce" — "aphoristic, self-referential summary sentences are a strong AI tell."
- **Preface lacks personal texture** — the round 4-to-5 cut overshot.

## 5. Recommended next-round edits

Per stopping rule, round 6 should branch from BEST_GAN prior (round 4's v3, since rounds 2/3/4/5 all 1/3 PASS but round 4 had the softest FAIL confidences). Round 6 needs to:

1. **Re-add a personal-grounding anchor to the Preface** — but make it less polished than the round-4 version. Critic explicitly noticed lack of personal texture at both seeds in round 5.
2. **Vary the semicolon-balanced antithesis cadence** — break ~6 instances of "X is Y; Z is W" balanced clauses across §3.2, §3.3, §7.3.
3. **Soften the abstract's "n = 6 ... do not clear conventional thresholds" hedged-precision phrase** — this was added in round 4 specifically for technical-register fit but reads as the canonical LLM tic.
4. **Reduce cross-reference density** — drop ~3-4 of the ~8 explicit "§N.M does X" forward/back references; let context do the work.
5. **Replace "phantom-USD"** with a less coined-feeling phrasing.

## 6. Trajectory note

| Round | Seed 1943 | Seed 1944 | Seed 1945 | Net PASS |
|-------|-----------|-----------|-----------|----------|
| 2 | lean toward FAIL | near certain FAIL | PASS | 1/3 |
| 3 | near certain FAIL | near certain FAIL | PASS | 1/3 |
| 4 | lean toward FAIL | lean toward FAIL | PASS | 1/3 |
| 5 | near certain FAIL | near certain FAIL | PASS | 1/3 |

Round 4 remains BEST_GAN. Branch round 6 from v3.
