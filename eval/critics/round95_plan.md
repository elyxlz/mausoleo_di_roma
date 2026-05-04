# Round 95 plan — STRATEGY A2: abstract-noun-subject scrub on best-on-A1 base (single-axis)

## Strategy

Per fresh dispatch STRATEGY A2: replace abstract-noun grammatical subjects with concrete agent subjects: "the system shows" → "we observed"; "the argument indicates" → "the case-3 trace indicates"; "the analysis reveals" → "[concrete subject]". Keep all other prose intact (no antithesis fixes added beyond R94's, no hedging delete, no opener rewrite).

## Branch

If R94 ≥ 2/3: branch from R94 (keep R94 antithesis edits + add A2 scrub).
If R94 < R80: branch from R80 baseline (commit 9ff974e), apply A2 only.

## Implementation

a. Identify every paragraph subject that is an abstract noun ("the argument", "the framework", "the system", "the analysis", "the index", "the architecture", "the comparison", "the experiment", "the results", "the evidence", "the framing", "the literature", "the lineage").
b. Where it can be rewritten with a concrete agent (we, the agent, the trace, the case-N data, the spot-check, Mausoleo, the historian) without distorting meaning, do so.
c. Preserve technical exposition where the abstract noun IS the agent (e.g. "the index holds" describing the data structure).

## Pareto rule

Same as R94. ≥ 2/3 = save as BEST_AXIS_A2. Otherwise revert to branching baseline.
