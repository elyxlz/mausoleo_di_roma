# §3 System-design diagrams

Mermaid diagrams for the Mausoleo dissertation, §3 *System design*.
One overview + one detail per sub-section (§3.1 OCR, §3.2 hierarchical index, §3.3 agent-mediated search).

## Figure 3.0 — Overview architecture

End-to-end pipeline from scanned newspaper pages to LLM-agent answers. The three modular stages (OCR, indexing, search) communicate through a single ClickHouse `nodes` table; the LLM agent only ever talks to the search/nav API.

```mermaid
flowchart LR
  A[Scanned JPEGs<br/>Il Messaggero<br/>1880-1945] --> B[§3.1 OCR pipeline<br/>2x RTX 3090, 30 min/issue]
  B --> C[Raw articles<br/>per-issue JSON]
  C --> D[(ClickHouse<br/>nodes table)]
  D --> E[§3.2 Recursive summariser<br/>vLLM + BGE-M3]
  E --> D
  D --> F[§3.3 Search/Nav API<br/>FastAPI + CLI]
  F --> G((LLM agent))
  G -- tool calls --> F
  G --> H[Human-readable answer]
```

## Figure 3.1 — OCR pipeline detail (§3.1)

Eight sub-pipelines run in two parallel GPU chains under a 30-min/issue budget. Their per-page JSON outputs flow into a deterministic ensemble: a 9-step REPLACE chain (col4 used twice), an ADDITIVE merge of the col6+ads source, and a quality-weighted text selector. Names match `eval/autoresearch/program.md`.

```mermaid
flowchart TB
  subgraph G0[GPU 0 chain ~30.5 min]
    P1[exp_107_fullpage_qwen25vl<br/>primary]
    P2[exp_045_qwen3vl_vllm]
    P3[exp_055_col6_ads_prompt]
    P4[exp_097_col4_qwen3vl_vllm]
  end
  subgraph G1[GPU 1 chain ~28.9 min]
    P5[exp_138_col4_qwen25_vllm]
    P6[exp_140_yolo_smallregion_vllm]
    P7[exp_142_col5_qwen25_vllm]
    P8[exp_102_fullpage_vllm]
  end
  IMG[Issue JPEGs<br/>~6 pages] --> G0 & G1
  G0 & G1 --> R[REPLACE chain<br/>9 entries, col4 x2<br/>per-source overlap + ratio]
  G0 & G1 --> AD[ADDITIVE merge<br/>exp_055_col6_ads_prompt]
  R --> QS[quality_text_select<br/>delta=0.10 body / 0.15 head]
  AD --> QS
  QS --> OUT[Issue articles JSON]
```

## Figure 3.2 — Index hierarchy for July 1943 (§3.2)

The case-study slice lifts only the first five of the seven production levels (paragraph -> article -> day -> week -> month). Counts shown are for July 1943 of *Il Messaggero*: ~6480 article nodes collapse into 31 day nodes (the 07-26 issue is absent and stored as an empty day so the chronology stays contiguous), then 5 weeks, then a single month root.

```mermaid
flowchart TB
  M[month: 1943-07<br/>1 node]
  M --> W1[week 1<br/>07-01..07-04]
  M --> W2[week 2<br/>07-05..07-11]
  M --> W3[week 3<br/>07-12..07-18]
  M --> W4[week 4<br/>07-19..07-25]
  M --> W5[week 5<br/>07-26..07-31]
  W1 --> D1[4 day nodes]
  W2 --> D2[7 day nodes]
  W3 --> D3[7 day nodes]
  W4 --> D4[7 day nodes]
  W5 --> D5[6 day nodes<br/>incl. 07-26 absent]
  D1 & D2 & D3 & D4 & D5 --> DAYS[31 day nodes total]
  DAYS --> ART[~6480 article nodes]
  ART --> PAR[paragraph leaves<br/>raw text + embedding]
```

## Figure 3.3 — Agent-mediated search interaction (§3.3)

A single agent turn for a Mussolini query: the agent walks down the chronology from `root` to a specific day, pulls full text, and in parallel issues a semantic search. Tree traversal gives provenance; semantic search is the escape hatch when the chronological drill-down misses something.

```mermaid
sequenceDiagram
  participant U as User
  participant A as LLM agent
  participant API as Search/Nav API
  participant CH as ClickHouse
  U->>A: "What did Il Messaggero say about Mussolini in late July 1943?"
  A->>API: GET /root
  API->>CH: select archive root
  API-->>A: archive node
  A->>API: GET /nodes/1943-07/children
  API-->>A: 5 week summaries
  A->>API: GET /nodes/1943-07_w4
  API-->>A: week node (07-19..07-25)
  A->>API: GET /nodes/1943-07_w4/children
  API-->>A: 7 day summaries
  A->>API: GET /nodes/1943-07-25
  API-->>A: day node summary
  A->>API: GET /nodes/1943-07-25/text
  API-->>A: reconstructed full text
  par parallel
    A->>API: POST /search/semantic {"q":"Mussolini","level":"article"}
    API->>CH: ANN over embeddings
    API-->>A: ranked article list
  end
  A-->>U: synthesised answer + citations
```
