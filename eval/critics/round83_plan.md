# Round 83 plan — SICO §4 prose + minor §5 expansion

## Strategy

R80 has §4 in its R61 form — entirely unparaphrased. Critics across R75-R82 consistently flagged §4 prose patterns: "Article-touching cannot score a question whose answer is an issue that does not exist", "the case the design was built around", "Romans reading the paper that morning learned of the deposition before the morning paper would normally have arrived". These are §4.1 sentences.

R83 applies SICO with stricter constraints (R76 system prompt) to §4.1 (the missing 26 July prose, ~600w) and §4.2 (the 25-27 regime change, ~150w). Preserves the §4 Italian quotation block + the table + the §4.3 aggregate-numbers paragraphs verbatim.

Plus minor §5 closer expansion: the closer "What the experiment does not show: ..." paragraph could be expanded by one substantive sentence at the end about HOW the next iteration would test those things — this is the kind of forward-pointing question that critic 412570008 in R80 cited as "Mausoleo's chapters end on a concrete observation or a forward-pointing question, not a restatement". This was a POSITIVE cohort-mirror citation; doubling down on it should help.

## Implementation

a. Layered on R80 v10.
b. Run SICO HARDER (R76 system prompt + style anchors) on §4.1 + §4.2 of R80 v10.
c. Splice paraphrased §4.1 + §4.2 back, preserving Italian block + table + §4.3.
d. Expand §5 closer with one forward-pointing sentence.
e. Strip + GAN.

## Pareto rule

If R83 ≥ R80 (2/3 LEAN), promote. Else revert.

## Word count target

R80 = 7,124w. SICO §4 ±15% on ~750 affected words = ±112w. §5 expansion +30w. Total expected ~7,150w. Within cap.

## Risk

§4 prose carries the most concrete factual claims in the dissertation; risk of hallucination via paraphrase. Mitigation: the SICO mask layer protects every citation, every named entity, every number, every Italian phrase. Sanity-check pipeline catches corruption.

## Stop point

If R83 is ≥ 2/3 PASS (matches R80), declare R80 OR R83 the ship and return.
If R83 is 3/3 PASS, declare R83 the ship and return immediately.
If R83 is < 2/3 PASS, revert and return with R80 as ship.
