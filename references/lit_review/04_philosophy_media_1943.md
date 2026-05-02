# Philosophy + Media Studies + 1943 Italy Context

## Why this matters for Mausoleo

Mausoleo is a hierarchical knowledge index over a one-month slice of *Il Messaggero* (1943). The system compresses thousands of articles into LLM-generated summaries arranged in a tree of decreasing granularity. The BASc rubric's Cat. 2 (disciplinary depth) and Cat. 4 (interdisciplinarity / synthesis) reward dissertations that situate the artefact in frameworks it silently presupposes. The three domains close that loop.

Philosophy of knowledge supplies the language for what Mausoleo *is* doing: summarising is a positioned, partial, testimonial act. The hermeneutic circle, situated knowledges, epistemic injustice, the epistemology of testimony, and the recent literature on LLM opacity together force the question of what is preserved and what lost when a month of fascist-era reportage collapses into one paragraph. Media studies adds the second layer: *Il Messaggero* in 1943 is not a window onto reality but a state-aligned construction of it. Agenda-setting, public-sphere theory, Foucault's archive, and the Frankfurt School's culture-industry critique reframe the project from "I built a tool" into "I built a tool that interrogates how an authoritarian press constructed reality, and how my tool risks reproducing or disrupting that construction." The historical context grounds the case studies in real headlines and real silences. The October 1943 window contains the editorial register-shift at *Il Messaggero* under German occupation and the most morally explosive non-event in modern Italian Jewish history — the 16 October ghetto raid, which the Roman press catastrophically failed to cover. That contrast is the dissertation's sharpest demonstration of what hierarchical summarisation can and cannot recover.

## Section A: Philosophy of knowledge / epistemology

### A1. Hermeneutic circle

- Schleiermacher, F. (1838) *Hermeneutik und Kritik*; the foundational text where understanding the whole requires understanding the parts and vice versa.
- Heidegger, M. (1927) *Being and Time*, §32: the circle is ontological — Dasein always already interprets from a fore-structure.
- Gadamer, H.-G. (1960) *Truth and Method*: the circle becomes a fusion of horizons; understanding is iterative, dialogical, linguistically mediated.
- Stanford Encyclopedia of Philosophy, "Hermeneutics" (Mantzavinos, 2024 update).

Connection: Mausoleo's tree is a hermeneutic circle made operational. To summarise a day the LLM needs the month; to summarise the month it needs the days. Recursive bottom-up / top-down passes are a computational implementation of Gadamerian iteration — not an engineering trick.

### A2. Situated knowledge / standpoint epistemology

- Haraway, D. (1988) "Situated Knowledges: The Science Question in Feminism and the Privilege of Partial Perspective", *Feminist Studies* 14(3): 575–599. The "god-trick" of "seeing everything from nowhere" is precisely what an LLM summary pretends to perform.
- Harding, S. (1991) *Whose Science? Whose Knowledge?*: strong objectivity through standpoint.
- Code, L. (1991) *What Can She Know?* on epistemic location.

Connection: Mausoleo's summaries arrive in the voice of a 2026 multilingual, English-dominated model. That standpoint is not neutral about 1943 Rome. Frame every node as a "view from somewhere" and expose the model's positioning.

### A3. Epistemology of summarization, abstraction, testimony

- Lackey, J. (2008) *Learning from Words: Testimony as a Source of Knowledge*. OUP. Foundational on testimonial transmission.
- Goldberg, S. (2010) *Relying on Others*. OUP.
- Stanford Encyclopedia of Philosophy, "Epistemological Problems of Testimony" (Adler, updated 2022).
- Recent: Freiman, O. (2024) "A phenomenology and epistemology of large language models: transparency, trust, and trustworthiness", *Ethics and Information Technology* 26.

Connection: A Mausoleo summary is a testimonial chain — article → daily → weekly → monthly. Each step asks the user to trust the previous. The reductionist / anti-reductionist debate maps onto "should the user trust the top of the tree, or only the leaves?"

### A4. Epistemic injustice in archives

- Fricker, M. (2007) *Epistemic Injustice: Power and the Ethics of Knowing*. OUP. The two forms — testimonial (deflated credibility) and hermeneutical (gaps in collective interpretive resources) — both cut deep here.
- Medina, J. (2013) *The Epistemology of Resistance*. OUP.
- Pohlhaus, G. (2012) "Relying on our own and each other's epistemic resources: wilful hermeneutical ignorance", *Hypatia* 27(4).

Connection: The Roman Jewish community in October 1943 is the textbook case. Their experience was systematically absent from *Il Messaggero* — censored, then occluded under Salò editorship. A naive Mausoleo summary ("October 1943: war news, bombings, civic notices") reproduces that gap. A self-aware Mausoleo flags it. Key case study and ethical claim.

### A5. AI as knowledge producer

- Burrell, J. (2016) "How the machine 'thinks': Understanding opacity in machine learning algorithms", *Big Data and Society* 3(1). Three forms of opacity (intentional, illiterate, intrinsic).
- Mittelstadt, B., Allo, P., Taddeo, M., Wachter, S., Floridi, L. (2016) "The ethics of algorithms: mapping the debate", *Big Data and Society* 3(2).
- Humphreys, P. (2009) "The philosophical novelty of computer simulation methods", *Synthese* 169.
- Recent: Kasirzadeh, A. and Gabriel, I. (2023) "In conversation with Artificial Intelligence: aligning language models with human values", *Philosophy and Technology* 36.

Connection: Hallucination is structural to compression without ground-truth retrieval. The dissertation must answer the critique "you've built a fancy hallucinator over priceless primary sources." Burrell's three opacities and Mittelstadt's inscrutability frame Mausoleo's citation-grounding as a deliberate response.

## Section B: Media studies

### B1. Agenda-setting

- McCombs, M. and Shaw, D. (1972) "The Agenda-Setting Function of Mass Media", *Public Opinion Quarterly* 36(2): 176–187. Chapel Hill study.
- McCombs, M. (2014) *Setting the Agenda* (2nd ed.). Polity.

Connection: A daily paper ranks as well as reports — page, column-inches, absence. Mausoleo's hierarchy *visualises* the agenda: a day's top node is what the editor (or the LLM's salience function) treated as central. The tree is itself a second-order agenda-setting act, and the dissertation should own this.

### B2. Public sphere theory

- Habermas, J. (1962/1989) *The Structural Transformation of the Public Sphere*. MIT Press.
- Habermas, J. (2022) "Reflections and hypotheses on a further structural transformation of the political public sphere", *Theory, Culture and Society* 39(4) — directly addresses platform-mediated and algorithmic publics.

Connection: 1943 *Il Messaggero* is the case where Habermas's "structural transformation" has already collapsed the public sphere into state-managed mass communication — no rational-critical debate, only *veline* (state directives to the press). Mausoleo retrospectively re-publishes that month into a (digital) public sphere eighty years later.

### B3. Foucault: archive and discourse

- Foucault, M. (1969/1972) *The Archaeology of Knowledge*. Pantheon. Especially Part III on "the statement and the archive".
- Foucault, M. (1971) "L'ordre du discours" / "The Order of Discourse".

Connection: For Foucault the archive is not the sum of texts but the *system* determining what can count as a statement. *Il Messaggero* in October 1943 has such an archive: the rules under which writing could become publishable news under occupation. Mausoleo, as meta-archive, inherits that rule-system unless it interrogates it.

### B4. Press and authoritarianism

- Cannistraro, P. (1975) *La fabbrica del consenso. Fascismo e mass media*. Laterza. Classic on MinCulPop (Ministry of Popular Culture, 1937–1944) and the *velina* system of daily editorial directives.
- Tranfaglia, N., Murialdi, P., Legnani, M. (1980) *La stampa italiana nell'età fascista*. Laterza.
- Bonsaver, G. (2007) *Censorship and Literature in Fascist Italy*. Toronto UP.
- Forgacs, D. and Gundle, S. (2007) *Mass Culture and Italian Society from Fascism to the Cold War*. Indiana UP.

Connection: Empirical grounding for what *Il Messaggero* could and could not say in 1943; backbone for the agenda-setting and epistemic-injustice arguments.

### B5. Critical theory of media

- Horkheimer, M. and Adorno, T. (1944/1947) *Dialectic of Enlightenment*, esp. "The Culture Industry: Enlightenment as Mass Deception".
- Adorno, T. (1991) *The Culture Industry*. Routledge.

Connection: Adorno's claim that mass-produced culture turns audiences passive, and that the same logic underwrote Hollywood and Nazi-Fascist media, is the register for a self-critique of Mausoleo. A frictionless LLM summary is exactly the "predigested" cultural content Adorno warned of — *a fortiori* over fascist propaganda. Mausoleo's citation grounding, expandable nodes, and exposure of model positioning are the counter-move.

## Section C: 1943 Italy historical context (essential for case studies)

### C1. The fall of Mussolini, 25 July 1943

- Deakin, F. W. (1962) *The Brutal Friendship: Mussolini, Hitler and the Fall of Italian Fascism*. Harper and Row.
- De Felice, R. (1990) *Mussolini l'alleato: L'Italia in guerra 1940–1943, II. Crisi e agonia del regime*. Einaudi.
- Bosworth, R. J. B. (2002) *Mussolini*. Arnold. Chs. 14–15.

Key facts: Grand Council of Fascism vote on the Grandi motion 24–25 July, 19–7–1; Mussolini arrested by carabinieri on leaving the King's audience; Marshal Pietro Badoglio appointed head of government; the regime formally ends but the war continues ("la guerra continua").

### C2. Armistice of Cassibile and German occupation, 8 September 1943

- Aga Rossi, E. (2003) *A Nation Collapses: The Italian Surrender of September 1943*. Cambridge UP.
- Klinkhammer, L. (1993) *Zwischen Bündnis und Besatzung: Das nationalsozialistische Deutschland und die Republik von Salò*. Niemeyer. (Italian: *L'occupazione tedesca in Italia 1943–1945*, Bollati Boringhieri.)

Key facts: armistice signed 3 September, announced 8 September. Operation Achse (German occupation) immediate. King and Badoglio flee Rome 9 September. Italy splits: Allied-controlled south, German-occupied centre-north. Mussolini liberated by Skorzeny at Gran Sasso 12 September. Italian Social Republic (RSI / Salò) declared 23 September.

### C3. *Il Messaggero* in 1943 specifically

- Il Messaggero, official 145th-anniversary historical retrospective (2023), https://www.ilmessaggero.it/speciale_145_anni/ — confirms Perrone-family ownership in 1943.
- Italian Wikipedia, *Il Messaggero*, with full chronology of directors.
- Murialdi, P. (1986) *La stampa del regime fascista*. Laterza. Best survey of the Italian press 1922–1943.

Key facts: founded 1878, owned by the Perrone family from 1915. Edited under fascism in close conformity with MinCulPop directives. After 25 July 1943 Tomaso Smith was appointed director and the issue of 26–27 July was famously co-signed by anti-fascist intellectuals (Pannunzio, Benedetti, Longanesi, Flaiano, Soldati). Under German occupation from 8 September the paper continued to publish: from late 1943 the editorship passed to Bruno Spampanato, an open Salò-aligned figure who later directed the X-MAS press. So *Il Messaggero* in 1943 traverses three regimes within five months: fascist, royal-Badoglian, RSI-occupation. This editorial whiplash is itself a case study.

### C4. Daily life in occupied Rome and the 16 October ghetto raid

- Katz, R. (2003) *The Battle for Rome: The Germans, the Allies, the Partisans, and the Pope, September 1943 – June 1944*. Simon and Schuster.
- Debenedetti, G. (1944/1999) *16 ottobre 1943*. Sellerio. The classic eyewitness essay.
- Picciotto, L. (1991/2002) *Il libro della memoria: Gli ebrei deportati dall'Italia 1943–1945*. Mursia.
- Zuccotti, S. (1987) *The Italians and the Holocaust*. Basic Books.
- Sarfatti, M. (2006) *The Jews in Mussolini's Italy: From Equality to Persecution*. Wisconsin UP.

Key facts: Nazi occupation of Rome 10 September 1943 to 4 June 1944. Bread ration cut to 150 g and progressively further. Kappler's 50-kg gold extortion 26–28 September. Razzia del ghetto 16 October 1943: 1,259 detained, 1,023 deported to Auschwitz, sixteen survivors. *Il Messaggero* did not report the raid as such — a textbook hermeneutical-injustice silence.

### C5. Italian fascist propaganda and historiography (orientation)

- De Felice, R. (1965–1997) *Mussolini* (4 vols, 8 books). Einaudi. The indispensable, controversial monument.
- Gentile, E. (1993/1996) *The Sacralization of Politics in Fascist Italy*. Harvard UP. Fascism as political religion.
- Corner, P. (2012) *The Fascist Party and Popular Opinion in Mussolini's Italy*. OUP. Consent from below — and its erosion by 1943.
- Pavone, C. (1991/2013) *A Civil War: A History of the Italian Resistance*. Verso. The three-fold war (patriotic, civil, class) that begins on 8 September 1943.
- Battaglia, R. (1953) *Storia della Resistenza italiana*. Einaudi.
- Bosworth, R. J. B. (2005) *Mussolini's Italy: Life under the Dictatorship 1915–1945*. Penguin.

## Case-study month: July 1943 (CORRECTED 2026-05-02)

The corpus actually digitised is **July 1943**, 30 days from 1943-07-01 to 1943-07-31 (1943-07-26 is missing from the source archive). This is the regime-collapse window, and the case for it is at least as strong as the October case below, on different axes.

1. *Within-month regime rupture, with a single observable hinge day.* On the night of 1943-07-24/25 the Grand Council voted Mussolini out (02:40, 25 July); the King had him arrested that afternoon. The morning issue of 1943-07-25 went to press during the meeting, so it carries pure late-fascist register: 273 articles, "Battaglia in Sicilia" bulletins, "DOVE ARRIVANO I LIBERATORI" sarcasm about the Allies, "BIECO FURORE BRITANNICO." 1943-07-26, the rupture day, is missing from the archive itself. 1943-07-27 onward should carry the Badoglio-government register. The dissertation can demonstrate regime change as an observable feature of the press across a single month, with the data's own missing day ratifying the political event.

2. *The data ratifies the historical claim.* The missing 1943-07-26 issue is not just an OCR gap; it is the political event made visible by the corpus's silence. The hermeneutical-injustice argument that the lit review developed for the October ghetto raid translates directly: Mausoleo can either reproduce the silence (a naïve summary "Il Messaggero, July 1943: war coverage, regime news") or it can flag the discontinuity. The 26 July gap is a smaller-scale but methodologically cleaner version of the same argument.

3. *Single-axis longitudinal experiment.* July gives a clean before/after split: roughly 1943-07-01 to 07-25 is fascist register; 1943-07-27 to 07-31 is Badoglio-interim register. The dissertation can run summarisation at day, week, and month levels and ask which level first surfaces the regime change. This is a concrete falsifiable empirical question of exactly the type Category 4 of the rubric rewards.

4. *Source availability.* BNC Roma, Biblioteca di Storia Moderna e Contemporanea, Emeroteca Digitale Italiana hold *Il Messaggero* July 1943. The 25 July fall is heavily cited (Deakin, De Felice, Bosworth, Pavone), so the citation pool is dense and well-defined.

October 1943 carries the more dramatic ethical case study (the ghetto raid silence) but lacks the within-month rupture: October is post-rupture, fully RSI, editorial regime stable. July is the rupture itself. For a dissertation whose central claim is that hierarchical summarisation enables qualitatively different access to the regime change as it appears in the press, July is the stronger month.

The October framing remains useful as a foil and for the discussion section: a brief comparison of what July's data can tell us versus what October's data could have told us anchors the limits-of-scope discussion.

## Key arguments to deploy

1. **Mausoleo's recursive bottom-up / top-down summarization is a computational hermeneutic circle** (Schleiermacher, Gadamer). Iteration is not a hack but a Gadamerian fusion of horizons; the architecture has philosophical grounding.

2. **Every node in the tree is a "view from somewhere"** (Haraway). The model has a standpoint — 2026, multilingual but English-dominated, post-hoc, non-Roman, non-Jewish, non-fascist, non-1943. Honest design surfaces this rather than hiding behind apparent objectivity.

3. **Hierarchical summarization is not neutral compression but a second-order agenda-setting act** (McCombs and Shaw; Habermas; Foucault). The tree's top node *is* the agenda; the dissertation must own this and either justify or interrogate the salience function.

4. **What *Il Messaggero* in October 1943 does *not* report is a hermeneutical injustice** (Fricker, Medina). The 16 October ghetto raid silence is the canonical example. Mausoleo can either reproduce the silence or, by retrieval-grounded comparison with secondary sources, expose it.

5. **LLM hallucination + opacity are real epistemic risks; citation-grounded retrieval is the response, not a bolt-on** (Burrell on opacity, Mittelstadt et al. on algorithmic ethics, Freiman 2024 on LLM trust). Ground every claim in a primary or named secondary source visible to the user.

6. **Mausoleo runs the risk of culture-industry recapitulation** (Adorno, Horkheimer). A frictionless, beautifully-summarised fascist newspaper risks aestheticising and predigesting it for a 2026 audience. The artefact must build in friction: visible citations, exposed silences, expandable nodes, refusal to smooth contradictions.

7. **The 1943 *Il Messaggero* offers a unique three-regime traversal in five months** (fascist, royal-Badoglian, RSI-occupied). October is the month where the third register is consolidated and where the system's ethical and historiographical stakes (the ghetto raid silence) are at their sharpest. The dissertation should defend October on these grounds and use the regime-shift as a longitudinal axis within the month.
