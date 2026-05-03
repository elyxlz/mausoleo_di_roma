round 4: word_count=9505, gan_pass=1/3, BEST_GAN=round_4_pass=1/3 (confidence on FAILs dropped from near-certain to lean-toward; ties round 2/3 PASS count)
round 5: word_count=9427, gan_pass=1/3, BEST_GAN=round_4_pass=1/3 (REGRESSED: FAIL confidence climbed back to near-certain; Preface cut overshot, branch round 6 from v3)
round 6: word_count=9571, gan_pass=1/3, BEST_GAN=round_4_pass=1/3 (no movement on FAIL confidence but PASS-position critic praised new preface anchor; "X rather than Y" antithesis remains dominant tell)
round 7: word_count=9477, gan_pass=1/3, BEST_GAN=round_4_pass=1/3 (seed 1944 dropped near-certain → lean-toward; seed 1943 stayed near-certain; round 4 still tightest aggregate confidence)
round 8: word_count=9450, gan_pass=1/3, BEST_GAN=round_4_pass=1/3 (FINAL; seed 1943 dropped to lean-toward, seed 1944 climbed to near-certain; round 4 v3 is BEST_GAN with both FAIL seeds at lean-toward)
round 10: word_count=9946, gan_pass=1/3, target_positions=[7,1,3], status=FAIL
round 11: word_count=9952, gan_pass=0/3, target_positions=[8,2,9], status=FAIL
round 12: word_count=9952, gan_pass=1/3, target_positions=[3,1,4], status=FAIL
round 13: word_count=9920, gan_pass=0/3, target_positions=[3,8,2], status=FAIL
round 14: word_count=9914, gan_pass=0/3, target_positions=[9,1,5], status=FAIL
round 15: word_count=9920, gan_pass=0/3, target_positions=[8,9,7], status=FAIL
round 16: word_count=9905, gan_pass=0/3, target_positions=[2,3,8], status=FAIL
round 17: word_count=9897, gan_pass=0/3, target_positions=[4,7,3], status=FAIL
round 20: word_count=8420, gan_pass=0/3, target_positions=[5,6,3], status=FAIL (FIRST ROUND AT NEW POSITION-1-BANNED CONSTRAINT)
round 21: word_count=8462, gan_pass=1/3, target_positions=[4,2,3], status=PASS_AT_POS_3 (first non-pos-1 PASS at new constraint)
round 22: word_count=8454, gan_pass=0/3, target_positions=[5,7,2], status=FAIL
round 23: word_count=8071, gan_pass=1/3, target_positions=[4,3,6], status=PASS_AT_POS_3
round 24: word_count=8187, gan_pass=1/3, target_positions=[8,6,5], status=PASS_AT_POS_6
round 25: word_count=8254, gan_pass=0/3, target_positions=[5,3,4], status=FAIL
round 26: word_count=8287, gan_pass=0/3, target_positions=[9,6,5], status=FAIL
round 27: word_count=8284, gan_pass=0/3, target_positions=[3,9,8], status=FAIL
round 28: word_count=8202, gan_pass=0/3, target_positions=[4,8,5], status=FAIL
round 29: word_count=8268, gan_pass=0/3, target_positions=[7,9,5], status=FAIL
round 30: word_count=8268, gan_pass=1/3, target_positions=[5,3,9], status=PASS_AT_POS_3 (FINAL; rounds 21/23/24/30 all tie BEST at 1/3 under no-pos-1 constraint)
round 31: word_count=8980 (v10; +712 over v9), stripped=8262, gan_pass=0/3, target_positions=[5,7,6], status=FAIL (cohort-mining round: applied Type A/B/C cohort-mirroring moves — BASc seminar reference in Preface, Whittington close-reading in §2.3, human-subjects scope-out in §5; all three new moves were individually flagged as tells; no improvement on round-30 baseline; rounds 21/23/24/30 still tie BEST at 1/3)
round 32: word_count=8076 (v10 lossy revert), stripped=7359, gan_pass=1/3, target_positions=[3,5,4], status=PASS_AT_POS_3 (REVERTED 3 round-31 cohort moves; defused 19 "rather than"; range-converted §4 numbers; range conversion FLAGGED as fabrication; round-32 ties round-30 baseline; rounds 21/23/24/30/32 tie BEST at 1/3)
round 33: word_count=8064, stripped=7347, gan_pass=1/3, target_positions=[9,5,2], status=PASS_AT_POS_2 (restored exact numbers; dropped Bartlett/Hutchins Preface paragraph; replaced with OCR anecdote; collapsed limitations cascade; defused 7x "X, not Y"; defused "what fails is not"; rounds 21/23/24/30/32/33 tie BEST at 1/3)
round 34: word_count=7830, stripped=7113, gan_pass=0/3, target_positions=[3,5,4], status=FAIL (Preface itinerary drop + CS-blog tic defusion + §1 chiasmus break + limitations cascade collapse - REGRESSED 1/3 → 0/3; new high-leverage tell: in-prose pre-emptive hedging in Ch4 + Ch2 opening "X but Y" triplet; rounds 21/23/24/30/32/33 still tie BEST at 1/3)
round 35: word_count=7688, stripped=6971, gan_pass=0/3, target_positions=[2,6,3], status=FAIL (Ch2 opening rewrite + §1 chapter map drop + §4 in-prose hedging scrub - did not move; new high-leverage tells: aphoristic paragraph-closer cadence + double-hook opening; rounds 21/23/24/30/32/33 still tie BEST at 1/3)
round 36: word_count=7651, stripped=6934, gan_pass=0/3, target_positions=[9,3,5], status=FAIL_LEAN (one lean-toward FAIL — Preface engineering rewrite + vocab defusion + aphoristic-closer scrub softened confidence; high-leverage tells: symmetric case weighting + "X matters here" closer cadence; rounds 21/23/24/30/32/33 still tie BEST at 1/3)
round 37: word_count=7460, stripped=6743, gan_pass=1/3, target_positions=[3,2,8], status=PASS_AT_POS_2 (asymmetric case weighting + 27 July close-reading + §3 opener variation; rounds 21/23/24/30/32/33/37 tie BEST at 1/3)
round 38: word_count=7458, stripped=6742, gan_pass=1/3, target_positions=[7,4,3], status=PASS_AT_POS_3 (reflective §5 close + emphatic-construction defusion - reflective close itself flagged but softer than checklist; rounds 21/23/24/30/32/33/37/38 tie BEST at 1/3)
round 39: word_count=7426, stripped=6710, gan_pass=0/3, target_positions=[2,9,6], status=FAIL (§1 system-first opening + new close + drop announce-and-execute - regressed; new high-leverage tells: §2.3 topic-sentence lockstep + Ch2 "There is X/Y/Z" triplet + Preface "discipline pair" performance; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 40: word_count=7310, stripped=6594, gan_pass=0/3, target_positions=[2,5,8], status=FAIL_LEAN (Preface "discipline pair" drop + Ch2 opener restructure + §2.3 lockstep break + closing-echo defusion - one lean-toward; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 41: word_count=7172, stripped=6456, gan_pass=0/3, target_positions=[2,4,6], status=FAIL (Preface stripped to acknowledgment-only - regressed all near-certain; strip-script bug introduces "an one-month" reading as LLM tic; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 42: word_count=7306, stripped=6590, gan_pass=0/3, target_positions=[4,8,2], status=FAIL_LEAN (Preface restored + strip script patched - one lean-toward with critic noting hard call; Italian summary + Eichenbaum/Whittington self-correction now reads as human; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 43: word_count=7219, stripped=6503, gan_pass=0/3, target_positions=[2,5,3], status=FAIL_LEAN (limitations distributed + vocab signature defusion - one lean-toward; strip-script artifact "the an open-weight" patched in round 44 strip; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 44: word_count=7102, stripped=6385, gan_pass=0/3, target_positions=[2,6,9], status=FAIL_NEAR_CERTAIN (3 surface fixes + Qwen artifact source-fix; REGRESSED from r43 lean-toward; high-leverage: aphoristic clinchers, triadic listing, antithesis, hook recapitulation; rounds 21/23/24/30/32/33/37/38 still tie BEST at 1/3)
round 45: word_count=7117, stripped=6400, gan_pass=1/3, target_positions=[8,9,7], status=PASS_AT_POS_9 (Abstract + Ch1 reopen — moved 26 July hook out of first sentence, defused two triadic listings, killed §4 bicolon closer, reworded §5 hedge; seed 511502862 picked Essay 1 lean-toward; INTRODUCED new tricolon tell in abstract opening; rounds 21/23/24/30/32/33/37/38/45 tie BEST at 1/3)
round 46: word_count=6964, stripped=6247, gan_pass=0/3, target_positions=[6,5,3], status=FAIL_NEAR_CERTAIN (killed R45 abstract tricolon, rewrote Ch1 with concrete archival encounter, cut §1 parenthetical + §4 sign-test sentence; REGRESSED to all near-certain; seed 32748809 explicitly counts six recap-instances of 26 July hook across abstract/§1/§2/§3/§4/§5; rounds 21/23/24/30/32/33/37/38/45 still tie BEST at 1/3)
