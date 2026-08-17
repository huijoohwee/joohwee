---
title: "Knowgrph Token Economics Model Demo - Storyboard Cost Driver Ports"
doc_type: "Storyboard TCO Demo"
date: "2026-05-29"
lang: "en-US"
schema: "kgc-computing-flow/v1"

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

"renderer:palette":
  nodes:
    idea: "var(--kg-canvas-accent)"
    hypothesis: "#f59e0b"
    execution: "#22c55e"
    pivot: "#f97316"
    alert: "#ef4444"
  edges:
    critical: "#ef4444"
    neutral: "#9CA3AF"

socket_types:
  demand_driver_signal: {color: "#f59e0b", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [demand_driver_signal]}
  platform_cost_signal: {color: "#22c55e", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [platform_cost_signal]}
  token_risk_signal: {color: "#ef4444", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [token_risk_signal]}
  stack_tco_metric: {color: "#f97316", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [stack_tco_metric]}
  revenue_driver_signal: {color: "var(--kg-canvas-accent)", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [revenue_driver_signal]}
  revenue_metric_signal: {color: "#22c55e", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [revenue_metric_signal]}
  journey_driver_signal: {color: "var(--kg-canvas-accent)", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [journey_driver_signal]}
  prediction_engine_signal: {color: "#f59e0b", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [prediction_engine_signal]}
  yield_engine_signal: {color: "#22c55e", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [yield_engine_signal]}
  payment_engine_signal: {color: "var(--kg-canvas-accent)", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [payment_engine_signal]}
  liquidity_exchange_signal: {color: "#f97316", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [liquidity_exchange_signal]}
  infrastructure_engine_signal: {color: "#9CA3AF", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [infrastructure_engine_signal]}
  closed_loop_signal: {color: "#f97316", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [closed_loop_signal]}
  decision_driver_signal: {color: "#9CA3AF", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [decision_driver_signal]}
  rich_media_chart_html: {color: "var(--kg-canvas-accent)", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [rich_media_chart_html]}

workflow_sections:
  - id: wf_ingest_drivers
    title: "Ingest demand, platform, token, and revenue drivers"
    nodes: [workload_drivers, shared_platform_drivers, token_exposure_drivers, revenue_drivers]
  - id: wf_calculate_stack_costs
    title: "Calculate per-stack TCO from typed cost-driver ports"
    nodes: [fetch_agentverse_tco, elizaos_ai16z_tco, virtuals_game_tco]
  - id: wf_simulate_revenue_margin
    title: "Simulate revenue, cost, net margin, and break-even path"
    nodes: [revenue_calculator, tco_calculator]
  - id: wf_web3_closed_user_journey
    title: "Evaluate the Web3 economics closed user journey value loop"
    nodes: [web3_economics_drivers, prediction_engine, yield_engine, payment_engine, liquidity_exchange_engine, infrastructure_engine, closed_value_loop]
  - id: wf_render_decision
    title: "Render ranked decision drivers and chart payload"
    nodes: [decision_ranking, tco_chart_panel, value_loop_chart_panel]

flow_diagrams:
  key: flow_diagrams
  type: object
  value:
    tco_pipeline_flowchart:
      key: tco_pipeline_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          workload_drivers["Workload Drivers\n(MAU · agent requests)"]
          shared_platform_drivers["Platform Drivers\n(subscription · model fee · hosting)"]
          token_exposure_drivers["Token Exposure\n(onchain · gas · volatility)"]
          revenue_drivers["Revenue Drivers\n(conversion · price · GMV · take-rate)"]
          tco_calculators["Stack TCO Calculators\n(Fetch · elizaOS · Virtuals)"]
          revenue_calculator["Revenue Calculator\n(gross · net · per-request)"]
          tco_calculator["TCO Calculator\n(ranked decision drivers)"]
          web3_engines["Web3 Economics Engines\n(prediction · yield · payment · liquidity · infra)"]
          closed_value_loop["Closed Value Loop\n(health score · journey)"]
          decision_ranking["Decision Ranking\n(GO · CONDITIONAL GO · NO-GO)"]
          tco_chart_panel["TCO Chart Panel\n(RichMediaPanel)"]
          value_loop_chart_panel["Value Loop Panel\n(RichMediaPanel)"]
          tco_source_input["TCO Source Input\n(InputWidget)"]
          tco_compute["TCO Compute\n(inline DCF verdict)"]
          workload_drivers -->|"demand_driver_signal"| tco_calculators
          workload_drivers -->|"demand_driver_signal"| revenue_calculator
          shared_platform_drivers -->|"platform_cost_signal"| tco_calculators
          token_exposure_drivers -->|"token_risk_signal"| tco_calculators
          revenue_drivers -->|"revenue_driver_signal"| revenue_calculator
          revenue_calculator -->|"revenue_metric_signal"| tco_calculator
          tco_calculators -->|"stack_tco_metric"| tco_calculator
          tco_calculator -->|"decision_driver_signal"| decision_ranking
          tco_calculator -->|"rich_media_chart_html"| tco_chart_panel
          web3_engines -->|"closed_loop_signal"| closed_value_loop
          closed_value_loop -->|"rich_media_chart_html"| value_loop_chart_panel
          tco_source_input -->|"typed ports × 6"| tco_compute
          tco_compute -->|"outputSrcDoc"| tco_chart_panel
    tco_gitgraph:
      key: tco_gitgraph
      type: mermaid_gitgraph
      floatingPanelView: "gitGraph"
      floatingPanelOpen: true
      bottomPanelTab: "gitGraph"
      bottomPanelOpen: true
      value: |-
        gitGraph
          commit id: "tco_source_input" tag: "driver intake"
          branch demand_platform_token
          checkout demand_platform_token
          commit id: "workload_drivers"
          commit id: "shared_platform_drivers"
          commit id: "token_exposure_drivers"
          checkout main
          branch revenue_contract
          checkout revenue_contract
          commit id: "revenue_drivers"
          commit id: "revenue_calculator"
          checkout main
          branch stack_tco
          checkout stack_tco
          commit id: "fetch_agentverse_tco"
          commit id: "elizaos_ai16z_tco"
          commit id: "virtuals_game_tco"
          checkout main
          merge demand_platform_token id: "merge_drivers"
          merge revenue_contract id: "merge_revenue"
          merge stack_tco id: "merge_stacks"
          commit id: "tco_calculator" tag: "ranked decision" type: HIGHLIGHT
          branch web3_economics
          checkout web3_economics
          commit id: "prediction_engine"
          commit id: "yield_engine"
          commit id: "payment_engine"
          commit id: "liquidity_exchange_engine"
          commit id: "infrastructure_engine"
          commit id: "closed_value_loop"
          checkout main
          merge web3_economics id: "merge_web3"
          commit id: "decision_ranking" tag: "GO/NO-GO"
          branch rich_media_panels
          checkout rich_media_panels
          commit id: "tco_chart_panel"
          commit id: "value_loop_chart_panel"
          checkout main
          merge rich_media_panels id: "merge_panels"
    tco_architecture:
      key: tco_architecture
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
          group providers(cloud)[Default provider BytePlus plus Stripe]
          service canvas(internet)[Canvas UI airvio.co knowgrph] in cloudflare
          service mcp(server)[MCP Agent Worker] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service d1(database)[D1 Run Manifest and TCO cache] in cloudflare
          service r2(database)[R2 chart and media assets] in cloudflare
          service byteplus(server)[BytePlus agnes and seed] in providers
          service stripe(database)[Stripe usage billing] in providers
          canvas:R --> L:mcp
          mcp:R --> L:gateway
          gateway:R --> L:byteplus
          mcp:B --> T:d1
          mcp:B --> T:r2
          mcp:R --> L:stripe
    tco_event_model:
      key: tco_event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui DriverIntakeSubmitted
        tf 02 cmd RunStackTcoCalculation
        tf 03 evt StackCostsReady
        tf 04 cmd RunRevenueCalculation
        tf 05 evt RevenueMetricsReady
        tf 06 cmd RunTcoDecisionRanking
        tf 07 evt DecisionRankingReady
        tf 08 pcr Web3EconomicsAgent
        tf 09 cmd EvaluateClosedValueLoop
        tf 10 evt ClosedLoopHealthReady
        tf 11 cmd RenderDecisionCharts
        tf 12 evt ChartsRenderedToPanel
        tf 13 cmd PersistTcoRunToD1
        tf 14 evt TcoRunPersisted
        tf 15 ui ReplayTcoFromCache
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "tco_source_input"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "TCO Source Input"}
      position: {key: position, type: object, value: {"x":-360,"y":0}}
      handles: {key: handles, type: object, value: {"source":["monthly_active_users","monthly_agent_requests","paid_conversion_rate","agent_token_take_rate","model_provider_fee_usd","platform_subscription_usd"]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"previewField":"tco_scenario","previewMaxChars":80,"onEdit":{"trigger":"runDownstream","targets":["tco_compute"]},"actions":[{"id":"edit","label":"Edit","icon":"pencil","trigger":"openFieldEditor","targetField":"tco_scenario"},{"id":"run","label":"Run","icon":"play","trigger":"runDownstream","targets":["tco_compute"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"monthly_active_users":"demand_driver_signal","monthly_agent_requests":"demand_driver_signal","paid_conversion_rate":"revenue_driver_signal","agent_token_take_rate":"revenue_driver_signal","model_provider_fee_usd":"platform_cost_signal","platform_subscription_usd":"platform_cost_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "tcoSourceInput"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Runnable entry widget: TCO scenario inputs for demand, revenue, and cost driver ports."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "input"}
      monthly_active_users: {key: monthly_active_users, type: number, value: 5000}
      monthly_agent_requests: {key: monthly_agent_requests, type: number, value: 120000}
      paid_conversion_rate: {key: paid_conversion_rate, type: number, value: 0.08}
      agent_token_take_rate: {key: agent_token_take_rate, type: number, value: 0.05}
      model_provider_fee_usd: {key: model_provider_fee_usd, type: number, value: 0.003}
      platform_subscription_usd: {key: platform_subscription_usd, type: number, value: 25}
      tco_scenario: {key: tco_scenario, type: string, value: "Fetch Agentverse Premium baseline — 5k MAU, 120k agent calls/month"}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "tco_compute"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "TCO Summary Compute"}
      position: {key: position, type: object, value: {"x":-60,"y":0}}
      handles: {key: handles, type: object, value: {"target":["monthly_active_users","monthly_agent_requests","paid_conversion_rate","agent_token_take_rate","model_provider_fee_usd","platform_subscription_usd"],"source":["output","imageUrl","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["monthly_active_users","monthly_agent_requests","paid_conversion_rate","agent_token_take_rate","model_provider_fee_usd","platform_subscription_usd"],"outputs":["output","imageUrl","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"tco_compute.output","field":"output"}],"sideEffects":[{"field":"run_status","set":"done"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"output","previewMaxChars":120,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["output","imageUrl","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_active_users":"demand_driver_signal","monthly_agent_requests":"demand_driver_signal","paid_conversion_rate":"revenue_driver_signal","agent_token_take_rate":"revenue_driver_signal","model_provider_fee_usd":"platform_cost_signal","platform_subscription_usd":"platform_cost_signal"},"out":{"output":"rich_media_chart_html","imageUrl":"rich_media_chart_html","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "tcoCompute"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Inline compute: derives monthly revenue, TCO, net margin, and decision verdict from typed cost-driver ports without calling any LLM."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      run_status: {key: run_status, type: string, value: "idle"}
      output: {key: output, type: markdown, value: "TCO summary is ready to run."}
      imageUrl: {key: imageUrl, type: svg_data_uri, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      semanticKey: {key: semanticKey, type: string, value: "tco-demo:compute:tco-summary"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const rn = (k, d) => { const v = Number(inputs && inputs[k]); return Number.isFinite(v) ? v : d; }
            const mau = rn('monthly_active_users', 5000)
            const req = rn('monthly_agent_requests', 120000)
            const cvr = rn('paid_conversion_rate', 0.08)
            const tkr = rn('agent_token_take_rate', 0.05)
            const mf = rn('model_provider_fee_usd', 0.003)
            const sub = rn('platform_subscription_usd', 25)
            const monthlyRev = Math.round(mau * cvr * 12 * tkr * 100) / 100
            const tco = Math.round((req * mf + sub * 12) * 100) / 100
            const netMargin = Math.round((monthlyRev - tco) * 100) / 100
            const verdict = netMargin > 0 ? 'VIABLE' : netMargin > -tco * 0.2 ? 'MARGINAL' : 'UNVIABLE'
            const esc = v => String(v||'').replace(/[&<>"']/g, c => c==='&'?'&amp;':c==='<'?'&lt;':c==='>'?'&gt;':c==='"'?'&quot;':'&#39;')
            const output = [
              '## ' + verdict + ' — Token Economics TCO Summary',
              '',
              '- Monthly revenue (annualised): $' + monthlyRev.toLocaleString('en-US'),
              '- Annual TCO (model + platform): $' + tco.toLocaleString('en-US'),
              '- Net margin: $' + netMargin.toLocaleString('en-US'),
              '- MAU: ' + mau.toLocaleString('en-US'),
              '- Agent requests/month: ' + req.toLocaleString('en-US'),
              '- Model provider fee: $' + mf + '/call',
              '- Paid conversion rate: ' + (cvr * 100).toFixed(1) + '%',
            ].join('\n')
            const vc = netMargin > 0 ? '#22c55e' : netMargin > -tco * 0.2 ? '#f59e0b' : '#ef4444'
            const svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 200"><rect width="640" height="200" fill="#f8fafc"/><text x="320" y="56" font-family="system-ui" font-size="24" font-weight="700" fill="' + esc(vc) + '" text-anchor="middle">' + esc(verdict) + '</text><text x="320" y="94" font-family="system-ui" font-size="13" fill="#475569" text-anchor="middle">Revenue $' + esc(String(monthlyRev.toLocaleString('en-US'))) + ' | TCO $' + esc(String(tco.toLocaleString('en-US'))) + ' | Net $' + esc(String(netMargin.toLocaleString('en-US'))) + '</text><text x="320" y="128" font-family="system-ui" font-size="12" fill="#64748b" text-anchor="middle">' + esc(mau.toLocaleString('en-US')) + ' MAU · ' + esc(req.toLocaleString('en-US')) + ' req/month · $' + esc(String(mf)) + '/call</text></svg>'
            const imageUrl = 'data:image/svg+xml,' + encodeURIComponent(svg)
            const outputSrcDoc = '<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}.kpi div{background:#fff;border:1px solid #e2e8f0;border-radius:10px;padding:10px}.label{font-size:11px;color:#64748b;text-transform:uppercase}.value{font-size:15px;font-weight:700}</style></head><body><div class="kpi"><div><p class="label">Revenue</p><p class="value">$' + esc(String(monthlyRev.toLocaleString('en-US'))) + '</p></div><div><p class="label">TCO</p><p class="value">$' + esc(String(tco.toLocaleString('en-US'))) + '</p></div><div><p class="label">Net Margin</p><p class="value">$' + esc(String(netMargin.toLocaleString('en-US'))) + '</p></div></div><p style="font-size:12px;color:#64748b">' + esc(verdict) + ' — ' + esc(mau.toLocaleString('en-US')) + ' MAU · ' + esc(req.toLocaleString('en-US')) + ' req/month</p></body></html>'
            return { output, imageUrl, outputSrcDoc }
          }
    - id: {key: id, type: string, value: "agent_token_take_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Agent Token Take Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:agent_token_take_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "avg_tokens_per_request"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Avg Tokens Per Request"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:avg_tokens_per_request`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "avg_tool_calls_per_request"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Avg Tool Calls Per Request"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:avg_tool_calls_per_request`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "closed_loop_health_score"}
      type: {key: type, type: string, value: "metric"}
      label: {key: label, type: string, value: "Closed Loop Health Score"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "metric"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:metric:closed_loop_health_score`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "closed_value_loop_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Closed Value Loop Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:closed_value_loop_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18.94427190999916}
    - id: {key: id, type: string, value: "decision_ranking_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Decision Ranking Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:decision_ranking_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "elizaos_ai16z"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Elizaos Ai16z"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:elizaos_ai16z`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "exchange_conversion_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Exchange Conversion Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:exchange_conversion_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "fetch_agentverse"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Fetch Agentverse"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:fetch_agentverse`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "hosting_or_cloud_runtime_usd"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Hosting Or Cloud Runtime Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:hosting_or_cloud_runtime_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "infrastructure_engine_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Infrastructure Engine Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:infrastructure_engine_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "infrastructure_unit_cost_usd"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Infrastructure Unit Cost Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:infrastructure_unit_cost_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "infrastructure_uptime_slo"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Infrastructure Uptime Slo"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:infrastructure_uptime_slo`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "liquidity_exchange_engine_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Liquidity Exchange Engine Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:liquidity_exchange_engine_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "liquidity_spread_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Liquidity Spread Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:liquidity_spread_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "managed_hosting_required"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Managed Hosting Required"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:managed_hosting_required`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "marketplace_gmv_usd"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Marketplace Gmv Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:marketplace_gmv_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "model_provider_fee_usd"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Model Provider Fee Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:model_provider_fee_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "monthly_active_users"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Monthly Active Users"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:monthly_active_users`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "monthly_agent_requests"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Monthly Agent Requests"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:monthly_agent_requests`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "monthly_revenue_usd"}
      type: {key: type, type: string, value: "metric"}
      label: {key: label, type: string, value: "Monthly Revenue Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 6}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 6}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "metric"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:metric:monthly_revenue_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 36}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 19.79795897113271}
    - id: {key: id, type: string, value: "net_margin_usd"}
      type: {key: type, type: string, value: "metric"}
      label: {key: label, type: string, value: "Net Margin Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "metric"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:metric:net_margin_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "net_revenue_usd"}
      type: {key: type, type: string, value: "metric"}
      label: {key: label, type: string, value: "Net Revenue Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "metric"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:metric:net_revenue_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
    - id: {key: id, type: string, value: "onchain_gas_and_token_fees"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Onchain Gas And Token Fees"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:onchain_gas_and_token_fees`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "onchain_token_launch_required"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Onchain Token Launch Required"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:onchain_token_launch_required`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "paid_conversion_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Paid Conversion Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:paid_conversion_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "payment_engine_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Payment Engine Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:payment_engine_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "payment_fee_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Payment Fee Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:payment_fee_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "payment_success_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Payment Success Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:payment_success_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "platform_subscription_usd"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Platform Subscription Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:platform_subscription_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
    - id: {key: id, type: string, value: "platform_unit_call_cost_usd"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Platform Unit Call Cost Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:platform_unit_call_cost_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "prediction_accuracy_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Prediction Accuracy Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:prediction_accuracy_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "prediction_engine_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Prediction Engine Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 4}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:prediction_engine_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 28}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18}
    - id: {key: id, type: string, value: "retry_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Retry Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:retry_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "revenue_calculator_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Revenue Calculator Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:revenue_calculator_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "social_api_rpc_data_api_fees"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Social Api Rpc Data Api Fees"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:social_api_rpc_data_api_fees`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "subscription_price_usd"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Subscription Price Usd"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:subscription_price_usd`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "support_refund_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Support Refund Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:support_refund_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "tco_calculator_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Tco Calculator Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:tco_calculator_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "tco_chart_panel_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Tco Chart Panel Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:tco_chart_panel_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "tco_score"}
      type: {key: type, type: string, value: "outcome"}
      label: {key: label, type: string, value: "Tco Score"}
      "graph:degree": {key: "graph:degree", type: number, value: 6}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "outcome"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:outcome:tco_score`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 36}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 19.79795897113271}
    - id: {key: id, type: string, value: "token_setup_exposure"}
      type: {key: type, type: string, value: "cost"}
      label: {key: label, type: string, value: "Token Setup Exposure"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "cost"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:cost:token_setup_exposure`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "user_journey_value_loop"}
      type: {key: type, type: string, value: "outcome"}
      label: {key: label, type: string, value: "User Journey Value Loop"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "outcome"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:outcome:user_journey_value_loop`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "value_loop_chart_panel_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Value Loop Chart Panel Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:value_loop_chart_panel_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "virtuals_game"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Virtuals Game"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:virtuals_game`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "wallet_activation_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Wallet Activation Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:wallet_activation_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
    - id: {key: id, type: string, value: "yield_engine_semantic"}
      type: {key: type, type: string, value: "component"}
      label: {key: label, type: string, value: "Yield Engine Semantic"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "component"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:component:yield_engine_semantic`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
    - id: {key: id, type: string, value: "yield_share_rate"}
      type: {key: type, type: string, value: "lever"}
      label: {key: label, type: string, value: "Yield Share Rate"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "lever"}
      "kgc:semantic": {key: "kgc:semantic", type: boolean, value: true}
      "kgc:sigil": {key: "kgc:sigil", type: string, value: "`@node:lever:yield_share_rate`"}
      "kgc:source": {key: "kgc:source", type: string, value: "markdown-sigil"}
    - id: {key: id, type: string, value: "workload_drivers"}
      type: {key: type, type: string, value: "CostDriverWidget"}
      label: {key: label, type: string, value: "Workload Cost Drivers"}
      position: {key: position, type: object, value: {"x":80,"y":120}}
      handles: {key: handles, type: object, value: {"source":["monthly_agent_requests","avg_tool_calls_per_request","avg_tokens_per_request","retry_rate"]}}
      avg_tokens_per_request: {key: avg_tokens_per_request, type: string, value: "bring-your-own model meter"}
      avg_tool_calls_per_request: {key: avg_tool_calls_per_request, type: number, value: 1}
      driver_group: {key: driver_group, type: string, value: "demand"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"monthly_agent_requests":"demand_driver_signal","avg_tool_calls_per_request":"demand_driver_signal","avg_tokens_per_request":"demand_driver_signal","retry_rate":"demand_driver_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:workload_drivers"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 5}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      monthly_agent_requests: {key: monthly_agent_requests, type: number, value: 888}
      retry_rate: {key: retry_rate, type: string, value: "tracked as risk, not baked into quoted platform fee"}
      size: {key: size, type: object, value: {"width":320,"height":190}}
      tags: {key: tags, type: array, value: ["hypothesis"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#f59e0b"}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18.94427190999916}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "shared_platform_drivers"}
      type: {key: type, type: string, value: "CostDriverWidget"}
      label: {key: label, type: string, value: "Shared Platform Drivers"}
      position: {key: position, type: object, value: {"x":80,"y":390}}
      handles: {key: handles, type: object, value: {"source":["platform_subscription_usd","platform_unit_call_cost_usd","managed_hosting_required","hosting_or_cloud_runtime_usd","model_provider_fee_usd","social_api_rpc_data_api_fees","ops_hours"]}}
      driver_group: {key: driver_group, type: string, value: "platform"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"platform_subscription_usd":"platform_cost_signal","platform_unit_call_cost_usd":"platform_cost_signal","managed_hosting_required":"platform_cost_signal","hosting_or_cloud_runtime_usd":"platform_cost_signal","model_provider_fee_usd":"platform_cost_signal","social_api_rpc_data_api_fees":"platform_cost_signal","ops_hours":"platform_cost_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:shared_platform_drivers"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 8}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 8}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      hosting_or_cloud_runtime_usd: {key: hosting_or_cloud_runtime_usd, type: string, value: "BYO runtime, cloud credits, or managed cloud instance cost"}
      managed_hosting_required: {key: managed_hosting_required, type: string, value: "true for managed demo, false for self-host baseline"}
      model_provider_fee_usd: {key: model_provider_fee_usd, type: string, value: "explicit external meter"}
      ops_hours: {key: ops_hours, type: string, value: "excluded from cash floor, scored separately"}
      platform_subscription_usd: {key: platform_subscription_usd, type: string, value: "0-25+ depending on stack and quota"}
      platform_unit_call_cost_usd: {key: platform_unit_call_cost_usd, type: string, value: "0.003 when using Virtuals GAME paid tier"}
      size: {key: size, type: object, value: {"width":320,"height":240}}
      social_api_rpc_data_api_fees: {key: social_api_rpc_data_api_fees, type: string, value: "external API meter"}
      tags: {key: tags, type: array, value: ["execution"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#22c55e"}
      "visual:importance": {key: "visual:importance", type: number, value: 44}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 21.31370849898476}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "token_exposure_drivers"}
      type: {key: type, type: string, value: "CostDriverWidget"}
      label: {key: label, type: string, value: "Token Exposure Drivers"}
      position: {key: position, type: object, value: {"x":80,"y":700}}
      handles: {key: handles, type: object, value: {"source":["onchain_token_launch_required","token_setup_exposure","onchain_gas_and_token_fees","token_price_volatility"]}}
      driver_group: {key: driver_group, type: string, value: "web3"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"onchain_token_launch_required":"token_risk_signal","token_setup_exposure":"token_risk_signal","onchain_gas_and_token_fees":"token_risk_signal","token_price_volatility":"token_risk_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:token_exposure_drivers"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 6}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 6}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      onchain_gas_and_token_fees: {key: onchain_gas_and_token_fees, type: string, value: "chain and wallet dependent"}
      onchain_token_launch_required: {key: onchain_token_launch_required, type: string, value: "only when tokenized agent launch is required"}
      size: {key: size, type: object, value: {"width":320,"height":210}}
      tags: {key: tags, type: array, value: ["alert"]}
      token_price_volatility: {key: token_price_volatility, type: string, value: "risk driver, kept token-denominated"}
      token_setup_exposure: {key: token_setup_exposure, type: string, value: "kept token-denominated"}
      "visual:fill": {key: "visual:fill", type: string, value: "#ef4444"}
      "visual:importance": {key: "visual:importance", type: number, value: 36}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 19.79795897113271}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
    - id: {key: id, type: string, value: "revenue_drivers"}
      type: {key: type, type: string, value: "RevenueDriverWidget"}
      label: {key: label, type: string, value: "Revenue Drivers"}
      position: {key: position, type: object, value: {"x":80,"y":990}}
      handles: {key: handles, type: object, value: {"source":["monthly_active_users","paid_conversion_rate","subscription_price_usd","marketplace_gmv_usd","agent_token_take_rate","support_refund_rate"]}}
      agent_token_take_rate: {key: agent_token_take_rate, type: number, value: 5}
      driver_group: {key: driver_group, type: string, value: "revenue"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"monthly_active_users":"revenue_driver_signal","paid_conversion_rate":"revenue_driver_signal","subscription_price_usd":"revenue_driver_signal","marketplace_gmv_usd":"revenue_driver_signal","agent_token_take_rate":"revenue_driver_signal","support_refund_rate":"revenue_driver_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:revenue_drivers"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 8}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 8}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      marketplace_gmv_usd: {key: marketplace_gmv_usd, type: number, value: 10000}
      monthly_active_users: {key: monthly_active_users, type: number, value: 25}
      paid_conversion_rate: {key: paid_conversion_rate, type: number, value: 3000}
      size: {key: size, type: object, value: {"width":320,"height":250}}
      subscription_price_usd: {key: subscription_price_usd, type: number, value: 19}
      support_refund_rate: {key: support_refund_rate, type: number, value: 0.12}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 44}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 21.31370849898476}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
    - id: {key: id, type: string, value: "web3_economics_drivers"}
      type: {key: type, type: string, value: "Web3EconomicsDriverWidget"}
      label: {key: label, type: string, value: "Web3 Economics Drivers"}
      position: {key: position, type: object, value: {"x":80,"y":1300}}
      handles: {key: handles, type: object, value: {"source":["prediction_accuracy_rate","wallet_activation_rate","yield_share_rate","payment_success_rate","payment_fee_rate","liquidity_spread_rate","exchange_conversion_rate","infrastructure_uptime_slo","infrastructure_unit_cost_usd"]}}
      driver_group: {key: driver_group, type: string, value: "web3_economics"}
      exchange_conversion_rate: {key: exchange_conversion_rate, type: number, value: 0.74}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"prediction_accuracy_rate":"journey_driver_signal","wallet_activation_rate":"journey_driver_signal","yield_share_rate":"journey_driver_signal","payment_success_rate":"journey_driver_signal","payment_fee_rate":"journey_driver_signal","liquidity_spread_rate":"journey_driver_signal","exchange_conversion_rate":"journey_driver_signal","infrastructure_uptime_slo":"journey_driver_signal","infrastructure_unit_cost_usd":"journey_driver_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:web3_economics_drivers"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 9}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 9}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      infrastructure_unit_cost_usd: {key: infrastructure_unit_cost_usd, type: number, value: 0.0004}
      infrastructure_uptime_slo: {key: infrastructure_uptime_slo, type: number, value: 0.995}
      liquidity_spread_rate: {key: liquidity_spread_rate, type: number, value: 0.008}
      payment_fee_rate: {key: payment_fee_rate, type: number, value: 0.012}
      payment_success_rate: {key: payment_success_rate, type: number, value: 0.97}
      prediction_accuracy_rate: {key: prediction_accuracy_rate, type: number, value: 0.68}
      size: {key: size, type: object, value: {"width":340,"height":280}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 48}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 22}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      wallet_activation_rate: {key: wallet_activation_rate, type: number, value: 0.42}
      yield_share_rate: {key: yield_share_rate, type: number, value: 0.18}
    - id: {key: id, type: string, value: "fetch_agentverse_tco"}
      type: {key: type, type: string, value: "TcoStackWidget"}
      label: {key: label, type: string, value: "Fetch.ai / Agentverse TCO"}
      position: {key: position, type: object, value: {"x":520,"y":110}}
      handles: {key: handles, type: object, value: {"target":["monthly_agent_requests","platform_subscription_usd","managed_hosting_required","model_provider_fee_usd","onchain_gas_and_token_fees"],"source":["fetch_monthly_tco_usd","fetch_quota_risk","fetch_tco_score"]}}
      fetch_monthly_tco_note: {key: fetch_monthly_tco_note, type: string, value: "0-25 platform floor before model/API/FET costs"}
      fetch_monthly_tco_usd: {key: fetch_monthly_tco_usd, type: number, value: 25}
      fetch_quota_risk: {key: fetch_quota_risk, type: string, value: "processed messages, compute seconds, storage"}
      fetch_tco_score: {key: fetch_tco_score, type: string, value: "best predictable managed starter TCO"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_agent_requests":"demand_driver_signal","platform_subscription_usd":"platform_cost_signal","managed_hosting_required":"platform_cost_signal","model_provider_fee_usd":"platform_cost_signal","onchain_gas_and_token_fees":"token_risk_signal"},"out":{"fetch_monthly_tco_usd":"stack_tco_metric","fetch_quota_risk":"token_risk_signal","fetch_tco_score":"stack_tco_metric"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:fetch_agentverse_tco"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      platform_subscription_usd: {key: platform_subscription_usd, type: string, value: "0 on Basic if quotas fit; 25 on Premium"}
      size: {key: size, type: object, value: {"width":360,"height":240}}
      stack: {key: stack, type: string, value: "Fetch.ai / Agentverse"}
      tags: {key: tags, type: array, value: ["execution"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#22c55e"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const req = n(inputs.monthly_agent_requests);
            const sub = req <= 10000 ? 0 : 25;
            const total = sub + n(inputs.model_provider_fee_usd) + n(inputs.onchain_gas_and_token_fees);
            return {
              fetch_monthly_tco_usd: Math.round(total * 100) / 100,
              fetch_quota_risk: req <= 10000 ? 'Basic quota fit at current request load' : 'Premium quota needed at current request load',
              fetch_tco_score: total <= 25 ? 'predictable low managed cash floor' : 'managed cost rises with external meters'
            };
          }
    - id: {key: id, type: string, value: "elizaos_ai16z_tco"}
      type: {key: type, type: string, value: "TcoStackWidget"}
      label: {key: label, type: string, value: "elizaOS / AI16Z TCO"}
      position: {key: position, type: object, value: {"x":520,"y":420}}
      handles: {key: handles, type: object, value: {"target":["monthly_agent_requests","hosting_or_cloud_runtime_usd","model_provider_fee_usd","social_api_rpc_data_api_fees","ops_hours"],"source":["eliza_monthly_tco_usd","eliza_ops_risk","eliza_tco_score"]}}
      eliza_monthly_tco_note: {key: eliza_monthly_tco_note, type: string, value: "0 public framework fee plus infra/model/ops"}
      eliza_monthly_tco_usd: {key: eliza_monthly_tco_usd, type: number, value: 0}
      eliza_ops_risk: {key: eliza_ops_risk, type: string, value: "highest operator-owned surface"}
      eliza_tco_score: {key: eliza_tco_score, type: string, value: "best FOSS/control baseline"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_agent_requests":"demand_driver_signal","hosting_or_cloud_runtime_usd":"platform_cost_signal","model_provider_fee_usd":"platform_cost_signal","social_api_rpc_data_api_fees":"platform_cost_signal","ops_hours":"platform_cost_signal"},"out":{"eliza_monthly_tco_usd":"stack_tco_metric","eliza_ops_risk":"platform_cost_signal","eliza_tco_score":"stack_tco_metric"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:elizaos_ai16z_tco"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      hosting_or_cloud_runtime_usd: {key: hosting_or_cloud_runtime_usd, type: string, value: "BYO when self-hosted; cloud credits when managed"}
      size: {key: size, type: object, value: {"width":360,"height":250}}
      stack: {key: stack, type: string, value: "elizaOS / AI16Z"}
      tags: {key: tags, type: array, value: ["hypothesis"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#f59e0b"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const total = n(inputs.hosting_or_cloud_runtime_usd) + n(inputs.model_provider_fee_usd) + n(inputs.social_api_rpc_data_api_fees);
            const ops = n(inputs.ops_hours);
            return {
              eliza_monthly_tco_usd: Math.round(total * 100) / 100,
              eliza_ops_risk: ops > 0 ? 'operator hours dominate the real TCO' : 'ops hours tracked outside cash floor',
              eliza_tco_score: total === 0 ? 'lowest cash floor with owner-operated runtime' : 'infra and provider meters drive cash cost'
            };
          }
    - id: {key: id, type: string, value: "virtuals_game_tco"}
      type: {key: type, type: string, value: "TcoStackWidget"}
      label: {key: label, type: string, value: "Virtuals / GAME TCO"}
      position: {key: position, type: object, value: {"x":520,"y":740}}
      handles: {key: handles, type: object, value: {"target":["monthly_agent_requests","platform_unit_call_cost_usd","onchain_token_launch_required","token_setup_exposure","onchain_gas_and_token_fees","token_price_volatility"],"source":["virtuals_monthly_tco_usd","virtuals_token_risk","virtuals_tco_score"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_agent_requests":"demand_driver_signal","platform_unit_call_cost_usd":"platform_cost_signal","onchain_token_launch_required":"token_risk_signal","token_setup_exposure":"token_risk_signal","onchain_gas_and_token_fees":"token_risk_signal","token_price_volatility":"token_risk_signal"},"out":{"virtuals_monthly_tco_usd":"stack_tco_metric","virtuals_token_risk":"token_risk_signal","virtuals_tco_score":"stack_tco_metric"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:virtuals_game_tco"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 8}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 6}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      platform_unit_call_cost_usd: {key: platform_unit_call_cost_usd, type: number, value: 0.003}
      size: {key: size, type: object, value: {"width":360,"height":260}}
      stack: {key: stack, type: string, value: "Virtuals Protocol / GAME"}
      tags: {key: tags, type: array, value: ["alert"]}
      virtuals_monthly_tco_note: {key: virtuals_monthly_tco_note, type: string, value: "30 platform call floor at 10k paid GAME calls"}
      virtuals_monthly_tco_usd: {key: virtuals_monthly_tco_usd, type: number, value: 30}
      virtuals_tco_score: {key: virtuals_tco_score, type: string, value: "best tokenized-agent economy fit"}
      virtuals_token_risk: {key: virtuals_token_risk, type: string, value: "launch fee, graduation threshold, gas, VIRTUAL price"}
      "visual:fill": {key: "visual:fill", type: string, value: "#ef4444"}
      "visual:importance": {key: "visual:importance", type: number, value: 44}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 21.31370849898476}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const req = n(inputs.monthly_agent_requests);
            const unit = n(inputs.platform_unit_call_cost_usd) || 0.003;
            const total = req * unit + n(inputs.onchain_gas_and_token_fees);
            return {
              virtuals_monthly_tco_usd: Math.round(total * 100) / 100,
              virtuals_token_risk: 'launch fee, graduation threshold, gas, and VIRTUAL price stay separate',
              virtuals_tco_score: total <= 30 ? 'tokenized distribution fit with per-call floor' : 'runtime cost scales with paid calls'
            };
          }
    - id: {key: id, type: string, value: "revenue_calculator"}
      type: {key: type, type: string, value: "RevenueCalculatorWidget"}
      label: {key: label, type: string, value: "Revenue Calculator"}
      position: {key: position, type: object, value: {"x":520,"y":1060}}
      handles: {key: handles, type: object, value: {"target":["monthly_agent_requests","monthly_active_users","paid_conversion_rate","subscription_price_usd","marketplace_gmv_usd","agent_token_take_rate","support_refund_rate"],"source":["monthly_revenue_usd","net_revenue_usd","revenue_per_request_usd","revenue_model_confidence"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_agent_requests":"demand_driver_signal","monthly_active_users":"revenue_driver_signal","paid_conversion_rate":"revenue_driver_signal","subscription_price_usd":"revenue_driver_signal","marketplace_gmv_usd":"revenue_driver_signal","agent_token_take_rate":"revenue_driver_signal","support_refund_rate":"revenue_driver_signal"},"out":{"monthly_revenue_usd":"revenue_metric_signal","net_revenue_usd":"revenue_metric_signal","revenue_per_request_usd":"revenue_metric_signal","revenue_model_confidence":"decision_driver_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:revenue_calculator"}
      formula: {key: formula, type: string, value: "net_revenue = (monthly_active_users * paid_conversion_rate * subscription_price_usd + marketplace_gmv_usd * agent_token_take_rate) * (1 - support_refund_rate)"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 13}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 7}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 6}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":360,"height":250}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 64}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 24.42220510185596}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const req = Math.max(1, n(inputs.monthly_agent_requests) || 10000);
            const users = n(inputs.monthly_active_users);
            const conversion = n(inputs.paid_conversion_rate);
            const price = n(inputs.subscription_price_usd);
            const marketplace = n(inputs.marketplace_gmv_usd);
            const take = n(inputs.agent_token_take_rate);
            const refund = Math.max(0, Math.min(0.95, n(inputs.support_refund_rate)));
            const gross = users * conversion * price + marketplace * take;
            const net = gross * (1 - refund);
            return {
              monthly_revenue_usd: Math.round(gross * 100) / 100,
              net_revenue_usd: Math.round(net * 100) / 100,
              revenue_per_request_usd: Math.round((net / req) * 10000) / 10000,
              revenue_model_confidence: net > 0 ? 'revenue-positive baseline, validate conversion and refunds' : 'no revenue yet, treat costs as burn'
            };
          }
    - id: {key: id, type: string, value: "tco_calculator"}
      type: {key: type, type: string, value: "TcoCalculatorWidget"}
      label: {key: label, type: string, value: "TCO Calculator"}
      position: {key: position, type: object, value: {"x":1040,"y":280}}
      handles: {key: handles, type: object, value: {"target":["monthly_revenue_usd","net_revenue_usd","fetch_monthly_tco_usd","eliza_monthly_tco_usd","virtuals_monthly_tco_usd","fetch_quota_risk","eliza_ops_risk","virtuals_token_risk"],"source":["lowest_cash_tco_driver","highest_margin_driver","breakeven_path_driver","lowest_lockin_driver","tokenized_distribution_driver","outputSrcDoc"]}}
      breakeven_path_driver: {key: breakeven_path_driver, type: string, value: "waits for net revenue and computed stack costs"}
      calculation_policy: {key: calculation_policy, type: string, value: "cash floors, net revenue, ops, and token-volatility risk stay separate until the calculator joins them"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_revenue_usd":"revenue_metric_signal","net_revenue_usd":"revenue_metric_signal","fetch_monthly_tco_usd":"stack_tco_metric","eliza_monthly_tco_usd":"stack_tco_metric","virtuals_monthly_tco_usd":"stack_tco_metric","fetch_quota_risk":"token_risk_signal","eliza_ops_risk":"platform_cost_signal","virtuals_token_risk":"token_risk_signal"},"out":{"lowest_cash_tco_driver":"decision_driver_signal","highest_margin_driver":"decision_driver_signal","breakeven_path_driver":"decision_driver_signal","lowest_lockin_driver":"decision_driver_signal","tokenized_distribution_driver":"decision_driver_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:tco_calculator"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 15}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 8}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 7}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      highest_margin_driver: {key: highest_margin_driver, type: string, value: "waits for net revenue and computed stack costs"}
      lowest_cash_tco_driver: {key: lowest_cash_tco_driver, type: string, value: "elizaOS self-host cash floor, if ops are available"}
      lowest_lockin_driver: {key: lowest_lockin_driver, type: string, value: "elizaOS local/self-host"}
      outputSrcDoc: {key: outputSrcDoc, type: string, value: "<!doctype html><html><body><p>TCO chart waits for calculator inputs.</p></body></html>"}
      size: {key: size, type: object, value: {"width":360,"height":260}}
      tags: {key: tags, type: array, value: ["pivot"]}
      tokenized_distribution_driver: {key: tokenized_distribution_driver, type: string, value: "Virtuals when agent token launch matters"}
      "visual:fill": {key: "visual:fill", type: string, value: "#f97316"}
      "visual:importance": {key: "visual:importance", type: number, value: 72}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 25.491933384829668}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const gross = n(inputs.monthly_revenue_usd);
            const net = n(inputs.net_revenue_usd);
            const rows = [
              ['elizaOS / AI16Z', n(inputs.eliza_monthly_tco_usd), '#f59e0b'],
              ['Fetch.ai / Agentverse', n(inputs.fetch_monthly_tco_usd), '#22c55e'],
              ['Virtuals / GAME', n(inputs.virtuals_monthly_tco_usd), '#ef4444'],
            ];
            const scored = rows.map(row => [row[0], row[1], Math.round((net - row[1]) * 100) / 100, row[2]]);
            const maxCost = rows.reduce((acc, row) => row[1] > acc ? row[1] : acc, 1);
            const best = scored.reduce((acc, row) => row[2] > acc[2] ? row : acc, scored[0]);
            const costBars = rows.map(row => `<section class="bar-row"><strong>${row[0]}</strong><span class="bar"><i style="width:${Math.max(4, Math.round((row[1] / maxCost) * 100))}%;background:${row[2]}"></i></span><b>$${row[1]}/mo</b></section>`).join('');
            const marginBars = scored.map(row => `<section class="bar-row"><strong>${row[0]}</strong><span class="bar"><i style="width:${Math.max(4, Math.min(100, Math.round(((row[2] + maxCost) / Math.max(1, net + maxCost)) * 100)))}%;background:${row[3]}"></i></span><b>$${row[2]}/mo</b></section>`).join('');
            const html = `<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;font:14px system-ui,Arial,sans-serif;background:#f8fafc;color:#111827}.wrap{padding:18px}h1{font-size:18px;margin:0 0 12px}h2{font-size:13px;margin:14px 0 8px;color:#374151}.bar-row{display:grid;grid-template-columns:150px 1fr 82px;gap:10px;align-items:center;margin:8px 0}.bar{height:16px;border-radius:5px;background:#e5e7eb;overflow:hidden}.bar i{display:block;height:100%}.kpi{display:flex;gap:10px;flex-wrap:wrap}.kpi b{background:white;border:1px solid #e5e7eb;border-radius:6px;padding:6px 8px}p{margin:10px 0 0;color:#4b5563}</style></head><body><main class="wrap"><h1>Revenue and TCO simulation</h1><section class="kpi"><b>Gross $${gross}/mo</b><b>Net $${net}/mo</b><b>Best margin ${best[0]}</b></section><h2>Monthly cost</h2>${costBars}<h2>Net margin after cost</h2>${marginBars}<p>Every bar is fed by a typed Storyboard Widget port; token, gas, ops, and quota risk remain separate driver handles.</p></main></body></html>`;
            return {
              lowest_cash_tco_driver: 'elizaOS self-host cash floor when operator time is available',
              highest_margin_driver: `${best[0]} net margin $${best[2]}/mo`,
              breakeven_path_driver: best[2] >= 0 ? 'current revenue clears selected cost floor' : 'revenue must rise or cost floor must fall',
              lowest_lockin_driver: 'elizaOS local/self-host',
              tokenized_distribution_driver: 'Virtuals when agent-token distribution matters',
              outputSrcDoc: html
            };
          }
    - id: {key: id, type: string, value: "prediction_engine"}
      type: {key: type, type: string, value: "PredictionEngineWidget"}
      label: {key: label, type: string, value: "Prediction Engine"}
      position: {key: position, type: object, value: {"x":960,"y":980}}
      handles: {key: handles, type: object, value: {"target":["monthly_active_users","paid_conversion_rate","prediction_accuracy_rate","wallet_activation_rate"],"source":["predicted_intent_quality_score","conversion_uplift_rate","demand_forecast_index"]}}
      engine_role: {key: engine_role, type: string, value: "turns observed user intent into a demand and conversion signal"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_active_users":"revenue_driver_signal","paid_conversion_rate":"revenue_driver_signal","prediction_accuracy_rate":"journey_driver_signal","wallet_activation_rate":"journey_driver_signal"},"out":{"predicted_intent_quality_score":"prediction_engine_signal","conversion_uplift_rate":"prediction_engine_signal","demand_forecast_index":"prediction_engine_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:prediction_engine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":340,"height":230}}
      tags: {key: tags, type: array, value: ["hypothesis"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#f59e0b"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const users = n(inputs.monthly_active_users);
            const conversion = n(inputs.paid_conversion_rate);
            const accuracy = Math.max(0, Math.min(1, n(inputs.prediction_accuracy_rate)));
            const activation = Math.max(0, Math.min(1, n(inputs.wallet_activation_rate)));
            const quality = Math.max(0, Math.min(1, accuracy * 0.7 + activation * 0.3));
            const uplift = conversion * quality;
            return {
              predicted_intent_quality_score: Math.round(quality * 1000) / 1000,
              conversion_uplift_rate: Math.round(uplift * 10000) / 10000,
              demand_forecast_index: Math.round(users * (1 + uplift) * 100) / 100
            };
          }
    - id: {key: id, type: string, value: "yield_engine"}
      type: {key: type, type: string, value: "YieldEngineWidget"}
      label: {key: label, type: string, value: "Yield Engine"}
      position: {key: position, type: object, value: {"x":1320,"y":980}}
      handles: {key: handles, type: object, value: {"target":["net_revenue_usd","revenue_per_request_usd","yield_share_rate","predicted_intent_quality_score","demand_forecast_index"],"source":["user_value_yield_usd","protocol_yield_score","retention_value_index"]}}
      engine_role: {key: engine_role, type: string, value: "converts revenue into user-retained value and protocol yield"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"net_revenue_usd":"revenue_metric_signal","revenue_per_request_usd":"revenue_metric_signal","yield_share_rate":"journey_driver_signal","predicted_intent_quality_score":"prediction_engine_signal","demand_forecast_index":"prediction_engine_signal"},"out":{"user_value_yield_usd":"yield_engine_signal","protocol_yield_score":"yield_engine_signal","retention_value_index":"yield_engine_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:yield_engine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":340,"height":230}}
      tags: {key: tags, type: array, value: ["execution"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#22c55e"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const net = n(inputs.net_revenue_usd);
            const perRequest = n(inputs.revenue_per_request_usd);
            const share = Math.max(0, Math.min(1, n(inputs.yield_share_rate)));
            const quality = Math.max(0, Math.min(1, n(inputs.predicted_intent_quality_score)));
            const yieldValue = net * share * Math.max(0.1, quality);
            const score = Math.min(100, (yieldValue / Math.max(1, net)) * 100);
            return {
              user_value_yield_usd: Math.round(yieldValue * 100) / 100,
              protocol_yield_score: Math.round(score * 100) / 100,
              retention_value_index: Math.round(Math.min(1, quality + perRequest) * 1000) / 1000
            };
          }
    - id: {key: id, type: string, value: "payment_engine"}
      type: {key: type, type: string, value: "PaymentEngineWidget"}
      label: {key: label, type: string, value: "Payment Engine"}
      position: {key: position, type: object, value: {"x":1680,"y":980}}
      handles: {key: handles, type: object, value: {"target":["net_revenue_usd","user_value_yield_usd","payment_success_rate","payment_fee_rate"],"source":["settled_payment_volume_usd","payment_fee_cost_usd","payment_value_capture_usd"]}}
      engine_role: {key: engine_role, type: string, value: "settles value capture through wallet/payment rails"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"net_revenue_usd":"revenue_metric_signal","user_value_yield_usd":"yield_engine_signal","payment_success_rate":"journey_driver_signal","payment_fee_rate":"journey_driver_signal"},"out":{"settled_payment_volume_usd":"payment_engine_signal","payment_fee_cost_usd":"payment_engine_signal","payment_value_capture_usd":"payment_engine_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:payment_engine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":340,"height":230}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const success = Math.max(0, Math.min(1, n(inputs.payment_success_rate)));
            const feeRate = Math.max(0, Math.min(1, n(inputs.payment_fee_rate)));
            const settled = (n(inputs.net_revenue_usd) + n(inputs.user_value_yield_usd)) * success;
            const fee = settled * feeRate;
            return {
              settled_payment_volume_usd: Math.round(settled * 100) / 100,
              payment_fee_cost_usd: Math.round(fee * 100) / 100,
              payment_value_capture_usd: Math.round((settled - fee) * 100) / 100
            };
          }
    - id: {key: id, type: string, value: "liquidity_exchange_engine"}
      type: {key: type, type: string, value: "LiquidityExchangeEngineWidget"}
      label: {key: label, type: string, value: "Liquidity & Exchange Engine"}
      position: {key: position, type: object, value: {"x":1320,"y":1260}}
      handles: {key: handles, type: object, value: {"target":["settled_payment_volume_usd","liquidity_spread_rate","exchange_conversion_rate","token_price_volatility"],"source":["exchange_liquidity_depth_usd","liquidity_slippage_cost_usd","token_exchange_efficiency_score"]}}
      engine_role: {key: engine_role, type: string, value: "turns settled payments into exchangeable liquidity"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"settled_payment_volume_usd":"payment_engine_signal","liquidity_spread_rate":"journey_driver_signal","exchange_conversion_rate":"journey_driver_signal","token_price_volatility":"token_risk_signal"},"out":{"exchange_liquidity_depth_usd":"liquidity_exchange_signal","liquidity_slippage_cost_usd":"liquidity_exchange_signal","token_exchange_efficiency_score":"liquidity_exchange_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:liquidity_exchange_engine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 6}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":360,"height":240}}
      tags: {key: tags, type: array, value: ["pivot"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#f97316"}
      "visual:importance": {key: "visual:importance", type: number, value: 36}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 19.79795897113271}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const settled = n(inputs.settled_payment_volume_usd);
            const spread = Math.max(0, Math.min(1, n(inputs.liquidity_spread_rate)));
            const conversion = Math.max(0, Math.min(1, n(inputs.exchange_conversion_rate)));
            const volatility = Math.max(0, n(inputs.token_price_volatility));
            const depth = settled * conversion;
            const slippage = settled * spread * (1 + volatility);
            const efficiency = Math.max(0, Math.min(100, conversion * 100 - spread * 100 - volatility * 10));
            return {
              exchange_liquidity_depth_usd: Math.round(depth * 100) / 100,
              liquidity_slippage_cost_usd: Math.round(slippage * 100) / 100,
              token_exchange_efficiency_score: Math.round(efficiency * 100) / 100
            };
          }
    - id: {key: id, type: string, value: "infrastructure_engine"}
      type: {key: type, type: string, value: "InfrastructureEngineWidget"}
      label: {key: label, type: string, value: "Infrastructure Engine"}
      position: {key: position, type: object, value: {"x":960,"y":1260}}
      handles: {key: handles, type: object, value: {"target":["monthly_agent_requests","infrastructure_unit_cost_usd","infrastructure_uptime_slo","exchange_liquidity_depth_usd","payment_fee_cost_usd"],"source":["infrastructure_cost_usd","uptime_value_score","infra_adjusted_value_usd"]}}
      engine_role: {key: engine_role, type: string, value: "prices the reliability layer that keeps the loop available"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"monthly_agent_requests":"demand_driver_signal","infrastructure_unit_cost_usd":"journey_driver_signal","infrastructure_uptime_slo":"journey_driver_signal","exchange_liquidity_depth_usd":"liquidity_exchange_signal","payment_fee_cost_usd":"payment_engine_signal"},"out":{"infrastructure_cost_usd":"infrastructure_engine_signal","uptime_value_score":"infrastructure_engine_signal","infra_adjusted_value_usd":"infrastructure_engine_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:infrastructure_engine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":350,"height":240}}
      tags: {key: tags, type: array, value: ["execution"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#22c55e"}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const cost = n(inputs.monthly_agent_requests) * n(inputs.infrastructure_unit_cost_usd);
            const uptime = Math.max(0, Math.min(1, n(inputs.infrastructure_uptime_slo)));
            const adjusted = n(inputs.exchange_liquidity_depth_usd) - cost - n(inputs.payment_fee_cost_usd);
            return {
              infrastructure_cost_usd: Math.round(cost * 100) / 100,
              uptime_value_score: Math.round(uptime * 10000) / 100,
              infra_adjusted_value_usd: Math.round(adjusted * 100) / 100
            };
          }
    - id: {key: id, type: string, value: "closed_value_loop"}
      type: {key: type, type: string, value: "ClosedValueLoopWidget"}
      label: {key: label, type: string, value: "Closed User Journey Value Loop"}
      position: {key: position, type: object, value: {"x":1680,"y":1260}}
      handles: {key: handles, type: object, value: {"target":["predicted_intent_quality_score","protocol_yield_score","payment_value_capture_usd","token_exchange_efficiency_score","uptime_value_score","infra_adjusted_value_usd","net_revenue_usd","highest_margin_driver"],"source":["closed_loop_health_score","user_journey_value_loop","web3_economics_decision_driver","outputSrcDoc"]}}
      engine_role: {key: engine_role, type: string, value: "scores the closed journey loop across all five Web3 economics engines"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"predicted_intent_quality_score":"prediction_engine_signal","protocol_yield_score":"yield_engine_signal","payment_value_capture_usd":"payment_engine_signal","token_exchange_efficiency_score":"liquidity_exchange_signal","uptime_value_score":"infrastructure_engine_signal","infra_adjusted_value_usd":"infrastructure_engine_signal","net_revenue_usd":"revenue_metric_signal","highest_margin_driver":"decision_driver_signal"},"out":{"closed_loop_health_score":"closed_loop_signal","user_journey_value_loop":"closed_loop_signal","web3_economics_decision_driver":"decision_driver_signal","outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:closed_value_loop"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 9}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 8}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      size: {key: size, type: object, value: {"width":380,"height":270}}
      tags: {key: tags, type: array, value: ["pivot"]}
      "visual:fill": {key: "visual:fill", type: string, value: "#f97316"}
      "visual:importance": {key: "visual:importance", type: number, value: 48}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 22}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const n = v => {
              const m = String(v ?? '').match(/-?[0-9]+(?:\.[0-9]+)?/);
              const x = m ? Number(m[0]) : Number(v);
              return Number.isFinite(x) ? x : 0;
            };
            const net = Math.max(1, n(inputs.net_revenue_usd));
            const predictionScore = Math.max(0, Math.min(100, n(inputs.predicted_intent_quality_score) * 100));
            const yieldScore = Math.max(0, Math.min(100, n(inputs.protocol_yield_score)));
            const captureScore = Math.max(0, Math.min(100, (n(inputs.payment_value_capture_usd) / net) * 100));
            const exchangeScore = Math.max(0, Math.min(100, n(inputs.token_exchange_efficiency_score)));
            const uptimeScore = Math.max(0, Math.min(100, n(inputs.uptime_value_score)));
            const infraValueScore = Math.max(0, Math.min(100, (n(inputs.infra_adjusted_value_usd) / net) * 100));
            const infraScore = Math.round(((uptimeScore + infraValueScore) / 2) * 100) / 100;
            const health = Math.round(((predictionScore + yieldScore + captureScore + exchangeScore + infraScore) / 5) * 100) / 100;
            const margin = String(inputs.highest_margin_driver || 'margin waits for TCO inputs');
            const html = `<!doctype html><html><head><meta charset="utf-8"><style>body{margin:0;font:14px system-ui,Arial,sans-serif;background:#f8fafc;color:#111827}.wrap{padding:18px}h1{font-size:18px;margin:0 0 10px}.grid{display:grid;grid-template-columns:1fr 72px;gap:8px;align-items:center}.bar{height:15px;border-radius:5px;background:#e5e7eb;overflow:hidden}.bar i{display:block;height:100%;background:#f97316}.kpi{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:10px}.kpi b{background:white;border:1px solid #e5e7eb;border-radius:6px;padding:6px 8px}p{color:#4b5563;margin:10px 0 0}</style></head><body><main class="wrap"><h1>Closed user journey value loop</h1><section class="kpi"><b>Health ${health}/100</b><b>${margin}</b></section><section class="grid"><span>Prediction Engine</span><b>${predictionScore}</b><span class="bar"><i style="width:${predictionScore}%"></i></span><span></span><span>Yield Engine</span><b>${yieldScore}</b><span class="bar"><i style="width:${yieldScore}%"></i></span><span></span><span>Payment Engine</span><b>${captureScore}</b><span class="bar"><i style="width:${captureScore}%"></i></span><span></span><span>Liquidity & Exchange Engine</span><b>${exchangeScore}</b><span class="bar"><i style="width:${exchangeScore}%"></i></span><span></span><span>Infrastructure Engine</span><b>${infraScore}</b><span class="bar"><i style="width:${infraScore}%"></i></span><span></span></section><p>The loop closes when prediction, yield, payment, liquidity, and infrastructure outputs all feed the next journey decision.</p></main></body></html>`;
            return {
              closed_loop_health_score: health,
              user_journey_value_loop: 'prediction -> yield -> payment -> liquidity/exchange -> infrastructure -> next prediction',
              web3_economics_decision_driver: health >= 70 ? 'closed value loop is viable under current drivers' : 'rebalance driver assumptions before scaling the loop',
              outputSrcDoc: html
            };
          }
    - id: {key: id, type: string, value: "decision_ranking"}
      type: {key: type, type: string, value: "DecisionWidget"}
      label: {key: label, type: string, value: "Decision Ranking"}
      position: {key: position, type: object, value: {"x":1500,"y":310}}
      handles: {key: handles, type: object, value: {"target":["lowest_cash_tco_driver","highest_margin_driver","breakeven_path_driver","lowest_lockin_driver","tokenized_distribution_driver"],"source":["recommended_demo_path","managed_demo_path","tokenized_demo_path","margin_optimized_path"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"lowest_cash_tco_driver":"decision_driver_signal","highest_margin_driver":"decision_driver_signal","breakeven_path_driver":"decision_driver_signal","lowest_lockin_driver":"decision_driver_signal","tokenized_distribution_driver":"decision_driver_signal"},"out":{"recommended_demo_path":"decision_driver_signal","managed_demo_path":"decision_driver_signal","tokenized_demo_path":"decision_driver_signal","margin_optimized_path":"decision_driver_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:decision_ranking"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      managed_demo_path: {key: managed_demo_path, type: string, value: "managed demo = Fetch Agentverse Basic/Premium + explicit model cap"}
      margin_optimized_path: {key: margin_optimized_path, type: string, value: "use calculator highest_margin_driver and validate conversion inputs"}
      recommended_demo_path: {key: recommended_demo_path, type: string, value: "local demo = elizaOS + local model + no token launch"}
      size: {key: size, type: object, value: {"width":340,"height":240}}
      tags: {key: tags, type: array, value: ["pivot"]}
      tokenized_demo_path: {key: tokenized_demo_path, type: string, value: "tokenized demo = Virtuals GAME + separate token setup meters"}
      "visual:fill": {key: "visual:fill", type: string, value: "#f97316"}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18.94427190999916}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "tco_chart_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "TCO Chart Panel"}
      position: {key: position, type: object, value: {"x":1500,"y":650}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output: {key: output, type: textarea, value: "Interactive chart panel receives calculator outputSrcDoc."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body><p>TCO chart waits for calculator output.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":420,"height":260}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
    - id: {key: id, type: string, value: "value_loop_chart_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Value Loop Chart Panel"}
      position: {key: position, type: object, value: {"x":2100,"y":1260}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_chart_html"},"out":{"outputSrcDoc":"rich_media_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:value_loop_chart_panel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output: {key: output, type: textarea, value: "Closed value-loop chart panel receives closed_value_loop outputSrcDoc."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: "<!doctype html><html><body><p>Value loop chart waits for engine outputs.</p></body></html>"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      size: {key: size, type: object, value: {"width":440,"height":270}}
      tags: {key: tags, type: array, value: ["idea"]}
      "visual:fill": {key: "visual:fill", type: string, value: "var(--kg-canvas-accent)"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:stroke": {key: "visual:stroke", type: string, value: "#9CA3AF"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
  edges:
    - {"id":"kgc-edge:drives:a1d6ca9c","source":"agent_token_take_rate","target":"monthly_revenue_usd","label":"drives"}
    - {"id":"kgc-edge:feeds:f03b58e2","source":"closed_value_loop_semantic","target":"value_loop_chart_panel_semantic","label":"feeds"}
    - {"id":"kgc-edge:produces:56fe28c4","source":"closed_value_loop_semantic","target":"closed_loop_health_score","label":"produces"}
    - {"id":"kgc-edge:produces:1840fda4","source":"closed_value_loop_semantic","target":"user_journey_value_loop","label":"produces"}
    - {"id":"kgc-edge:accumulates:6c290dbe","source":"hosting_or_cloud_runtime_usd","target":"tco_score","label":"accumulates"}
    - {"id":"kgc-edge:drives:4c426f7a","source":"hosting_or_cloud_runtime_usd","target":"elizaos_ai16z","label":"drives"}
    - {"id":"kgc-edge:feeds:cfe8f73a","source":"infrastructure_engine_semantic","target":"closed_value_loop_semantic","label":"feeds"}
    - {"id":"kgc-edge:feeds:c38269ae","source":"liquidity_exchange_engine_semantic","target":"infrastructure_engine_semantic","label":"feeds"}
    - {"id":"kgc-edge:drives:97c5f8bd","source":"managed_hosting_required","target":"platform_subscription_usd","label":"drives"}
    - {"id":"kgc-edge:drives:d0772e09","source":"marketplace_gmv_usd","target":"monthly_revenue_usd","label":"drives"}
    - {"id":"kgc-edge:accumulates:94436e49","source":"model_provider_fee_usd","target":"tco_score","label":"accumulates"}
    - {"id":"kgc-edge:drives:219b719f","source":"monthly_active_users","target":"monthly_revenue_usd","label":"drives"}
    - {"id":"kgc-edge:drives:31a5001f","source":"monthly_agent_requests","target":"platform_unit_call_cost_usd","label":"drives"}
    - {"id":"kgc-edge:accumulates:124b87bf","source":"net_revenue_usd","target":"net_margin_usd","label":"accumulates"}
    - {"id":"kgc-edge:accumulates:755017f2","source":"onchain_gas_and_token_fees","target":"tco_score","label":"accumulates"}
    - {"id":"kgc-edge:drives:525d867e","source":"onchain_token_launch_required","target":"token_setup_exposure","label":"drives"}
    - {"id":"kgc-edge:drives:c87f22e4","source":"paid_conversion_rate","target":"monthly_revenue_usd","label":"drives"}
    - {"id":"kgc-edge:feeds:e76a34f7","source":"payment_engine_semantic","target":"liquidity_exchange_engine_semantic","label":"feeds"}
    - {"id":"kgc-edge:accumulates:60367f38","source":"platform_subscription_usd","target":"tco_score","label":"accumulates"}
    - {"id":"kgc-edge:drives:02675c2c","source":"platform_subscription_usd","target":"fetch_agentverse","label":"drives"}
    - {"id":"kgc-edge:accumulates:389cc7f8","source":"platform_unit_call_cost_usd","target":"tco_score","label":"accumulates"}
    - {"id":"kgc-edge:drives:a6e68b1a","source":"prediction_accuracy_rate","target":"prediction_engine_semantic","label":"drives"}
    - {"id":"kgc-edge:feeds:5ce6ff90","source":"prediction_engine_semantic","target":"closed_value_loop_semantic","label":"feeds"}
    - {"id":"kgc-edge:feeds:337735ff","source":"prediction_engine_semantic","target":"yield_engine_semantic","label":"feeds"}
    - {"id":"kgc-edge:produces:7f5068e0","source":"revenue_calculator_semantic","target":"monthly_revenue_usd","label":"produces"}
    - {"id":"kgc-edge:produces:d2d1a86e","source":"revenue_calculator_semantic","target":"net_revenue_usd","label":"produces"}
    - {"id":"kgc-edge:drives:24650fce","source":"subscription_price_usd","target":"monthly_revenue_usd","label":"drives"}
    - {"id":"kgc-edge:reduces:908de8fb","source":"support_refund_rate","target":"net_revenue_usd","label":"reduces"}
    - {"id":"kgc-edge:feeds:e41580f0","source":"tco_calculator_semantic","target":"tco_chart_panel_semantic","label":"feeds"}
    - {"id":"kgc-edge:produces:4c51319b","source":"tco_calculator_semantic","target":"decision_ranking_semantic","label":"produces"}
    - {"id":"kgc-edge:accumulates:c85190db","source":"tco_score","target":"net_margin_usd","label":"accumulates"}
    - {"id":"kgc-edge:drives:71c6c6af","source":"token_setup_exposure","target":"virtuals_game","label":"drives"}
    - {"id":"kgc-edge:drives:6f8a7d69","source":"wallet_activation_rate","target":"prediction_engine_semantic","label":"drives"}
    - {"id":"kgc-edge:feeds:ab48b8d0","source":"yield_engine_semantic","target":"payment_engine_semantic","label":"feeds"}
    - {"id":"e-workload-fetch","source":"workload_drivers","sourceHandle":"monthly_agent_requests","target":"fetch_agentverse_tco","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-workload-eliza","source":"workload_drivers","sourceHandle":"monthly_agent_requests","target":"elizaos_ai16z_tco","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-workload-virtuals","source":"workload_drivers","sourceHandle":"monthly_agent_requests","target":"virtuals_game_tco","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-workload-revenue","source":"workload_drivers","sourceHandle":"monthly_agent_requests","target":"revenue_calculator","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-subscription-fetch","source":"shared_platform_drivers","sourceHandle":"platform_subscription_usd","target":"fetch_agentverse_tco","targetHandle":"platform_subscription_usd","label":"platform_subscription_usd","type":"platform_cost_signal"}
    - {"id":"e-hosting-fetch","source":"shared_platform_drivers","sourceHandle":"managed_hosting_required","target":"fetch_agentverse_tco","targetHandle":"managed_hosting_required","label":"managed_hosting_required","type":"platform_cost_signal"}
    - {"id":"e-model-fetch","source":"shared_platform_drivers","sourceHandle":"model_provider_fee_usd","target":"fetch_agentverse_tco","targetHandle":"model_provider_fee_usd","label":"model_provider_fee_usd","type":"platform_cost_signal"}
    - {"id":"e-hosting-eliza","source":"shared_platform_drivers","sourceHandle":"hosting_or_cloud_runtime_usd","target":"elizaos_ai16z_tco","targetHandle":"hosting_or_cloud_runtime_usd","label":"hosting_or_cloud_runtime_usd","type":"platform_cost_signal"}
    - {"id":"e-model-eliza","source":"shared_platform_drivers","sourceHandle":"model_provider_fee_usd","target":"elizaos_ai16z_tco","targetHandle":"model_provider_fee_usd","label":"model_provider_fee_usd","type":"platform_cost_signal"}
    - {"id":"e-api-eliza","source":"shared_platform_drivers","sourceHandle":"social_api_rpc_data_api_fees","target":"elizaos_ai16z_tco","targetHandle":"social_api_rpc_data_api_fees","label":"social_api_rpc_data_api_fees","type":"platform_cost_signal"}
    - {"id":"e-ops-eliza","source":"shared_platform_drivers","sourceHandle":"ops_hours","target":"elizaos_ai16z_tco","targetHandle":"ops_hours","label":"ops_hours","type":"platform_cost_signal"}
    - {"id":"e-unit-virtuals","source":"shared_platform_drivers","sourceHandle":"platform_unit_call_cost_usd","target":"virtuals_game_tco","targetHandle":"platform_unit_call_cost_usd","label":"platform_unit_call_cost_usd","type":"platform_cost_signal"}
    - {"id":"e-token-launch-virtuals","source":"token_exposure_drivers","sourceHandle":"onchain_token_launch_required","target":"virtuals_game_tco","targetHandle":"onchain_token_launch_required","label":"onchain_token_launch_required","type":"token_risk_signal"}
    - {"id":"e-token-setup-virtuals","source":"token_exposure_drivers","sourceHandle":"token_setup_exposure","target":"virtuals_game_tco","targetHandle":"token_setup_exposure","label":"token_setup_exposure","type":"token_risk_signal"}
    - {"id":"e-gas-fetch","source":"token_exposure_drivers","sourceHandle":"onchain_gas_and_token_fees","target":"fetch_agentverse_tco","targetHandle":"onchain_gas_and_token_fees","label":"onchain_gas_and_token_fees","type":"token_risk_signal"}
    - {"id":"e-gas-virtuals","source":"token_exposure_drivers","sourceHandle":"onchain_gas_and_token_fees","target":"virtuals_game_tco","targetHandle":"onchain_gas_and_token_fees","label":"onchain_gas_and_token_fees","type":"token_risk_signal"}
    - {"id":"e-volatility-virtuals","source":"token_exposure_drivers","sourceHandle":"token_price_volatility","target":"virtuals_game_tco","targetHandle":"token_price_volatility","label":"token_price_volatility","type":"token_risk_signal"}
    - {"id":"e-revenue-users","source":"revenue_drivers","sourceHandle":"monthly_active_users","target":"revenue_calculator","targetHandle":"monthly_active_users","label":"monthly_active_users","type":"revenue_driver_signal"}
    - {"id":"e-revenue-conversion","source":"revenue_drivers","sourceHandle":"paid_conversion_rate","target":"revenue_calculator","targetHandle":"paid_conversion_rate","label":"paid_conversion_rate","type":"revenue_driver_signal"}
    - {"id":"e-revenue-price","source":"revenue_drivers","sourceHandle":"subscription_price_usd","target":"revenue_calculator","targetHandle":"subscription_price_usd","label":"subscription_price_usd","type":"revenue_driver_signal"}
    - {"id":"e-revenue-gmv","source":"revenue_drivers","sourceHandle":"marketplace_gmv_usd","target":"revenue_calculator","targetHandle":"marketplace_gmv_usd","label":"marketplace_gmv_usd","type":"revenue_driver_signal"}
    - {"id":"e-revenue-take","source":"revenue_drivers","sourceHandle":"agent_token_take_rate","target":"revenue_calculator","targetHandle":"agent_token_take_rate","label":"agent_token_take_rate","type":"revenue_driver_signal"}
    - {"id":"e-revenue-refund","source":"revenue_drivers","sourceHandle":"support_refund_rate","target":"revenue_calculator","targetHandle":"support_refund_rate","label":"support_refund_rate","type":"revenue_driver_signal"}
    - {"id":"e-revenue-gross-calc","source":"revenue_calculator","sourceHandle":"monthly_revenue_usd","target":"tco_calculator","targetHandle":"monthly_revenue_usd","label":"monthly_revenue_usd","type":"revenue_metric_signal"}
    - {"id":"e-revenue-net-calc","source":"revenue_calculator","sourceHandle":"net_revenue_usd","target":"tco_calculator","targetHandle":"net_revenue_usd","label":"net_revenue_usd","type":"revenue_metric_signal"}
    - {"id":"e-fetch-calc","source":"fetch_agentverse_tco","sourceHandle":"fetch_monthly_tco_usd","target":"tco_calculator","targetHandle":"fetch_monthly_tco_usd","label":"fetch_monthly_tco_usd","type":"stack_tco_metric"}
    - {"id":"e-eliza-calc","source":"elizaos_ai16z_tco","sourceHandle":"eliza_monthly_tco_usd","target":"tco_calculator","targetHandle":"eliza_monthly_tco_usd","label":"eliza_monthly_tco_usd","type":"stack_tco_metric"}
    - {"id":"e-virtuals-calc","source":"virtuals_game_tco","sourceHandle":"virtuals_monthly_tco_usd","target":"tco_calculator","targetHandle":"virtuals_monthly_tco_usd","label":"virtuals_monthly_tco_usd","type":"stack_tco_metric"}
    - {"id":"e-fetch-risk-calc","source":"fetch_agentverse_tco","sourceHandle":"fetch_quota_risk","target":"tco_calculator","targetHandle":"fetch_quota_risk","label":"fetch_quota_risk","type":"token_risk_signal"}
    - {"id":"e-eliza-risk-calc","source":"elizaos_ai16z_tco","sourceHandle":"eliza_ops_risk","target":"tco_calculator","targetHandle":"eliza_ops_risk","label":"eliza_ops_risk","type":"platform_cost_signal"}
    - {"id":"e-virtuals-risk-calc","source":"virtuals_game_tco","sourceHandle":"virtuals_token_risk","target":"tco_calculator","targetHandle":"virtuals_token_risk","label":"virtuals_token_risk","type":"token_risk_signal"}
    - {"id":"e-users-prediction","source":"revenue_drivers","sourceHandle":"monthly_active_users","target":"prediction_engine","targetHandle":"monthly_active_users","label":"monthly_active_users","type":"revenue_driver_signal"}
    - {"id":"e-conversion-prediction","source":"revenue_drivers","sourceHandle":"paid_conversion_rate","target":"prediction_engine","targetHandle":"paid_conversion_rate","label":"paid_conversion_rate","type":"revenue_driver_signal"}
    - {"id":"e-accuracy-prediction","source":"web3_economics_drivers","sourceHandle":"prediction_accuracy_rate","target":"prediction_engine","targetHandle":"prediction_accuracy_rate","label":"prediction_accuracy_rate","type":"journey_driver_signal"}
    - {"id":"e-wallet-prediction","source":"web3_economics_drivers","sourceHandle":"wallet_activation_rate","target":"prediction_engine","targetHandle":"wallet_activation_rate","label":"wallet_activation_rate","type":"journey_driver_signal"}
    - {"id":"e-net-yield","source":"revenue_calculator","sourceHandle":"net_revenue_usd","target":"yield_engine","targetHandle":"net_revenue_usd","label":"net_revenue_usd","type":"revenue_metric_signal"}
    - {"id":"e-request-yield","source":"revenue_calculator","sourceHandle":"revenue_per_request_usd","target":"yield_engine","targetHandle":"revenue_per_request_usd","label":"revenue_per_request_usd","type":"revenue_metric_signal"}
    - {"id":"e-share-yield","source":"web3_economics_drivers","sourceHandle":"yield_share_rate","target":"yield_engine","targetHandle":"yield_share_rate","label":"yield_share_rate","type":"journey_driver_signal"}
    - {"id":"e-quality-yield","source":"prediction_engine","sourceHandle":"predicted_intent_quality_score","target":"yield_engine","targetHandle":"predicted_intent_quality_score","label":"predicted_intent_quality_score","type":"prediction_engine_signal"}
    - {"id":"e-demand-yield","source":"prediction_engine","sourceHandle":"demand_forecast_index","target":"yield_engine","targetHandle":"demand_forecast_index","label":"demand_forecast_index","type":"prediction_engine_signal"}
    - {"id":"e-net-payment","source":"revenue_calculator","sourceHandle":"net_revenue_usd","target":"payment_engine","targetHandle":"net_revenue_usd","label":"net_revenue_usd","type":"revenue_metric_signal"}
    - {"id":"e-yield-payment","source":"yield_engine","sourceHandle":"user_value_yield_usd","target":"payment_engine","targetHandle":"user_value_yield_usd","label":"user_value_yield_usd","type":"yield_engine_signal"}
    - {"id":"e-success-payment","source":"web3_economics_drivers","sourceHandle":"payment_success_rate","target":"payment_engine","targetHandle":"payment_success_rate","label":"payment_success_rate","type":"journey_driver_signal"}
    - {"id":"e-fee-payment","source":"web3_economics_drivers","sourceHandle":"payment_fee_rate","target":"payment_engine","targetHandle":"payment_fee_rate","label":"payment_fee_rate","type":"journey_driver_signal"}
    - {"id":"e-settled-liquidity","source":"payment_engine","sourceHandle":"settled_payment_volume_usd","target":"liquidity_exchange_engine","targetHandle":"settled_payment_volume_usd","label":"settled_payment_volume_usd","type":"payment_engine_signal"}
    - {"id":"e-spread-liquidity","source":"web3_economics_drivers","sourceHandle":"liquidity_spread_rate","target":"liquidity_exchange_engine","targetHandle":"liquidity_spread_rate","label":"liquidity_spread_rate","type":"journey_driver_signal"}
    - {"id":"e-conversion-liquidity","source":"web3_economics_drivers","sourceHandle":"exchange_conversion_rate","target":"liquidity_exchange_engine","targetHandle":"exchange_conversion_rate","label":"exchange_conversion_rate","type":"journey_driver_signal"}
    - {"id":"e-volatility-liquidity","source":"token_exposure_drivers","sourceHandle":"token_price_volatility","target":"liquidity_exchange_engine","targetHandle":"token_price_volatility","label":"token_price_volatility","type":"token_risk_signal"}
    - {"id":"e-workload-infra","source":"workload_drivers","sourceHandle":"monthly_agent_requests","target":"infrastructure_engine","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-unit-infra","source":"web3_economics_drivers","sourceHandle":"infrastructure_unit_cost_usd","target":"infrastructure_engine","targetHandle":"infrastructure_unit_cost_usd","label":"infrastructure_unit_cost_usd","type":"journey_driver_signal"}
    - {"id":"e-uptime-infra","source":"web3_economics_drivers","sourceHandle":"infrastructure_uptime_slo","target":"infrastructure_engine","targetHandle":"infrastructure_uptime_slo","label":"infrastructure_uptime_slo","type":"journey_driver_signal"}
    - {"id":"e-depth-infra","source":"liquidity_exchange_engine","sourceHandle":"exchange_liquidity_depth_usd","target":"infrastructure_engine","targetHandle":"exchange_liquidity_depth_usd","label":"exchange_liquidity_depth_usd","type":"liquidity_exchange_signal"}
    - {"id":"e-paymentfee-infra","source":"payment_engine","sourceHandle":"payment_fee_cost_usd","target":"infrastructure_engine","targetHandle":"payment_fee_cost_usd","label":"payment_fee_cost_usd","type":"payment_engine_signal"}
    - {"id":"e-prediction-loop","source":"prediction_engine","sourceHandle":"predicted_intent_quality_score","target":"closed_value_loop","targetHandle":"predicted_intent_quality_score","label":"predicted_intent_quality_score","type":"prediction_engine_signal"}
    - {"id":"e-yield-loop","source":"yield_engine","sourceHandle":"protocol_yield_score","target":"closed_value_loop","targetHandle":"protocol_yield_score","label":"protocol_yield_score","type":"yield_engine_signal"}
    - {"id":"e-capture-loop","source":"payment_engine","sourceHandle":"payment_value_capture_usd","target":"closed_value_loop","targetHandle":"payment_value_capture_usd","label":"payment_value_capture_usd","type":"payment_engine_signal"}
    - {"id":"e-exchange-loop","source":"liquidity_exchange_engine","sourceHandle":"token_exchange_efficiency_score","target":"closed_value_loop","targetHandle":"token_exchange_efficiency_score","label":"token_exchange_efficiency_score","type":"liquidity_exchange_signal"}
    - {"id":"e-uptime-loop","source":"infrastructure_engine","sourceHandle":"uptime_value_score","target":"closed_value_loop","targetHandle":"uptime_value_score","label":"uptime_value_score","type":"infrastructure_engine_signal"}
    - {"id":"e-infra-value-loop","source":"infrastructure_engine","sourceHandle":"infra_adjusted_value_usd","target":"closed_value_loop","targetHandle":"infra_adjusted_value_usd","label":"infra_adjusted_value_usd","type":"infrastructure_engine_signal"}
    - {"id":"e-net-loop","source":"revenue_calculator","sourceHandle":"net_revenue_usd","target":"closed_value_loop","targetHandle":"net_revenue_usd","label":"net_revenue_usd","type":"revenue_metric_signal"}
    - {"id":"e-margin-loop","source":"tco_calculator","sourceHandle":"highest_margin_driver","target":"closed_value_loop","targetHandle":"highest_margin_driver","label":"highest_margin_driver","type":"decision_driver_signal"}
    - {"id":"e-lowest-cash-decision","source":"tco_calculator","sourceHandle":"lowest_cash_tco_driver","target":"decision_ranking","targetHandle":"lowest_cash_tco_driver","label":"lowest_cash_tco_driver","type":"decision_driver_signal"}
    - {"id":"e-margin-decision","source":"tco_calculator","sourceHandle":"highest_margin_driver","target":"decision_ranking","targetHandle":"highest_margin_driver","label":"highest_margin_driver","type":"decision_driver_signal"}
    - {"id":"e-breakeven-decision","source":"tco_calculator","sourceHandle":"breakeven_path_driver","target":"decision_ranking","targetHandle":"breakeven_path_driver","label":"breakeven_path_driver","type":"decision_driver_signal"}
    - {"id":"e-lockin-decision","source":"tco_calculator","sourceHandle":"lowest_lockin_driver","target":"decision_ranking","targetHandle":"lowest_lockin_driver","label":"lowest_lockin_driver","type":"decision_driver_signal"}
    - {"id":"e-tokenized-decision","source":"tco_calculator","sourceHandle":"tokenized_distribution_driver","target":"decision_ranking","targetHandle":"tokenized_distribution_driver","label":"tokenized_distribution_driver","type":"decision_driver_signal"}
    - {"id":"e-calculator-chart","source":"tco_calculator","sourceHandle":"outputSrcDoc","target":"tco_chart_panel","targetHandle":"outputSrcDoc","label":"outputSrcDoc","type":"rich_media_chart_html"}
    - {"id":"e-value-loop-chart","source":"closed_value_loop","sourceHandle":"outputSrcDoc","target":"value_loop_chart_panel","targetHandle":"outputSrcDoc","label":"outputSrcDoc","type":"rich_media_chart_html"}
    - {"id":"e-tco-entry-mau","source":"tco_source_input","sourceHandle":"monthly_active_users","target":"tco_compute","targetHandle":"monthly_active_users","label":"monthly_active_users","type":"demand_driver_signal"}
    - {"id":"e-tco-entry-req","source":"tco_source_input","sourceHandle":"monthly_agent_requests","target":"tco_compute","targetHandle":"monthly_agent_requests","label":"monthly_agent_requests","type":"demand_driver_signal"}
    - {"id":"e-tco-entry-cvr","source":"tco_source_input","sourceHandle":"paid_conversion_rate","target":"tco_compute","targetHandle":"paid_conversion_rate","label":"paid_conversion_rate","type":"revenue_driver_signal"}
    - {"id":"e-tco-entry-tkr","source":"tco_source_input","sourceHandle":"agent_token_take_rate","target":"tco_compute","targetHandle":"agent_token_take_rate","label":"agent_token_take_rate","type":"revenue_driver_signal"}
    - {"id":"e-tco-entry-mf","source":"tco_source_input","sourceHandle":"model_provider_fee_usd","target":"tco_compute","targetHandle":"model_provider_fee_usd","label":"model_provider_fee_usd","type":"platform_cost_signal"}
    - {"id":"e-tco-entry-sub","source":"tco_source_input","sourceHandle":"platform_subscription_usd","target":"tco_compute","targetHandle":"platform_subscription_usd","label":"platform_subscription_usd","type":"platform_cost_signal"}
    - {"id":"e-tco-compute-chart","source":"tco_compute","sourceHandle":"outputSrcDoc","target":"tco_chart_panel","targetHandle":"outputSrcDoc","label":"tco summary → chart panel","type":"rich_media_chart_html"}
kgParserRoutingContract:
  version: "knowgrph-parser-routing/v1"
  parserLogic: "opening frontmatter and authored source payloads are SSOT; parsers materialize graphData without renderer-local aliases"
  routingKeys:
    surface: "kgCanvasSurfaceMode"
    renderMode: "kgCanvasRenderMode"
    renderer: "kgCanvas2dRenderer"
    semanticMode: "kgDocumentSemanticMode"
    frontmatterMode: "kgFrontmatterModeEnabled"
    flowGraph: "flow"
    flowNodes: "flow.nodes"
    flowEdges: "flow.edges"
    mermaidBlocks: "flow_diagrams"
    strybldrStoryboard: "kgStrybldrStoryboard"
  diagramKinds:
    - "mermaid_flowchart"
    - "mermaid_gitgraph"
    - "mermaid_architecture"
    - "mermaid_eventmodeling"
    - "mermaid_gantt"
    - "frontmatter_flow"
    - "strybldr_storyboard"
  surfaces:
    - "2D Renderer: Storyboard"
    - "2D Renderer: Storyboard"
    - "BottomPanel/FloatingPanel Mermaid panels"
  edgePolicy: "explicit graphData.edges, flow.edges, workflow.edges, and diagram edges are source-owned SSOT; renderers project visible connectors only"
  forkPolicy: "fork, branch, candidate, and publish metadata remain authored source fields and surface through parsed graph edges without downstream remapping"
---
node_types:
  - metric
  - lever
  - cost
  - outcome
  - component
edge_predicates:
  - drives
  - reduces
  - caps
  - accumulates
  - penalises
  - emits
  - bounds
  - informs
  - sequences
  - improves
  - lowers
  - triggers
  - feeds
  - wraps
  - validates
  - produces
  - consumes
tags:
  - knowgrph
  - token-economics
  - web3-economics
  - web3-ai-agents
  - closed-user-journey
  - tco
  - kgc
modelSelection:
  selectionModel: "projected-data"            # renderers project these typed option groups as dropdowns; they do not branch on them
  scope: "local-overrides-global"             # a node-local options.model overrides the matching group's global default
  groups:
    text:
      global: "agnes-2.0-flash"               # group-global default; override per node via options.model
      options:
        - "agnes-2.0-flash"
        - "seed-2-0-mini-260215"
        - "seed-2-0-lite-260228"
        - "seed-2-0-pro-260328"
        - "seed-1-8-251228"
    image:
      global: "seedream-4-0-250828"
      options:
        - "seedream-4-0-250828"
        - "seedream-4-5-251128"
        - "seedream-5-0-260128"
    video:
      global: "seedance-1-0-pro-fast-251015"
      options:
        - "seedance-1-0-pro-fast-251015"
        - "seedance-1-5-pro-251215"
        - "dreamina-seedance-2-0-fast-260128"
        - "dreamina-seedance-2-0-260128"

# Knowgrph Token Economics Model Demo - Storyboard

## Scope

This demo compares the total cost of ownership (TCO) for three Web3 AI agent stacks as a native `2D Renderer: Storyboard` cost-driver graph:

1. Virtuals Protocol / GAME
2. Fetch.ai / Agentverse
3. elizaOS / AI16Z

Market-cap lists are not perfectly aligned. CoinGecko's AI Agents category currently surfaces Venice Token, Artificial Superintelligence Alliance, and Virtuals Protocol near the top, while CoinMarketCap's AI Agents category lists Virtuals Protocol, Artificial Superintelligence Alliance, and Kite near the top. QuickNode's Web3 AI agent guide highlights Virtuals Protocol, AI16Z DAO by Eliza Labs, AIXBT, and Fetch.ai. For TCO, this document compares deployable agent stacks rather than pure token tickers.

Not investment advice. Prices, quotas, token requirements, and product terms change. Treat this as an executable TCO model template, not a live quote.

## Storyboard Widget Runtime Contract

The frontmatter `flow:` block is the source of truth for this demo. Each widget exposes port handles named after a cost driver, risk driver, TCO metric, revenue metric, value-loop metric, rendered report payload, or decision driver. The Storyboard Widget should render those handles as connectable widget ports, and each normal edge must keep one canonical driver key across `sourceHandle`, `targetHandle`, and `label`.

In this document, "cost driver" is intentionally broad: anything that changes monthly cost, token exposure, revenue offset, margin, break-even posture, infrastructure value, or rendered decision output is modeled as a driver handle. The handle itself is the semantic key used by ingestion, parsing, workflow computation, edge rendering, and Rich Media Panel output.

The normalized `{key,type,value}` frontmatter shape is part of the E2E fixture contract. Storyboard Widget must map each row by the wrapper `key` and normalized schema path, not by the declaration container name. For example, the `Revenue Drivers` widget exposes `agent_token_take_rate` as one inline-editable KTV row with the output port handle attached to that row. A second non-inline `agent_token_take_rate` row is invalid because it splits the editable value from the functional port.

## Cost-Driver Port-Handle Contract

The Storyboard Widget canvas should read each visible handle as an economic driver, not as a generic UI socket. A valid driver edge follows this identity rule:

```text
source node driver handle -> target node driver handle
sourceHandle == targetHandle == edge label
```

Widget port interpretation stays uniform across the canvas:

| Port Site | Driver Meaning |
| `handles.source` on driver widgets | Emits editable assumptions such as workload, platform, token, revenue, and Web3 journey drivers. |
| `handles.target` on calculator and engine widgets | Consumes the exact same driver key emitted upstream; no widget-local alias is introduced. |
| `handles.source` on calculator and engine widgets | Emits computed cost, revenue, risk, value-loop, or decision drivers for downstream widgets. |
| `handles.target` and `handles.source` on Rich Media Panel widgets | Carries `outputSrcDoc` as the rendered report payload driver, so chart rendering remains part of the same driver graph. |

This keeps the graph neutral and inspectable:

- Driver inputs such as `monthly_agent_requests`, `hosting_or_cloud_runtime_usd`, and `token_price_volatility` stay named at the widget boundary where they are consumed.
- Computed outputs such as `fetch_monthly_tco_usd`, `payment_fee_cost_usd`, and `closed_loop_health_score` become downstream driver handles instead of hidden recalculations.
- `outputSrcDoc` is treated as the rendered cost-report payload driver for Rich Media Panel widgets, so charts remain connected through the same port-handle contract.
- There are no visual-only aliases such as `left`, `right`, `in`, `out`, or stack-local remaps in the edge layer.
- `socket_types` and `flow:portTypes` decorate an existing driver handle; they do not create a second handle vocabulary.
- `handles.source` and `handles.target` list which driver keys are exposed on each side. They are not replacement handle names, and rendered rows must not collapse driver handles into `handles.source` or `handles.target`.

Driver-handle families:

| Driver Family | Storyboard Widget Port Role | Port Handles |
| Demand | Workload meters that fan out to stack, revenue, and infrastructure widgets. | `monthly_agent_requests`, `avg_tool_calls_per_request`, `avg_tokens_per_request`, `retry_rate` |
| Platform | Cash-cost, runtime, provider, external API, and operator meters. | `platform_subscription_usd`, `platform_unit_call_cost_usd`, `managed_hosting_required`, `hosting_or_cloud_runtime_usd`, `model_provider_fee_usd`, `social_api_rpc_data_api_fees`, `ops_hours` |
| Token | On-chain launch, gas, token setup, and volatility exposure. | `onchain_token_launch_required`, `token_setup_exposure`, `onchain_gas_and_token_fees`, `token_price_volatility` |
| Revenue | Product, marketplace, and refund drivers that offset TCO. | `monthly_active_users`, `paid_conversion_rate`, `subscription_price_usd`, `marketplace_gmv_usd`, `agent_token_take_rate`, `support_refund_rate` |
| Web3 Journey | Prediction, wallet, yield, payment, liquidity, exchange, and infrastructure assumptions. | `prediction_accuracy_rate`, `wallet_activation_rate`, `yield_share_rate`, `payment_success_rate`, `payment_fee_rate`, `liquidity_spread_rate`, `exchange_conversion_rate`, `infrastructure_uptime_slo`, `infrastructure_unit_cost_usd` |
| Stack TCO | Per-stack cost and risk outputs consumed by the TCO calculator. | `fetch_monthly_tco_usd`, `eliza_monthly_tco_usd`, `virtuals_monthly_tco_usd`, `fetch_quota_risk`, `eliza_ops_risk`, `virtuals_token_risk`, `fetch_tco_score`, `eliza_tco_score`, `virtuals_tco_score` |
| Revenue Metrics | Computed revenue and request-normalized revenue outputs. | `monthly_revenue_usd`, `net_revenue_usd`, `revenue_per_request_usd`, `revenue_model_confidence` |
| Value Loop Metrics | Computed engine outputs that score the closed user journey loop. | `predicted_intent_quality_score`, `conversion_uplift_rate`, `demand_forecast_index`, `user_value_yield_usd`, `protocol_yield_score`, `retention_value_index`, `settled_payment_volume_usd`, `payment_fee_cost_usd`, `payment_value_capture_usd`, `exchange_liquidity_depth_usd`, `liquidity_slippage_cost_usd`, `token_exchange_efficiency_score`, `infrastructure_cost_usd`, `uptime_value_score`, `infra_adjusted_value_usd`, `closed_loop_health_score`, `user_journey_value_loop` |
| Decisions | Ranked path outputs emitted by calculator and decision widgets. | `lowest_cash_tco_driver`, `highest_margin_driver`, `breakeven_path_driver`, `lowest_lockin_driver`, `tokenized_distribution_driver`, `web3_economics_decision_driver`, `recommended_demo_path`, `managed_demo_path`, `tokenized_demo_path`, `margin_optimized_path` |
| Render Payload | Chart payload handle for Rich Media Panel widgets. | `outputSrcDoc` |

| Widget | Input Port Handles | Output Port Handles | Purpose |
| `workload_drivers` | n/a | `monthly_agent_requests`, `avg_tool_calls_per_request`, `avg_tokens_per_request`, `retry_rate` | Demand-side cost drivers shared by every stack. |
| `shared_platform_drivers` | n/a | `platform_subscription_usd`, `platform_unit_call_cost_usd`, `managed_hosting_required`, `hosting_or_cloud_runtime_usd`, `model_provider_fee_usd`, `social_api_rpc_data_api_fees`, `ops_hours` | Platform, runtime, provider, API, and ops meters that can hit any stack. |
| `token_exposure_drivers` | n/a | `onchain_token_launch_required`, `token_setup_exposure`, `onchain_gas_and_token_fees`, `token_price_volatility` | Web3-specific token and gas exposure. |
| `revenue_drivers` | n/a | `monthly_active_users`, `paid_conversion_rate`, `subscription_price_usd`, `marketplace_gmv_usd`, `agent_token_take_rate`, `support_refund_rate` | Revenue-side drivers used by the margin simulation. |
| `web3_economics_drivers` | n/a | `prediction_accuracy_rate`, `wallet_activation_rate`, `yield_share_rate`, `payment_success_rate`, `payment_fee_rate`, `liquidity_spread_rate`, `exchange_conversion_rate`, `infrastructure_uptime_slo`, `infrastructure_unit_cost_usd` | Closed journey assumptions shared by the five Web3 economics engines. |
| `fetch_agentverse_tco` | `monthly_agent_requests`, `platform_subscription_usd`, `managed_hosting_required`, `model_provider_fee_usd`, `onchain_gas_and_token_fees` | `fetch_monthly_tco_usd`, `fetch_quota_risk`, `fetch_tco_score` | Hosted/Web3 agent TCO widget. |
| `elizaos_ai16z_tco` | `monthly_agent_requests`, `hosting_or_cloud_runtime_usd`, `model_provider_fee_usd`, `social_api_rpc_data_api_fees`, `ops_hours` | `eliza_monthly_tco_usd`, `eliza_ops_risk`, `eliza_tco_score` | FOSS/self-host TCO widget. |
| `virtuals_game_tco` | `monthly_agent_requests`, `platform_unit_call_cost_usd`, `onchain_token_launch_required`, `token_setup_exposure`, `onchain_gas_and_token_fees`, `token_price_volatility` | `virtuals_monthly_tco_usd`, `virtuals_token_risk`, `virtuals_tco_score` | Tokenized-agent TCO widget. |
| `revenue_calculator` | `monthly_agent_requests`, `monthly_active_users`, `paid_conversion_rate`, `subscription_price_usd`, `marketplace_gmv_usd`, `agent_token_take_rate`, `support_refund_rate` | `monthly_revenue_usd`, `net_revenue_usd`, `revenue_per_request_usd`, `revenue_model_confidence` | Computes monthly revenue and per-request revenue from business drivers. |
| `tco_calculator` | `monthly_revenue_usd`, `net_revenue_usd`, `fetch_monthly_tco_usd`, `eliza_monthly_tco_usd`, `virtuals_monthly_tco_usd`, `fetch_quota_risk`, `eliza_ops_risk`, `virtuals_token_risk` | `lowest_cash_tco_driver`, `highest_margin_driver`, `breakeven_path_driver`, `lowest_lockin_driver`, `tokenized_distribution_driver`, `outputSrcDoc` | Joins cost and revenue paths, computes margin drivers, and emits chart HTML without hiding assumptions. |
| `prediction_engine` | `monthly_active_users`, `paid_conversion_rate`, `prediction_accuracy_rate`, `wallet_activation_rate` | `predicted_intent_quality_score`, `conversion_uplift_rate`, `demand_forecast_index` | Converts closed-journey intent signals into demand and conversion forecasts. |
| `yield_engine` | `net_revenue_usd`, `revenue_per_request_usd`, `yield_share_rate`, `predicted_intent_quality_score`, `demand_forecast_index` | `user_value_yield_usd`, `protocol_yield_score`, `retention_value_index` | Converts revenue into user-retained value and protocol yield. |
| `payment_engine` | `net_revenue_usd`, `user_value_yield_usd`, `payment_success_rate`, `payment_fee_rate` | `settled_payment_volume_usd`, `payment_fee_cost_usd`, `payment_value_capture_usd` | Converts yielded value into settled payment volume and value capture. |
| `liquidity_exchange_engine` | `settled_payment_volume_usd`, `liquidity_spread_rate`, `exchange_conversion_rate`, `token_price_volatility` | `exchange_liquidity_depth_usd`, `liquidity_slippage_cost_usd`, `token_exchange_efficiency_score` | Converts settled payment volume into token/liquidity exchange efficiency. |
| `infrastructure_engine` | `monthly_agent_requests`, `infrastructure_unit_cost_usd`, `infrastructure_uptime_slo`, `exchange_liquidity_depth_usd`, `payment_fee_cost_usd` | `infrastructure_cost_usd`, `uptime_value_score`, `infra_adjusted_value_usd` | Prices the reliability layer required to keep the journey loop available. |
| `closed_value_loop` | `predicted_intent_quality_score`, `protocol_yield_score`, `payment_value_capture_usd`, `token_exchange_efficiency_score`, `uptime_value_score`, `infra_adjusted_value_usd`, `net_revenue_usd`, `highest_margin_driver` | `closed_loop_health_score`, `user_journey_value_loop`, `web3_economics_decision_driver`, `outputSrcDoc` | Scores the full closed user journey loop and emits the value-loop chart. |
| `decision_ranking` | `lowest_cash_tco_driver`, `highest_margin_driver`, `breakeven_path_driver`, `lowest_lockin_driver`, `tokenized_distribution_driver` | `recommended_demo_path`, `managed_demo_path`, `tokenized_demo_path`, `margin_optimized_path` | Converts calculator outputs into recommended demo paths. |
| `tco_chart_panel` | `outputSrcDoc` | `outputSrcDoc` | Rich Media Panel chart fed by the calculator output. |
| `value_loop_chart_panel` | `outputSrcDoc` | `outputSrcDoc` | Rich Media Panel chart fed by the closed value-loop evaluator. |

Renderer checks:

- `kgCanvas2dRenderer` is `storyboard`.
- `flow.nodes[*].handles.target` defines the visible input handles.
- `flow.nodes[*].handles.source` defines the visible output handles.
- `flow.costDriverPortModel.driverFamilies` is the semantic allowlist for those visible handles.
- Every visible widget handle resolves through `flow.costDriverPortModel.driverFamilies` before any socket styling, side placement, or widget-specific rendering is considered.
- `flow.edges[*].sourceHandle`, `flow.edges[*].targetHandle`, and `flow.edges[*].label` use the same canonical driver key for normal driver edges.
- `flow.computed` is enabled so the calculator can emit decision drivers and a chart `outputSrcDoc`.
- `tco_chart_panel` is a Rich Media Panel; its only visible port is the chart payload handle.
- Token exposure stays a separate driver group instead of being converted into fixed USD values.
- `socket_types` color every handle and edge by shared renderer palette role: hypothesis for demand/prediction, execution for platform/yield/infrastructure, alert for token risk, pivot for stack TCO/liquidity/closed-loop decisions, and the canvas accent for revenue/payment/chart payloads.
- `workflow_sections` keeps the MainPanel Workflow Manager view aligned with the same graph contract: ingest drivers, calculate stack costs, simulate margin, evaluate the five-engine Web3 value loop, and render decisions.

## Storyboard Widget Palette And Workflow

The document reuses the existing FloatingPanel Renderer palette keys instead of inventing stack-specific colors.

| Flow Segment | Socket Type | Palette Role | Handle Meaning |
| Demand drivers | `demand_driver_signal` | `hypothesis` | Workload assumptions that should be tested. |
| Platform costs | `platform_cost_signal` | `execution` | Cash-cost meters and operational meters. |
| Token exposure | `token_risk_signal` | `alert` | Token, gas, quota, volatility, and launch risks. |
| Stack TCO metrics | `stack_tco_metric` | `pivot` | Computed per-stack monthly TCO outputs. |
| Revenue drivers | `revenue_driver_signal` | `idea` | Product and marketplace revenue assumptions. |
| Revenue metrics | `revenue_metric_signal` | `execution` | Computed gross revenue, net revenue, and revenue/request. |
| Journey drivers | `journey_driver_signal` | `idea` | Wallet, payment, liquidity, prediction, and infrastructure assumptions. |
| Prediction Engine | `prediction_engine_signal` | `hypothesis` | Forecasted user intent, conversion uplift, and demand index. |
| Yield Engine | `yield_engine_signal` | `execution` | User-retained value, protocol yield, and retention value. |
| Payment Engine | `payment_engine_signal` | `idea` | Settled payment volume, payment fees, and captured value. |
| Liquidity & Exchange Engine | `liquidity_exchange_signal` | `pivot` | Exchange depth, slippage, and token exchange efficiency. |
| Infrastructure Engine | `infrastructure_engine_signal` | `neutral` | Availability cost, uptime score, and infrastructure-adjusted value. |
| Closed value loop | `closed_loop_signal` | `pivot` | Composite closed user journey health. |
| Decisions | `decision_driver_signal` | `neutral` | Ranked path outputs and break-even commentary. |
| Chart payload | `rich_media_chart_html` | `idea` | Rich Media Panel `outputSrcDoc`. |

## Web3 Economics Closed User Journey

The five engine widgets model a closed value loop rather than a one-way funnel:

```text
Prediction Engine
  -> Yield Engine
  -> Payment Engine
  -> Liquidity & Exchange Engine
  -> Infrastructure Engine
  -> next Prediction Engine decision
```

Engine formulas:

```text
predicted_intent_quality_score =
  prediction_accuracy_rate * 0.70
  + wallet_activation_rate * 0.30

user_value_yield =
  net_revenue * yield_share_rate * max(0.10, predicted_intent_quality_score)

settled_payment_volume =
  (net_revenue + user_value_yield) * payment_success_rate

liquidity_slippage_cost =
  settled_payment_volume * liquidity_spread_rate * (1 + token_price_volatility)

infrastructure_cost =
  monthly_agent_requests * infrastructure_unit_cost

closed_loop_health =
  average(protocol_yield_score, payment_capture_score, token_exchange_efficiency_score, uptime_value_score, infra_adjusted_value_score)
```

The loop remains neutral: every rate and cost is an editable port driver, and no engine assumes a specific wallet, chain, exchange, custodian, or hosting vendor.

## Semantic Graph Seed

This document declares the core TCO levers in KGC-compatible typed sigils:

- `@node:lever:monthly_agent_requests`
- `@node:lever:avg_tool_calls_per_request`
- `@node:lever:avg_tokens_per_request`
- `@node:lever:retry_rate`
- `@node:lever:managed_hosting_required`
- `@node:lever:onchain_token_launch_required`
- `@node:lever:monthly_active_users`
- `@node:lever:paid_conversion_rate`
- `@node:lever:subscription_price_usd`
- `@node:lever:marketplace_gmv_usd`
- `@node:lever:agent_token_take_rate`
- `@node:lever:support_refund_rate`
- `@node:lever:prediction_accuracy_rate`
- `@node:lever:wallet_activation_rate`
- `@node:lever:yield_share_rate`
- `@node:lever:payment_success_rate`
- `@node:lever:payment_fee_rate`
- `@node:lever:liquidity_spread_rate`
- `@node:lever:exchange_conversion_rate`
- `@node:lever:infrastructure_uptime_slo`
- `@node:lever:infrastructure_unit_cost_usd`
- `@node:cost:platform_subscription_usd`
- `@node:cost:platform_unit_call_cost_usd`
- `@node:cost:hosting_or_cloud_runtime_usd`
- `@node:cost:model_provider_fee_usd`
- `@node:cost:social_api_rpc_data_api_fees`
- `@node:cost:onchain_gas_and_token_fees`
- `@node:cost:token_setup_exposure`
- `@node:metric:monthly_revenue_usd`
- `@node:metric:net_revenue_usd`
- `@node:metric:net_margin_usd`
- `@node:metric:closed_loop_health_score`
- `@node:outcome:tco_score`
- `@node:outcome:user_journey_value_loop`
- `@node:component:virtuals_game`
- `@node:component:fetch_agentverse`
- `@node:component:elizaos_ai16z`
- `@node:component:revenue_calculator_semantic`
- `@node:component:tco_calculator_semantic`
- `@node:component:prediction_engine_semantic`
- `@node:component:yield_engine_semantic`
- `@node:component:payment_engine_semantic`
- `@node:component:liquidity_exchange_engine_semantic`
- `@node:component:infrastructure_engine_semantic`
- `@node:component:closed_value_loop_semantic`
- `@node:component:decision_ranking_semantic`
- `@node:component:tco_chart_panel_semantic`
- `@node:component:value_loop_chart_panel_semantic`

Relationships:

- `@edge:drives:monthly_agent_requests->platform_unit_call_cost_usd`
- `@edge:drives:managed_hosting_required->platform_subscription_usd`
- `@edge:drives:onchain_token_launch_required->token_setup_exposure`
- `@edge:drives:monthly_active_users->monthly_revenue_usd`
- `@edge:drives:paid_conversion_rate->monthly_revenue_usd`
- `@edge:drives:subscription_price_usd->monthly_revenue_usd`
- `@edge:drives:marketplace_gmv_usd->monthly_revenue_usd`
- `@edge:drives:agent_token_take_rate->monthly_revenue_usd`
- `@edge:reduces:support_refund_rate->net_revenue_usd`
- `@edge:drives:token_setup_exposure->virtuals_game`
- `@edge:drives:hosting_or_cloud_runtime_usd->elizaos_ai16z`
- `@edge:drives:platform_subscription_usd->fetch_agentverse`
- `@edge:accumulates:platform_subscription_usd->tco_score`
- `@edge:accumulates:platform_unit_call_cost_usd->tco_score`
- `@edge:accumulates:hosting_or_cloud_runtime_usd->tco_score`
- `@edge:accumulates:model_provider_fee_usd->tco_score`
- `@edge:accumulates:onchain_gas_and_token_fees->tco_score`
- `@edge:produces:revenue_calculator_semantic->monthly_revenue_usd`
- `@edge:produces:revenue_calculator_semantic->net_revenue_usd`
- `@edge:accumulates:net_revenue_usd->net_margin_usd`
- `@edge:accumulates:tco_score->net_margin_usd`
- `@edge:drives:prediction_accuracy_rate->prediction_engine_semantic`
- `@edge:drives:wallet_activation_rate->prediction_engine_semantic`
- `@edge:feeds:prediction_engine_semantic->yield_engine_semantic`
- `@edge:feeds:yield_engine_semantic->payment_engine_semantic`
- `@edge:feeds:payment_engine_semantic->liquidity_exchange_engine_semantic`
- `@edge:feeds:liquidity_exchange_engine_semantic->infrastructure_engine_semantic`
- `@edge:feeds:prediction_engine_semantic->closed_value_loop_semantic`
- `@edge:feeds:infrastructure_engine_semantic->closed_value_loop_semantic`
- `@edge:produces:closed_value_loop_semantic->closed_loop_health_score`
- `@edge:produces:closed_value_loop_semantic->user_journey_value_loop`
- `@edge:produces:tco_calculator_semantic->decision_ranking_semantic`
- `@edge:feeds:tco_calculator_semantic->tco_chart_panel_semantic`
- `@edge:feeds:closed_value_loop_semantic->value_loop_chart_panel_semantic`

## TCO Formula

Monthly TCO:

```text
monthly_tco =
  platform_subscription
  + platform_usage_calls * platform_unit_call_cost
  + hosting_or_cloud_runtime
  + model_input_output_tokens * model_provider_rate
  + storage_and_vector_index
  + social_api_rpc_data_api_fees
  + onchain_gas_and_token_fees
  + ops_hours * hourly_rate
```

Revenue simulation:

```text
monthly_revenue =
  monthly_active_users * paid_conversion_rate * subscription_price
  + marketplace_gmv * agent_token_take_rate

net_revenue =
  monthly_revenue * (1 - support_refund_rate)

net_margin_by_stack =
  net_revenue - monthly_tco_by_stack

breakeven_path =
  net_margin_by_stack >= 0 ? current revenue clears selected cost floor : reduce cost or raise conversion
```

This demo uses a normalized baseline:

| Lever | Baseline |
|---|---:|
| Workload | 10,000 agent requests / month |
| Agent count | 1 production agent |
| Runtime | Public internet reachable |
| Model provider | Excluded unless the stack bundles it or publishes a unit fee |
| Labor | Excluded from dollar totals, scored separately |
| Token setup cost | Tracked as token-denominated exposure unless public docs give a fixed USD price |
| Revenue | 2,500 monthly active users, 3% paid conversion, $19 subscription, $10,000 marketplace GMV, 0.5% agent-token take rate, 12% support/refund holdback |

## Executive Comparison

| Rank for Low TCO | Stack | Best Fit | Known Public Platform Cost | 10k Request Demo Cost | TCO Risk | Verdict |
|---:|---|---|---|---:|---|---|
| 1 | Fetch.ai / Agentverse | Hosted or local agents with clear quotas | Basic free; Premium $25/month; Enterprise custom | $0 if Basic quotas fit, otherwise $25/month before model or FET transaction costs | Quotas, FET wallet operations, paid plan upkeep | Best predictable starter TCO for hosted Web3 agents. |
| 2 | elizaOS / AI16Z | Open-source agent framework and own-infra control | Framework license $0; Eliza Cloud uses account credits; self-hosting is BYO | Public platform fee is $0 for self-host; managed cloud cost is not publicly fixed in docs | Ops burden, model API costs, cloud credits, plugin sprawl | Best FOSS/control profile, but TCO shifts to infra and operations. |
| 3 | Virtuals Protocol / GAME | Tokenized agent economy and Virtuals-native launch | GAME paid tier is $0.003/API call; launch modes add VIRTUAL-denominated setup costs | $30/month for 10k GAME calls, before token launch, gas, social/API extras | Token price volatility, launch mechanics, per-inference/on-chain economics | Strong if tokenized agent distribution matters; not the cheapest neutral demo path. |

## Dynamic Simulation Baseline

The Storyboard calculator emits these values from the frontmatter ports, so changing any driver handle updates the chart payload and decision handles.

| Stack | Computed Monthly TCO | Net Revenue Input | Simulated Net Margin | Driver Notes |
|---|---:|---:|---:|---|
| elizaOS / AI16Z | $0 | $1,298 | $1,298 | Lowest cash floor when operator-owned runtime is acceptable. |
| Fetch.ai / Agentverse | $0 on Basic, $25 if Premium is required | $1,298 | $1,298 on Basic, $1,273 on Premium | Quota state determines whether the managed cash floor is zero or Premium. |
| Virtuals / GAME | $30 | $1,298 | $1,268 | Per-call GAME cost is dynamic; token setup and gas remain separate risk handles. |

Closed journey engine baseline:

| Engine | Main Driver Ports | Computed Output Ports | Baseline Readout |
| Prediction Engine | `prediction_accuracy_rate`, `wallet_activation_rate`, `monthly_active_users`, `paid_conversion_rate` | `predicted_intent_quality_score`, `conversion_uplift_rate`, `demand_forecast_index` | Intent quality and demand forecast rise only when prediction and wallet activation both improve. |
| Yield Engine | `net_revenue_usd`, `yield_share_rate`, `predicted_intent_quality_score` | `user_value_yield_usd`, `protocol_yield_score`, `retention_value_index` | User-retained value is tied to net revenue, not token price alone. |
| Payment Engine | `payment_success_rate`, `payment_fee_rate`, `user_value_yield_usd` | `settled_payment_volume_usd`, `payment_fee_cost_usd`, `payment_value_capture_usd` | Payment value capture stays visible after fee drag. |
| Liquidity & Exchange Engine | `liquidity_spread_rate`, `exchange_conversion_rate`, `token_price_volatility` | `exchange_liquidity_depth_usd`, `liquidity_slippage_cost_usd`, `token_exchange_efficiency_score` | Liquidity health falls when spread or volatility rises. |
| Infrastructure Engine | `infrastructure_uptime_slo`, `infrastructure_unit_cost_usd`, `monthly_agent_requests` | `infrastructure_cost_usd`, `uptime_value_score`, `infra_adjusted_value_usd` | Infrastructure value depends on uptime and per-request cost discipline. |
| Closed User Journey Value Loop | all five engine outputs | `closed_loop_health_score`, `user_journey_value_loop`, `web3_economics_decision_driver` | The loop is viable only when prediction, yield, payment, liquidity, and infrastructure outputs all remain healthy. |

## Stack Details

### 1. Fetch.ai / Agentverse

Agentverse is the lowest-friction hosted comparison when the goal is a Web3 agent that can be discovered, hosted, and messaged without building a custom deployment stack.

Cost profile:

| Component | Public Signal | TCO Impact |
| Basic plan | Free tier lists 8 hosted agents, 8 local agents, 60K seconds computation time, 10K processed messages, and 5MB storage | Baseline demo can fit if one request maps to one processed message and compute remains modest. |
| Premium plan | $25/month with 25 hosted agents, 25 local agents, 500K seconds computation time, 1M processed messages, and 100MB storage | Predictable small-team plan; 12-month subscription cost is $300 before model/API/FET costs. |
| Enterprise | Custom | Use only when quotas, support, or team constraints exceed Premium. |
| Agent type | Hosted agents are managed in Agentverse; local agents run on your own infrastructure; mailbox agents bridge intermittent local availability | Lets the same agent move between lowest-cash-cost local mode and managed uptime. |
| Web3 payments | Fetch docs describe FET token transactions, Almanac registration, and agent discovery | Token operations add wallet, transaction, and governance overhead even if hosting is inexpensive. |

TCO readout:

```text
Fetch Basic baseline = $0/month platform subscription
Fetch Premium baseline = $25/month platform subscription
12-month Premium cash floor = $300
```

Best use in Knowgrph:

- Use Fetch Agentverse when the demo needs hosted uptime, marketplace discovery, and a published quota table.
- Keep model-provider calls metered separately.
- Add a budget alert when processed messages approach quota.

### 2. elizaOS / AI16Z

elizaOS is the lowest-lock-in framework comparison. It is useful when the key TCO question is "what do we own ourselves?" rather than "which platform hosts the agent for us?"

Cost profile:

| Component | Public Signal | TCO Impact |
| Framework | elizaOS docs position it as an open TypeScript framework with local, Docker, Eliza Cloud, or own-infrastructure deployment | Framework license cost is $0; real cost moves to hosting, model providers, plugins, and operations. |
| Cloud deployment | Eliza Cloud deploys with `elizaos login` and `elizaos deploy`; docs say each deployment gets a dedicated EC2 t4g.small ARM server, HTTPS, health monitoring, and logs | Managed convenience is high, but docs refer to account credits rather than publishing a simple monthly price in the deploy guide. |
| Model providers | elizaOS uses plugins for providers such as OpenAI, Anthropic, Google GenAI, OpenRouter, and local Ollama | Cost can be near zero for local dev with Ollama, or unbounded if hosted model calls loop. |
| Operations | Self-hosting means Docker, secrets, uptime, monitoring, database, memory, and plugin version management | Lower vendor lock-in, higher engineering TCO. |

TCO readout:

```text
elizaOS self-host framework cost = $0/month
elizaOS managed cloud cost = credit-based / not fixed in public deploy docs
12-month public platform cash floor = $0 + infra + model/provider usage + ops
```

Best use in Knowgrph:

- Use elizaOS when FOSS, provider neutrality, and local/browser-side experimentation matter more than managed platform convenience.
- Use local models for draft demos and budget-capped cloud models for production.
- Track each plugin as its own cost node, because social, chain, search, and model plugins can each introduce separate usage fees.

### 3. Virtuals Protocol / GAME

Virtuals is the clearest match when the agent itself is part of an on-chain creator, token, and commerce economy.

Cost profile:

| Component | Public Signal | TCO Impact |
| GAME SDK free tier | GAME docs say the SDK is free with default limits of 10 GAME requests per 5 minutes and 10 X requests per 15 minutes | Good for prototyping; not enough for sustained production load. |
| GAME paid tier | GAME docs publish $0.003 per API call for the pay-as-you-go upgrade | 10,000 calls/month = $30/month before other providers. |
| Prototype agent launch | Virtuals Genesis docs describe a 100 VIRTUAL setup cost for a prototype bonding curve and 42K VIRTUAL needed for graduation | Token-denominated setup creates market-price exposure. |
| Other launch mechanics | Virtuals launch mechanics also describe a 1,000 VIRTUAL non-refundable creation fee for founders in the launch system | Pick the correct launch path before budgeting; do not assume all Virtuals launches have one fixed setup cost. |
| Agent inference payments | Virtuals docs describe public API access, predetermined per-inference costs, and VIRTUAL-denominated wallet deductions | Runtime can become token-metered if exposing agent APIs. |

TCO readout:

```text
GAME paid baseline = 10,000 calls * $0.003 = $30/month
12-month GAME call floor = $360
Token setup exposure = 100 VIRTUAL prototype path OR 1,000 VIRTUAL launch creation path, depending on launch mode
```

Best use in Knowgrph:

- Use Virtuals when the demo needs agent-token launch, agent commerce, or VIRTUAL-native distribution.
- Avoid it for a neutral zero-TCO document demo unless tokenized launch mechanics are the subject.
- Keep launch fee, graduation threshold, gas, and per-inference payments as separate nodes so token volatility cannot be hidden inside a single "platform fee" number.

## Optional Service Benchmark: AIXBT

AIXBT is useful as a reference point for "buy access to an existing Web3 AI agent/product" rather than "build a new general-purpose agent stack."

| Access Path | Public Price Signal | Best Fit |
|---|---:|---|
| Trader subscription | $40/month | Human terminal access, alerts, reports |
| Data subscription | $100/month | API, MCP, CLI, historical snapshots, recipes |
| Pro subscription | $200/month | Chat with AIXBT, custom reports, agent API |
| x402 key pass | $10/day, $50/week, $100/4 weeks | Temporary API access paid on Base |
| Indigo agent x402 call | $2/call | Occasional agent endpoint calls without a subscription |
| Holder path | 600K AIXBT held | Token-backed access with market exposure |

This is a high-signal comparison row for buyer TCO, but it is not a direct substitute for the three build/deploy stacks above.

## Scenario Matrix

| Scenario | Fetch.ai / Agentverse | elizaOS / AI16Z | Virtuals / GAME |
| Cheapest local prototype | Good with local agents and mailbox | Best with local Docker/Ollama | Good only if staying in free GAME limits |
| Cheapest managed prototype | Best if Basic quotas fit | Unknown until cloud credits/pricing are checked | $0 SDK until limits, then $0.003/call |
| Predictable small production | Premium at $25/month plus usage | Self-host if ops are available; cloud if credits are acceptable | $30/month per 10k calls plus token/gas costs |
| Best FOSS posture | Medium | High | Medium |
| Best on-chain agent economy | Medium | Medium | High |
| Lowest token volatility exposure | Medium | High if self-hosted and no token launch | Low |
| Lowest operator burden | High | Medium on cloud, low when self-hosted | Medium |

## Recommendation For This Demo

For a Knowgrph token-economics demo, use this decision rule:

1. Use elizaOS for the FOSS/local baseline. It keeps framework cost at zero and makes model/infra costs explicit.
2. Use Fetch Agentverse as the managed-hosting baseline. Its public quota table makes TCO easy to explain.
3. Use Virtuals only when the demo needs tokenized agent launch or agent-commerce economics.
4. Treat AIXBT as a buyer-side market-data agent benchmark, not as the main build stack.

The lowest transparent TCO path is:

```text
local demo = elizaOS + local model + no token launch
managed demo = Fetch Agentverse Basic/Premium + explicit model-provider cap
tokenized demo = Virtuals GAME + separate token setup and per-call meters
```

## Source Links

- [CoinGecko AI Agents category](https://www.coingecko.com/en/categories/ai-agents)
- [CoinMarketCap AI Agents category](https://coinmarketcap.com/view/ai-agents/)
- [QuickNode Top 10 AI Agents in Web3](https://www.quicknode.com/builders-guide/best/top-10-ai-agents-in-web3)
- [Virtuals GAME SDK usage and pricing](https://docs.game.virtuals.io/game-sdk-usage-and-pricing)
- [Virtuals Genesis launch modes](https://whitepaper.virtuals.io/builders-hub/genesis-launch/modes)
- [Virtuals launch mechanics](https://whitepaper.virtuals.io/about-virtuals/tokenization/agent-tokenization-platform/virtuals-launch-mechanics)
- [Virtuals agent inference payments](https://whitepaper.virtuals.io/about-virtuals/the-protocol/virtual-agents-as-programmable-decentralized-entities/agent-inference-payments)
- [Fetch.ai concepts and Agentverse architecture](https://fetch.ai/docs/concepts)
- [Agentverse subscriptions and quotas](https://docs.agentverse.ai/documentation/advanced-usages/agentverse-subscriptions-and-quotas)
- [Fetch.ai hosted, local, mailbox, and proxy agents](https://uagents.fetch.ai/docs/guides/types)
- [elizaOS overview](https://docs.elizaos.ai)
- [elizaOS deploy to cloud](https://docs.elizaos.ai/guides/deploy-to-cloud)
- [elizaOS language model configuration](https://docs.elizaos.ai/plugin-registry/llm)
- [AIXBT subscription pricing](https://aixbt.tech/subscribe)
- [AIXBT builder access paths](https://docs.aixbt.tech/builders/getting-started)
- [AIXBT REST API access levels](https://docs.aixbt.tech/builders/rest-api)

## Validation Checklist

- The document has renderer frontmatter for Knowgrph.
- The comparison is market-source aware instead of claiming one universal ranking.
- Every hard dollar/token number is linked to a public source.
- Model-provider and ops costs are not hidden inside platform fees.
- Token-denominated costs stay token-denominated; no fixed USD conversion is embedded.
- Every widget port handle corresponds to a named cost, revenue, risk, metric, decision, or rendered-report driver.
- Widget type, side, and position do not remap a port handle; the handle id is the cost-driver key.
- Normal frontmatter-flow edges preserve driver identity with matching `sourceHandle`, `targetHandle`, and `label`.
- Matching field/port schema paths render as one editable KTV row with the functional port handle on that row; duplicate read-only rows for the same key are forbidden.
- `Revenue Drivers -> agent_token_take_rate` renders as an inline-editable output-port row, not as a separate value row plus a separate port row.
- Computing-flow propagation uses shared shared frontmatter-flow dataflow helpers so edits to driver rows recompute Rich Media Panel outputs without renderer-local recalculation or filename-specific branches.
- `socket_types` and node tags reuse the renderer palette roles exposed by the FloatingPanel Renderer settings.
- `workflow_sections` mirrors the MainPanel Workflow Manager execution path from driver ingestion through chart rendering.
- The five Web3 economics engines are first-class Storyboard widgets, not prose-only rows.
- The closed user journey value loop emits both decision drivers and a Rich Media Panel chart payload.
