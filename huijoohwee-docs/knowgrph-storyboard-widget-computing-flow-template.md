---
title: "Universal Go No-Go Investment Decision Flow Template Computing Flow"
graphId: "md:knowgrph-storyboard-widget-computing-flow-template-computing-flow"
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
socket_types:
  template_text_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_text_signal]}
  template_number_signal: {color: "#84cc16", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_number_signal]}
  template_image_signal: {color: "#38bdf8", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [template_image_signal]}
  template_chart_html: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [template_chart_html]}
template_flow_demo:
  schema_version: "computing-flow-template/v1"
  run_id: {key: run_id, type: string, value: "kgcf_template_run"}
  active_graph_mutated: {key: active_graph_mutated, type: boolean, value: false}
  mode: {key: mode, type: string, value: "local-template"}
  input_fields: {key: input_fields, type: array, value: ["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target"]}
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
          commit id: "source_input" tag: "KTV inputs"
          branch request_contract
          checkout request_contract
          commit id: "input_query"
          commit id: "input_context"
          commit id: "input_evidence"
          checkout main
          branch presentation_contract
          checkout presentation_contract
          commit id: "input_audience"
          commit id: "input_format"
          commit id: "input_tone"
          checkout main
          branch guardrail_contract
          checkout guardrail_contract
          commit id: "input_constraints"
          checkout main
          branch metric_contract
          checkout metric_contract
          commit id: "input_metric_label"
          commit id: "input_metric_target"
          checkout main
          merge request_contract id: "merge_request_contract"
          merge presentation_contract id: "merge_presentation_contract"
          merge guardrail_contract id: "merge_guardrail_contract"
          merge metric_contract id: "merge_metric_contract"
          commit id: "compute_summary" tag: "compute" type: HIGHLIGHT
          branch rich_media_panels
          checkout rich_media_panels
          commit id: "panel_text_output"
          commit id: "panel_image_output"
          commit id: "panel_chart_output"
          checkout main
          merge rich_media_panels id: "merge_rich_media_panels"
          commit id: "run_body_tokens" tag: "response"
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
      handles: {key: handles, type: object, value: {"source":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target"]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"previewField":"input_query","previewMaxChars":80,"onEdit":{"trigger":"runDownstream","targets":["compute_summary"]},"actions":[{"id":"edit","label":"Edit","icon":"pencil","trigger":"openFieldEditor","targetField":"input_query"},{"id":"run","label":"Run","icon":"play","trigger":"runDownstream","targets":["compute_summary"]}]}}
      evidenceKind: {key: evidenceKind, type: string, value: "user-edit"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"input_query":"template_text_signal","input_context":"template_text_signal","input_audience":"template_text_signal","input_format":"template_text_signal","input_constraints":"template_text_signal","input_evidence":"template_text_signal","input_tone":"template_text_signal","input_metric_label":"template_text_signal","input_metric_target":"template_number_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "templateInput"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 9}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 9}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      input_audience: {key: input_audience, type: string, value: "research reviewer, creators"}
      input_constraints: {key: input_constraints, type: textarea, value: "State uncertainty; avoid unsupported claims; keep the answer MECE."}
      input_context: {key: input_context, type: textarea, value: "Use only supplied source text or connected upstream output."}
      input_evidence: {key: input_evidence, type: textarea, value: ""}
      input_format: {key: input_format, type: string, value: "concise markdown response"}
      input_metric_label: {key: input_metric_label, type: string, value: "words"}
      input_metric_target: {key: input_metric_target, type: number, value: 500}
      input_query: {key: input_query, type: textarea, value: "Universal Go No-Go Investment Decision Flow Template"}
      input_tone: {key: input_tone, type: string, value: "direct"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Reusable source widget with granular query, context, audience, format, constraints, evidence, tone, metric label, and metric target inputs."}
      strybldrCamera: {key: strybldrCamera, type: object, value: {"angle":"right-side","level":"low-angle","shot":"medium","note":"","orbitX":0.25,"orbitY":0.5}}
      strybldrUserApprovedAtMs: {key: strybldrUserApprovedAtMs, type: number, value: 1781443336372}
      "template:nodeType": {key: "template:nodeType", type: string, value: "input"}
      "visual:importance": {key: "visual:importance", type: number, value: 48}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 22}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "compute_summary"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Compute Summary Outputs"}
      position: {key: position, type: object, value: {"x":380,"y":0}}
      handles: {key: handles, type: object, value: {"target":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target"],"source":["output","imageUrl","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["input_query","input_context","input_audience","input_format","input_constraints","input_evidence","input_tone","input_metric_label","input_metric_target"],"outputs":["output","imageUrl","outputSrcDoc"],"updateBody":true,"bodyTokens":[{"token":"compute_summary.output","field":"output"},{"token":"compute_summary.imageUrl","field":"imageUrl"},{"token":"compute_summary.outputSrcDoc","field":"outputSrcDoc"},{"token":"source_input.input_query","field":"input_query"},{"token":"source_input.input_context","field":"input_context"},{"token":"source_input.input_audience","field":"input_audience"},{"token":"source_input.input_format","field":"input_format"},{"token":"source_input.input_constraints","field":"input_constraints"},{"token":"source_input.input_evidence","field":"input_evidence"},{"token":"source_input.input_tone","field":"input_tone"},{"token":"source_input.input_metric_label","field":"input_metric_label"},{"token":"source_input.input_metric_target","field":"input_metric_target"}],"sideEffects":[{"field":"run_status","set":"done"},{"field":"template_flow_demo.active_graph_mutated","set":true},{"field":"template_flow_demo.run_id","pattern":"kgcf_run_yyyyMMddHHmm"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"output","previewMaxChars":100,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["output","imageUrl","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"input_query":"template_text_signal","input_context":"template_text_signal","input_audience":"template_text_signal","input_format":"template_text_signal","input_constraints":"template_text_signal","input_evidence":"template_text_signal","input_tone":"template_text_signal","input_metric_label":"template_text_signal","input_metric_target":"template_number_signal"},"out":{"output":"template_text_signal","imageUrl":"template_image_signal","outputSrcDoc":"template_chart_html"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "templateCompute"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 12}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 9}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageUrl: {key: imageUrl, type: svg_data_uri, value: ""}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Compute widget with semantic ports for granular inputs and text, image, and outputSrcDoc outputs."}
      output: {key: output, type: markdown, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: ""}
      run_status: {key: run_status, type: string, value: "idle"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      "visual:importance": {key: "visual:importance", type: number, value: 60}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 23.856406460551018}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
            const read = key => String(inputs?.[key] || "").trim()
            const query = read("input_query")
            const context = read("input_context")
            const audience = read("input_audience")
            const format = read("input_format")
            const constraints = read("input_constraints")
            const evidence = read("input_evidence")
            const tone = read("input_tone")
            const metricLabel = read("input_metric_label") || "items"
            const metricTargetRaw = Number(read("input_metric_target"))
            const metricTarget = Number.isFinite(metricTargetRaw) && metricTargetRaw > 0 ? metricTargetRaw : 1
            const raw = [query, context, evidence].filter(Boolean).join("\n\n")
            if (!raw) return { output: "", imageUrl: "", outputSrcDoc: "" }
            const count = metricLabel.toLowerCase().includes("word")
              ? raw.split(/\s+/).filter(Boolean).length
              : raw.length
            const pct = Math.max(0, Math.min(100, Math.round((count / metricTarget) * 100)))
            const preview = raw.slice(0, 240)
            const escapeHtml = value => String(value || "").replace(/[&<>"']/g, ch => {
              if (ch === "&") return "&amp;"
              if (ch === "<") return "&lt;"
              if (ch === ">") return "&gt;"
              if (ch.charCodeAt(0) === 34) return "&quot;"
              return "&#39;"
            })
            const parts = [
              preview,
              audience ? "**Audience:** " + audience : "",
              format ? "**Format:** " + format : "",
              constraints ? "**Constraints:** " + constraints : "",
              tone ? "**Tone:** " + tone : ""
            ].filter(Boolean)
            const output = parts.join("\n\n")
            const title = (query || context || evidence || "Output").slice(0, 96)
            const svg = "<svg xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"0 0 640 200\">" +
              "<rect width=\"640\" height=\"200\" fill=\"#f8fafc\"/>" +
              "<text x=\"320\" y=\"84\" font-family=\"system-ui\" font-size=\"14\" font-weight=\"700\" fill=\"#0f172a\" text-anchor=\"middle\">" + escapeHtml(title) + "</text>" +
              "<text x=\"320\" y=\"116\" font-family=\"system-ui\" font-size=\"12\" fill=\"#475569\" text-anchor=\"middle\">" + count + " " + escapeHtml(metricLabel) + " · " + pct + "% of target</text>" +
              "</svg>"
            const imageUrl = "data:image/svg+xml," + encodeURIComponent(svg)
            const outputSrcDoc = "<!doctype html><html><head><meta charset=\"utf-8\"><style>" +
              "body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}" +
              "h2{font-size:14px;font-weight:600;margin:0 0 10px}.track{height:16px;background:#e2e8f0;border-radius:8px;overflow:hidden}" +
              ".bar{height:100%;background:#22c55e;border-radius:8px;width:" + pct + "%}.note{margin-top:8px;font-size:12px;color:#64748b}" +
              "</style></head><body><h2>" + escapeHtml(title) + "</h2><div class=\"track\"><div class=\"bar\"></div></div>" +
              "<p class=\"note\">" + count + " " + escapeHtml(metricLabel) + " · " + pct + "% of " + metricTarget + " target</p></body></html>"
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
- Metric: {{source_input.input_metric_label}} / {{source_input.input_metric_target}}
