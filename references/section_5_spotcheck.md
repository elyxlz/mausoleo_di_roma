# §5.3 Quality assessment — spot-check artefact

Source data: `eval/section_5_spotcheck.json`. Generation script:
`scripts/section_5_spotcheck.py`. Model: `claude-sonnet-4-5-20250929` over
the OAuth subscription path (`~/.claude/.credentials.json`,
`anthropic-beta: oauth-2025-04-20`). Run date: 2026-05-03.

## 1. Random spot-check on 10 day summaries

Sampling protocol: `random.Random(1943).sample([d for d in range(1,32) if d != 26], 10)` —
deterministic, excludes the absent-day node `1943-07-26` (analysed separately
in §6.2). For each day, the day summary is read, Claude extracts the top-5
named entities (people / places / organisations) ranked by salience, and each
entity is checked for presence in that day's hand-cleaned transcription
(`eval/transcriptions/{date}.json`) via accent-stripped, case-folded
substring match. A token-level fallback admits long-token partial hits
(`Cardinale Marchetti Selvaggiani` matches via `cardinale`).

Verdict per day: `PASS` ≥ 4/5 entities recovered, `PARTIAL` 2-3/5, `FAIL` ≤1/5.

| Date | Top-5 entities (PERSON / PLACE / ORG) | Hits | Verdict |
|---|---|---:|:---:|
| 1943-07-02 | Palermo, Roosevelt, Quartier Generale, Sicilia, Senato USA | 5/5 | PASS |
| 1943-07-08 | Mussolini, Palermo, Sicilia, Comitato Corporativo Centrale, Catania | 5/5 | PASS |
| 1943-07-12 | Sicilia, Alessandro Pavolini, Mussolini, Roma, Inghilterra | 5/5 | PASS |
| 1943-07-13 | Sicilia, Enrico Francisci, Achille d'Havet, Quartier Generale FFAA, Bjelgorod | 5/5 | PASS |
| 1943-07-16 | Sicilia, Napoli, Torino, Hermann Goering, Conte di Torino | 5/5 | PASS |
| 1943-07-19 | Sicilia, Napoli, Carlo Scorza, Roosevelt, Churchill | 5/5 | PASS |
| 1943-07-20 | Papa Pio XII\*, Roma, Basilica di San Lorenzo fuori le mura, Sicilia, Armata Rossa | 4/5 | PASS |
| 1943-07-22 | Pio XII, Roma, Basilica di San Lorenzo, Sicilia, Cardinale Marchetti Selvaggiani | 5/5 | PASS |
| 1943-07-23 | Roma, Sicilia, Mussolini, Hitler, Papa Pio XII\* | 4/5 | PASS |
| 1943-07-28 | Badoglio, Roma, Sicilia, Mussolini, Casa Savoia | 5/5 | PASS |

\* Both `MISS` items are `Papa Pio XII` — the press uses `Pio XII` /
`il Pontefice`, never the prefix `Papa`. The summariser added an editorial
honorific; an entity-resolution check (vs. surface-substring) would flip
both to hits.

**Aggregate (10 days, 50 entities)**: **10 PASS / 0 PARTIAL / 0 FAIL**;
48/50 entities recovered, 2 misses are the `Papa Pio XII` honorific.
Day-level summarisation faithfully preserves the most salient named
entities in the hand-cleaned source.

## 2. Information loss across levels

Day picked: `1943-07-03` (`random.Random(1944).choice(...)`, excluding the
10 spot-check days). Procedure: take the 3 longest article-level summary
JSONs for that day, extract every named entity from each *transcription*
(not the article summary — we want the article-level ground-truth pool),
union them, then check for presence at day / week / month level by
extracting NER on those summaries and intersecting normalised surface forms.

Top 3 articles (by article-summary length, all 3 ≥ 2200 chars):
- `1943-07-03_a097` — *Servizio del lavoro* mobilisation order (15 ORGs)
- `1943-07-03_a022` — Pacific (Rendova) bulletin + agricultural-administration article (10 PLACEs, 2 PERSONs, 5 ORGs)
- `1943-07-03_a006` — front-page editorial on Allied bombings, Lisbon press digest, fronts overview (4 PLACEs, 3 PERSONs, 5 ORGs)

Article-level NER union: **36 distinct entities**.

| Level | Distinct article-level entities still present | % of article-level |
|---|---:|---:|
| Article (top 3, union) | 36 | 100.0% |
| Day (`1943-07-03`) | 7 | 19.4% |
| Week (`1943-W26-tail`) | 6 | 16.7% |
| Month (`1943-07`) | 1 | 2.8% |

Survival by entity type (counts of *article-level* entities of each type that
also appear at the higher level):

| Type | Article | Day | Week | Month |
|---|---:|---:|---:|---:|
| PLACE | 17 | 6 | 2 | 0 |
| ORG | 15 | 1 | 2 | 1 |
| PERSON | 5 | 0 | 2 | 0 |

The single entity that survives all the way to month is `Il Messaggero` itself
(meta-mention of the source). Substantively zero of the 1943-07-03 article-
level named entities reach the month summary — the month summary covers the
day only thematically (`bombardamenti alleati`) and via the surrounding
narrative arc (Sicilian invasion, Roma 19-luglio bombing, regime change), not
via the day's own named protagonists.

**Compression order** (which types compress out first, on this trace):

1. **Generic ORGs collapse fastest at day-level**: `a097`'s 9 bureaucratic
   acronyms (`O.N.M.I.`, `G.U.F. dell'Urbe`, `Federazioni dei Fasci di
   Combattimento`, etc.) drop to one day-level survivor.
2. **Specific PERSONs survive to week, not to month**: `Duce`, `Paoletti`
   reappear at `1943-W26-tail` but are subsumed under `Mussolini` / "regime"
   by month.
3. **PLACEs are most resilient at day-level** (6/17 survive — day summaries
   are organised by front: Sicilia / Russia / Pacifico) but collapse hardest
   at month-level (0/17 — the month summary names later-month places like
   Tiburtino, Prenestino, San Lorenzo).

**Headline finding**: under 3% of article-level named entities for an
ordinary mid-corpus day reach the month summary. The hierarchy compresses
*named-entity density* and replaces it with *thematic density*: the day's
`topics` (`battaglia di Rendova`, `bombardamenti su Palermo`, `mercato nero
e corruzione`) survive into week- and month-level topic vocabulary.
Month-level navigation is for *what kind of day it was*, not *who was in it*.

## 3. The 25 July example trace

Files: `eval/summaries/day/1943-07-25.json`, `eval/summaries/week/1943-W29.json`
(W29 covers 19-25 July, 7 days; 25 July is W29's last day, NOT W30 as the
spec note assumed), `eval/summaries/month/1943-07.json`.

| Aspect | Day (1943-07-25, 273 articles, ~2.7k chars) | Week (1943-W29, 19-25 Jul, 7 days, ~2.3k chars) | Month (1943-07, 5 weeks, ~2.85k chars) |
|---|---|---|---|
| Headline framing | "Sintesi della giornata del 25 luglio 1943" — pure within-day register | "la settimana del bombardamento" (Roma 19-luglio is the spine) | "il mese della svolta" (caduta del fascismo) |
| Sicilian front | Sgombero di Palermo (com. 24 luglio); CLXI/CLXIII gruppo artiglieria; aerosiluranti italiani; Capo Peloro / Villa San Giovanni | Sgombero di Palermo named (24 luglio); aerosiluranti named (Celli, Di Bella, Pighini) | Compressed to "sbarco in Sicilia" theme; specific 24-luglio Palermo evacuation absent |
| Bologna 24-luglio bombing | Detailed: Basilica di San Francesco, casa natale Marconi, Palazzo del Governo, ospedali, time-stamp 9.50-12.30 | Named (Basilica San Francesco, casa Marconi, Palazzo del Governo, ospedali) | Absent — Bologna does not appear in month summary |
| Roma post-bombing | Continued aid, 100 children to colonia G.I.L., Istituto Fascista Case Popolari, 400 famiglie | Subsumed: 717 morti / 1.659 feriti, San Lorenzo damage, Pio XII visit, Hazon + Barengo | Repeated: 717 morti / 1.659 feriti, San Lorenzo, Pio XII, Hazon + Barengo (verbatim from week) |
| Pacifico | Munda / Nuova Georgia, Rendova affondamento | Absent | Absent |
| **02:40 Grand Council vote** | **Absent from day summary** — and absent from the source itself: the morning paper of 25 July went to print before the vote concluded at 02:40, so the day-level node faithfully records what *Il Messaggero* knew, which was nothing | **Absent from in-week prose, but flagged proleptically**: "*Sconosciuto ai lettori del Messaggero: il giorno successivo, 25 luglio, avverrà l'arresto di Mussolini.*" (the week summariser knows the historical fact and tags the silence) | **Partial**: month summary says "*L'edizione del 26 luglio è assente dal fondo archivistico: la lacuna documenta le 24 ore di vuoto tra l'arresto di Mussolini (25 luglio) e la riorganizzazione editoriale.*" — the arrest is named, but the 02:40 timestamp and the Grand Council vote mechanism are compressed away |
| **King's arrest of Mussolini** | Not in the day summary (regime did not break the news in the morning paper); 25 July day-level represents the regime's last coherent self-presentation | Tagged proleptically (see above quote) | Named (`arresto di Mussolini (25 luglio)`); the King is not named at month level either; the arrest is described but not attributed to Vittorio Emanuele III |
| Editorial register | Pure late-fascist: "strenuo valore", Feldmaresciallo Richtofen handing 1.143.050 lire to "i sinistrati di Roma", "spontanea offerta dei soldati germanici" | Mixed: still fascist register for in-week events; the prolepsis sentence is the *only* meta-historical break | Synthetic narrative arc: "transizione traumatica dalla propaganda di regime alla caduta del fascismo" |

**Verdict on the §5.3 question** ("at month level, is the 02:40 Grand
Council vote and the King's arrest of Mussolini still present?"): **the
arrest is preserved at month level; the 02:40 timestamp and the Grand
Council vote mechanism are compressed away.** The month names "l'arresto
di Mussolini (25 luglio)" as a single point event. Mechanistic detail —
02:40 Grand Council vote, Grandi's motion, the King at Villa Savoia —
exists only in the §6.2 absent-day analysis, because *Il Messaggero* itself
never reported it: the 25 July morning paper went to press before the vote
concluded, the 26 July issue is absent, and the 27 July paper led with the
Badoglio proclamation. §5.3 shows the index faithfully compresses *what
was reported*; §6.2 shows the absent-day node lets the agent reason about
*what was not reported*, which is where the regime-change mechanism lives.

---

**Reproducibility**: re-run via `python3 scripts/section_5_spotcheck.py`;
seeds 1943 (spot-check), 1944 (info-loss day) are pinned in the script.
Raw evidence in `eval/section_5_spotcheck.json` (entity lists, hits, full
summaries for the trace). All Claude calls via OAuth subscription path; no
API keys used.
