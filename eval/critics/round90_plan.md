# Round 90 plan — Strategy 9: §2 single-chapter reshape (no subsection scaffolding)

## Strategy

Per dispatch's Strategy 9 unexplored option: "Restructure §2 as a SINGLE chapter on 'Reading the corpus' without subsection scaffolding — one continuous prose argument that weaves the three (now two) literatures + corpus context naturally."

Currently §2 has explicit subsection headers ("Existing digitised newspaper archives", "The hierarchical-retrieval lineage", "Memory, hierarchy and external structure"). Multiple critics have flagged this subsection scaffolding as LLM-generated section template. R85 critic 497651923 explicitly cited the chapter headers as STRUCTURAL tell.

R90 removes the 3 subsection headers from §2 and reorders the content so it flows as continuous argument. Same body content, different scaffolding.

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. Drop "### Existing digitised newspaper archives" header.
c. Drop "### The hierarchical-retrieval lineage" header.
d. Drop "### Memory, hierarchy and external structure" header.
e. Adjust paragraph transitions so they flow without subsection breaks.
f. Strip + GAN at 3 fresh non-pos-1 seeds.

## Pareto rule

If R90 ≥ 2/3, promote v10. If R90 = 3/3, ship and STOP. If R90 < 2/3, revert to R80.

## Word count target

R80 = 7,124w. -3 subsection headers = -15w. Maybe minor transitional sentence adjustments. ~7,110w. Within cap.

## Risk

Subsection headers help reader navigation. Dropping them may make §2 read as a single dense block. R85+R86 critics flagged the subsection headers as STRUCTURAL tell, so dropping should help. Risk: a continuous §2 may itself read as auto-generated long-form.
