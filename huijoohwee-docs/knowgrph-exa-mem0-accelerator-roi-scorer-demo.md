---
title: "Knowgrph Exa + mem0 - AcceleratorROI Scorer + EcosystemPulse Dashboard"
graphId: "md:knowgrph-exa-mem0-accelerator-roi-scorer-demo"
doc_type: "Exa + mem0 Computing Flow Demo"
date: "2026-06-13"
updated: "2026-06-13"
lang: "en-US"
schema: "kgc-computing-flow/v1"
status: draft
author: airvio/joohwee

# ── stack ─────────────────────────────────────────────────────────────────────
product: Knowgrph / airvio
track: Startup Ecosystem
theme: Track what happens to startups after accelerator graduation
stack:
  search: exa-mcp-server (web_search_exa, deep_search_exa, company_research, crawling, linkedin_search)
  memory: mem0ai/mem0 v1.0.0 (MIT) — self-hosted on Oracle ARM · REST callable from CF Workers
  wire_format: csv-first (flat) · minified-json (nested only) · plain-text (crawl prose)
  runtime: Cloudflare Workers + Pages
  storage: D1 (read cache) · R2 (long-term archival only) · KV (hot index)
  frontend: React · D3.js · Chart.js
  orchestration: KGC harness · Hermes Agent (MCP-callable)
  tco: near-zero (Exa API + Cloudflare free tier + mem0 self-hosted)

# ── domain identity variables ─────────────────────────────────────────────────
domain_vars:
  accelerator: "{{accelerator}}"       # e.g. Y Combinator, Antler, EF
  cohort_year: "{{cohort_year}}"       # e.g. 2022, 2023
  company: "{{company}}"              # individual startup name
  sector: "{{sector}}"                # e.g. fintech, deeptech, b2b-saas
  snapshot_date: "{{snapshot_date}}"  # ISO date of last Exa scan

# ── roi score ─────────────────────────────────────────────────────────────────
roi:
  formula: "(Impact × Reach) / (Build Hours + Monthly TCO + Token Cost/Month)"
  impact: 8      # live signal on ~$2B+ annual accelerator market
  reach: 7       # founders, VCs, program managers, ecosystem researchers
  build_hours: 0.5
  monthly_tco: 2
  token_cost_month: 4
  score: 10.5

# ── orchestration ─────────────────────────────────────────────────────────────
orchestration_class: fan-out-aggregate
entry_point: InputWidget[AcceleratorSelector]
exit_point: RichMediaPanel[EcosystemPulseDashboard]
mcp_tools:
  - deep_search_exa    # survival, follow-on, time-to-A signals
  - company_research   # per-company structured crawl
  - web_search_exa     # exits, sector signals, movers
  - linkedin_search    # founder journey, stealth detection
  - crawling           # digital visibility index computation

# ── canvas config ─────────────────────────────────────────────────────────────
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: true
kgDocumentStructureBaselineLock: false
kgWorkflowManagerModeEnabled: true
kgAutoSaveEnabled: true
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
kgBottomPanelOpen: true
kgBottomPanelTab: "eventModeling"
kgFloatingPanelOpen: true
kgFloatingPanelView: "eventModeling"
kgStorageTarget: "cloudflare"
kgStorageAccountId: "170e89fdb8679ff2fcc2900e25ed04f4"
kgStorageWorkspaceId: "kgws:canonical-docs"
kgStorageDocPath: "huijoohwee/docs/knowgrph-exa-mem0-accelerator-roi-scorer-demo.md"
kgStorageDocTarget: "cloudflare-d1"
kgStorageMediaBucket: "knowgrph-media"
kgStorageMediaBaseUrl: "https://airvio.co/knowgrph/r2"
kgStorageMediaKeyScheme: "runs/{runId}/{stageId}/{shotId}.{ext}"
kgMediaPersistPolicy: "copy-on-generate"
kgForbidPlatform: ["vercel", "aws"]
kgReplayEnabled: true
kgReplayFromStorageWithoutLlm: true
kgReplayMediaFields: ["imageUrl", "outputSrcDoc"]
kgReplayAccessScope: "run-entitled"
demo_status: "dev-source capability demo; no Prod or Cloudflare deploy claim"
deployed_api_claim: false
mem0_credential_policy: "MEM0_HOST lives in host environment only; never hardcoded, browser-stored, or repo-stored"
exa_credential_policy: "EXA_API_KEY lives in host environment only; never hardcoded, browser-stored, or repo-stored"

# ── shared renderer contract ──────────────────────────────────────────────────
kgSharedRendererContract:
  version: "shared-renderer-contract/v1"
  semanticIdentity: "buildScopedGraphSemanticKey"
  cardPreview: "CardMediaPreview + CardMarkdownPreview"
  widgetCard: "canvas:widgetCard"
  richMediaPanel: "RichMediaPanel"
  storyboardDisplay: "2D Renderer: Storyboard Card (default) and Widget variants"
  storyboardSurfaces: ["Cards", "Widgets", "Rich Media Panels"]
  edgeModel: "active graph edges from the selected source graph"
  timelineSurface: "TimelineTransportControls + shared bottom-panel surface"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"

# ── socket types ──────────────────────────────────────────────────────────────
socket_types:
  text_signal: {color: "#0ea5e9", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [text_signal]}
  number_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [number_signal]}
  rich_media_chart_html: {color: "var(--kg-canvas-accent)", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [rich_media_chart_html]}
  exa_result_signal: {color: "#22c55e", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [exa_result_signal]}
  memory_signal: {color: "#8b5cf6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [memory_signal]}
  approval_signal: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [approval_signal]}

# ── workflow sections ─────────────────────────────────────────────────────────
workflow_sections:
  - id: wf_memory_read
    title: "Pre-scan mem0 read — hydrate prior scores, DVI cache, Ghost flags"
    nodes: [n_input, n_mem0]
  - id: wf_program_layer
    title: "Program layer — deep_search_exa batch + TOPSIS engine"
    nodes: [n_prg_fetcher, n_topsis]
  - id: wf_company_layer
    title: "Company layer — company_research fan-out + DVI probe + status classify"
    nodes: [n_co_fetcher, n_dvi, n_classify]
  - id: wf_memory_write
    title: "Post-scan mem0 write — persist TOPSIS, DVI, status, Ghost flags"
    nodes: [n_mem0]
  - id: wf_dashboard
    title: "EcosystemPulse Dashboard — 5 panels"
    nodes: [panel_p1, panel_p2, panel_p3, panel_p4, panel_p5]

# ── flow diagrams ─────────────────────────────────────────────────────────────
flow_diagrams:
  key: flow_diagrams
  type: object
  value:
    harness_gitgraph:
      key: harness_gitgraph
      type: mermaid_gitgraph
      floatingPanelView: "gitGraph"
      floatingPanelOpen: true
      bottomPanelTab: "gitGraph"
      bottomPanelOpen: true
      title: "AcceleratorROI + EcosystemPulse + mem0 parallel lanes"
      value: |-
        gitGraph
          commit id:"accelerator_input" tag:"{{accelerator}}+{{cohort_year}}"
          branch mem0_read
          checkout mem0_read
          commit id:"mem0_search_pre_scan"
          checkout main
          branch program_layer
          checkout program_layer
          commit id:"deep_search_exa_batch"
          commit id:"topsis_engine"
          checkout main
          branch company_layer
          checkout company_layer
          commit id:"company_research_fanout"
          commit id:"dvi_probe_cache_check"
          commit id:"status_classify"
          checkout main
          merge mem0_read id:"prior_scores_hydrated"
          merge program_layer id:"program_scores"
          merge company_layer id:"company_signals"
          commit id:"mem0_write_post_scan"
          commit id:"ecosystem_pulse_dashboard" tag:"5-panel"
    harness_gantt:
      key: harness_gantt
      type: mermaid_gantt
      floatingPanelView: "gantt"
      floatingPanelOpen: true
      bottomPanelTab: "gantt"
      bottomPanelOpen: true
      title: "Exa + mem0 AcceleratorROI critical path"
      value: |-
        gantt
          title computing flow: exa-mem0-accelerator-roi-scorer
          dateFormat YYYY-MM-DD
          section Input + Memory
          Accelerator selector :done, accel_input, 2026-06-13, 1d
          mem0 pre-scan read :mem0_read, after accel_input, 1d
          section Program layer
          deep_search_exa batch :prg_fetch, after mem0_read, 1d
          TOPSIS engine :crit, topsis, after prg_fetch, 1d
          section Company layer
          company_research fan-out :co_fetch, after mem0_read, 2d
          DVI probe (cache miss only) :dvi, after co_fetch, 1d
          Status classify :classify, after dvi, 1d
          section Memory + Dashboard
          mem0 post-scan write :mem0_write, after topsis classify, 1d
          EcosystemPulse render :crit, dashboard, after mem0_write, 1d
    harness_flowchart:
      key: harness_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          accel_input["AcceleratorSelector\n(InputWidget)\n{{accelerator}} · {{cohort_year}}"]
          mem0["Mem0MemoryLayer\n(MemoryWidget)\nsearch → add · user_id=namespace"]
          prg_fetcher["ProgramDataFetcher\n(ComputeWidget)\ndeep_search_exa × 4 criteria"]
          co_fetcher["CompanyDataFetcher\n(ComputeWidget)\ncompany_research × N"]
          topsis["TOPSISEngine\n(ComputeWidget)\nnormalize → weight → rank · C_i"]
          dvi["DigitalVisibilityIndex\n(ComputeWidget)\nweb + linkedin + crawl · cache miss only"]
          classify["StatusClassifier\n(ComputeWidget)\nactive/stealth/pivoted/defunct"]
          dashboard["EcosystemPulseDashboard\n(RichMediaPanel)\n5 panels"]
          accel_input -->|"text_signal: namespace key"| mem0
          mem0 -->|"memory_signal: prior TOPSIS scores"| topsis
          mem0 -->|"memory_signal: cached DVI (24h)"| dvi
          mem0 -->|"memory_signal: Ghost flags + prior status"| classify
          accel_input -->|"text_signal: program query"| prg_fetcher
          accel_input -->|"text_signal: company list"| co_fetcher
          prg_fetcher -->|"exa_result_signal: criteria vectors"| topsis
          co_fetcher -->|"exa_result_signal: visibility probes"| dvi
          co_fetcher -->|"exa_result_signal: funding + pivot"| classify
          topsis -->|"memory_signal: write TOPSIS scores"| mem0
          dvi -->|"memory_signal: write DVI + timestamp"| mem0
          classify -->|"memory_signal: write status + Ghost flags"| mem0
          topsis -->|"rich_media_chart_html: C_i rank vector"| dashboard
          dvi -->|"rich_media_chart_html: DVI[0-100]"| dashboard
          classify -->|"rich_media_chart_html: status taxonomy"| dashboard
    architecture:
      key: architecture
      type: mermaid_architecture
      floatingPanelView: "architecture"
      floatingPanelOpen: true
      bottomPanelTab: "architecture"
      bottomPanelOpen: true
      forbidPlatform: ["vercel", "aws"]
      value: |-
        architecture-beta
          group operator(cloud)[Operator]
          group cloudflare(cloud)[Cloudflare Control Plane]
          group exa(cloud)[Exa MCP]
          group oracle(cloud)[Oracle Always Free ARM]
          service canvas(internet)[Canvas UI airvio.co knowgrph] in cloudflare
          service worker(server)[Exa mem0 Worker Cloudflare] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service d1(database)[D1 Read Cache] in cloudflare
          service r2(database)[R2 Long-term Archive] in cloudflare
          service kv(database)[KV Hot Index] in cloudflare
          service exa_search(server)[exa-mcp-server] in exa
          service mem0_api(server)[mem0 FastAPI REST] in oracle
          service qdrant(database)[Qdrant vector store] in oracle
          canvas:R --> L:worker
          worker:R --> L:gateway
          gateway:R --> L:exa_search
          worker:B --> T:d1
          worker:B --> T:r2
          worker:B --> T:kv
          worker:R --> L:mem0_api
          mem0_api:B --> T:qdrant
    event_model:
      key: event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui AcceleratorCohortSubmitted
        tf 02 cmd Mem0PreScanSearch
        tf 03 evt PriorScoresDVICacheGhostFlagsHydrated
        tf 04 cmd FetchProgramData
        tf 05 evt ProgramCriteriaVectorsReady
        tf 06 pcr TOPSISEngine
        tf 07 evt TOPSISRankReady
        tf 08 cmd FanOutCompanyResearch
        tf 09 evt CompanySignalBundleReady
        tf 10 cmd ComputeDVI
        tf 11 evt DVIScoresReady
        tf 12 cmd ClassifyStatuses
        tf 13 evt StatusVectorReady
        tf 14 cmd Mem0PostScanWrite
        tf 15 evt SnapshotMemoriesWritten
        tf 16 cmd RenderEcosystemPulse
        tf 17 evt DashboardReady

---


# Knowgrph Exa + mem0 - AcceleratorROI Scorer + EcosystemPulse Dashboard

> TOPSIS-ranked accelerator intelligence · cohort survival · pivot detection · `Low-score ≠ dead` · mem0-powered cross-session memory

---

## What This Demo Proves

| Capability | Required behavior |
|---|---|
| Exa MCP search | `deep_search_exa`, `company_research`, `web_search_exa`, `linkedin_search`, `crawling` route through exa-mcp-server |
| mem0 memory layer | `mem0.search()` pre-scan hydrates prior TOPSIS scores, DVI cache, Ghost flags — replaces R2 blob reads |
| DVI cache hit | If mem0 DVI age < 24h, `web_search_exa` probe is skipped entirely |
| Top Movers delta | TOPSIS Δ computed vs mem0 prior scores — `awaiting-baseline` on first scan |
| Ghost escalation | ≥3 consecutive Ghost flags from mem0 triggers `linkedin_search` confirm |
| mem0 write | Post-scan `mem0.add()` persists TOPSIS scores, DVI, status changes, Ghost flag increments |
| Wire format | CSV for flat data · minified JSON + CSV split (Template C) for `company_research` · plain text for crawl |
| Token economics | ~82% token reduction at N=20 vs stateless Exa-only baseline |
| TCO | near-zero — Exa API + Cloudflare free tier + mem0 self-hosted on Oracle Always Free ARM |
| Guard | Missing `exa_api_key` or `mem0_host` keeps live calls readiness-gated; demo mode runs inline with simulated memory |

---

## Running This Demo

### Step 1 - Open in Knowgrph Storyboard

Load this file into the Knowgrph canvas. The frontmatter defines all nodes, edges, and inline compute logic. No external build step required.

### Step 2 — Set inputs

Edit `AcceleratorSelector` (node `n_input`):
- `accelerator` — e.g. `"Y Combinator"`, `"Antler"`, `"Entrepreneur First"`
- `cohort_year` — e.g. `2022`, `2023`
- `company_list` — comma-separated startup names (up to 20 for demo)
- `exa_api_key` — leave blank for demo mode
- `mem0_host` — e.g. `https://your-oracle-arm-host` (leave blank for demo mode)
- `run_mode` — `"demo"` (default) or `"live"` (requires both keys)

### Step 3 — Pre-scan mem0 read

`Mem0MemoryLayer` fires first. In `run_mode=live` it calls:

```jsonc
POST https://{{mem0_host}}/v1/memories/search
{
  "query": "TOPSIS scores DVI status {{cohort_year}}",
  "user_id": "{{accelerator_slug}}-{{cohort_year}}",
  "limit": 50
}
```

Returns: prior TOPSIS per company, cached DVI (24h TTL check), Ghost flag counts, prior status. These hydrate downstream nodes before any Exa call fires.

In `run_mode=demo` the node returns simulated memory fragments — the full DAG still runs.

### Step 4 — Program layer

Click **Run** on `ProgramDataFetcher`. In live mode this fires:

```jsonc
{
  "tool": "deep_search_exa",
  "query": "{{accelerator}} cohort {{cohort_year}} survival rate funding raised Series A exits statistics",
  "num_results": 8
}
```

Output is extracted as **CSV** (Template A) at the synthesis node — ~80% token reduction vs pretty JSON. `TOPSISEngine` then runs TOPSIS on the criteria vectors.

### Step 5 — Company layer

Click **Run** on `CompanyDataFetcher`. In live mode this fires one `company_research` call per company using **Template C split** output:

```
Block 1: minified JSON (company record)
---SPLIT---
Block 2: CSV (funding events, FK on company_slug)
```

Then run `DigitalVisibilityIndex` — it checks the mem0 DVI cache first. If age < 24h the `web_search_exa` probe is skipped. Cache source shown per-company as `▲ mem0` or `⚡ exa`.

Run `StatusClassifier` — it reads mem0 Ghost flag counts. Any company with ≥3 consecutive Ghost flags is flagged `⚑ escalate→linkedin`.

### Step 6 — Post-scan mem0 write

After all compute nodes complete, mem0 write signals flow back to `Mem0MemoryLayer`:
- `topsis_write` — current TOPSIS scores per company
- `dvi_write` — current DVI + timestamp
- `status_write` — status changes + Ghost flag increments

In live mode: one `mem0.add()` call per company via `POST https://{{mem0_host}}/v1/memories`.

### Step 7 — Dashboard panels

Five panels populate automatically as upstream signals arrive:

| Panel | Node | What it shows |
|---|---|---|
| Panel 1 | `n_prg_fetcher` | TOPSIS rank + C_i score breakdown |
| mem0 panel | `n_mem0` | Namespace · prior score count · DVI cache entries · Ghost flags |
| Panel 2 | `n_dvi` | DVI bar chart · cache-hit vs probe source per company |
| Panel 3 | `n_classify` | Status donut · Ghost flag counts · ⚑ escalation markers |
| Panel 4 | `n_top_movers` | Δ TOPSIS gainers + losers vs mem0 prior · `awaiting-baseline` on first scan |
| Panel 5 | `n_quadrant` | Quadrant scatter: Rising Star / Quiet Champion / Struggling / Ghost |

### Ghost quadrant rule

A company in the Ghost quadrant (low TOPSIS + low DVI) is flagged `status: investigate`. This does **not** confirm shutdown. Before escalating to `status: likely-defunct` the pipeline must confirm both:

1. `crawl_404: true` — via `crawling` tool on company domain
2. `founders_departed: true` — via `linkedin_search` on founders

mem0 Ghost flag count gates this: if `ghost_n ≥ 3` the linkedin check is triggered automatically. If `ghost_n < 3` the company stays `investigate`.

---

## Exa MCP Tool Reference

| Tool | Node | Purpose | Wire format |
|---|---|---|---|
| `deep_search_exa` | `ProgramDataFetcher` | Batched program criteria: survival, funding, time-to-A, exits | **CSV** (Template A) |
| `company_research` | `CompanyDataFetcher` | Per-company structured crawl: status, funding, team, product | **minified JSON + CSV** (Template C split) |
| `web_search_exa` | `DigitalVisibilityIndex` | Blog/news mentions + job postings (DVI signals) · cache miss only | **CSV** (Template A) |
| `linkedin_search` | `DigitalVisibilityIndex` | Founder activity check; Ghost quadrant escalation guard | **CSV** (Template A) |
| `crawling` | `DigitalVisibilityIndex` | Domain freshness probe; `crawl_404` evidence for defunct check | plain text (Template D) |

---

## mem0 Integration

**Source:** [github.com/mem0ai/mem0](https://github.com/mem0ai/mem0) · MIT license · v1.0.0  
**Benchmarks:** +26% accuracy vs OpenAI Memory · 91% faster than full-context · 90% fewer tokens  
**Deploy:** `pip install mem0ai qdrant-client fastapi uvicorn` on Oracle Always Free ARM

### Namespace design

```
user_id = "{{accelerator_slug}}-{{cohort_year}}"
# e.g. "yc-2023", "antler-sg-2024", "ef-ldn-2023"
```

One namespace per accelerator × cohort pair. All company memories share that namespace; `mem0.search()` scoped to `user_id` keeps queries isolated.

### Memory schema

| Memory type | String template | Metadata keys |
|---|---|---|
| TOPSIS snapshot | `{{company}} TOPSIS score {{topsis}} on {{snapshot_date}}` | `company`, `topsis`, `snapshot_date` |
| DVI snapshot | `{{company}} DVI {{dvi}} on {{snapshot_date}}` | `company`, `dvi`, `snapshot_date` |
| Status change | `{{company}} status changed from {{prior}} to {{new}} on {{snapshot_date}}` | `company`, `prior_status`, `new_status` |
| Ghost flag | `{{company}} Ghost flag count {{ghost_n}} as of {{snapshot_date}}` | `company`, `ghost_n` |
| Founder confirm | `{{founder}} confirmed as founder at {{company}} via LinkedIn on {{date}}` | `founder`, `company`, `confirmed_date` |
| Funding event | `{{company}} raised {{round_type}} of ${{amount_m}}M announced {{date}}` | `company`, `round_type`, `amount_m` |

### Self-hosted setup

```bash
pip install mem0ai qdrant-client fastapi uvicorn
```

```python
# mem0_api.py — thin FastAPI wrapper callable from CF Workers via fetch()
from fastapi import FastAPI
from mem0 import Memory

app = FastAPI()
m = Memory.from_config("mem0_config.json")

@app.post("/v1/memories")
def add(p: dict):
    return m.add(p["messages"], user_id=p["user_id"], metadata=p.get("metadata", {}))

@app.post("/v1/memories/search")
def search(p: dict):
    return m.search(p["query"], user_id=p["user_id"], limit=p.get("limit", 10))
```

No Python runtime on Cloudflare required — CF Workers call `fetch("https://{{mem0_host}}/v1/memories/search", { method:"POST", body: JSON.stringify({...}) })`.

---

## TOPSIS Spec

### Criteria + weight matrix

| # | Criterion | `id` | Weight | Direction | `null` handling |
|---|---|---|---|---|---|
| 1 | Survival rate | `survival_rate` | **0.30** | benefit ↑ | exclude from matrix |
| 2 | Median funding raised | `median_funding_m` | **0.28** | benefit ↑ | substitute 0 |
| 3 | Time to Series A | `months_series_a` | **0.25** | cost ↓ | substitute 40 (worst-case penalty) |
| 4 | Notable exits | `exits_per_100` | **0.17** | benefit ↑ | substitute 0 |

Weights sum to `1.00`. Asserted on init: `abs(sum - 1.0) <= 0.001`.

### Steps

```
1. Build D[m×n]  (m accelerators × n criteria)
2. Normalize     R = D / ||D||_col
3. Weight        V = R × w_j
4. Ideal best    A+  max col if benefit, min col if cost
   Ideal worst   A−  min col if benefit, max col if cost
5. Distance      d+_i = ||V_i − A+||₂  ·  d−_i = ||V_i − A−||₂
6. Closeness     C_i  = d−_i / (d+_i + d−_i)   ∈ [0, 1]
7. Rank          sort descending by C_i
```

---

## Token Economics

| Step | Tool | Est. tokens raw | After format | Frequency | mem0 effect |
|---|---|---|---|---|---|
| Memory read | `mem0.search()` | ~150 | ~150 (minified JSON) | pre-scan (always) | replaces R2 blob read |
| Program fetch | `deep_search_exa` × 1 batch | ~2 400 | **~130** (CSV) | once per session | — |
| Company fetch | `company_research` × N | ~800 × N | **~180 × N** (JSON + CSV split) | once per cohort | — |
| DVI probe | `web_search_exa` × N | ~400 × N | **~60 × N** (CSV) | cache miss only (24h TTL) | skipped if mem0 hit |
| Status classify | Claude synthesis | ~600 × N | ~600 × N | cache miss only | mem0 Ghost flags reduce context |
| Top Movers explain | Claude synthesis | ~300 × movers | ~300 × movers | on-demand | mem0 replaces ~600-token R2 blob |
| Memory write | `mem0.add()` | ~80 × N | ~80 × N | post-scan (always) | — |

> At N=20: **net ~82% token reduction** vs stateless Exa-only baseline (20 400 → ~3 700 tokens/scan).

---

## Wire Format Reference

| Exa tool | Data shape | Format | Saving |
|---|---|---|---|
| `deep_search_exa` → TOPSIS criteria | flat tabular | **CSV** (Template A) | ~80% vs pretty JSON |
| `web_search_exa` → DVI signals | flat rows | **CSV** (Template A) | ~75% |
| `company_research` → company object | nested + sub-array | **minified JSON + CSV** (Template C split) | ~30% / ~75% |
| `linkedin_search` → founder profile | flat record | **CSV** (Template A) | ~65% |
| `crawling` → page content | prose | plain text (Template D) | n/a |
| `mem0.search()` → memory fragments | semi-nested | minified JSON | ~30% vs pretty |

**Template C** (company_research pattern):
```
Return TWO blocks separated by ---SPLIT---.
Block 1: minified JSON of the company record (no whitespace).
Block 2: CSV of the funding_events array.
  Header: company_slug,round_type,amount_m,date,source_url
No other text.
```

---

## KGC Schema

### Node types

| Sigil | `id` pattern | Type | Key fields |
|---|---|---|---|
| `@node` | `prg-{{accelerator_slug}}` | Program | `name:text`, `topsis_score:number`, `rank:number`, `cohort_size:number` |
| `@node` | `co-{{company_slug}}` | Company | `name:text`, `status:text`, `dvi:number`, `topsis:number`, `sector:text` |
| `@node` | `ev-{{company_slug}}-{{date}}` | FundingEvent | `round_type:text`, `amount_m:number`, `date:text`, `source_url:text` |
| `@node` | `snap-{{accelerator_slug}}-{{date}}` | Snapshot | `snapshot_date:text`, `cohort_year:text`, `scores:number[]` |
| `@node` | `mem-{{accelerator_slug}}-{{cohort_year}}` | MemoryStore | `mem0_user_id:text`, `host:text`, `last_write:text`, `memory_count:number` |

### Edge types

| Sigil | `id` pattern | Relationship | Required fields |
|---|---|---|---|
| `@edge` | `graduated-{{co}}-{{prg}}` | Company → Program | `cohort_year:text` |
| `@edge` | `raised-{{co}}-{{ev}}` | Company → FundingEvent | `months_post_grad:number`, `source_url:text` (required) |
| `@edge` | `pivoted-{{co}}-{{co2}}` | Company → Company | `pivot_type:text`, `evidence_url:text` |
| `@edge` | `acquired-{{acquirer}}-{{co}}` | Acquirer → Company | `acquisition_date:text`, `amount_m:number` |

### Cluster types

| Sigil | `id` | Cluster | Contains |
|---|---|---|---|
| `@cluster` | `cohort-{{prg}}-{{year}}` | Cohort | all `co-*` for that batch |
| `@cluster` | `sector-{{sector}}` | Sector | all `co-*` sharing sector |
| `@cluster` | `quadrant-{{q}}` | Quadrant | `rising-star` / `quiet-champion` / `struggling` / `ghost` |

---

## Validation Rules

1. `topsis_score ∈ [0, 1]` — clamp before write
2. `dvi ∈ [0, 100]` — round to integer
3. `status: defunct` requires **both** `crawl_404: true` AND `founders_departed: true` — never infer from DVI alone (`Low-score ≠ dead`)
4. `months_series_a: null` → substitute 40 in TOPSIS matrix; preserve `null` in `@node` field
5. All `@edge: raised-*` must have `source_url` — no unsourced funding events written to graph
6. `TopMovers` panel requires prior TOPSIS scores from `mem0.search()`; if no prior scores (first scan), render `status: awaiting-baseline` — do not read from R2
7. `mem0.add()` must be called post-scan for every company processed; failure to write is logged but does not block dashboard render
8. DVI cache: if `mem0.search("DVI {{company}}")` returns age < 24h, skip `web_search_exa` probe entirely
9. Ghost escalation: if `ghost_n ≥ 3` consecutive, trigger `linkedin_search` on founders before status update
10. Weights must sum to `1.00 ± 0.001` — assert on TOPSIS init

---

## ADRs

| # | Question | Default | Trigger for revisit |
|---|---|---|---|
| ADR-01 | TOPSIS or AHP for program ranking? | TOPSIS (deterministic, zero infra) | If pairwise weight justification is requested |
| ADR-02 | Companies per cohort before DVI cost exceeds budget? | Cap 20 for demo; full cohort async | Token cost > $2 threshold |
| ADR-03 | Ghost quadrant: auto-escalate to `defunct` after N days silent? | No auto-escalate; human-in-loop confirm | Product v2 scope |
| ADR-04 | mem0 self-hosted vs managed (app.mem0.ai)? | Self-hosted — MIT, zero SaaS cost, co-located with PocketBase on Oracle Always Free ARM | If Oracle ARM uptime issues or mem0 managed tier becomes free-tier viable |
| ADR-05 | R2 for snapshots? | mem0 for rolling 90d; R2 retained for long-term archival only (>90d cold JSON blobs). KV TTL index retired. | If mem0 self-host goes down; fallback to R2 cold read |
| ADR-06 | Sector taxonomy L1 only or L1+L2? | L1 only; L2 (`fintech/wealthtech` etc.) deferred | Post-demo if heatmap too coarse |
