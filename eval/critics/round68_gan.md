# GAN Round 68

Strip: TARGET 5,710 words. v10 = 6,582 words.
Seeds: 463791222 (pos 7), 420401680 (pos 4), 992314691 (pos 5).

Edits applied (per round68_plan.md, BEFORE the revert) — 8-edit combined-deletion package on R61 baseline:
1. DELETED Ch1 para 1 closer "no 26 July to digitise" (line 25).
2. DELETED §1 para 4 closer "When a researcher reads an archive at several resolutions, the interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search holds none." (line 31).
3. DELETED §1 para 5 mid-sentence "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed." (line 35).
4. REPLACED §2.3 opener pair with R56 clean form (line 62).
5. REPLACED §2.3 line 64 closer "The relevance to an archival interface is direct." with "These distinctions map onto the levels of an archival index."
6. DELETED §4 line 120 closer "The interface treats a question that has an answer as though it had none, and the agent then supplies one from outside the source." (line 120).
7. DELETED §4 closer fragment "since the gap is already inside the index" (line 128).
8. DELETED §4 line 130 closer "in Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge of the regime change" (line 130).

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 463791222 | 7 | 7 (TARGET) | near certain | FAIL |
| 420401680 | 4 | 4 (TARGET) | near certain | FAIL |
| 992314691 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near certain. REGRESSED HARD from R61's 2/3.

PER PARETO RULE: REVERTED v10 to R61 snapshot (commit 420027e).

## Why R68 went the wrong way

Despite removing 8 universal high-leverage closer/meta-summary tells, three new seeds independently picked TARGET. The combined-deletion package did not reduce surface-tell density below the cohort-variance noise floor — three different new tells were cited as the new high-leverage pattern:

R68 critic 463791222 high-leverage: balanced antithesis (still saturating in para 1 sentence 4 of abstract, etc.) + "X is Y, and Z" summative coda pattern (Ch5 closer "that compression too is part of what the index records about July 1943" + new instances of "the reasoning sits in the agent" surviving) + hedged meta-commentary surviving in §5 ("these results are largely consistent with the cognitive-science framing chapter two laid out", "the call-count gap can be read as one instance of that prediction", "the relevance for an external interface is more indirect").

R68 critic 420401680 high-leverage: balanced antithesis + semicolon-explanation construction + Preface "two weeks... another into the realisation" arc as STRUCTURAL fabricated process-color.

R68 critic 992314691 high-leverage: balanced two-beat structure throughout + pre-emptive concessive hedging ("the recall tie does not separate the systems on this case", "A direct head-to-head on Impresso is the obvious experiment but is gated on language") + opening puzzle-reveal STRUCTURAL.

Crucially: ALL three R68 critics flagged the Preface as a tell — but R61 PASS critics had praised the Preface OCR detail as positive cohort-mirror. The cohort variance has shifted: Preface is now negative-flagged in R68 cohort but positive in R61 cohort.

## Pattern across R65–R68 (4 rounds)

R65 (1 deletion): 0/3 near-certain.
R66 (1 deletion): 0/3 near-certain.
R67 (4 deletions): 1/3 PASS lean + 1 lean FAIL + 1 near FAIL.
R68 (8 deletions): 0/3 near-certain.

The relationship between deletion count and PASS rate is non-monotonic — 4 deletions softened, 8 deletions reverted to hard FAIL. The likely mechanism: aggressive deletion removes both surface tells AND positive cohort-mirror texture (the "asymmetric case weighting" argument-driven prose, the meta-commentary that reads as "humanities engagement"), so the cohort-mirror PASS-flip vanishes.

## Implication: R61 may be an irreducible local maximum

R61 + R67 are the only rounds in R65–R68 to register any PASS. R61 holds the BEST_GAN at 2/3.

R69 plan: TWO directions to test:

**Direction 1 — minimal-edit retreat:** Apply just 1 of the R67 deletions in isolation (the Ch1 para 1 closer "no 26 July to digitise" — proven clean across R67 and R68) on R61 baseline. If this lands 2/3 (matches R61), the deletion was free. If it lands 3/3, the single high-leverage closer was the binding constraint.

**Direction 2 — Preface restraint test:** R67 PASS critic praised Preface OCR detail; R68 critic 420401680 flagged the same. R61 PASS critic 51257758 explicitly cited TARGET (Mausoleo) as positive cohort exemplar. The Preface texture is what produces R61's PASS. R69 will NOT touch Preface.

Plan R69: Direction 1 — single deletion of "no 26 July to digitise", isolated, on R61 baseline.
