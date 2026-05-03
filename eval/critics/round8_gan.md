# GAN critic — Phase 3 Stage B, round 8 (FINAL)

Run date: 2026-05-03 ~15:50 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v7.md` (round-7 verdict edits applied: model name density reduced in §3.2/§6.5 with full disclosure preserved at §6.1, §2 closing meta-summary varied, §7.1 hedged-confidence pair softened, ~6 more "rather than" antithesis instances varied)
Cohort: 8 BASc 1st-class dissertations
Critic: claude-opus-4-7 via OAuth
Strip: `/tmp/gan_round8/strip_years.py`; stripped: `/tmp/gan_round8/stripped/`; runs: `/tmp/gan_round8/runs/`

## 1. Year-strip verification

42 target / 271 ref tags stripped, uniform across 9 essays. Target main-body: 9,450w.

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span |
|------|-----------------|---------------|------------|-----------|-----------------------|
| 1943 | 9 | Essay 9 | lean toward | FAIL | "Formulaic result-then-hedge construction" + "Performatively tidy limitations confession" + "Too-neat preface self-positioning" |
| 1944 | 9 | Essay 9 | near certain | FAIL | "Triadic parallel constructions saturating exposition" + "Calibrated self-hedging on own results" + "Copular thesis-restatement tic" |
| 1945 | 1 | Essay 6 (= 2022RDBR1, a reference) | lean toward | PASS | "Textbook/encyclopedia opener" + "Confident misattribution to Arendt" |

## 3. Overall verdict

**FAIL at 2 of 3 positions, PASS = 1/3.**

Seed 1943 dropped near-certain → lean-toward (gain), seed 1944 stayed/slipped to near-certain (round-7 had lean-toward at 1944). So round 8 trades confidence between the two FAIL seeds without changing net PASS count.

**Final BEST_GAN: round 4** (v3) — only round with both FAIL seeds at "lean toward". All other rounds had at least one "near certain" FAIL seed.

## 4. Final tells flagged in round 8

### Seed 1943 (lean toward)
- "Formulaic result-then-hedge construction" — "The mean differences are visible at the n = 6 sample size even where the sign tests fall short of conventional thresholds."
- "Performatively tidy limitations confession" — §7.2 limitations list reads as AI compliance.
- "Too-neat preface self-positioning" — round-7's still-trimmed preface still flagged as "lacking the lived specificity of genuine student prefaces".
- "Numbers feel manufactured" — `~29.7 GPU-hours`, `$29 USD-equivalent`, `76.7 s wall`, `κ = 0.14` — uniform precision across very different metric types reads as fabricated.

### Seed 1944 (near certain)
- "Triadic parallel constructions" — RAPTOR/GraphRAG/Mausoleo three-beat in §3.2 (and §1, §2.2): structurally hard to remove without changing the substantive comparison.
- "Calibrated self-hedging on own results" — same phrase family as seed 1943.
- "Copular thesis-restatement tic" — "The missing-data case is architectural" / "The architectural point is what the case turns on" — short declaratives that summarise the preceding paragraph.
- "Implausibly tidy citation integration" — uniform "Author et al. (year)" rhythm across §2.2 lit review.

## 5. Cross-round summary

| Round | Seed 1943 | Seed 1944 | Seed 1945 | PASS | Notes |
|-------|-----------|-----------|-----------|------|-------|
| 2 | lean toward FAIL | near certain FAIL | PASS | 1/3 | baseline v2 |
| 3 | near certain FAIL | near certain FAIL | PASS | 1/3 | cohort-fit edits regressed seed 1943 |
| 4 | lean toward FAIL | lean toward FAIL | PASS | 1/3 | **BEST_GAN — both FAILs softened to lean toward** |
| 5 | near certain FAIL | near certain FAIL | PASS | 1/3 | preface cut overshot, regressed both seeds |
| 6 | near certain FAIL | near certain FAIL | PASS | 1/3 | preface re-anchor helped PASS-position only |
| 7 | near certain FAIL | lean toward FAIL | PASS | 1/3 | partial recovery on seed 1944 |
| 8 | lean toward FAIL | near certain FAIL | PASS | 1/3 | confidence trades between seeds |

PASS-position critic at seed 1945 picked Essay 6 (= 2022RDBR1) in 5 of 7 rounds and Essay 8 / Essay 2 once each — strong position-1 effect dominated by the reference essays' visible factual confabulations.

## 6. Final BEST_GAN

**Round 4 / v3** — `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v3.md` — 9,505 main-body words.

Reasons:
- Both FAIL seeds at "lean toward" (no other round achieved this).
- Lean-technical shift fully executed (abstract + §1 opening + §6.2 reframing + §7.3 historiography-as-background).
- Round-3 verdict tells fixed (Braudelian-triad refrain broken, aphoristic single-sentence paragraphs cut, malformed bibliography normalised).
- Carried fewer second-order tells than rounds 5/6/7/8 (the round-5 Preface cut + later re-anchors introduced new "manufactured authenticity" tells that subsequent rounds couldn't fully remove).

Recommended next move: Stage C plagiarism / citation / coherence reviewers on round 4 v3, since GAN convergence has plateaued at 1/3 PASS across 7 rounds with diminishing marginal returns and it is unlikely an 11th-hour 9th round at the same wall-clock budget would clear 3/3.
