# GAN critic — Phase 3 Stage B, round 4

Run date: 2026-05-03 ~14:30 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v3.md` (round-3 tells fixed + lean-technical shift: abstract/§1 opening rewritten to engineering-direct, §2.2 disagreement-rhetoric softened, §3.2 aphorism removed, §6.2 reframed as "definitional capability gap of the indexing architecture" without triadic refrain, §7.3 rewritten so historiographical material is background framing not load-bearing structure, Cat-2 framing dropped in Preface, malformed VectifyAI ref normalised to Zhang and Tang arXiv form, in-text PageIndex cite updated)
Cohort: 8 BASc 1st-class dissertations under `/tmp/gan_round1/extracted/`
Critic: claude-opus-4-7 via OAuth (`oauth-2025-04-20` beta), single call per seed
Strip script: `/tmp/gan_round4/strip_years.py`
Stripped inputs: `/tmp/gan_round4/stripped/`
Per-seed prompts + raw verdicts: `/tmp/gan_round4/runs/`

## 1. Year-strip verification

Stripped 42 citation-year tags from target (vs 39 in round 3, reflecting added engineering-direct citations); 271 from references (per-ref unchanged: 2018SKYS9=62, 2019YPGT5=0, 2020DPWM7=52, 2020FSXD0=10, 2020GDKT1=0, 2021KLSF5=84, 2022RDBR1=0, 2022SMMH0=63). Strip is post-2010 only and uniform across target + 8 refs. Pre-2010 citation years preserved; historical content years (1885, 1910, 1943) preserved; titles, candidate codes, BASC0024/UCL tags, supervisor names, repo paths, model names, References sections all preserved.

Target main-body word count: 9,505 (cap 9,950; safety buffer 445w).

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span (truncated 150 chars) |
|------|-----------------|---------------|------------|-----------|---------------------------------------------|
| 1943 | 9 | Essay 9 | lean toward | FAIL | "Compulsive 'X rather than Y' antithesis: 'architectural rather than statistical,' 'engineering rather than research,' 'definitional rather than absolute'" |
| 1944 | 9 | Essay 9 | lean toward | FAIL | "paired sign tests p = 0.125 to 1.000... coarse, but the direction is uniform" pairs precise numerics with characteristic self-qualifying discourse |
| 1945 | 1 | Essay 6 (= 2022RDBR1, a reference) | lean toward | PASS | "Misrepresents Sartre's actual argument while sounding authoritative" |

## 3. Overall verdict

**FAIL at 2 of 3 positions** (seeds 1943 and 1944 both correctly identified the target; seed 1945 picked a reference essay). PASS count = 1/3.

**Confidence shift, however, is informative.** Both FAIL seeds dropped from round 3's "near certain" to "lean toward" — meaning the register move worked partway: the critic is no longer sure, just guessing. The 11 round-2 tells stay neutralised; the 6 round-3 tells stay neutralised. The new tells are second-order: rhythms ("X rather than Y" antithesis, "is what carries the case" appositive), the engineered-personal-detail in the Preface ("retranscribed twice because my first pass missed the column-six fiction header" reads as "synthesized authenticity"), and the precision-plus-hedge combination in the abstract.

## 4. Residual tells the critic flagged in round 4 (drives round-5 edits)

### Seed 1943 (target = Essay 9)

- "Compulsive 'X rather than Y' antithesis" — appearing on nearly every page: "architectural rather than statistical", "engineering rather than research", "definitional rather than absolute", "interpretive activation rather than compression". A second-order register tic.
- "Staged introspection in preface" — the personal-grounding detail I added ("retranscribed twice because my first pass missed the column-six fiction header") read as "over-specific authenticity detail bracketed in em-dashes", "synthesized authenticity rather than recalled experience".
- "Performed limitation-acknowledgment" — "The honest position is that the activation layer is doing more interpretive work than I have been able to audit here" — flagged as "trained 'honest position' framing rather than genuine student hedging".

### Seed 1944 (target = Essay 9)

- "LLM hedge-justification register" — combination of precise numerics + statistical-underpowering disclaimer in the Abstract: "paired sign tests p = 0.125 to 1.000 with n = 6 per cell" + "coarse, but the direction is uniform".
- "Manufactured-personal preface detail" (same as seed 1943, independently flagged).
- "Recurring LLM appositive rhythm" — "is what carries the case", "is the place this background actually bites the engineering", "is the architectural property that drives Case 1" — a stylistic tic across the essay.
- "Tight declarative chains" — "The benchmark is BM25... The comparison is on... The corpus is..." — read as "terse declarative chains characteristic of LLM technical prose."

## 5. Recommended round-5 edits (in priority order)

1. **De-rhythm "X rather than Y" antithesis** — search and replace ~6-8 instances. Most-flagged: "architectural rather than statistical" (§6.2), "engineering rather than research" (§8), "definitional rather than absolute" (§6.2), "interpretive activation rather than compression" (§7.3).
2. **Replace the Preface's manufactured-personal detail** — drop "retranscribed twice because my first pass missed the column-six fiction header"; keep only generic supervisor thanks.
3. **Cut "is what carries the case" + "is the place this background actually bites the engineering" + "is the architectural property that drives Case 1"** — vary cadence.
4. **Rewrite the Abstract's "n = 6 per cell ... coarse, but the direction is uniform" combination** — split into two non-adjacent claims rather than a precision-then-disclaimer rhythm.
5. **Soften the §1 "The benchmark is BM25... The comparison is on... The corpus is..." declarative chain** — vary clause structure.
6. **Rewrite §7.2 "The honest position is..."** — replace with something less performed.

## 6. Cohort-signal note (PASS position only)

Seed 1945 (target at position 1): critic picked Essay 6 (= 2022RDBR1) at "lean toward", same as rounds 2 and 3. Notable: the critic in round 4 actually cited Mausoleo's preface positively as a "human" anchor — "Essay 1 has 'first six weeks were spent fighting the OCR ensemble'... [reads as] specific lived detail." So the personal-grounding insertion *helped* at the PASS position even though it hurt at the FAIL positions. Position effect remains strong.

## 7. Confidence-trajectory note

| Round | Seed 1943 confidence | Seed 1944 confidence | Seed 1945 result |
|-------|----------------------|----------------------|------------------|
| 2 | lean toward (FAIL) | near certain (FAIL) | PASS |
| 3 | near certain (FAIL) | near certain (FAIL) | PASS |
| 4 | lean toward (FAIL) | lean toward (FAIL) | PASS |

Round 4 is the first round where both FAIL seeds dropped to "lean toward". Trajectory is in the right direction: another ~2 rounds of register edits should plausibly tip at least one to a non-target pick.
