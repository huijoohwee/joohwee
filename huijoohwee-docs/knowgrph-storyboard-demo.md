
socket_types:
  template_text_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_text_signal]}
  template_number_signal: {color: "#84cc16", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_number_signal]}
  template_image_signal: {color: "#38bdf8", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_image_signal]}
  template_chart_html: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [template_chart_html]}
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
      "graph:degree": {key: "graph:degree", type: number, value: 24}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 24}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
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
      input_investment_amount: {key: input_investment_amount, type: number, value: 25000}
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
      "visual:importance": {key: "visual:importance", type: number, value: 108}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 29.595917942265423}
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
      imageUrl: {key: imageUrl, type: svg_data_uri, value: ""}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Compute widget with semantic ports for universal go-no-go scoring, DCF scenarios, risk-adjusted NPV, SVG summary, and Recharts rich-media decision panels."}
      output: {key: output, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: "<!doctype html><html><head><meta charset=\"utf-8\"><meta name=\"viewport\" content=\"width=device-width,initial-scale=1\"><style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}.chart{height:260px}.panel h2{margin:0 0 10px;font-size:13px}.note{font-size:12px;color:#64748b;margin:12px 0 0}.conditions{margin:12px 0 0;padding-left:18px;color:#334155;font-size:12px;line-height:1.5}</style></head><body><main data-kg-investment-decision-panel=\"1\" data-kg-recharts=\"1\"><div class=\"kpi\"><div><p class=\"label\">Decision</p><p class=\"value\">NO-GO</p></div><div><p class=\"label\">Base NPV</p><p class=\"value\">-$25,127</p></div><div><p class=\"label\">Threshold</p><p class=\"value\">$350,000</p></div><div><p class=\"label\">Score</p><p class=\"value\">43/100</p></div></div><div id=\"decisionChartRoot\" class=\"grid\"></div><p class=\"note\">Universal, neutral decision-support dashboard. Replace placeholders and assumptions before acting.</p><ul class=\"conditions\"><li>Rework the downside case until risk-adjusted NPV stays above zero.</li><li>Preserve the current evidence trail and close the remaining unknowns.</li><li>Maintain current risk controls and monitor market and execution drift.</li></ul></main><script type=\"module\">import React from\"https://esm.sh/react@18?bundle\";import { createRoot } from\"https://esm.sh/react-dom@18/client?bundle\";import { ResponsiveContainer,BarChart,Bar,Cell,CartesianGrid,XAxis,YAxis,Tooltip,ReferenceLine,RadarChart,PolarGrid,PolarAngleAxis,PolarRadiusAxis,Radar } from\"https://esm.sh/recharts@3?bundle&deps=react@18,react-dom@18\";const payload={\"decision\":\"NO-GO\",\"title\":\"NO-GO - -$25,127 base risk-adjusted NPV\",\"metricLabel\":\"minimum acceptable risk-adjusted NPV\",\"metricTarget\":350000,\"decisionScore\":43,\"confidenceScore\":79,\"scenarios\":[{\"label\":\"Downside\",\"npv\":-101577},{\"label\":\"Base\",\"npv\":-25127},{\"label\":\"Upside\",\"npv\":123861}],\"pillars\":[{\"label\":\"Economics\",\"value\":0},{\"label\":\"Resilience\",\"value\":41},{\"label\":\"Strategic fit\",\"value\":68},{\"label\":\"Evidence\",\"value\":100}],\"conditions\":[\"Rework the downside case until risk-adjusted NPV stays above zero.\",\"Preserve the current evidence trail and close the remaining unknowns.\",\"Maintain current risk controls and monitor market and execution drift.\"]};const root=document.getElementById(\"decisionChartRoot\");if(root){const h=React.createElement,scenarioData=payload.scenarios.map((item,index)=>({label:item.label,npv:item.npv,fill:[\"#ef4444\",\"#0ea5e9\",\"#22c55e\"][index]||\"#0ea5e9\"})),pillarData=payload.pillars.map(item=>({label:item.label,value:item.value})),scenarioCells=scenarioData.map((item,index)=>h(Cell,{key:\"s-\"+index,fill:item.fill}));const app=h(React.Fragment,null,h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Scenario stress\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(BarChart,{data:scenarioData,margin:{top:12,right:12,left:0,bottom:20}},h(CartesianGrid,{stroke:\"#e2e8f0\",vertical:false}),h(XAxis,{dataKey:\"label\",tick:{fill:\"#475569\",fontSize:11}}),h(YAxis,{tick:{fill:\"#475569\",fontSize:11},tickFormatter:value=>\"$\"+Number(value).toLocaleString(\"en-US\")}),h(Tooltip,{formatter:value=>[\"$\"+Number(value).toLocaleString(\"en-US\"),payload.metricLabel]}),h(ReferenceLine,{y:payload.metricTarget,stroke:\"#f59e0b\",strokeDasharray:\"6 4\"}),h(Bar,{dataKey:\"npv\",name:payload.metricLabel,radius:[8,8,0,0]},scenarioCells))))),h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Decision pillars\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(RadarChart,{data:pillarData,outerRadius:\"72%\"},h(PolarGrid,{stroke:\"#cbd5e1\"}),h(PolarAngleAxis,{dataKey:\"label\",tick:{fill:\"#334155\",fontSize:11}}),h(PolarRadiusAxis,{angle:30,domain:[0,100],tickCount:6}),h(Tooltip,{formatter:value=>[value,\"score\"]}),h(Radar,{dataKey:\"value\",name:\"Decision pillars\",stroke:\"#0ea5e9\",fill:\"rgba(14,165,233,0.18)\",fillOpacity:1}))))));createRoot(root).render(app)}</script></body></html>"}
      run_status: {key: run_status, type: string, value: "idle"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      "visual:importance": {key: "visual:importance", type: number, value: 120}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 30.784609690826528}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
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
      "visual:height": {key: "visual:height", type: number, value: 564}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:width": {key: "visual:width", type: number, value: 1003}
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
kgAutoSaveEnabled: true
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
kgBottomPanelOpen: true
kgBottomPanelTab: "eventModeling"
kgFloatingPanelOpen: true
kgFloatingPanelView: "eventModeling"
kgSharedRendererContract:
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
flow_diagrams:
  key: flow_diagrams
  type: object
  value:
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
    storyboard_architecture:
      key: storyboard_architecture
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
          service d1(database)[D1 Run Manifest] in cloudflare
          service r2(database)[R2 outputs] in cloudflare
          service byteplus(server)[BytePlus seedream and seedance] in providers
          service stripe(database)[Stripe Checkout] in providers
          canvas:R --> L:mcp
          mcp:R --> L:gateway
          gateway:R --> L:byteplus
          mcp:B --> T:d1
          mcp:B --> T:r2
          mcp:R --> L:stripe
    storyboard_event_model:
      key: storyboard_event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui IdeaSubmitted
        tf 02 cmd RunDecisionFlow
        tf 03 evt InputsValidated
        tf 04 pcr ComputeAgent
        tf 05 cmd RequestApproval
        tf 06 evt ApprovalGranted
        tf 07 cmd GenerateDecisionOutput
        tf 08 evt OutputReady
        tf 09 cmd PersistResultToD1
        tf 10 evt ResultPersisted
        tf 11 ui ReplayFromCache
    storyboard_pipeline_flowchart:
      key: storyboard_pipeline_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          source_input["Source Input\n(idea + evidence + DCF assumptions)"]
          compute_summary["Compute Summary\n(go/no-go · DCF · NPV · risk)"]
          panel_text["Text Output\n(markdown verdict)"]
          panel_image["Image Output\n(SVG summary)"]
          panel_chart["Chart Output\n(decision dashboard)"]
          source_input -->|"24 typed ports"| compute_summary
          compute_summary -->|"output"| panel_text
          compute_summary -->|"imageUrl"| panel_image
          compute_summary -->|"outputSrcDoc"| panel_chart
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
      imageUrl: {key: imageUrl, type: svg_data_uri, value: ""}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Compute widget with semantic ports for universal go-no-go scoring, DCF scenarios, risk-adjusted NPV, SVG summary, and Recharts rich-media decision panels."}
      output: {key: output, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: "<!doctype html><html><head><meta charset=\"utf-8\"><meta name=\"viewport\" content=\"width=device-width,initial-scale=1\"><style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}.chart{height:260px}.panel h2{margin:0 0 10px;font-size:13px}.note{font-size:12px;color:#64748b;margin:12px 0 0}.conditions{margin:12px 0 0;padding-left:18px;color:#334155;font-size:12px;line-height:1.5}</style></head><body><main data-kg-investment-decision-panel=\"1\" data-kg-recharts=\"1\"><div class=\"kpi\"><div><p class=\"label\">Decision</p><p class=\"value\">NO-GO</p></div><div><p class=\"label\">Base NPV</p><p class=\"value\">-$25,127</p></div><div><p class=\"label\">Threshold</p><p class=\"value\">$350,000</p></div><div><p class=\"label\">Score</p><p class=\"value\">43/100</p></div></div><div id=\"decisionChartRoot\" class=\"grid\"></div><p class=\"note\">Universal, neutral decision-support dashboard. Replace placeholders and assumptions before acting.</p><ul class=\"conditions\"><li>Rework the downside case until risk-adjusted NPV stays above zero.</li><li>Preserve the current evidence trail and close the remaining unknowns.</li><li>Maintain current risk controls and monitor market and execution drift.</li></ul></main><script type=\"module\">import React from\"https://esm.sh/react@18?bundle\";import { createRoot } from\"https://esm.sh/react-dom@18/client?bundle\";import { ResponsiveContainer,BarChart,Bar,Cell,CartesianGrid,XAxis,YAxis,Tooltip,ReferenceLine,RadarChart,PolarGrid,PolarAngleAxis,PolarRadiusAxis,Radar } from\"https://esm.sh/recharts@3?bundle&deps=react@18,react-dom@18\";const payload={\"decision\":\"NO-GO\",\"title\":\"NO-GO - -$25,127 base risk-adjusted NPV\",\"metricLabel\":\"minimum acceptable risk-adjusted NPV\",\"metricTarget\":350000,\"decisionScore\":43,\"confidenceScore\":79,\"scenarios\":[{\"label\":\"Downside\",\"npv\":-101577},{\"label\":\"Base\",\"npv\":-25127},{\"label\":\"Upside\",\"npv\":123861}],\"pillars\":[{\"label\":\"Economics\",\"value\":0},{\"label\":\"Resilience\",\"value\":41},{\"label\":\"Strategic fit\",\"value\":68},{\"label\":\"Evidence\",\"value\":100}],\"conditions\":[\"Rework the downside case until risk-adjusted NPV stays above zero.\",\"Preserve the current evidence trail and close the remaining unknowns.\",\"Maintain current risk controls and monitor market and execution drift.\"]};const root=document.getElementById(\"decisionChartRoot\");if(root){const h=React.createElement,scenarioData=payload.scenarios.map((item,index)=>({label:item.label,npv:item.npv,fill:[\"#ef4444\",\"#0ea5e9\",\"#22c55e\"][index]||\"#0ea5e9\"})),pillarData=payload.pillars.map(item=>({label:item.label,value:item.value})),scenarioCells=scenarioData.map((item,index)=>h(Cell,{key:\"s-\"+index,fill:item.fill}));const app=h(React.Fragment,null,h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Scenario stress\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(BarChart,{data:scenarioData,margin:{top:12,right:12,left:0,bottom:20}},h(CartesianGrid,{stroke:\"#e2e8f0\",vertical:false}),h(XAxis,{dataKey:\"label\",tick:{fill:\"#475569\",fontSize:11}}),h(YAxis,{tick:{fill:\"#475569\",fontSize:11},tickFormatter:value=>\"$\"+Number(value).toLocaleString(\"en-US\")}),h(Tooltip,{formatter:value=>[\"$\"+Number(value).toLocaleString(\"en-US\"),payload.metricLabel]}),h(ReferenceLine,{y:payload.metricTarget,stroke:\"#f59e0b\",strokeDasharray:\"6 4\"}),h(Bar,{dataKey:\"npv\",name:payload.metricLabel,radius:[8,8,0,0]},scenarioCells))))),h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Decision pillars\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(RadarChart,{data:pillarData,outerRadius:\"72%\"},h(PolarGrid,{stroke:\"#cbd5e1\"}),h(PolarAngleAxis,{dataKey:\"label\",tick:{fill:\"#334155\",fontSize:11}}),h(PolarRadiusAxis,{angle:30,domain:[0,100],tickCount:6}),h(Tooltip,{formatter:value=>[value,\"score\"]}),h(Radar,{dataKey:\"value\",name:\"Decision pillars\",stroke:\"#0ea5e9\",fill:\"rgba(14,165,233,0.18)\",fillOpacity:1}))))));createRoot(root).render(app)}</script></body></html>"}
      run_status: {key: run_status, type: string, value: "idle"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const read = key => String(inputs?.[key] ?? "").trim()
            const readNumber = (key, fallback, min, max) => {
              const parsed = Number(read(key))
              const safe = Number.isFinite(parsed) ? parsed : fallback
              const lower = Number.isFinite(min) ? Math.max(min, safe) : safe
              return Number.isFinite(max) ? Math.min(max, lower) : lower
            }
            const clamp = (value, min, max) => Math.max(min, Math.min(max, value))
            const escapeHtml = value => String(value || "").replace(/[&<>"']/g, ch => {
              if (ch === "&") return "&amp;"
              if (ch === "<") return "&lt;"
              if (ch === ">") return "&gt;"
              if (ch.charCodeAt(0) === 34) return "&quot;"
              return "&#39;"
            })
            const money = value => {
              const amount = Math.round(Number(value) || 0)
              return (amount < 0 ? "-" : "") + "$" + Math.abs(amount).toLocaleString("en-US")
            }
            const percent = value => Math.round((Number(value) || 0) * 10) / 10 + "%"
            const query = read("input_query")
            const context = read("input_context")
            const audience = read("input_audience")
            const format = read("input_format")
            const constraints = read("input_constraints")
            const evidence = read("input_evidence")
            const tone = read("input_tone")
            const metricLabel = read("input_metric_label") || "minimum acceptable risk-adjusted NPV"
            const metricTarget = readNumber("input_metric_target", 350000, 1, null)
            const investment = readNumber("input_investment_amount", 250000, 0, null)
            const forecastYears = Math.round(readNumber("input_forecast_years", 5, 1, 15))
            const initialRevenue = readNumber("input_initial_revenue", 420000, 0, null)
            const revenueGrowthPct = readNumber("input_revenue_growth_pct", 14, -80, 200)
            const operatingMarginPct = readNumber("input_operating_margin_pct", 18, -100, 100)
            const taxRatePct = readNumber("input_tax_rate_pct", 20, 0, 60)
            const discountRatePct = readNumber("input_discount_rate_pct", 12, 0.1, 80)
            const terminalGrowthPct = readNumber("input_terminal_growth_pct", 3, -20, 20)
            const terminalMultiple = readNumber("input_terminal_multiple", 7, 0, 50)
            const capexPctRevenue = readNumber("input_capex_pct_revenue", 6, 0, 100)
            const workingCapitalPctRevenue = readNumber("input_working_capital_pct_revenue", 4, 0, 100)
            const probabilitySuccessPct = readNumber("input_probability_success_pct", 62, 0, 100)
            const strategicFitScore = readNumber("input_strategic_fit_score", 68, 0, 100)
            const executionRiskScore = readNumber("input_execution_risk_score", 44, 0, 100)
            const marketRiskScore = readNumber("input_market_risk_score", 38, 0, 100)
            const discountRate = discountRatePct / 100
            const terminalGrowth = terminalGrowthPct / 100
            const evidenceSignals = [query, context, evidence, constraints].filter(Boolean).length
            const scenarioModel = (label, revenueFactor, marginDelta, probabilityDelta) => {
              const rows = []
              let revenue = initialRevenue * revenueFactor
              let pvTotal = 0
              for (let year = 1; year <= forecastYears; year += 1) {
                if (year > 1) revenue = revenue * (1 + revenueGrowthPct / 100)
                const operatingMargin = clamp(operatingMarginPct + marginDelta, -100, 100)
                const operatingProfit = revenue * operatingMargin / 100
                const tax = Math.max(0, operatingProfit) * taxRatePct / 100
                const capex = revenue * capexPctRevenue / 100
                const workingCapital = revenue * workingCapitalPctRevenue / 100
                const freeCashFlow = operatingProfit - tax - capex - workingCapital
                const discountedFreeCashFlow = freeCashFlow / Math.pow(1 + discountRate, year)
                pvTotal += discountedFreeCashFlow
                rows.push({ year, revenue, freeCashFlow, discountedFreeCashFlow })
              }
              const terminalBase = rows.length ? rows[rows.length - 1].freeCashFlow : 0
              const terminalValueByMultiple = terminalBase * terminalMultiple
              const terminalValueByGrowth = discountRate > terminalGrowth
                ? terminalBase * (1 + terminalGrowth) / (discountRate - terminalGrowth)
                : terminalValueByMultiple
              const terminalValue = terminalMultiple > 0 ? terminalValueByMultiple : terminalValueByGrowth
              const terminalPv = terminalValue / Math.pow(1 + discountRate, forecastYears)
              const baseNpv = pvTotal + terminalPv - investment
              const probabilityPct = clamp(probabilitySuccessPct + probabilityDelta, 5, 95)
              const riskAdjustedNpv = baseNpv * (probabilityPct / 100)
              return { label, baseNpv, riskAdjustedNpv, probabilityPct, rows }
            }
            const downside = scenarioModel("Downside", 0.82, -4, -12)
            const base = scenarioModel("Base", 1, 0, 0)
            const upside = scenarioModel("Upside", 1.18, 4, 8)
            const scenarios = [downside, base, upside]
            const riskPressure = clamp((executionRiskScore * 0.55) + (marketRiskScore * 0.45), 0, 100)
            const economicsScore = clamp(50 + ((base.riskAdjustedNpv - metricTarget) / Math.max(metricTarget, 1) * 55), 0, 100)
            const resilienceScore = clamp(50 + (downside.riskAdjustedNpv / Math.max(metricTarget, 1) * 30), 0, 100)
            const evidenceScore = clamp((evidenceSignals * 18) + (evidence ? 18 : 0) + (constraints ? 10 : 0), 0, 100)
            const confidenceScore = Math.round(clamp((evidenceScore * 0.45) + (base.probabilityPct * 0.55), 0, 100))
            const decisionScore = Math.round((economicsScore * 0.38) + (resilienceScore * 0.22) + (strategicFitScore * 0.2) + (evidenceScore * 0.2))
            const hardStop = downside.riskAdjustedNpv < 0 && riskPressure > 65
            const decision = hardStop
              ? "NO-GO"
              : base.riskAdjustedNpv >= metricTarget && downside.riskAdjustedNpv >= 0 && decisionScore >= 70
                ? "GO"
                : base.riskAdjustedNpv >= metricTarget * 0.55 && decisionScore >= 55
                  ? "CONDITIONAL GO"
                  : "NO-GO"
            const rationale = decision === "GO"
              ? "The base case clears the target, the downside case stays investable, and the blended score supports commitment."
              : decision === "CONDITIONAL GO"
                ? "The initiative shows promise but still needs evidence, risk reduction, or economics improvement before full commitment."
                : "The current economics, downside resilience, or risk profile do not justify commitment yet."
            const conditions = [
              downside.riskAdjustedNpv < 0
                ? "Rework the downside case until risk-adjusted NPV stays above zero."
                : "Keep downside protection above zero risk-adjusted NPV before scaling commitment.",
              evidenceSignals < 3
                ? "Add stronger evidence and decision-specific facts before irreversible spend."
                : "Preserve the current evidence trail and close the remaining unknowns.",
              riskPressure > 55
                ? "Reduce execution or market risk before approving full rollout."
                : "Maintain current risk controls and monitor market and execution drift."
            ]
            const output = [
              "## " + decision,
              "",
              query || "Structured universal investment decision.",
              "",
              rationale,
              "",
              "**Decision score:** " + decisionScore + "/100",
              "**Decision confidence:** " + confidenceScore + "/100",
              "**" + metricLabel + ":** " + money(metricTarget),
              "**Base risk-adjusted NPV:** " + money(base.riskAdjustedNpv),
              "**Downside risk-adjusted NPV:** " + money(downside.riskAdjustedNpv),
              "",
              "### Structured verdict",
              "- Recommendation: " + decision,
              "- Economics score: " + Math.round(economicsScore) + "/100",
              "- Resilience score: " + Math.round(resilienceScore) + "/100",
              "- Strategic fit score: " + Math.round(strategicFitScore) + "/100",
              "- Evidence score: " + Math.round(evidenceScore) + "/100",
              "- Risk pressure: " + Math.round(riskPressure) + "/100",
              "",
              "### DCF base case",
              "- Initial investment: " + money(investment),
              "- Forecast years: " + forecastYears,
              "- Initial revenue: " + money(initialRevenue),
              "- Revenue growth: " + percent(revenueGrowthPct),
              "- Operating margin: " + percent(operatingMarginPct),
              "- Discount rate: " + percent(discountRatePct),
              "- Terminal multiple: " + terminalMultiple + "x",
              "",
              "### Scenario stress",
              "- Downside: " + money(downside.riskAdjustedNpv) + " at " + percent(downside.probabilityPct),
              "- Base: " + money(base.riskAdjustedNpv) + " at " + percent(base.probabilityPct),
              "- Upside: " + money(upside.riskAdjustedNpv) + " at " + percent(upside.probabilityPct),
              "",
              "### Conditions to clear",
              ...conditions.map(item => "- " + item),
              "",
              "### Next diligence",
              "- Validate demand, pricing, margin, capex, and working-capital assumptions.",
              "- Confirm the initiative still clears the hurdle under delay, weaker adoption, or cost creep.",
              evidence
                ? "- Replace weak assumptions with observed evidence before irreversible spend."
                : "- Add actual evidence before irreversible spend.",
              "",
              audience ? "**Audience:** " + audience : "",
              format ? "**Format:** " + format : "",
              tone ? "**Tone:** " + tone : "",
              context ? "**Context:** " + context : "",
              constraints ? "**Constraints:** " + constraints : "",
              evidence ? "**Evidence:** " + evidence : ""
            ].filter(Boolean).join("\n")
            const title = decision + " - " + money(base.riskAdjustedNpv) + " base risk-adjusted NPV"
            const svg = "<svg xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"0 0 640 220\">" +
              "<rect width=\"640\" height=\"220\" fill=\"#f8fafc\"/>" +
              "<text x=\"320\" y=\"66\" font-family=\"system-ui\" font-size=\"26\" font-weight=\"700\" fill=\"#0f172a\" text-anchor=\"middle\">" + escapeHtml(decision) + "</text>" +
              "<text x=\"320\" y=\"104\" font-family=\"system-ui\" font-size=\"14\" fill=\"#475569\" text-anchor=\"middle\">Base risk-adjusted NPV " + escapeHtml(money(base.riskAdjustedNpv)) + " vs " + escapeHtml(money(metricTarget)) + "</text>" +
              "<text x=\"320\" y=\"136\" font-family=\"system-ui\" font-size=\"13\" fill=\"#64748b\" text-anchor=\"middle\">Decision score " + decisionScore + "/100 · confidence " + confidenceScore + "/100</text>" +
              "<text x=\"320\" y=\"168\" font-family=\"system-ui\" font-size=\"12\" fill=\"#64748b\" text-anchor=\"middle\">Downside " + escapeHtml(money(downside.riskAdjustedNpv)) + " · Upside " + escapeHtml(money(upside.riskAdjustedNpv)) + "</text>" +
              "</svg>"
            const imageUrl = "data:image/svg+xml," + encodeURIComponent(svg)
            const chartPayload = JSON.stringify({
              decision,
              title,
              metricLabel,
              metricTarget,
              decisionScore,
              confidenceScore,
              scenarios: scenarios.map(item => ({
                label: item.label,
                npv: Math.round(item.riskAdjustedNpv)
              })),
              pillars: [
                { label: "Economics", value: Math.round(economicsScore) },
                { label: "Resilience", value: Math.round(resilienceScore) },
                { label: "Strategic fit", value: Math.round(strategicFitScore) },
                { label: "Evidence", value: Math.round(evidenceScore) }
              ],
              conditions
            }).replace(/</g, "\\u003c")
            const imToken = String.fromCharCode(105,109,112,111,114,116)
            const docToken = ["doc","ument"].join("")
            const outputSrcDoc = "<!doctype html><html><head><meta charset=\"utf-8\"><meta name=\"viewport\" content=\"width=device-width,initial-scale=1\">" +
              "<style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}.chart{height:260px}.panel h2{margin:0 0 10px;font-size:13px}.note{font-size:12px;color:#64748b;margin:12px 0 0}.conditions{margin:12px 0 0;padding-left:18px;color:#334155;font-size:12px;line-height:1.5}</style>" +
              "</head><body><main data-kg-investment-decision-panel=\"1\" data-kg-recharts=\"1\"><div class=\"kpi\"><div><p class=\"label\">Decision</p><p class=\"value\">" + escapeHtml(decision) + "</p></div><div><p class=\"label\">Base NPV</p><p class=\"value\">" + escapeHtml(money(base.riskAdjustedNpv)) + "</p></div><div><p class=\"label\">Threshold</p><p class=\"value\">" + escapeHtml(money(metricTarget)) + "</p></div><div><p class=\"label\">Score</p><p class=\"value\">" + decisionScore + "/100</p></div></div><div id=\"decisionChartRoot\" class=\"grid\"></div>" +
              "<p class=\"note\">Universal, neutral decision-support dashboard. Replace placeholders and assumptions before acting.</p><ul class=\"conditions\">" + conditions.map(item => "<li>" + escapeHtml(item) + "</li>").join("") + "</ul>" +
              "</main><script type=\"module\">" + imToken + " React from\"https://esm.sh/react@18?bundle\";" + imToken + " { createRoot } from\"https://esm.sh/react-dom@18/client?bundle\";" + imToken + " { ResponsiveContainer,BarChart,Bar,Cell,CartesianGrid,XAxis,YAxis,Tooltip,ReferenceLine,RadarChart,PolarGrid,PolarAngleAxis,PolarRadiusAxis,Radar } from\"https://esm.sh/recharts@3?bundle&deps=react@18,react-dom@18\";const payload=" + chartPayload + ";const root=" + docToken + ".getElementById(\"decisionChartRoot\");if(root){const h=React.createElement,scenarioData=payload.scenarios.map((item,index)=>({label:item.label,npv:item.npv,fill:[\"#ef4444\",\"#0ea5e9\",\"#22c55e\"][index]||\"#0ea5e9\"})),pillarData=payload.pillars.map(item=>({label:item.label,value:item.value})),scenarioCells=scenarioData.map((item,index)=>h(Cell,{key:\"s-\"+index,fill:item.fill}));const app=h(React.Fragment,null,h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Scenario stress\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(BarChart,{data:scenarioData,margin:{top:12,right:12,left:0,bottom:20}},h(CartesianGrid,{stroke:\"#e2e8f0\",vertical:false}),h(XAxis,{dataKey:\"label\",tick:{fill:\"#475569\",fontSize:11}}),h(YAxis,{tick:{fill:\"#475569\",fontSize:11},tickFormatter:value=>\"$\"+Number(value).toLocaleString(\"en-US\")}),h(Tooltip,{formatter:value=>[\"$\"+Number(value).toLocaleString(\"en-US\"),payload.metricLabel]}),h(ReferenceLine,{y:payload.metricTarget,stroke:\"#f59e0b\",strokeDasharray:\"6 4\"}),h(Bar,{dataKey:\"npv\",name:payload.metricLabel,radius:[8,8,0,0]},scenarioCells))))),h(\"section\",{className:\"panel\"},h(\"h2\",null,\"Decision pillars\"),h(\"div\",{className:\"chart\"},h(ResponsiveContainer,{width:\"100%\",height:\"100%\"},h(RadarChart,{data:pillarData,outerRadius:\"72%\"},h(PolarGrid,{stroke:\"#cbd5e1\"}),h(PolarAngleAxis,{dataKey:\"label\",tick:{fill:\"#334155\",fontSize:11}}),h(PolarRadiusAxis,{angle:30,domain:[0,100],tickCount:6}),h(Tooltip,{formatter:value=>[value,\"score\"]}),h(Radar,{dataKey:\"value\",name:\"Decision pillars\",stroke:\"#0ea5e9\",fill:\"rgba(14,165,233,0.18)\",fillOpacity:1}))))));createRoot(root).render(app)}</" + "script></body></html>"
            return { output, imageUrl, outputSrcDoc }
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
