---

title: "Knowgrph GTM Builders - AcceleratorROI Scorer + EcosystemPulse Dashboard"
graphId: "md:knowgrph-gtm-builders-exa"
doc_type: "GTM Builders Exa Demo"
date: "2026-06-12"
updated: "2026-06-12"
lang: "en-US"
schema: "kgc-computing-flow/v1"
status: draft
author: airvio/joohwee

# ── stack ────────────────────────────────────────────────────────────────────
product: Knowgrph / airvio
track: Startup Ecosystem
theme: Track what happens to startups after accelerator graduation
stack:
  search: exa-mcp-server (web_search_exa, deep_search_exa, company_research, crawling, linkedin_search)
  runtime: Cloudflare Workers + Pages
  storage: D1 (read cache) · R2 (snapshot blobs) · KV (ttl index)
  frontend: React · D3.js · Chart.js
  orchestration: KGC harness · Hermes Agent (MCP-callable)
  tco: near-zero (Exa API + Cloudflare free tier)

# ── domain identity variables ─────────────────────────────────────────────────
domain_vars:
  accelerator: "{{accelerator}}"       # e.g. Y Combinator, Antler, EF
  cohort_year: "{{cohort_year}}"       # e.g. 2022, 2023
  company: "{{company}}"              # individual startup name
  sector: "{{sector}}"                # e.g. fintech, deeptech, b2b-saas
  snapshot_date: "{{snapshot_date}}"  # ISO date of last Exa scan

# ── roi ───────────────────────────────────────────────────────────────────────
roi:
  formula: "(Impact × Reach) / (Build Hours + Monthly TCO + Token Cost/Month)"
  impact: 8
  reach: 7
  build_hours: 0.5
  monthly_tco: 2
  token_cost_month: 4
  score: 10.5

# ── orchestration ─────────────────────────────────────────────────────────────
orchestration_class: fan-out-aggregate
entry_point: InputWidget[AcceleratorSelector]
exit_point: RichMediaPanel[EcosystemPulseDashboard]
mcp_tools:
  - deep_search_exa
  - company_research
  - web_search_exa
  - linkedin_search
  - crawling

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
kgStorageDocPath: "huijoohwee/docs/knowgrph-gtm-builders-exa.md"
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
  chart_signal: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [chart_signal]}
  text_signal: {color: "#0ea5e9", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [text_signal]}
  number_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [number_signal]}
  rich_media_chart_html: {color: "var(--kg-canvas-accent)", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [rich_media_chart_html]}
  exa_result_signal: {color: "#22c55e", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [exa_result_signal]}
  approval_signal: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [approval_signal]}

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
      title: "AcceleratorROI + EcosystemPulse parallel lanes"
      value: |-
        gitGraph
          commit id:"accelerator_input" tag:"{{accelerator}}+{{cohort_year}}"
          branch program_layer
          checkout program_layer
          commit id:"deep_search_exa_batch"
          commit id:"topsis_engine"
          checkout main
          branch company_layer
          checkout company_layer
          commit id:"company_research_fanout"
          commit id:"dvi_probe"
          commit id:"status_classify"
          checkout main
          merge program_layer id:"program_scores"
          merge company_layer id:"company_signals"
          commit id:"ecosystem_pulse_dashboard" tag:"5-panel"
    harness_gantt:
      key: harness_gantt
      type: mermaid_gantt
      floatingPanelView: "gantt"
      floatingPanelOpen: true
      bottomPanelTab: "gantt"
      bottomPanelOpen: true
      title: "GTM builders Exa critical path"
      value: |-
        gantt
          title computing flow: gtm-builders-exa
          dateFormat YYYY-MM-DD
          section Input
          Accelerator selector :done, accel_input, 2026-06-12, 1d
          section Program layer
          deep_search_exa batch :prg_fetch, after accel_input, 1d
          TOPSIS engine :crit, topsis, after prg_fetch, 1d
          section Company layer
          company_research fan-out :co_fetch, after accel_input, 2d
          DVI probe (web_search_exa) :dvi, after co_fetch, 1d
          Status classify :classify, after dvi, 1d
          section Dashboard
          EcosystemPulse render :crit, dashboard, after topsis classify, 1d
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
          prg_fetcher["ProgramDataFetcher\n(ComputeWidget)\ndeep_search_exa × 4 criteria"]
          co_fetcher["CompanyDataFetcher\n(ComputeWidget)\ncompany_research × N"]
          topsis["TOPSISEngine\n(ComputeWidget)\nnormalize → weight → rank"]
          dvi["DigitalVisibilityIndex\n(ComputeWidget)\nweb + linkedin + crawl"]
          classify["StatusClassifier\n(ComputeWidget)\nactive/stealth/pivoted/defunct"]
          dashboard["EcosystemPulseDashboard\n(RichMediaPanel)\n5 panels"]
          accel_input -->|"text_signal: program query"| prg_fetcher
          accel_input -->|"text_signal: company list"| co_fetcher
          prg_fetcher -->|"exa_result_signal: criteria vectors"| topsis
          co_fetcher -->|"number_signal: visibility probes"| dvi
          co_fetcher -->|"exa_result_signal: funding + pivot"| classify
          topsis -->|"chart_signal: C_i rank vector"| dashboard
          dvi -->|"chart_signal: DVI[0-100]"| dashboard
          classify -->|"chart_signal: status taxonomy"| dashboard
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
          service canvas(internet)[Canvas UI airvio.co knowgrph] in cloudflare
          service worker(server)[GTM Worker Cloudflare] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service d1(database)[D1 KV TTL Index] in cloudflare
          service r2(database)[R2 Snapshot Blobs] in cloudflare
          service kv(database)[KV 24h Cache] in cloudflare
          service exa_search(server)[exa-mcp-server] in exa
          canvas:R --> L:worker
          worker:R --> L:gateway
          gateway:R --> L:exa_search
          worker:B --> T:d1
          worker:B --> T:r2
          worker:B --> T:kv
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
        tf 02 cmd FetchProgramData
        tf 03 evt ProgramCriteriaVectorsReady
        tf 04 pcr TOPSISEngine
        tf 05 evt TOPSISRankReady
        tf 06 cmd FanOutCompanyResearch
        tf 07 evt CompanySignalBundleReady
        tf 08 cmd ComputeDVI
        tf 09 evt DVIScoresReady
        tf 10 cmd ClassifyStatuses
        tf 11 evt StatusVectorReady
        tf 12 cmd RenderEcosystemPulse
        tf 13 evt DashboardReady
        tf 14 cmd TakeSnapshot
        tf 15 evt SnapshotStoredR2
        tf 16 ui ReplayFromSnapshot

# ── flow nodes ────────────────────────────────────────────────────────────────
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    # ── n_input ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_input"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "AcceleratorSelector + Exa API"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      handles: {key: handles, type: object, value: {"source":["accelerator","cohort_year","company_list","exa_api_key","run_mode"]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"previewField":"accelerator","previewMaxChars":80,"onEdit":{"trigger":"runDownstream","targets":["n_prg_fetcher","n_co_fetcher"]},"actions":[{"id":"edit","label":"Edit","icon":"pencil","trigger":"openFieldEditor","targetField":"accelerator"},{"id":"run","label":"Run All","icon":"play","trigger":"runDownstream","targets":["n_prg_fetcher","n_co_fetcher"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"accelerator":"text_signal","cohort_year":"text_signal","company_list":"text_signal","exa_api_key":"text_signal","run_mode":"text_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmAcceleratorSelector"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Entry widget. Set exa_api_key + run_mode=live to call real Exa MCP. Leave run_mode=demo for inline simulated output."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "input"}
      accelerator: {key: accelerator, type: string, value: "Y Combinator"}
      cohort_year: {key: cohort_year, type: number, value: 2023}
      company_list: {key: company_list, type: textarea, value: "Airbnb, Dropbox, Stripe, Brex, Gusto, Cruise, Coinbase, Reddit, DoorDash, Instacart"}
      exa_api_key: {key: exa_api_key, type: string, value: ""}
      run_mode: {key: run_mode, type: string, value: "demo"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    # ── n_prg_fetcher ────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_prg_fetcher"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "ProgramDataFetcher"}
      position: {key: position, type: object, value: {"x":460,"y":-280}}
      handles: {key: handles, type: object, value: {"target":["accelerator","cohort_year","exa_api_key","run_mode"],"source":["criteria_vector","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["accelerator","cohort_year","exa_api_key","run_mode"],"outputs":["criteria_vector","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_prg_fetcher.criteria_vector","field":"criteria_vector"},{"token":"n_prg_fetcher.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"criteria_vector","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["criteria_vector","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"accelerator":"text_signal","cohort_year":"text_signal","exa_api_key":"text_signal","run_mode":"text_signal"},"out":{"criteria_vector":"exa_result_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmProgramDataFetcher"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "run_mode=live → calls deep_search_exa via Exa MCP and runs TOPSIS. run_mode=demo → inline simulated TOPSIS."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      criteria_vector: {key: criteria_vector, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const acc = String(inputs?.accelerator||'Y Combinator').trim()
            const yr = String(inputs?.cohort_year||'2023').trim()
            const apiKey = String(inputs?.exa_api_key||'').trim()
            const isLive = String(inputs?.run_mode||'demo').trim() === 'live' && apiKey.length > 0
            // Live Exa: set run_mode=live + exa_api_key → calls deep_search_exa
            // Demo: runs inline TOPSIS with simulated data
            const seed = (acc.length + Number(yr)) % 7
            const data = [
              {name:acc,         s:72+seed,  f:4.2+seed*0.3, a:18-seed, e:8+seed},
              {name:'Antler',    s:61,       f:1.8,          a:24,      e:3},
              {name:'EF',        s:68,       f:2.9,          a:22,      e:5},
              {name:'Techstars', s:65,       f:3.1,          a:26,      e:6},
            ]
            const w = [0.30,0.28,0.25,0.17]
            const valid = Math.abs(w.reduce((a,b)=>a+b,0)-1.0)<=0.001
            const m = data.map(d=>[d.s,d.f,d.a,d.e])
            const norms = [0,1,2,3].map(j=>Math.sqrt(m.reduce((s,r)=>s+r[j]*r[j],0))||1)
            const V = m.map(r=>r.map((v,j)=>v/norms[j]*w[j]))
            const dir=[1,1,-1,1]
            const Ap=[0,1,2,3].map(j=>dir[j]===1?Math.max(...V.map(r=>r[j])):Math.min(...V.map(r=>r[j])))
            const Am=[0,1,2,3].map(j=>dir[j]===1?Math.min(...V.map(r=>r[j])):Math.max(...V.map(r=>r[j])))
            const Ci=V.map(row=>{const dp=Math.sqrt(row.reduce((s,v,j)=>s+(v-Ap[j])**2,0));const dm=Math.sqrt(row.reduce((s,v,j)=>s+(v-Am[j])**2,0));return dm/(dp+dm+1e-9)})
            const ranked=data.map((d,i)=>({...d,ci:Ci[i]})).sort((a,b)=>b.ci-a.ci)
            const modeLabel = isLive ? '⚡ Live mode: connect Exa MCP to run deep_search_exa' : 'Demo · set run_mode=live + exa_api_key for live data'
            const rows=ranked.map((d,i)=>'| '+(i+1)+' | '+esc(d.name)+' | '+d.ci.toFixed(3)+' | '+d.s+'% | $'+d.f+'M | '+d.a+' mo | '+d.e+' |').join('\n')
            const criteria_vector=['## TOPSIS — '+esc(acc)+' '+yr,'','| # | Accelerator | C_i | Survival | Funding | Months→A | Exits/100 |','|---|---|---|---|---|---|---|',rows,'','Weight assertion: '+(valid?'✓ sum=1.00':'✗ FAILED'),'> '+modeLabel].join('\n')
            const cards=ranked.map((d,i)=>'<div class="c"><span class="r">#'+(i+1)+'</span><b>'+esc(d.name)+'</b><span class="ci">C_i '+d.ci.toFixed(3)+'</span><span class="m">Survival '+d.s+'% · $'+d.f+'M · '+d.a+' mo·A · '+d.e+' exits/100</span></div>').join('')
            const outputSrcDoc='<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}.c{background:#fff;border:1px solid #e2e8f0;border-radius:8px;padding:8px 12px;margin-bottom:6px;display:flex;align-items:center;gap:8px;flex-wrap:wrap}.r{font-size:17px;font-weight:700;color:#6366f1;min-width:26px}.ci{font-size:11px;background:#ede9fe;color:#4f46e5;padding:2px 7px;border-radius:4px;font-weight:600}.m{font-size:11px;color:#64748b;flex:1 1 100%}h2{font-size:13px;font-weight:700;margin:0 0 8px;color:#1e293b}</style></head><body><h2>TOPSIS Program Rank — '+esc(acc)+' '+yr+'</h2>'+cards+'<p style="font-size:11px;color:#94a3b8;margin-top:6px">'+esc(modeLabel)+'</p></body></html>'
            return {criteria_vector, outputSrcDoc}
          }
    # ── n_co_fetcher ─────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_co_fetcher"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "CompanyDataFetcher"}
      position: {key: position, type: object, value: {"x":460,"y":240}}
      handles: {key: handles, type: object, value: {"target":["accelerator","cohort_year","company_list","exa_api_key","run_mode"],"source":["signal_bundle","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["accelerator","cohort_year","company_list","exa_api_key","run_mode"],"outputs":["signal_bundle","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_co_fetcher.signal_bundle","field":"signal_bundle"},{"token":"n_co_fetcher.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"signal_bundle","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["signal_bundle","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"accelerator":"text_signal","cohort_year":"text_signal","company_list":"text_signal","exa_api_key":"text_signal","run_mode":"text_signal"},"out":{"signal_bundle":"exa_result_signal","outputSrcDoc":"chart_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmCompanyDataFetcher"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "run_mode=live → calls Exa company_research per company. run_mode=demo → inline simulated signal bundle."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      signal_bundle: {key: signal_bundle, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const acc = String(inputs?.accelerator||'Y Combinator').trim()
            const yr = String(inputs?.cohort_year||'2023').trim()
            const raw = String(inputs?.company_list||'').trim()
            const apiKey = String(inputs?.exa_api_key||'').trim()
            const isLive = String(inputs?.run_mode||'demo').trim() === 'live' && apiKey.length > 0
            const cos = raw.split(/[,\n]+/).map(s=>s.trim()).filter(Boolean).slice(0,10)
            if(!cos.length) return {signal_bundle:'Enter company names.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>Enter company names in AcceleratorSelector.</p></body></html>'}
            const sts=['active','fundraising','stealth','pivoted','acquired','ipo','active','fundraising','active','stealth']
            const secs=['b2b-saas','consumer','fintech','deeptech','b2b-saas','healthtech','marketplace','consumer','fintech','b2b-saas']
            const rds=['Series B','Series C','Series A','Seed','IPO','Acquired','Series B','Series A','Series D','Stealth']
            const pal={active:'#d1fae5',fundraising:'#dbeafe',stealth:'#f1f5f9',pivoted:'#fef3c7',acquired:'#ede9fe',ipo:'#dcfce7'}
            const modeLabel = isLive ? '⚡ Live mode: connect Exa MCP to run company_research' : 'Demo · set run_mode=live + exa_api_key for live data'
            const entries = cos.map((c,i)=>({name:c, status:sts[i%sts.length], sector:secs[i%secs.length], round:rds[i%rds.length]}))
            const rows = entries.map(e=>'| '+[esc(e.name),e.status,e.sector,e.round].join(' | ')+' |').join('\n')
            const signal_bundle = ['## Company Signal Bundle — '+esc(acc)+' '+yr,'','| Company | Status | Sector | Last Round |','|---|---|---|---|',rows,'','> '+modeLabel].join('\n')
            const cards=entries.map(e=>'<div class="c"><b>'+esc(e.name)+'</b><span class="b" style="background:'+(pal[e.status]||'#f1f5f9')+'">'+e.status+'</span><span class="m">'+e.sector+' · '+e.round+'</span></div>').join('')
            const outputSrcDoc='<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}.c{background:#fff;border:1px solid #e2e8f0;border-radius:8px;padding:7px 12px;margin-bottom:5px;display:flex;align-items:center;gap:7px;flex-wrap:wrap}.b{font-size:11px;padding:1px 8px;border-radius:4px;font-weight:600;color:#1e293b}.m{font-size:11px;color:#64748b}h2{font-size:13px;font-weight:700;margin:0 0 8px;color:#1e293b}</style></head><body><h2>Company Signals — '+esc(acc)+' '+yr+'</h2>'+cards+'<p style="font-size:11px;color:#94a3b8;margin-top:6px">'+entries.length+' companies · '+esc(modeLabel)+'</p></body></html>'
            return {signal_bundle, outputSrcDoc}
          }
    # ── panel_p1 ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "panel_p1"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Panel 1 — TOPSIS Rank"}
      position: {key: position, type: object, value: {"x":900,"y":-280}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel 1 — TOPSIS Rank — receives outputSrcDoc from upstream ComputeWidget."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output: {key: output, type: textarea, value: "Panel 1 — TOPSIS Rank. Run ProgramDataFetcher to populate."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body style=\"font-family:system-ui;padding:16px\"><h2>Panel 1 — TOPSIS Rank</h2><p>Run ProgramDataFetcher to populate.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 28}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
    # ── n_dvi ────────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_dvi"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "DigitalVisibilityIndex"}
      position: {key: position, type: object, value: {"x":460,"y":520}}
      handles: {key: handles, type: object, value: {"target":["signal_bundle","exa_api_key","run_mode"],"source":["dvi_scores","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["signal_bundle","exa_api_key","run_mode"],"outputs":["dvi_scores","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_dvi.dvi_scores","field":"dvi_scores"},{"token":"n_dvi.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"dvi_scores","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["dvi_scores","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"signal_bundle":"exa_result_signal","exa_api_key":"text_signal","run_mode":"text_signal"},"out":{"dvi_scores":"number_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmDVI"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "run_mode=live → web_search_exa + linkedin_search + crawling. run_mode=demo → deterministic DVI."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      dvi_scores: {key: dvi_scores, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 30}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const raw = String(inputs?.signal_bundle||'').trim()
            const apiKey = String(inputs?.exa_api_key||'').trim()
            const isLive = String(inputs?.run_mode||'demo').trim() === 'live' && apiKey.length > 0
            if(!raw) return {dvi_scores:'Run CompanyDataFetcher first.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>Run CompanyDataFetcher first.</p></body></html>'}
            const coLines=raw.split('\n').filter(l=>l.startsWith('|')&&!l.includes('---')&&!l.includes('Company'))
            const cos=coLines.map(l=>l.split('|').map(s=>s.trim()).filter(Boolean)[0]).filter(Boolean).slice(0,10)
            if(!cos.length) return {dvi_scores:'No companies parsed.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>No companies.</p></body></html>'}
            const modeLabel = isLive ? '⚡ Live mode: connect Exa MCP to run web_search_exa probes' : 'Demo · set run_mode=live + exa_api_key for live data'
            const dviData=cos.map((c,i)=>{const base=30+((c.charCodeAt(0)+i*13)%55);const dvi=Math.min(100,Math.round(base));return{c,dvi,ghost:dvi<20}})
            const rows=dviData.map(d=>'| '+[esc(d.c),d.dvi,d.ghost?'⚠ Ghost':''].join(' | ')+' |').join('\n')
            const dvi_scores=['## Digital Visibility Index','','| Company | DVI [0-100] | Ghost? |','|---|---|---|',rows,'','> Low DVI ≠ defunct · '+modeLabel].join('\n')
            const bars=dviData.map(d=>'<div class="r"><span class="l">'+esc(d.c)+'</span><div class="w"><div class="b" style="width:'+d.dvi+'%;background:'+(d.dvi>=50?'#22c55e':d.dvi>=25?'#f59e0b':'#ef4444')+'"></div></div><span class="v">'+d.dvi+(d.ghost?' ⚠':'')+'</span></div>').join('')
            const outputSrcDoc='<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}h2{font-size:13px;font-weight:700;margin:0 0 8px;color:#1e293b}.r{display:flex;align-items:center;gap:8px;margin-bottom:6px}.l{min-width:100px;font-size:12px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.w{flex:1;height:13px;background:#e2e8f0;border-radius:6px;overflow:hidden}.b{height:100%;border-radius:6px}.v{font-size:11px;color:#64748b;min-width:28px;text-align:right}</style></head><body><h2>Digital Visibility Index</h2>'+bars+'<p style="font-size:11px;color:#94a3b8;margin-top:8px">Low DVI ≠ defunct · '+esc(modeLabel)+'</p></body></html>'
            return {dvi_scores, outputSrcDoc}
          }
    # ── panel_p2 ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "panel_p2"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Panel 2 — Digital Visibility Index"}
      position: {key: position, type: object, value: {"x":900,"y":520}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel 2 — Digital Visibility Index — receives outputSrcDoc from upstream ComputeWidget."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output: {key: output, type: textarea, value: "Panel 2 — Digital Visibility Index. Run DVI to populate."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body style=\"font-family:system-ui;padding:16px\"><h2>Panel 2 — DVI</h2><p>Run CompanyDataFetcher + DVI to populate.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 28}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
    # ── n_classify ───────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_classify"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "StatusClassifier"}
      position: {key: position, type: object, value: {"x":460,"y":760}}
      handles: {key: handles, type: object, value: {"target":["signal_bundle"],"source":["status_vector","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["signal_bundle"],"outputs":["status_vector","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_classify.status_vector","field":"status_vector"},{"token":"n_classify.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"status_vector","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["status_vector","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"signal_bundle":"exa_result_signal"},"out":{"status_vector":"text_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmStatusClassifier"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "MECE status donut from signal bundle. defunct = crawl_404 AND founders_departed only."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      status_vector: {key: status_vector, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 28}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 6}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const raw = String(inputs?.signal_bundle||'').trim()
            if(!raw) return {status_vector:'Run CompanyDataFetcher first.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>Run CompanyDataFetcher first.</p></body></html>'}
            const lines=raw.split('\n').filter(l=>l.startsWith('|')&&!l.includes('---')&&!l.includes('Company'))
            const entries=lines.map(l=>{const p=l.split('|').map(s=>s.trim()).filter(Boolean);return p.length>=2?{name:p[0],status:p[1],sector:p[2]||'other',round:p[3]||''}:null}).filter(Boolean)
            if(!entries.length) return {status_vector:'No company data.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>No data.</p></body></html>'}
            const counts={}
            entries.forEach(e=>{counts[e.status]=(counts[e.status]||0)+1})
            const pal={active:'#1D9E75',fundraising:'#378ADD',stealth:'#888780',pivoted:'#EF9F27',acquired:'#534AB7',ipo:'#639922',defunct:'#E24B4A'}
            const rows=entries.map(e=>'| '+[esc(e.name),e.status,e.sector,e.round].join(' | ')+' |').join('\n')
            const status_vector=['## Status Vector','','| Company | Status | Sector | Last Round |','|---|---|---|---|',rows,'','> defunct = crawl_404 AND founders_departed · never from DVI alone'].join('\n')
            const donut=Object.entries(counts).map(([st,n])=>'<span class="s"><span class="d" style="background:'+(pal[st]||'#9ca3af')+'"></span>'+esc(st)+' '+n+'</span>').join('')
            const cards=entries.map(e=>'<div class="c"><span class="d" style="background:'+(pal[e.status]||'#9ca3af')+'"></span><b>'+esc(e.name)+'</b><span class="st">'+e.status+'</span><span class="meta">'+e.sector+' · '+e.round+'</span></div>').join('')
            const outputSrcDoc='<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}h2{font-size:13px;font-weight:700;margin:0 0 7px;color:#1e293b}.dn{display:flex;flex-wrap:wrap;gap:6px;padding:8px;background:#fff;border:1px solid #e2e8f0;border-radius:8px;margin-bottom:8px}.s{display:flex;align-items:center;gap:4px;font-size:12px}.d{width:9px;height:9px;border-radius:50%;flex-shrink:0}.c{display:flex;align-items:center;gap:6px;background:#fff;border:1px solid #e2e8f0;border-radius:6px;padding:6px 10px;margin-bottom:5px;flex-wrap:wrap}.st{font-size:11px;background:#f1f5f9;padding:1px 7px;border-radius:4px}.meta{font-size:11px;color:#64748b;flex:1 1 100%}</style></head><body><h2>Status Donut ('+entries.length+' companies)</h2><div class="dn">'+donut+'</div>'+cards+'<p style="font-size:11px;color:#94a3b8;margin-top:6px">defunct = crawl_404 + founders_departed</p></body></html>'
            return {status_vector, outputSrcDoc}
          }
    # ── panel_p3 ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "panel_p3"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Panel 3 — Status Donut"}
      position: {key: position, type: object, value: {"x":900,"y":760}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel 3 — Status Donut — receives outputSrcDoc from upstream ComputeWidget."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output: {key: output, type: textarea, value: "Panel 3 — Status Donut. Run StatusClassifier to populate."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body style=\"font-family:system-ui;padding:16px\"><h2>Panel 3 — Status Donut</h2><p>Run CompanyDataFetcher + StatusClassifier to populate.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 26}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 6}
    # ── n_funding ────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_funding"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "FundingTimeline"}
      position: {key: position, type: object, value: {"x":460,"y":1000}}
      handles: {key: handles, type: object, value: {"target":["signal_bundle","exa_api_key","run_mode"],"source":["funding_events","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["signal_bundle","exa_api_key","run_mode"],"outputs":["funding_events","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_funding.funding_events","field":"funding_events"},{"token":"n_funding.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"funding_events","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["funding_events","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"signal_bundle":"exa_result_signal","exa_api_key":"text_signal","run_mode":"text_signal"},"out":{"funding_events":"text_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmFundingTimeline"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "run_mode=live → deep_search_exa funding rounds. run_mode=demo → deterministic timeline."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      funding_events: {key: funding_events, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 26}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 8}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const raw = String(inputs?.signal_bundle||'').trim()
            const apiKey = String(inputs?.exa_api_key||'').trim()
            const isLive = String(inputs?.run_mode||'demo').trim() === 'live' && apiKey.length > 0
            if(!raw) return {funding_events:'Run CompanyDataFetcher first.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>Run CompanyDataFetcher first.</p></body></html>'}
            const coLines=raw.split('\n').filter(l=>l.startsWith('|')&&!l.includes('---')&&!l.includes('Company'))
            const entries=coLines.map(l=>{const p=l.split('|').map(s=>s.trim()).filter(Boolean);return p.length>=4?{name:p[0],status:p[1],sector:p[2],round:p[3]}:null}).filter(Boolean).slice(0,10)
            if(!entries.length) return {funding_events:'No company data.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>No data.</p></body></html>'}
            const modeLabel = isLive ? '⚡ Live mode: connect Exa MCP to run deep_search_exa funding search' : 'Demo · set run_mode=live + exa_api_key for live data'
            const rdAmt={Seed:2,'Series A':8,'Series B':25,'Series C':60,'Series D':100,IPO:0,Acquired:0,Stealth:0}
            const events = entries.map((e,i)=>{const yr=2020+(i%4);const mo=1+(i*3)%9;return{...e,amount:rdAmt[e.round]||0,date:`${yr}-0${mo}-01`}})
            const rows=events.map(e=>'| '+[esc(e.name),e.round,e.amount?'$'+e.amount+'M':'—',e.date.slice(0,7)].join(' | ')+' |').join('\n')
            const funding_events=['## Funding Timeline','','| Company | Round | Amount | Date |','|---|---|---|---|',rows,'','> '+modeLabel].join('\n')
            const tlItems=events.map((e,i)=>{const pct=Math.round((i/Math.max(events.length-1,1))*100);const col=e.round.includes('Series')?'#378ADD':e.round==='IPO'?'#639922':e.round==='Acquired'?'#534AB7':'#6366f1';return'<div class="ev" style="left:'+pct+'%"><div class="dot" style="background:'+col+'"></div><div class="lbl"><b>'+esc(e.name.slice(0,10))+'</b><span>'+e.round+(e.amount?' $'+e.amount+'M':'')+'</span><span>'+e.date.slice(0,7)+'</span></div></div>'}).join('')
            const outputSrcDoc='<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}h2{font-size:13px;font-weight:700;margin:0 0 12px;color:#1e293b}.tl{position:relative;height:4px;background:#e2e8f0;border-radius:2px;margin:40px 4px 70px}.ev{position:absolute;transform:translateX(-50%)}.dot{width:12px;height:12px;border-radius:50%;margin:-4px auto 0}.lbl{position:absolute;top:14px;left:50%;transform:translateX(-50%);text-align:center;white-space:nowrap;font-size:10px;color:#475569;display:flex;flex-direction:column;gap:1px}b{font-size:11px;color:#1e293b;font-weight:600}</style></head><body><h2>Funding Timeline</h2><div class="tl">'+tlItems+'</div><p style="font-size:11px;color:#94a3b8;margin-top:66px">'+esc(modeLabel)+'</p></body></html>'
            return {funding_events, outputSrcDoc}
          }
    # ── panel_p4 ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "panel_p4"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Panel 4 — Funding Timeline"}
      position: {key: position, type: object, value: {"x":900,"y":1000}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel 4 — Funding Timeline — receives outputSrcDoc from upstream ComputeWidget."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output: {key: output, type: textarea, value: "Panel 4 — Funding Timeline. Run FundingTimeline to populate."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body style=\"font-family:system-ui;padding:16px\"><h2>Panel 4 — Funding Timeline</h2><p>Run CompanyDataFetcher + FundingTimeline to populate.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 8}
    # ── n_quadrant ───────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "n_quadrant"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "QuadrantMap"}
      position: {key: position, type: object, value: {"x":460,"y":-560}}
      handles: {key: handles, type: object, value: {"target":["criteria_vector","dvi_scores"],"source":["quadrant_data","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["criteria_vector","dvi_scores"],"outputs":["quadrant_data","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"n_quadrant.quadrant_data","field":"quadrant_data"},{"token":"n_quadrant.outputSrcDoc","field":"outputSrcDoc"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"quadrant_data","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["quadrant_data","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"criteria_vector":"exa_result_signal","dvi_scores":"number_signal"},"out":{"quadrant_data":"text_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "gtmQuadrantMap"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "SVG scatter plot: TOPSIS C_i (x) × DVI (y). Ghost ≠ defunct."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      quadrant_data: {key: quadrant_data, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const esc = v => String(v||'').replace(/[&<>"']/g,c=>c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const rankRaw=String(inputs?.criteria_vector||'').trim()
            const dviRaw=String(inputs?.dvi_scores||'').trim()
            if(!rankRaw) return {quadrant_data:'Run ProgramDataFetcher first.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>Run ProgramDataFetcher first.</p></body></html>'}
            const rankLines=rankRaw.split('\n').filter(l=>l.startsWith('|')&&!l.includes('---')&&!l.includes('#'))
            const rankE=rankLines.map(l=>{const p=l.split('|').map(s=>s.trim()).filter(Boolean);return p.length>=3?{name:p[1],ci:parseFloat(p[2])||0}:null}).filter(Boolean)
            const dviLines=dviRaw.split('\n').filter(l=>l.startsWith('|')&&!l.includes('---')&&!l.includes('Company'))
            const dviE=dviLines.map(l=>{const p=l.split('|').map(s=>s.trim()).filter(Boolean);return p.length>=2?{name:p[0],dvi:parseInt(p[1])||0}:null}).filter(Boolean)
            if(!rankE.length) return {quadrant_data:'No rank data.',outputSrcDoc:'<!doctype html><html><body style="font-family:system-ui;padding:16px"><p>No data.</p></body></html>'}
            const medCi=rankE.reduce((s,e)=>s+e.ci,0)/rankE.length
            const medDvi=dviE.length?dviE.reduce((s,e)=>s+e.dvi,0)/dviE.length:50
            const quad=(ci,dvi)=>ci>=medCi&&dvi>=medDvi?'Rising Star':ci>=medCi?'Quiet Champion':dvi>=medDvi?'Struggling':'Ghost ⚠'
            const points=rankE.map(r=>{const d=dviE.find(d=>d.name===r.name);const dvi=d?d.dvi:Math.round(40+r.ci*30);return{...r,dvi,q:quad(r.ci,dvi)}})
            const rows=points.map(p=>'| '+[esc(p.name),p.ci.toFixed(3),p.dvi,p.q].join(' | ')+' |').join('\n')
            const quadrant_data=['## Quadrant Map','','| Company | C_i | DVI | Quadrant |','|---|---|---|---|',rows,'','> Ghost ⚠ ≠ defunct — requires crawl_404 + founders_departed confirm'].join('\n')
            const W=480,H=300,PAD=50
            const maxCi=Math.max(...points.map(p=>p.ci),1)
            const maxDvi=Math.max(...points.map(p=>p.dvi),100)
            const px=ci=>PAD+Math.round((ci/maxCi)*(W-PAD*2))
            const py=dvi=>H-PAD-Math.round((dvi/maxDvi)*(H-PAD*2))
            const dots=points.map(p=>{const x=px(p.ci),y=py(p.dvi),col=p.q==='Rising Star'?'#22c55e':p.q==='Quiet Champion'?'#8b5cf6':p.q==='Struggling'?'#f59e0b':'#ef4444';return`<circle cx="${x}" cy="${y}" r="7" fill="${col}" opacity="0.85"/><text x="${x}" y="${y-11}" font-size="9" text-anchor="middle" fill="#1e293b">${esc(p.name.slice(0,12))}</text>`}).join('')
            const mX=px(medCi),mY=py(medDvi)
            const svgBody=`<line x1="${mX}" y1="${PAD}" x2="${mX}" y2="${H-PAD}" stroke="#cbd5e1" stroke-dasharray="4"/><line x1="${PAD}" y1="${mY}" x2="${W-PAD}" y2="${mY}" stroke="#cbd5e1" stroke-dasharray="4"/>${dots}<text x="${PAD}" y="${H-5}" font-size="9" fill="#94a3b8">C_i →</text><text x="5" y="${PAD}" font-size="9" fill="#94a3b8">DVI</text>`
            const outputSrcDoc=`<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:14px;font-family:system-ui,sans-serif;background:#f8fafc}h2{font-size:13px;font-weight:700;margin:0 0 8px;color:#1e293b}svg{display:block;max-width:100%}.legend{display:flex;gap:10px;flex-wrap:wrap;margin-top:8px;font-size:11px}.li{display:flex;align-items:center;gap:4px}.dot{width:9px;height:9px;border-radius:50%}</style></head><body><h2>Quadrant Map</h2><svg viewBox="0 0 ${W} ${H}">${svgBody}</svg><div class="legend"><span class="li"><span class="dot" style="background:#22c55e"></span>Rising Star</span><span class="li"><span class="dot" style="background:#8b5cf6"></span>Quiet Champion</span><span class="li"><span class="dot" style="background:#f59e0b"></span>Struggling</span><span class="li"><span class="dot" style="background:#ef4444"></span>Ghost ⚠</span></div><p style="font-size:11px;color:#94a3b8;margin-top:6px">Ghost ≠ defunct · Median lines shown</p></body></html>`
            return {quadrant_data, outputSrcDoc}
          }
    # ── panel_p5 ─────────────────────────────────────────────────────────────
    - id: {key: id, type: string, value: "panel_p5"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Panel 5 — Quadrant Map"}
      position: {key: position, type: object, value: {"x":900,"y":-560}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel 5 — Quadrant Map — receives outputSrcDoc from upstream ComputeWidget."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output: {key: output, type: textarea, value: "Panel 5 — Quadrant Map. Run QuadrantMap to populate."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body style=\"font-family:system-ui;padding:16px\"><h2>Panel 5 — Quadrant Map</h2><p>Run ProgramDataFetcher + DVI + QuadrantMap to populate.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 30}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
  edges:
    - {"id":"e_input_prg","source":"n_input","sourceHandle":"accelerator","target":"n_prg_fetcher","targetHandle":"accelerator"}
    - {"id":"e_input_yr","source":"n_input","sourceHandle":"cohort_year","target":"n_prg_fetcher","targetHandle":"cohort_year"}
    - {"id":"e_input_key_prg","source":"n_input","sourceHandle":"exa_api_key","target":"n_prg_fetcher","targetHandle":"exa_api_key"}
    - {"id":"e_input_mode_prg","source":"n_input","sourceHandle":"run_mode","target":"n_prg_fetcher","targetHandle":"run_mode"}
    - {"id":"e_input_co","source":"n_input","sourceHandle":"company_list","target":"n_co_fetcher","targetHandle":"company_list"}
    - {"id":"e_input_acc_co","source":"n_input","sourceHandle":"accelerator","target":"n_co_fetcher","targetHandle":"accelerator"}
    - {"id":"e_input_key_co","source":"n_input","sourceHandle":"exa_api_key","target":"n_co_fetcher","targetHandle":"exa_api_key"}
    - {"id":"e_input_mode_co","source":"n_input","sourceHandle":"run_mode","target":"n_co_fetcher","targetHandle":"run_mode"}
    - {"id":"e_prg_p1","source":"n_prg_fetcher","sourceHandle":"outputSrcDoc","target":"panel_p1","targetHandle":"outputSrcDoc","label":"TOPSIS rank cards","type":"rich_media_chart_html"}
    - {"id":"e_co_dvi","source":"n_co_fetcher","sourceHandle":"signal_bundle","target":"n_dvi","targetHandle":"signal_bundle"}
    - {"id":"e_input_key_dvi","source":"n_input","sourceHandle":"exa_api_key","target":"n_dvi","targetHandle":"exa_api_key"}
    - {"id":"e_input_mode_dvi","source":"n_input","sourceHandle":"run_mode","target":"n_dvi","targetHandle":"run_mode"}
    - {"id":"e_dvi_p2","source":"n_dvi","sourceHandle":"outputSrcDoc","target":"panel_p2","targetHandle":"outputSrcDoc","label":"DVI bar chart","type":"rich_media_chart_html"}
    - {"id":"e_co_classify","source":"n_co_fetcher","sourceHandle":"signal_bundle","target":"n_classify","targetHandle":"signal_bundle"}
    - {"id":"e_classify_p3","source":"n_classify","sourceHandle":"outputSrcDoc","target":"panel_p3","targetHandle":"outputSrcDoc","label":"status donut","type":"rich_media_chart_html"}
    - {"id":"e_co_funding","source":"n_co_fetcher","sourceHandle":"signal_bundle","target":"n_funding","targetHandle":"signal_bundle"}
    - {"id":"e_input_key_funding","source":"n_input","sourceHandle":"exa_api_key","target":"n_funding","targetHandle":"exa_api_key"}
    - {"id":"e_input_mode_funding","source":"n_input","sourceHandle":"run_mode","target":"n_funding","targetHandle":"run_mode"}
    - {"id":"e_funding_p4","source":"n_funding","sourceHandle":"outputSrcDoc","target":"panel_p4","targetHandle":"outputSrcDoc","label":"funding timeline","type":"rich_media_chart_html"}
    - {"id":"e_prg_quad","source":"n_prg_fetcher","sourceHandle":"criteria_vector","target":"n_quadrant","targetHandle":"criteria_vector"}
    - {"id":"e_dvi_quad","source":"n_dvi","sourceHandle":"dvi_scores","target":"n_quadrant","targetHandle":"dvi_scores"}
    - {"id":"e_quad_p5","source":"n_quadrant","sourceHandle":"outputSrcDoc","target":"panel_p5","targetHandle":"outputSrcDoc","label":"quadrant scatter","type":"rich_media_chart_html"}
---
# AcceleratorROI Scorer + EcosystemPulse Dashboard

> TOPSIS-ranked accelerator intelligence · cohort survival · pivot detection · `Low-score ≠ dead`

---

## 1. Product Overview

Two coupled views over the same Exa-sourced data spine:

| Layer | View | Unit of analysis | Output |
|---|---|---|---|
| Program | AcceleratorROI Scorer | Accelerator program | TOPSIS rank + score breakdown |
| Cohort | EcosystemPulse Dashboard | Individual startup | 5-panel status dashboard |

The program ranker answers: **which accelerator produces the best post-graduation outcomes?**
The cohort dashboard answers: **what is happening right now inside a specific batch?**

Both run off the same harness. `{{accelerator}}` + `{{cohort_year}}` are the only required inputs.

---

## 2. Running This Demo

### Step 1 - Open in Knowgrph Storyboard

Load this file into the Knowgrph canvas. The frontmatter defines all nodes, edges, and compute inline. No external build step required.

### Step 2 — Set inputs

Edit `AcceleratorSelector` (node `n_input`):
- `accelerator` — e.g. `"Y Combinator"`, `"Antler"`, `"Entrepreneur First"`
- `cohort_year` — e.g. `2022`, `2023`
- `company_list` — comma-separated startup names

### Step 3 — Run program layer (Exa MCP)

Click **Fetch Program Data** on `ProgramDataFetcher`. This fires:

```jsonc
// MCP call — exa-mcp-server
{
  "tool": "deep_search_exa",
  "query": "{{accelerator}} cohort {{cohort_year}} survival rate funding raised Series A exits statistics",
  "num_results": 8
}
```

Then click **Run TOPSIS** on `TOPSISEngine` to produce the `C_i` rank vector.

### Step 4 — Run company layer (Exa MCP fan-out)

Click **Fetch Company Data** on `CompanyDataFetcher`. This fires one `company_research` call per company (capped at 20 for demo; results KV-cached 24h):

```jsonc
{
  "tool": "company_research",
  "company_url": "https://{{company_domain}}",
  "goal": "Extract: current status, last funding round, product description, founding team"
}
```

Then run **Compute DVI** and **Classify Statuses** in any order — both depend only on the signal bundle.

### Step 5 — View EcosystemPulse Dashboard

The `RichMediaPanel[EcosystemPulseDashboard]` auto-updates when all three upstream signals arrive. Five panels render inline.

### Ghost quadrant rule

A company with low TOPSIS + low DVI is placed in the **Ghost quadrant** (`status: investigate`). This does **not** confirm shutdown. Before escalating to `status: likely-defunct` the pipeline must confirm both:

1. `crawl_404: true` — via `crawling` tool on company domain
2. `founders_departed: true` — via `linkedin_search` on founders

```jsonc
// Triggered only when DVI < 20
{
  "tool": "linkedin_search",
  "query": "{{founder_name}} {{company}} founder",
  "num_results": 1
}
```

---

## 3. Exa MCP Tool Reference

All search calls route through `exa-mcp-server`. The five tools used in this demo:

| Tool | Used by node | Purpose |
|---|---|---|
| `deep_search_exa` | `ProgramDataFetcher` | Batched program-level criteria: survival, funding, time-to-A, exits |
| `company_research` | `CompanyDataFetcher` | Per-company structured crawl: status, funding, team, product |
| `web_search_exa` | `DigitalVisibilityIndex` | Blog/news mentions + job postings (DVI signals) |
| `linkedin_search` | `DigitalVisibilityIndex` | Founder activity check; Ghost quadrant escalation guard |
| `crawling` | `DigitalVisibilityIndex` | Domain freshness probe; `crawl_404` evidence for defunct check |

### Token budget

| Step | Tool | Est. tokens | Frequency |
|---|---|---|---|
| Program fetch | `deep_search_exa` × 1 batch | ~2 400 | once per session |
| Company fetch | `company_research` × N | ~800 × N | once per cohort; KV 24h |
| DVI probe | `web_search_exa` × N | ~400 × N | KV 24h |
| Status classify | Claude synthesis | ~600 × N | KV 24h |
| Delta explain | Claude synthesis | ~300 × movers | on-demand |

> Optimization: pre-cache company-level results in KV with 24h TTL. Program-level TOPSIS only recomputes on explicit user refresh. Snapshots stored in R2 as `snapshot-{{accelerator_slug}}-{{cohort_year}}-{{snapshot_date}}.json`.

---

## 4. TOPSIS Spec

### Criteria + weight matrix

| # | Criterion | `id` | Weight | Direction | Unit | `null` handling |
|---|---|---|---|---|---|---|
| 1 | Survival rate | `survival_rate` | **0.30** | benefit ↑ | % | exclude from matrix |
| 2 | Median funding raised | `median_funding_m` | **0.28** | benefit ↑ | $M | substitute 0 |
| 3 | Time to Series A | `months_series_a` | **0.25** | cost ↓ | months | substitute 40 (worst-case) |
| 4 | Notable exits | `exits_per_100` | **0.17** | benefit ↑ | exits/100 | substitute 0 |

Weights sum to `1.00`. Asserted on init: `abs(sum - 1.0) <= 0.001`.

### TOPSIS steps

```
1. Build D[m×n]  (m accelerators × n criteria)
2. Normalize     R = D / ||D||_col
3. Weight        V = R × w_j
4. Ideal best    A+  max col if benefit, min col if cost
   Ideal worst   A−  min col if benefit, max col if cost
5. Distance      d+_i = ||V_i − A+||₂
                 d−_i = ||V_i − A−||₂
6. Closeness     C_i  = d−_i / (d+_i + d−_i)   ∈ [0, 1]
7. Rank          sort descending by C_i
```

---

## 5. Dashboard Panels

### Panel 1 — Quadrant Map

D3 scatter · X = TOPSIS score · Y = DVI · quadrant lines at `median(x)`, `median(y)` · click company → CompanyCard overlay.

```
        high DVI
            │
  Struggling│  Rising Star
  (visible, │  (high score,
   low score)│  high visible)
─────────────┼─────────────── TOPSIS score
  Ghost      │  Quiet Champion
  (investigate│ (high score,
   ≠ dead)   │  low visible / stealth)
            │
        low DVI
```

### Panel 2 — Status Donut

Chart.js doughnut · center label = cohort size · color palette:

| Status | Code | Color |
|---|---|---|
| Active | `active` | `#1D9E75` |
| Fundraising | `fundraising` | `#378ADD` |
| Stealth | `stealth` | `#888780` |
| Pivoted | `pivoted` | `#EF9F27` |
| Acquired | `acquired` | `#534AB7` |
| IPO'd | `ipo` | `#639922` |
| Likely Defunct | `defunct` | `#E24B4A` |

### Panel 3 — Funding Timeline

D3 horizontal timeline · Y = company · X = date · bubble size = amount · hover → tooltip · click → open source URL.

Exa sourcing per company:
```
deep_search_exa:  "{{company}}" funding raised 2023 2024 2025 press release
web_search_exa:   "{{company}}" Series A seed round announced
```

### Panel 4 — Sector Heatmap

D3 heatmap · X = accelerator · Y = sector · fill = mean TOPSIS score · cell label = count · click cell → filter QuadrantMap.

Sector L1 taxonomy: `fintech` · `deeptech` · `b2b-saas` · `consumer` · `healthtech` · `climatetech` · `marketplace` · `other`

### Panel 5 — Top Movers

Top 3 gainers (teal) + top 3 losers (coral) vs prior `{{snapshot_date}}`. Requires R2 snapshot baseline; renders `status: awaiting-baseline` if missing.

Change driver explanation prompt (on-demand, per mover):
```
Given that {{company}} moved from TOPSIS {{prior}} to {{current}},
identify the most likely cause from recent Exa signals:
funding event / founder departure / product launch / press / silence.
Return: { driver: string, confidence: low|med|high, evidence_url: string }
```

---

## 6. KGC Schema

### Node types

| Sigil | `id` pattern | Type | Key fields |
|---|---|---|---|
| `@node` | `prg-{{accelerator_slug}}` | Program | `name:text`, `topsis_score:number`, `rank:number` |
| `@node` | `co-{{company_slug}}` | Company | `name:text`, `status:text`, `dvi:number`, `topsis:number`, `sector:text` |
| `@node` | `ev-{{company_slug}}-{{date}}` | FundingEvent | `round_type:text`, `amount_m:number`, `source_url:text` |
| `@node` | `snap-{{accelerator_slug}}-{{date}}` | Snapshot | `snapshot_date:text`, `cohort_year:text`, `scores:number[]` |

### Edge types

| Sigil | `id` pattern | Relationship | Typed fields |
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

## 7. Validation Rules

1. `topsis_score ∈ [0, 1]` — clamp before write
2. `dvi ∈ [0, 100]` — round to integer
3. `status: defunct` requires **both** `crawl_404: true` AND `founders_departed: true` — never infer from DVI alone (`Low-score ≠ dead`)
4. `months_series_a: null` → substitute 40 in TOPSIS matrix; preserve `null` in `@node` field
5. All `@edge: raised-*` must have `source_url` — no unsourced funding events written to graph
6. `TopMovers` panel requires `snapshot_prior` in R2; if missing, render empty with `status: awaiting-baseline`
7. Weights must sum to `1.00 ± 0.001` — assert on TOPSIS init

---

## 8. Open Questions / ADRs

| # | Question | Default | Trigger for revisit |
|---|---|---|---|
| ADR-01 | TOPSIS or AHP for program ranking? | TOPSIS (deterministic, zero infra) | If pairwise weight justification is requested |
| ADR-02 | Companies per cohort before DVI cost exceeds budget? | Cap 20 for demo; full cohort async | Token cost > $2 threshold |
| ADR-03 | Ghost quadrant: auto-escalate to `defunct` after N days silent? | No auto-escalate; human-in-loop | Product v2 scope |
| ADR-04 | Store snapshots in R2 or D1? | R2 (blob) for JSON snapshots; D1 for queryable index only | Cross-cohort queries become primary |
| ADR-05 | Sector taxonomy L1 only or L1+L2? | L1 only; L2 (`fintech/wealthtech` etc.) deferred | Post-demo if heatmap too coarse |
