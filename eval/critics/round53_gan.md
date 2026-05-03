# GAN Round 53

Strip: TARGET 6,140 words (after R53 edits, before revert). v10 was 7,035 words.
Seeds: 445553435 (pos 3), 907617731 (pos 7), 790334867 (pos 4).

Edits applied (per round53_plan.md, BEFORE the revert):
- Defused §2.3 four-beat enumeration: dropped "and they are worth taking in turn" + "Take hierarchical memory first" + "A second strand concerns chunking" + "On the neural side the recent work shows" + "Cognitive-offloading work then closes the picture". Each opener replaced with non-discourse-marker phrasing.
- Deleted Ch5 mid-paragraph hedge "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested" (the source of R52's duplicate-hedge tell).
- Re-applied R52's tripartite-enumeration scrubs: Ch2 heading, §2.1 opener, abstract "Three questions", Ch1 closer "Three case studies", Ch3 opener "Three loosely coupled stages".
- Did NOT touch R51 §4 closer or R51 Ch5 closer.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 445553435 | 3 | 3 (TARGET) | near certain | FAIL |
| 907617731 | 7 | 7 (TARGET) | near certain | FAIL |
| 790334867 | 4 | 4 (TARGET) | near certain | FAIL |

Result: 0/3 PASS, all near-certain. REGRESSED from R51's 1/3 lean-toward PASS.

PER PARETO RULE: REVERTED v10 to R51 snapshot (commit 967807f). Round 54 will branch from R51 baseline with a DIFFERENT move class (excluding §2.3 enumeration scrubs and tripartite-enumeration scrubs that landed flat in R53).

## Why R53 regressed

The §2.3 enumeration scrub did not register as a confidence move; the duplicate-hedge fix removed the duplicate but the surviving Ch5 closer "An editorial silence in a regime-aligned daily..." was flagged AGAIN by ALL THREE seeds as the canonical aphoristic-closer tell:
- Seed 445553435: "*An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it... These elevated single-sentence summary lines are an LLM tic.*"
- Seed 907617731: "*An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it... These aphoristic single-sentence paragraph-enders are an LLM tell.*"
- Seed 790334867: "*An editorial silence in a regime-aligned daily during a regime change is part of what the source records, and the catalogue needs a place to put it... The other dissertations close sections with workmanlike summaries, not curated maxims.*"

This is the SAME closer that R51 kept (and R51 PASSED 1/3). The R51 PASS critic happened to be a cohort-mirror; the actual closer-tell signal has been consistent across many rounds.

Other consistent high-leverage tells (in common across all R53 FAILs and R51 FAILs):
- Balanced antithesis / paired-clause cadence — saturating
- Pre-emptive thesis-restatement at chapter boundaries (NEW formulation: "Each chapter opens with a meta-claim that telegraphs what the chapter will demonstrate")
- Aphoristic single-sentence section closers
- "X holds Y" / "X carries Y" abstract-noun-as-agent construction
- Branded term "calendar-shaped" / "calendar-given" recurring as trademark

## Round 54 plan (PRELIMINARY)

R51 baseline. Excluded moves: §2.3 enumeration scrubs (R53), tripartite-enumeration scrubs (R53, R52), Ch5 closer rewrite (R52 duplicate-hedge), Preface roughness adds (R50).

NEW high-leverage tell to target (NOT touched in any prior round): "**pre-emptive thesis-restatement at chapter boundaries**" — *"The case studies in this chapter ask whether the architectural argument of chapter three makes a measurable difference for a researcher trying to answer real questions about July 1943"* (Ch4 opener) + *"The literatures the system needs to be read against are several"* (Ch2 opener) + similar at Ch3, Ch5.

PRIMARY for R54: defuse the chapter-opening meta-claim pattern at TWO chapter openers (Ch4 + Ch2). Drop the "the case studies in this chapter ask whether..." and the "the literatures the system needs to be read against are several" — replace with in-medias-res factual openers.

SECONDARY: defuse the Ch5 final closer "An editorial silence in a regime-aligned daily..." but WITHOUT the R52 duplicate-hedge mistake. Replace with a flat factual sentence about Murialdi-style follow-up rather than another hedge.

EXCLUDE: do NOT add new content; do NOT modify §2.3 again; do NOT touch Preface.
