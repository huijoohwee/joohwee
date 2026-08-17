---
title: "Knowgrph Universal Go No-Go Investment Decision Flow Template"
graphId: "doc:knowgrph-storyboard-widget-computing-flow-template"
doc_type: "Computing Flow Template"
date: "2026-06-08"
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
  edgeModel: "active graph edges with typed sourceHandle and targetHandle"
  timelineSurface: "TimelineTransportControls + shared bottom-panel surface"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"
socket_types:
  template_text_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_text_signal]}
  template_number_signal: {color: "#84cc16", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_number_signal]}
  template_image_signal: {color: "#38bdf8", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_image_signal]}
  template_chart_html: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [template_chart_html]}
template_flow_demo:
  schema_version: "computing-flow-template/v1"
  run_id: {key: run_id, type: string, value: "kgcf_template_run"}
  active_graph_mutated: {key: active_graph_mutated, type: boolean, value: false}
  mode: {key: mode, type: string, value: "universal-go-no-go-investment-template"}
  input_fields: {key: input_fields, type: array, value: ["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target","input_investment_amount","input_forecast_years","input_initial_revenue","input_revenue_growth_pct","input_operating_margin_pct","input_tax_rate_pct","input_discount_rate_pct","input_terminal_growth_pct","input_terminal_multiple","input_capex_pct_revenue","input_working_capital_pct_revenue","input_probability_success_pct","input_strategic_fit_score","input_execution_risk_score","input_market_risk_score"]}
  output_fields: {key: output_fields, type: array, value: ["output","imageUrl","outputSrcDoc"]}
kgVideoSequenceTimeline: true
kgVideoSequenceSources:
  - id: "clip_1907994077"
    originalName: "Seedance_2.0_is_on_Artlist-77FAnT935IE.mp4"
    relativePath: "Seedance_2.0_is_on_Artlist-77FAnT935IE.mp4"
    importMode: "url"
    sourceUrl: ""
    mimeHint: "video/mp4"
    byteSize: 3778691
    durationSeconds: 51.754666666666665
    frameRate: 24
flow_diagrams:
  key: flow_diagrams
  type: object
  value:
    video_media_timeline:
      key: "video_media_timeline"
      type: mermaid_gantt
      value: |-
        gantt
          title Video Sequence
          dateFormat HH:mm
          axisFormat %H:%M
          section Source video
          Seedance_2.0_is_on_Artlist-77FAnT935IE.mp4 : clip_1907994077, kgsrc_0_51_755, kgpos_0, 0.863m
    template_gitgraph:
      key: template_gitgraph
      type: mermaid_gitgraph
      floatingPanelView: "gitGraph"
      floatingPanelOpen: true
      bottomPanelTab: "gitGraph"
      bottomPanelOpen: true
      value: |-
        gitGraph
          commit id: "source_input" tag: "decision intake"
          branch intake_contract
          checkout intake_contract
          commit id: "input_query" tag: "initiative"
          commit id: "input_context" tag: "scope"
          commit id: "input_evidence" tag: "evidence"
          checkout main
          branch economics_contract
          checkout economics_contract
          commit id: "input_investment_amount"
          commit id: "input_initial_revenue"
          commit id: "input_revenue_growth_pct"
          commit id: "input_discount_rate_pct"
          commit id: "input_metric_target"
          checkout main
          branch decision_quality
          checkout decision_quality
          commit id: "input_constraints"
          commit id: "input_audience"
          commit id: "input_format"
          commit id: "input_tone"
          checkout main
          branch risk_contract
          checkout risk_contract
          commit id: "input_probability_success_pct"
          commit id: "input_strategic_fit_score"
          commit id: "input_execution_risk_score"
          commit id: "input_market_risk_score"
          checkout main
          merge intake_contract id: "merge_intake_contract"
          merge economics_contract id: "merge_economics_contract"
          merge decision_quality id: "merge_decision_quality"
          merge risk_contract id: "merge_risk_contract"
          commit id: "compute_summary" tag: "go no-go decision" type: HIGHLIGHT
          branch rich_media_panels
          checkout rich_media_panels
          commit id: "panel_text_output"
          commit id: "panel_image_output"
          commit id: "panel_chart_output"
          checkout main
          merge rich_media_panels id: "merge_rich_media_panels"
          commit id: "run_body_tokens" tag: "response"
    template_architecture:
      key: template_architecture
      type: mermaid_architecture
      floatingPanelView: "architecture"
      floatingPanelOpen: true
      bottomPanelTab: "architecture"
      bottomPanelOpen: true
      value: |-
        architecture-beta
          group user(cloud)[Operator]
          group cloudflare(cloud)[Cloudflare Control Plane]
          group providers(cloud)[Default provider BytePlus plus Stripe]
          service workspace(internet)[Canvas UI airvio.co knowgrph] in cloudflare
          service mcp(server)[MCP Agent Worker] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service manifest(database)[Run Manifest D1] in cloudflare
          service r2(database)[R2 image and video assets] in cloudflare
          service byteplus(server)[BytePlus seedream and seedance] in providers
          service stripe(database)[Stripe Checkout] in providers
          workspace:R --> L:mcp
          mcp:R --> L:gateway
          gateway:R --> L:byteplus
          mcp:B --> T:manifest
          mcp:B --> T:r2
          mcp:R --> L:stripe
    template_event_model:
      key: template_event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui IdeaSubmitted
        tf 02 cmd RunComputeFlow
        tf 03 evt InputsValidated
        tf 04 pcr ComputeAgent
        tf 05 cmd RequestApproval
        tf 06 evt ApprovalGranted
        tf 07 cmd GenerateOutput
        tf 08 evt OutputReady
        tf 09 cmd PersistResult
        tf 10 evt ResultPersisted
        tf 11 ui ReplayFromStorage
    template_flowchart:
      key: template_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      render_on: [flow_editor]
      value: |-
        flowchart LR
          source_input["Source Input\n(idea + evidence + DCF assumptions)"]
          compute_summary["Compute Summary\n(go/no-go · DCF · NPV · risk)"]
          approval_gate{"Approval Gate"}
          panel_text["Text Output\n(markdown verdict)"]
          panel_image["Image Output\n(SVG summary)"]
          panel_chart["Chart Output\n(Recharts dashboard)"]
          source_input -->|"24 typed ports"| compute_summary
          compute_summary -->|"output"| panel_text
          compute_summary -->|"imageUrl"| panel_image
          compute_summary -->|"outputSrcDoc"| panel_chart
          compute_summary -->|"approval gate"| approval_gate
          approval_gate -->|"GO / CONDITIONAL GO"| panel_text
          approval_gate -->|"NO-GO"| source_input
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "source_input"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "Source Input"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      handles: {key: handles, type: object, value: {"source":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target","input_investment_amount","input_forecast_years","input_initial_revenue","input_revenue_growth_pct","input_operating_margin_pct","input_tax_rate_pct","input_discount_rate_pct","input_terminal_growth_pct","input_terminal_multiple","input_capex_pct_revenue","input_working_capital_pct_revenue","input_probability_success_pct","input_strategic_fit_score","input_execution_risk_score","input_market_risk_score"]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"previewField":"input_query","previewMaxChars":80,"onEdit":{"trigger":"runDownstream","targets":["compute_summary"]},"actions":[{"id":"edit","label":"Edit","icon":"pencil","trigger":"openFieldEditor","targetField":"input_query"},{"id":"run","label":"Run","icon":"play","trigger":"runDownstream","targets":["compute_summary"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"input_query":"template_text_signal","input_context":"template_text_signal","input_audience":"template_text_signal","input_format":"template_text_signal","input_constraints":"template_text_signal","input_evidence":"template_text_signal","input_tone":"template_text_signal","input_metric_label":"template_text_signal","input_metric_target":"template_number_signal","input_investment_amount":"template_number_signal","input_forecast_years":"template_number_signal","input_initial_revenue":"template_number_signal","input_revenue_growth_pct":"template_number_signal","input_operating_margin_pct":"template_number_signal","input_tax_rate_pct":"template_number_signal","input_discount_rate_pct":"template_number_signal","input_terminal_growth_pct":"template_number_signal","input_terminal_multiple":"template_number_signal","input_capex_pct_revenue":"template_number_signal","input_working_capital_pct_revenue":"template_number_signal","input_probability_success_pct":"template_number_signal","input_strategic_fit_score":"template_number_signal","input_execution_risk_score":"template_number_signal","input_market_risk_score":"template_number_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "templateInput"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      input_audience: {key: input_audience, type: string, value: "sponsor, operator, reviewer"}
      input_capex_pct_revenue: {key: input_capex_pct_revenue, type: number, value: 6}
      input_constraints: {key: input_constraints, type: textarea, value: "Use supplied assumptions only; surface uncertainty; do not imply guaranteed returns; keep the decision neutral and auditable."}
      input_context: {key: input_context, type: textarea, value: "Use the same decision flow for any initiative where time, capital, engineering effort, or operating resources are being committed."}
      input_discount_rate_pct: {key: input_discount_rate_pct, type: number, value: 12}
      input_evidence: {key: input_evidence, type: textarea, value: "Replace with the strongest facts, unknowns, dependencies, diligence notes, operating assumptions, and file or project specific evidence."}
      input_execution_risk_score: {key: input_execution_risk_score, type: number, value: 44}
      input_forecast_years: {key: input_forecast_years, type: number, value: 5}
      input_format: {key: input_format, type: string, value: "structured markdown decision memo with scenarios"}
      input_initial_revenue: {key: input_initial_revenue, type: number, value: 420000}
      input_investment_amount: {key: input_investment_amount, type: number, value: 250000}
      input_market_risk_score: {key: input_market_risk_score, type: number, value: 38}
      input_metric_label: {key: input_metric_label, type: string, value: "minimum acceptable risk-adjusted NPV"}
      input_metric_target: {key: input_metric_target, type: number, value: 350000}
      input_operating_margin_pct: {key: input_operating_margin_pct, type: number, value: 18}
      input_probability_success_pct: {key: input_probability_success_pct, type: number, value: 62}
      input_query: {key: input_query, type: textarea, value: "Decide whether to GO, CONDITIONAL GO, or NO-GO on any project, file, workflow, asset, initiative, or capital allocation using structured economics, scenario stress, and neutral risk evidence."}
      input_revenue_growth_pct: {key: input_revenue_growth_pct, type: number, value: 14}
      input_strategic_fit_score: {key: input_strategic_fit_score, type: number, value: 68}
      input_tax_rate_pct: {key: input_tax_rate_pct, type: number, value: 20}
      input_terminal_growth_pct: {key: input_terminal_growth_pct, type: number, value: 3}
      input_terminal_multiple: {key: input_terminal_multiple, type: number, value: 7}
      input_tone: {key: input_tone, type: string, value: "direct"}
      input_working_capital_pct_revenue: {key: input_working_capital_pct_revenue, type: number, value: 4}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Reusable universal investment-decision source widget with neutral request, context, audience, constraints, evidence, DCF assumptions, and decision-quality scores."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "input"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "compute_summary"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Compute Summary Outputs"}
      position: {key: position, type: object, value: {"x":380,"y":0}}
      handles: {key: handles, type: object, value: {"target":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target","input_investment_amount","input_forecast_years","input_initial_revenue","input_revenue_growth_pct","input_operating_margin_pct","input_tax_rate_pct","input_discount_rate_pct","input_terminal_growth_pct","input_terminal_multiple","input_capex_pct_revenue","input_working_capital_pct_revenue","input_probability_success_pct","input_strategic_fit_score","input_execution_risk_score","input_market_risk_score"],"source":["output","imageUrl","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target","input_investment_amount","input_forecast_years","input_initial_revenue","input_revenue_growth_pct","input_operating_margin_pct","input_tax_rate_pct","input_discount_rate_pct","input_terminal_growth_pct","input_terminal_multiple","input_capex_pct_revenue","input_working_capital_pct_revenue","input_probability_success_pct","input_strategic_fit_score","input_execution_risk_score","input_market_risk_score"],"outputs":["output","imageUrl","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"compute_summary.output","field":"output"},{"token":"compute_summary.imageUrl","field":"imageUrl"},{"token":"compute_summary.outputSrcDoc","field":"outputSrcDoc"},{"token":"source_input.input_query","field":"input_query"},{"token":"source_input.input_context","field":"input_context"},{"token":"source_input.input_audience","field":"input_audience"},{"token":"source_input.input_format","field":"input_format"},{"token":"source_input.input_constraints","field":"input_constraints"},{"token":"source_input.input_evidence","field":"input_evidence"},{"token":"source_input.input_tone","field":"input_tone"},{"token":"source_input.input_metric_label","field":"input_metric_label"},{"token":"source_input.input_metric_target","field":"input_metric_target"},{"token":"source_input.input_investment_amount","field":"input_investment_amount"},{"token":"source_input.input_forecast_years","field":"input_forecast_years"},{"token":"source_input.input_initial_revenue","field":"input_initial_revenue"},{"token":"source_input.input_revenue_growth_pct","field":"input_revenue_growth_pct"},{"token":"source_input.input_operating_margin_pct","field":"input_operating_margin_pct"},{"token":"source_input.input_tax_rate_pct","field":"input_tax_rate_pct"},{"token":"source_input.input_discount_rate_pct","field":"input_discount_rate_pct"},{"token":"source_input.input_terminal_growth_pct","field":"input_terminal_growth_pct"},{"token":"source_input.input_terminal_multiple","field":"input_terminal_multiple"},{"token":"source_input.input_capex_pct_revenue","field":"input_capex_pct_revenue"},{"token":"source_input.input_working_capital_pct_revenue","field":"input_working_capital_pct_revenue"},{"token":"source_input.input_probability_success_pct","field":"input_probability_success_pct"},{"token":"source_input.input_strategic_fit_score","field":"input_strategic_fit_score"},{"token":"source_input.input_execution_risk_score","field":"input_execution_risk_score"},{"token":"source_input.input_market_risk_score","field":"input_market_risk_score"}],"sideEffects":[{"field":"run_status","set":"done"},{"field":"template_flow_demo.active_graph_mutated","set":true},{"field":"template_flow_demo.run_id","pattern":"kgcf_run_yyyyMMddHHmm"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"output","previewMaxChars":100,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["output","imageUrl","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"input_query":"template_text_signal","input_context":"template_text_signal","input_audience":"template_text_signal","input_format":"template_text_signal","input_constraints":"template_text_signal","input_evidence":"template_text_signal","input_tone":"template_text_signal","input_metric_label":"template_text_signal","input_metric_target":"template_number_signal","input_investment_amount":"template_number_signal","input_forecast_years":"template_number_signal","input_initial_revenue":"template_number_signal","input_revenue_growth_pct":"template_number_signal","input_operating_margin_pct":"template_number_signal","input_tax_rate_pct":"template_number_signal","input_discount_rate_pct":"template_number_signal","input_terminal_growth_pct":"template_number_signal","input_terminal_multiple":"template_number_signal","input_capex_pct_revenue":"template_number_signal","input_working_capital_pct_revenue":"template_number_signal","input_probability_success_pct":"template_number_signal","input_strategic_fit_score":"template_number_signal","input_execution_risk_score":"template_number_signal","input_market_risk_score":"template_number_signal"},"out":{"output":"template_text_signal","imageUrl":"template_image_signal","outputSrcDoc":"template_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "templateCompute"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 27}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 24}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageUrl: {key: imageUrl, type: svg_data_uri, value: "data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%20640%20220%22%3E%3Crect%20width%3D%22640%22%20height%3D%22220%22%20fill%3D%22%23f8fafc%22%2F%3E%3Ctext%20x%3D%22320%22%20y%3D%2266%22%20font-family%3D%22system-ui%22%20font-size%3D%2226%22%20font-weight%3D%22700%22%20fill%3D%22%23f59e0b%22%20text-anchor%3D%22middle%22%3ECONDITIONAL%20GO%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22104%22%20font-family%3D%22system-ui%22%20font-size%3D%2214%22%20fill%3D%22%23475569%22%20text-anchor%3D%22middle%22%3EBase%20risk-adjusted%20NPV%20-%244%2C316%20vs%20%24350%2C000%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22136%22%20font-family%3D%22system-ui%22%20font-size%3D%2213%22%20fill%3D%22%2364748b%22%20text-anchor%3D%22middle%22%3EDecision%20score%2047%2F100%20-%20confidence%2082%2F100%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22168%22%20font-family%3D%22system-ui%22%20font-size%3D%2212%22%20fill%3D%22%2364748b%22%20text-anchor%3D%22middle%22%3EDownside%20-%2491%2C845%20-%20Upside%20%24182%2C873%3C%2Ftext%3E%3C%2Fsvg%3E"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Compute widget with semantic ports for universal go-no-go scoring, DCF scenarios, risk-adjusted NPV, SVG summary, and Recharts rich-media decision panels."}
      output:
        key: output
        type: markdown
        value: |
          ## CONDITIONAL GO
          
          Decide whether to GO, CONDITIONAL GO, or NO-GO on any project, file, workflow, asset, initiative, or capital allocation using structured economics, scenario stress, and neutral risk evidence.
          
          **Decision score:** 47/100
          **Decision confidence:** 82/100
          **minimum acceptable risk-adjusted NPV:** $350,000
          **Base risk-adjusted NPV:** -$4,316
          **Downside risk-adjusted NPV:** -$91,845
          
          ### Structured verdict
          - Recommendation: CONDITIONAL GO
          - Economics score: 0/100
          - Resilience score: 63/100
          - Strategic fit score: 68/100
          - Evidence score: 100/100
          - Risk pressure: 41/100
          
          ### DCF base case
          - Initial investment: $250,000
          - Forecast years: 5
          - Initial revenue: $420,000
          - Revenue growth: 14%
          - Operating margin: 18%
          - Discount rate: 12%
          - Terminal multiple: 7x
          
          ### Scenario stress
          - Downside: -$91,845 at 37%
          - Base: -$4,316 at 62%
          - Upside: $182,873 at 71%
          
          ### Conditions to clear
          - Rework the downside case until risk-adjusted NPV clears the minimum acceptable risk-adjusted NPV threshold.
          
          ### Next diligence
          - Validate demand, pricing, margin, capex, and working-capital assumptions.
          - Confirm the initiative clears the hurdle under delay, weaker adoption, or cost creep.
          - Replace weak assumptions with observed evidence before irreversible spend.
          
          **Audience:** sponsor, operator, reviewer
          **Format:** structured markdown decision memo with scenarios
          **Tone:** direct
          **Context:** Use the same decision flow for any initiative where time, capital, engineering effort, or operating resources are being committed.
          **Constraints:** Use supplied assumptions only; surface uncertainty; do not imply guaranteed returns; keep the decision neutral and auditable.
          **Evidence:** Replace with the strongest facts, unknowns, dependencies, diligence notes, operating assumptions, and file or project specific evidence.
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: "<!doctype html><html><head><meta charset=\"utf-8\"><meta name=\"viewport\" content=\"width=device-width,initial-scale=1\"><style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.panel{margin-bottom:12px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.panel h2{margin:0 0 10px;font-size:13px}.row{display:flex;align-items:center;gap:8px;margin:6px 0;font-size:12px}.rl{width:90px;color:#475569}.rt{flex:1;height:14px;background:#e2e8f0;border-radius:7px;overflow:hidden}.rb{display:block;height:100%;border-radius:7px}.rv{width:96px;text-align:right;color:#0f172a;font-weight:600}.note{font-size:12px;color:#64748b;margin:12px 0 0}.conditions{margin:8px 0 0;padding-left:18px;color:#334155;font-size:12px;line-height:1.5}</style></head><body><main data-kg-investment-decision-panel=\"1\"><div class=\"kpi\"><div><p class=\"label\">Decision</p><p class=\"value\">CONDITIONAL GO</p></div><div><p class=\"label\">Base NPV</p><p class=\"value\">-$4,316</p></div><div><p class=\"label\">Threshold</p><p class=\"value\">$350,000</p></div><div><p class=\"label\">Score</p><p class=\"value\">47/100</p></div></div><section class=\"panel\"><h2>Scenario stress (risk-adjusted NPV)</h2><div class=\"row\"><span class=\"rl\">Downside</span><span class=\"rt\"><span class=\"rb\" style=\"width:50%;background:#ef4444\"></span></span><span class=\"rv\">-$91,845</span></div><div class=\"row\"><span class=\"rl\">Base</span><span class=\"rt\"><span class=\"rb\" style=\"width:2%;background:#0ea5e9\"></span></span><span class=\"rv\">-$4,316</span></div><div class=\"row\"><span class=\"rl\">Upside</span><span class=\"rt\"><span class=\"rb\" style=\"width:100%;background:#22c55e\"></span></span><span class=\"rv\">$182,873</span></div></section><section class=\"panel\"><h2>Decision pillars</h2><div class=\"row\"><span class=\"rl\">Economics</span><span class=\"rt\"><span class=\"rb\" style=\"width:0%;background:#0ea5e9\"></span></span><span class=\"rv\">0/100</span></div><div class=\"row\"><span class=\"rl\">Resilience</span><span class=\"rt\"><span class=\"rb\" style=\"width:63%;background:#0ea5e9\"></span></span><span class=\"rv\">63/100</span></div><div class=\"row\"><span class=\"rl\">Strategic fit</span><span class=\"rt\"><span class=\"rb\" style=\"width:68%;background:#0ea5e9\"></span></span><span class=\"rv\">68/100</span></div><div class=\"row\"><span class=\"rl\">Evidence</span><span class=\"rt\"><span class=\"rb\" style=\"width:100%;background:#0ea5e9\"></span></span><span class=\"rv\">100/100</span></div></section><p class=\"note\">Universal, neutral decision-support dashboard. Current raw target: 350000 target. Replace placeholders and assumptions before acting.</p><ul class=\"conditions\"><li>Rework the downside case until risk-adjusted NPV clears the minimum acceptable risk-adjusted NPV threshold.</li></ul></main></body></html>"}
      run_status: {key: run_status, type: string, value: "idle"}
      semanticKey: {key: semanticKey, type: string, value: "computing-flow:compute:decision-summary"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      "visual:importance": {key: "visual:importance", type: number, value: 120}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 30.784609690826528}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
          const rn = (k,d) => { const v = Number(inputs && inputs[k]); return Number.isFinite(v) ? v : d; };
          const rs = (k,d) => { const v = String((inputs && inputs[k]) || '').trim(); return v || d; };
          const inv = rn('input_investment_amount', 250000);
          const yrs = Math.max(1, Math.min(20, rn('input_forecast_years', 5)));
          const rev0 = rn('input_initial_revenue', 420000);
          const g = rn('input_revenue_growth_pct', 14) / 100;
          const om = rn('input_operating_margin_pct', 18) / 100;
          const tx = rn('input_tax_rate_pct', 20) / 100;
          const dr = rn('input_discount_rate_pct', 12) / 100;
          const tg = rn('input_terminal_growth_pct', 3) / 100;
          const tm = rn('input_terminal_multiple', 7);
          const cx = rn('input_capex_pct_revenue', 6) / 100;
          const wc = rn('input_working_capital_pct_revenue', 4) / 100;
          const ps = rn('input_probability_success_pct', 62) / 100;
          const sf = rn('input_strategic_fit_score', 68);
          const er = rn('input_execution_risk_score', 44);
          const mr = rn('input_market_risk_score', 38);
          const mt = rn('input_metric_target', 35);
          const ml = rs('input_metric_label', 'minimum acceptable risk-adjusted NPV');
          const query = rs('input_query', '');
          const cxt = rs('input_context', '');
          const audience = rs('input_audience', '');
          const fmt = rs('input_format', '');
          const constraints = rs('input_constraints', '');
          const evidence = rs('input_evidence', '');
          const tone = rs('input_tone', '');
          const dcf = (gm, omm, dro) => {
          let pv = 0; let revY = rev0;
          for (let y = 1; y <= yrs; y++) {
          revY *= (1 + g * gm);
          const fcf = revY * (om * omm) * (1 - tx) - revY * cx - revY * wc;
          pv += fcf / Math.pow(1 + dr + dro, y);
          }
          const termRev = revY * (1 + tg);
          const termFcf = termRev * (om * omm) * (1 - tx) - termRev * cx - termRev * wc;
          const tv = tm > 0 ? termFcf * tm : termFcf / Math.max(0.001, dr + dro - tg);
          return Math.round(pv + tv / Math.pow(1 + dr + dro, yrs) - inv);
          };
          const npvBase = dcf(1, 1, 0);
          const npvDown = dcf(0.6, 0.7, 0.04);
          const npvUp = dcf(1.3, 1.2, -0.02);
          const raBase = Math.round(npvBase * ps);
          const raDown = Math.round(npvDown * (ps * 0.6));
          const raUp = Math.round(npvUp * Math.min(0.99, ps * 1.15));
          const thr = mt;
          const econ = raBase >= thr ? 100 : raBase >= 0 ? Math.round((raBase / thr) * 60 + 20) : 0;
          const resil = raDown >= 0 ? 100 : Math.max(0, Math.round(100 + (raDown / (inv || 1)) * 100));
          const riskP = Math.round((er + mr) / 2);
          const evid = evidence.length > 40 ? 100 : evidence.length > 10 ? 60 : evidence.length > 0 ? 30 : 0;
          const dec = Math.round(econ * 0.35 + resil * 0.15 + sf * 0.2 + evid * 0.15 + (100 - riskP) * 0.15);
          const conf = Math.min(100, Math.round(50 + ps * 30 + Math.min(20, evidence.length / 10)));
          const verdict = dec >= 70 && raBase >= thr ? 'GO' : dec >= 45 && raBase >= -thr * 0.5 ? 'CONDITIONAL GO' : 'NO-GO';
          const money = (n) => { const s = '$' + Math.round(Math.abs(n)).toLocaleString('en-US'); return n < 0 ? '-' + s : s; };
          const esc = (v) => String(v || '').replace(/[&<>"']/g, c => c === '&' ? '&amp;' : c === '<' ? '&lt;' : c === '>' ? '&gt;' : c === '"' ? '&quot;' : '&#39;');
          const cond = [];
          if (raBase < thr) cond.push('Rework the downside case until risk-adjusted NPV clears the ' + ml + ' threshold.');
          if (resil < 50) cond.push('Stress-test the downside scenario; base resilience is below the acceptable floor.');
          if (evid < 60) cond.push('Strengthen the evidence base before committing irreversible spend.');
          if (riskP > 55) cond.push('Reduce execution and market risk exposure before proceeding.');
          if (cond.length === 0) cond.push('Maintain current risk controls and monitor market and execution drift.');
          const pillars = [['Economics', econ], ['Resilience', resil], ['Strategic fit', sf], ['Evidence', evid]];
          const scen = [['Downside', raDown, '#ef4444'], ['Base', raBase, '#0ea5e9'], ['Upside', raUp, '#22c55e']];
          const lines = ['## ' + verdict, '', query, '', '**Decision score:** ' + dec + '/100', '**Decision confidence:** ' + conf + '/100', '**' + ml + ':** ' + money(thr), '**Base risk-adjusted NPV:** ' + money(raBase), '**Downside risk-adjusted NPV:** ' + money(raDown), '', '### Structured verdict', '- Recommendation: ' + verdict, '- Economics score: ' + econ + '/100', '- Resilience score: ' + resil + '/100', '- Strategic fit score: ' + sf + '/100', '- Evidence score: ' + evid + '/100', '- Risk pressure: ' + riskP + '/100', '', '### DCF base case', '- Initial investment: ' + money(inv), '- Forecast years: ' + yrs, '- Initial revenue: ' + money(rev0), '- Revenue growth: ' + Math.round(g * 100) + '%', '- Operating margin: ' + Math.round(om * 100) + '%', '- Discount rate: ' + Math.round(dr * 100) + '%', '- Terminal multiple: ' + tm + 'x', '', '### Scenario stress', '- Downside: ' + money(raDown) + ' at ' + Math.round(ps * 60) + '%', '- Base: ' + money(raBase) + ' at ' + Math.round(ps * 100) + '%', '- Upside: ' + money(raUp) + ' at ' + Math.round(Math.min(99, ps * 115)) + '%', '', '### Conditions to clear'];
          for (let i = 0; i < cond.length; i++) lines.push('- ' + cond[i]);
          lines.push('', '### Next diligence', '- Validate demand, pricing, margin, capex, and working-capital assumptions.', '- Confirm the initiative clears the hurdle under delay, weaker adoption, or cost creep.', '- Replace weak assumptions with observed evidence before irreversible spend.', '', '**Audience:** ' + audience, '**Format:** ' + fmt, '**Tone:** ' + tone);
          if (cxt) lines.push('**Context:** ' + cxt);
          if (constraints) lines.push('**Constraints:** ' + constraints);
          if (evidence) lines.push('**Evidence:** ' + evidence);
          const output = lines.join('\n');
          const vc = verdict === 'GO' ? '#22c55e' : verdict === 'CONDITIONAL GO' ? '#f59e0b' : '#ef4444';
          const svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 220"><rect width="640" height="220" fill="#f8fafc"/><text x="320" y="66" font-family="system-ui" font-size="26" font-weight="700" fill="' + vc + '" text-anchor="middle">' + esc(verdict) + '</text><text x="320" y="104" font-family="system-ui" font-size="14" fill="#475569" text-anchor="middle">Base risk-adjusted NPV ' + esc(money(raBase)) + ' vs ' + esc(money(thr)) + '</text><text x="320" y="136" font-family="system-ui" font-size="13" fill="#64748b" text-anchor="middle">Decision score ' + dec + '/100 - confidence ' + conf + '/100</text><text x="320" y="168" font-family="system-ui" font-size="12" fill="#64748b" text-anchor="middle">Downside ' + esc(money(raDown)) + ' - Upside ' + esc(money(raUp)) + '</text></svg>';
          const imageUrl = 'data:image/svg+xml,' + encodeURIComponent(svg);
          const maxAbs = Math.max(1, Math.abs(raDown), Math.abs(raBase), Math.abs(raUp));
          let bars = '';
          for (let i = 0; i < scen.length; i++) { const w = Math.round((Math.abs(scen[i][1]) / maxAbs) * 100); bars += '<div class="row"><span class="rl">' + esc(scen[i][0]) + '</span><span class="rt"><span class="rb" style="width:' + w + '%;background:' + scen[i][2] + '"></span></span><span class="rv">' + esc(money(scen[i][1])) + '</span></div>'; }
          let pbar = '';
          for (let i = 0; i < pillars.length; i++) { const w = Math.max(0, Math.min(100, pillars[i][1])); pbar += '<div class="row"><span class="rl">' + esc(pillars[i][0]) + '</span><span class="rt"><span class="rb" style="width:' + w + '%;background:#0ea5e9"></span></span><span class="rv">' + pillars[i][1] + '/100</span></div>'; }
          let cli = '';
          for (let i = 0; i < cond.length; i++) cli += '<li>' + esc(cond[i]) + '</li>';
          const css = 'body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.panel{margin-bottom:12px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.panel h2{margin:0 0 10px;font-size:13px}.row{display:flex;align-items:center;gap:8px;margin:6px 0;font-size:12px}.rl{width:90px;color:#475569}.rt{flex:1;height:14px;background:#e2e8f0;border-radius:7px;overflow:hidden}.rb{display:block;height:100%;border-radius:7px}.rv{width:96px;text-align:right;color:#0f172a;font-weight:600}.note{font-size:12px;color:#64748b;margin:12px 0 0}.conditions{margin:8px 0 0;padding-left:18px;color:#334155;font-size:12px;line-height:1.5}';
          const outputSrcDoc = '<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><style>' + css + '</style></head><body><main data-kg-investment-decision-panel="1"><div class="kpi"><div><p class="label">Decision</p><p class="value">' + esc(verdict) + '</p></div><div><p class="label">Base NPV</p><p class="value">' + esc(money(raBase)) + '</p></div><div><p class="label">Threshold</p><p class="value">' + esc(money(thr)) + '</p></div><div><p class="label">Score</p><p class="value">' + dec + '/100</p></div></div><section class="panel"><h2>Scenario stress (risk-adjusted NPV)</h2>' + bars + '</section><section class="panel"><h2>Decision pillars</h2>' + pbar + '</section><p class="note">Universal, neutral decision-support dashboard. Current raw target: ' + mt + ' target. Replace placeholders and assumptions before acting.</p><ul class="conditions">' + cli + '</ul></main></body></html>';
          return { output: output, imageUrl: imageUrl, outputSrcDoc: outputSrcDoc };
          }
    - id: {key: id, type: string, value: "panel_text_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Text Output"}
      position: {key: position, type: object, value: {"x":760,"y":240}}
      handles: {key: handles, type: object, value: {"target":["output"],"source":["output"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"output":"template_text_signal"},"out":{"output":"template_text_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Text Rich Media Panel receives the output field."}
      output: {key: output, type: textarea, value: ""}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "panel_image_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Image Output"}
      position: {key: position, type: object, value: {"x":760,"y":0}}
      handles: {key: handles, type: object, value: {"target":["imageUrl"],"source":["imageUrl"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"imageUrl":"template_image_signal"},"out":{"imageUrl":"template_image_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageUrl: {key: imageUrl, type: text, value: ""}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Image Rich Media Panel receives the imageUrl field."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "panel_chart_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Chart Output"}
      position: {key: position, type: object, value: {"x":760,"y":-240}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"template_chart_html"},"out":{"outputSrcDoc":"template_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Chart Rich Media Panel receives the outputSrcDoc field."}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: ""}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
  edges:
    - {"id":"edge_input_query_to_compute","source":"source_input","sourceHandle":"input_query","target":"compute_summary","targetHandle":"input_query","label":"input_query","type":"template_text_signal"}
    - {"id":"edge_input_context_to_compute","source":"source_input","sourceHandle":"input_context","target":"compute_summary","targetHandle":"input_context","label":"input_context","type":"template_text_signal"}
    - {"id":"edge_input_audience_to_compute","source":"source_input","sourceHandle":"input_audience","target":"compute_summary","targetHandle":"input_audience","label":"input_audience","type":"template_text_signal"}
    - {"id":"edge_input_format_to_compute","source":"source_input","sourceHandle":"input_format","target":"compute_summary","targetHandle":"input_format","label":"input_format","type":"template_text_signal"}
    - {"id":"edge_input_constraints_to_compute","source":"source_input","sourceHandle":"input_constraints","target":"compute_summary","targetHandle":"input_constraints","label":"input_constraints","type":"template_text_signal"}
    - {"id":"edge_input_evidence_to_compute","source":"source_input","sourceHandle":"input_evidence","target":"compute_summary","targetHandle":"input_evidence","label":"input_evidence","type":"template_text_signal"}
    - {"id":"edge_input_tone_to_compute","source":"source_input","sourceHandle":"input_tone","target":"compute_summary","targetHandle":"input_tone","label":"input_tone","type":"template_text_signal"}
    - {"id":"edge_input_metric_label_to_compute","source":"source_input","sourceHandle":"input_metric_label","target":"compute_summary","targetHandle":"input_metric_label","label":"input_metric_label","type":"template_text_signal"}
    - {"id":"edge_input_metric_target_to_compute","source":"source_input","sourceHandle":"input_metric_target","target":"compute_summary","targetHandle":"input_metric_target","label":"input_metric_target","type":"template_number_signal"}
    - {"id":"edge_input_investment_amount_to_compute","source":"source_input","sourceHandle":"input_investment_amount","target":"compute_summary","targetHandle":"input_investment_amount","label":"input_investment_amount","type":"template_number_signal"}
    - {"id":"edge_input_forecast_years_to_compute","source":"source_input","sourceHandle":"input_forecast_years","target":"compute_summary","targetHandle":"input_forecast_years","label":"input_forecast_years","type":"template_number_signal"}
    - {"id":"edge_input_initial_revenue_to_compute","source":"source_input","sourceHandle":"input_initial_revenue","target":"compute_summary","targetHandle":"input_initial_revenue","label":"input_initial_revenue","type":"template_number_signal"}
    - {"id":"edge_input_revenue_growth_pct_to_compute","source":"source_input","sourceHandle":"input_revenue_growth_pct","target":"compute_summary","targetHandle":"input_revenue_growth_pct","label":"input_revenue_growth_pct","type":"template_number_signal"}
    - {"id":"edge_input_operating_margin_pct_to_compute","source":"source_input","sourceHandle":"input_operating_margin_pct","target":"compute_summary","targetHandle":"input_operating_margin_pct","label":"input_operating_margin_pct","type":"template_number_signal"}
    - {"id":"edge_input_tax_rate_pct_to_compute","source":"source_input","sourceHandle":"input_tax_rate_pct","target":"compute_summary","targetHandle":"input_tax_rate_pct","label":"input_tax_rate_pct","type":"template_number_signal"}
    - {"id":"edge_input_discount_rate_pct_to_compute","source":"source_input","sourceHandle":"input_discount_rate_pct","target":"compute_summary","targetHandle":"input_discount_rate_pct","label":"input_discount_rate_pct","type":"template_number_signal"}
    - {"id":"edge_input_terminal_growth_pct_to_compute","source":"source_input","sourceHandle":"input_terminal_growth_pct","target":"compute_summary","targetHandle":"input_terminal_growth_pct","label":"input_terminal_growth_pct","type":"template_number_signal"}
    - {"id":"edge_input_terminal_multiple_to_compute","source":"source_input","sourceHandle":"input_terminal_multiple","target":"compute_summary","targetHandle":"input_terminal_multiple","label":"input_terminal_multiple","type":"template_number_signal"}
    - {"id":"edge_input_capex_pct_revenue_to_compute","source":"source_input","sourceHandle":"input_capex_pct_revenue","target":"compute_summary","targetHandle":"input_capex_pct_revenue","label":"input_capex_pct_revenue","type":"template_number_signal"}
    - {"id":"edge_input_working_capital_pct_revenue_to_compute","source":"source_input","sourceHandle":"input_working_capital_pct_revenue","target":"compute_summary","targetHandle":"input_working_capital_pct_revenue","label":"input_working_capital_pct_revenue","type":"template_number_signal"}
    - {"id":"edge_input_probability_success_pct_to_compute","source":"source_input","sourceHandle":"input_probability_success_pct","target":"compute_summary","targetHandle":"input_probability_success_pct","label":"input_probability_success_pct","type":"template_number_signal"}
    - {"id":"edge_input_strategic_fit_score_to_compute","source":"source_input","sourceHandle":"input_strategic_fit_score","target":"compute_summary","targetHandle":"input_strategic_fit_score","label":"input_strategic_fit_score","type":"template_number_signal"}
    - {"id":"edge_input_execution_risk_score_to_compute","source":"source_input","sourceHandle":"input_execution_risk_score","target":"compute_summary","targetHandle":"input_execution_risk_score","label":"input_execution_risk_score","type":"template_number_signal"}
    - {"id":"edge_input_market_risk_score_to_compute","source":"source_input","sourceHandle":"input_market_risk_score","target":"compute_summary","targetHandle":"input_market_risk_score","label":"input_market_risk_score","type":"template_number_signal"}
    - {"id":"edge_compute_to_text_panel","source":"compute_summary","sourceHandle":"output","target":"panel_text_output","targetHandle":"output","label":"text output","type":"template_text_signal"}
    - {"id":"edge_compute_to_image_panel","source":"compute_summary","sourceHandle":"imageUrl","target":"panel_image_output","targetHandle":"imageUrl","label":"image output","type":"template_image_signal"}
    - {"id":"edge_compute_to_chart_panel","source":"compute_summary","sourceHandle":"outputSrcDoc","target":"panel_chart_output","targetHandle":"outputSrcDoc","label":"chart output","type":"template_chart_html"}
---
## Response

{{compute_summary.output}}

## Inputs

- Query: {{source_input.input_query}}
- Context: {{source_input.input_context}}
- Audience: {{source_input.input_audience}}
- Format: {{source_input.input_format}}
- Constraints: {{source_input.input_constraints}}
- Evidence: {{source_input.input_evidence}}
- Tone: {{source_input.input_tone}}
- Metric label: {{source_input.input_metric_label}}
- Metric target: {{source_input.input_metric_target}}
- Investment amount: {{source_input.input_investment_amount}}
- Forecast years: {{source_input.input_forecast_years}}
- Initial revenue: {{source_input.input_initial_revenue}}
- Revenue growth %: {{source_input.input_revenue_growth_pct}}
- Operating margin %: {{source_input.input_operating_margin_pct}}
- Tax rate %: {{source_input.input_tax_rate_pct}}
- Discount rate %: {{source_input.input_discount_rate_pct}}
- Terminal growth %: {{source_input.input_terminal_growth_pct}}
- Terminal multiple: {{source_input.input_terminal_multiple}}
- Capex % revenue: {{source_input.input_capex_pct_revenue}}
- Working capital % revenue: {{source_input.input_working_capital_pct_revenue}}
- Probability success %: {{source_input.input_probability_success_pct}}
- Strategic fit score: {{source_input.input_strategic_fit_score}}
- Execution risk score: {{source_input.input_execution_risk_score}}
- Market risk score: {{source_input.input_market_risk_score}}
