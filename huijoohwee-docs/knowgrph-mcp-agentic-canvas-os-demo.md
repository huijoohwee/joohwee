---
title: "Knowgrph MCP Agentic Canvas OS Demo - Reference Video To Sold Remix"
graphId: "md:knowgrph-mcp-agentic-canvas-os-demo"
doc_type: "MCP Agentic Canvas OS Demo"
date: "2026-06-10"
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
kgBottomPanelOpen: true
kgBottomPanelTab: "eventModeling"
kgFloatingPanelOpen: true
kgFloatingPanelView: "eventModeling"
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
kgStorageTarget: "cloudflare"
kgStorageAccountId: "170e89fdb8679ff2fcc2900e25ed04f4"
kgStorageWorkspaceId: "kgws:canonical-docs"
kgStorageDocPath: "huijoohwee/docs/knowgrph-mcp-agentic-canvas-os-demo.md"
kgStorageDocTarget: "cloudflare-d1"
kgStorageMediaBucket: "knowgrph-media"
kgStorageMediaBaseUrl: "https://airvio.co/knowgrph/r2"
kgStorageMediaKeyScheme: "runs/{runId}/{stageId}/{shotId}.{ext}"
kgMediaPersistPolicy: "copy-on-generate"
kgProviderUrlEphemeral: true
kgMediaDedupeBy: "sha256"
kgReplayEnabled: true
kgReplayFromStorageWithoutLlm: true
kgReplayMediaFields: ["imageAssetUrl", "videoUrl"]
kgReplayAccessScope: "run-entitled"
kgForbidPlatform: ["vercel", "aws"]
demos: "knowgrph-mcp-agentic-canvas-os-prd-tad"
source_prd_tad: "huijoohwee.github.io/docs/documents/knowgrph-mcp-agentic-canvas-os-prd-tad.md"
control_plane_endpoint: "airvio.co/knowgrph/mcp"
mcp_tool: "knowgrph.video_remix.run"
socket_types:
  idea_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [idea_signal]}
  evidence_signal: {color: "#22c55e", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [evidence_signal]}
  approval_signal: {color: "#f59e0b", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [approval_signal]}
  artifact_signal: {color: "#8b5cf6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [artifact_signal]}
mcp_agentic_canvas_os_demo:
  schema_version: "mcp-agentic-canvas-os-demo/v1"
  run_id: {key: run_id, type: string, value: "kg_acos_reference_to_sold_remix_demo"}
  active_graph_mutated: {key: active_graph_mutated, type: boolean, value: false}
  mode: {key: mode, type: string, value: "dry-run-first; live behind approval tokens"}
  source_truth: {key: source_truth, type: string, value: "parsed frontmatter + typed Run_Manifest; never file-path assumptions"}
  mutation_policy: {key: mutation_policy, type: string, value: "no paid/external action in live mode without a verified per-gate Approval_Token; default dry-run"}
  tools: {key: tools, type: array, value: ["knowgrph.video_remix.run","knowgrph.video_remix.storyboard","knowgrph.video_remix.image","knowgrph.video_remix.video","knowgrph.video_remix.checkout"]}
  approval_gates: {key: approval_gates, type: array, value: ["paid-model-call","render-action","payment-action","cloud-deploy","consumer-repo-write","authenticated-browser"]}
  input_fields: {key: input_fields, type: array, value: ["referenceUrl","brief","budgetUsd","mode","approvals"]}
  output_fields: {key: output_fields, type: array, value: ["state","stages","approvalGates","budgetMeters","storyboard","imageUrl","videoUrl","commerce","demoPack"]}
flow_diagrams:
  key: flow_diagrams
  type: object
  value:
    reference_to_remix_gitgraph:
      key: reference_to_remix_gitgraph
      type: mermaid_gitgraph
      floatingPanelView: "gitGraph"
      floatingPanelOpen: true
      bottomPanelTab: "gitGraph"
      bottomPanelOpen: true
      value: |-
        gitGraph
          commit id: "import_url" tag: "youtu.be/77FAnT935IE"
          commit id: "storyboard" tag: "kgc-flow"
          branch b5_quick_cut
          checkout b5_quick_cut
          commit id: "img_seedream_4_0"
          commit id: "vid_seedance_1_0_fast"
          checkout main
          branch b25_full_promo
          checkout b25_full_promo
          commit id: "img_seedream_4_5"
          commit id: "vid_seedance_1_5"
          checkout main
          branch b50_multi_variant
          checkout b50_multi_variant
          commit id: "img_seedream_5_0"
          commit id: "vid_dreamina_2_0"
          checkout main
          commit id: "r2_assets" tag: "replay-no-llm"
          commit id: "stripe_checkout" tag: "sold"
          commit id: "demo_pack" tag: "7/7"
    agentic_canvas_architecture:
      key: agentic_canvas_architecture
      type: mermaid_architecture
      floatingPanelView: "architecture"
      floatingPanelOpen: true
      bottomPanelTab: "architecture"
      bottomPanelOpen: true
      forbidPlatform: ["vercel", "aws"]
      value: |-
        architecture-beta
          group user(cloud)[User surface]
          group cloudflare(cloud)[Cloudflare]
          group providers(cloud)[Default provider BytePlus plus Stripe]
          service web(internet)[Cloudflare UI airvio.co knowgrph] in cloudflare
          service mcp(server)[McpAgent Worker] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service manifest(database)[Run Manifest DO] in cloudflare
          service r2(database)[R2 image and video assets] in cloudflare
          service byteplus(server)[BytePlus seedream and seedance] in providers
          service stripe(database)[Stripe] in providers
          web:R --> L:mcp
          mcp:B --> T:manifest
          mcp:R --> L:gateway
          gateway:R --> L:byteplus
          mcp:B --> T:r2
          mcp:R --> L:stripe
    agent_run_event_model:
      key: agent_run_event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui UserBrief
        tf 02 cmd StartVideoRemixRun
        tf 03 evt RunManifestCreated
        tf 04 pcr DirectorAgent
        tf 05 cmd RequestStoryboard
        tf 06 evt StoryboardReady
        tf 07 cmd RequestApprovalToken
        tf 08 evt ApprovalGranted
        tf 09 cmd GenerateImage
        tf 10 evt ImageAssetReady
        tf 11 cmd GenerateVideo
        tf 12 evt VideoAssetReady
        tf 13 cmd CreateCheckout
        tf 14 evt PaymentSessionCreated
        tf 15 ui DemoPackReady
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
    mcp_pipeline_flowchart:
      key: mcp_pipeline_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          source_input["Run Brief Input\n(referenceUrl · brief · budgetUsd · mode · approvals)"]
          compute_summary["Compute Run Manifest\n(BLOCKED / DRY-RUN / SOLD)"]
          approval_gate{"Approval Gates\n(paid-model-call · render · payment)"}
          panel_text["Run Manifest Panel\n(RichMediaPanel · text)"]
          panel_image["Image Panel\n(R2 · seedream)"]
          panel_video["Video Panel\n(R2 · seedance)"]
          panel_chart["Dashboard Panel\n(RichMediaPanel · HTML)"]
          source_input -->|"idea_signal + budget"| compute_summary
          compute_summary -->|"dry-run state"| approval_gate
          approval_gate -->|"all gates verified"| panel_text
          approval_gate -->|"imageAssetUrl"| panel_image
          approval_gate -->|"videoUrl"| panel_video
          approval_gate -->|"outputSrcDoc"| panel_chart
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "source_input"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "Run Brief Input"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      handles: {key: handles, type: object, value: {"source":["referenceUrl","brief","budgetUsd","mode","approvals"]}}
      approvals: {key: approvals, type: array, value: []}
      brief: {key: brief, type: textarea, value: "Turn this reference clip into a 30s vertical promo. "}
      budgetUsd: {key: budgetUsd, type: number, value: 25}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"previewField":"referenceUrl","previewMaxChars":80,"onEdit":{"trigger":"runDownstream","targets":["compute_summary"]},"actions":[{"id":"edit","label":"Edit","icon":"pencil","trigger":"openFieldEditor","targetField":"brief"},{"id":"run","label":"Run","icon":"play","trigger":"runDownstream","targets":["compute_summary"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"referenceUrl":"idea_signal","brief":"idea_signal","budgetUsd":"evidence_signal","mode":"idea_signal","approvals":"approval_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "demoInput"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Reusable run-brief source widget: reference URL, creative brief, budget cap, mode, and approval tokens for the video-remix agent loop."}
      mode: {key: mode, type: string, value: "live"}
      referenceUrl: {key: referenceUrl, type: string, value: "https://youtu.be/77FAnT935IE"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "input"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "compute_summary"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Compute Run Manifest"}
      position: {key: position, type: object, value: {"x":380,"y":0}}
      handles: {key: handles, type: object, value: {"target":["referenceUrl","brief","budgetUsd","mode","approvals"],"source":["output","imageAssetUrl","videoUrl","outputSrcDoc"]}}
      "canvas:runAction": {key: "canvas:runAction", type: object, value: {"fn":"compute","inputs":["referenceUrl","brief","budgetUsd","mode","approvals"],"outputs":["output","imageUrl","outputSrcDoc"],"updateBody":false,"sideEffects":[{"field":"run_status","set":"done"},{"field":"mcp_agentic_canvas_os_demo.active_graph_mutated","set":true},{"field":"mcp_agentic_canvas_os_demo.run_id","pattern":"kg_acos_run_yyyyMMddHHmm"}]}}
      "canvas:widgetCard": {key: "canvas:widgetCard", type: object, value: {"statusField":"run_status","statusValues":{"idle":"gray","running":"amber","done":"green","error":"red"},"previewField":"output","previewMaxChars":100,"actions":[{"id":"run","label":"Run","icon":"play","primary":true,"trigger":"compute"},{"id":"reset","label":"Reset","icon":"refresh","trigger":"clearOutputs","clearFields":["output","imageUrl","outputSrcDoc"]}]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"referenceUrl":"idea_signal","brief":"idea_signal","budgetUsd":"evidence_signal","mode":"idea_signal","approvals":"approval_signal"},"out":{"output":"artifact_signal","imageAssetUrl":"artifact_signal","videoUrl":"artifact_signal","outputSrcDoc":"artifact_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "demoCompute"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 9}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 5}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 4}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageAssetUrl: {key: imageAssetUrl, type: image_url, value: "https://airvio.co/knowgrph/r2/runs/kg_acos_reference_to_sold_remix_demo/image/shot-1.png"}
      imageUrl: {key: imageUrl, type: svg_data_uri, value: "data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%20640%20220%22%3E%3Crect%20width%3D%22640%22%20height%3D%22220%22%20fill%3D%22%23f8fafc%22%2F%3E%3Ctext%20x%3D%22320%22%20y%3D%2262%22%20font-family%3D%22system-ui%22%20font-size%3D%2226%22%20font-weight%3D%22700%22%20fill%3D%22%23f59e0b%22%20text-anchor%3D%22middle%22%3EBLOCKED%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22100%22%20font-family%3D%22system-ui%22%20font-size%3D%2214%22%20fill%3D%22%23475569%22%20text-anchor%3D%22middle%22%3Efull%20promo%20-%20~6%20shots%20-%20seedance-1-5-pro-251215%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22132%22%20font-family%3D%22system-ui%22%20font-size%3D%2213%22%20fill%3D%22%2364748b%22%20text-anchor%3D%22middle%22%3EBudget%20cap%20%2425%20-%20estimated%20spend%20%240%3C%2Ftext%3E%3Ctext%20x%3D%22320%22%20y%3D%22164%22%20font-family%3D%22system-ui%22%20font-size%3D%2212%22%20fill%3D%22%2364748b%22%20text-anchor%3D%22middle%22%3E3%20spend%20gate(s)%20awaiting%20approval%20-%207%20cited%20sources%3C%2Ftext%3E%3C%2Fsvg%3E"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Compute widget that turns the run brief into a gated Run_Manifest: stages, approval gates, budget meters, evidence pack, and a 7-section demo pack."}
      output:
        key: output
        type: markdown
        value: |
          ## BLOCKED - reference-to-sold remix
          
          Turn this reference clip into a 30s vertical promo.
          
          **Reference:** https://youtu.be/77FAnT935IE
          **Mode:** live
          **Budget cap:** $25
          **Treatment:** full promo (seedance-1-5-pro-251215, ~6 shots)
          **Estimated reconciled spend:** $0
          **State:** BLOCKED
          
          Live run halted at the first spend gate with zero paid actions. Approve the spend gates and re-submit the same run to proceed.
          
          ### Stages
          - import_url: planned
          - research: halted
          - storyboard: planned
          - render: planned
          - checkout: planned
          - demo_pack: planned
          
          ### Approval gates
          - paid-model-call: required
          - render-action: required
          - payment-action: required
          
          ### Evidence pack
          - Cited sources: 7
          - Weak-signal floor: 3 sources (halts before storyboard if unmet)
          
          ### Budget meters
          - Cap: $25
          - Estimated spend: $0
          - Headroom: $25
          
          ### Demo pack
          - Sections: Agent Overview, Autonomy, Actions & Tool Use, Orchestration, Human-in-the-Loop, Failure Handling, Demo & Presentation
          - Verified only when each URL or artifact is reachable.
          
      outputSrcDoc: {key: outputSrcDoc, type: html_srcdoc, value: "<!doctype html><html><head><meta charset=\"utf-8\"><meta name=\"viewport\" content=\"width=device-width,initial-scale=1\"><style>body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.panel{margin-bottom:12px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.panel h2{margin:0 0 10px;font-size:13px}.row{display:flex;align-items:center;gap:8px;margin:6px 0;font-size:12px}.rl{width:96px;color:#475569}.rt{flex:1;height:14px;background:#e2e8f0;border-radius:7px;overflow:hidden}.rb{display:block;height:100%;border-radius:7px}.rv{width:64px;text-align:right;color:#0f172a;font-weight:600}.chips{display:flex;flex-wrap:wrap;gap:6px}.chip{font-size:11px;padding:3px 8px;border-radius:999px;font-weight:600}.meter{height:16px;background:#e2e8f0;border-radius:8px;overflow:hidden}.meter span{display:block;height:100%;background:#0ea5e9;border-radius:8px}.note{font-size:12px;color:#64748b;margin:12px 0 0}</style></head><body><main data-kg-acos-remix-panel=\"1\"><div class=\"kpi\"><div><p class=\"label\">State</p><p class=\"value\">BLOCKED</p></div><div><p class=\"label\">Budget cap</p><p class=\"value\">$25</p></div><div><p class=\"label\">Est. spend</p><p class=\"value\">$0</p></div><div><p class=\"label\">Shots</p><p class=\"value\">~6</p></div></div><section class=\"panel\"><h2>Stage pipeline</h2><div class=\"row\"><span class=\"rl\">import_url</span><span class=\"rt\"><span class=\"rb\" style=\"width:12%;background:#cbd5e1\"></span></span><span class=\"rv\">planned</span></div><div class=\"row\"><span class=\"rl\">research</span><span class=\"rt\"><span class=\"rb\" style=\"width:50%;background:#f59e0b\"></span></span><span class=\"rv\">halted</span></div><div class=\"row\"><span class=\"rl\">storyboard</span><span class=\"rt\"><span class=\"rb\" style=\"width:12%;background:#cbd5e1\"></span></span><span class=\"rv\">planned</span></div><div class=\"row\"><span class=\"rl\">render</span><span class=\"rt\"><span class=\"rb\" style=\"width:12%;background:#cbd5e1\"></span></span><span class=\"rv\">planned</span></div><div class=\"row\"><span class=\"rl\">checkout</span><span class=\"rt\"><span class=\"rb\" style=\"width:12%;background:#cbd5e1\"></span></span><span class=\"rv\">planned</span></div><div class=\"row\"><span class=\"rl\">demo_pack</span><span class=\"rt\"><span class=\"rb\" style=\"width:12%;background:#cbd5e1\"></span></span><span class=\"rv\">planned</span></div></section><section class=\"panel\"><h2>Approval gates</h2><div class=\"chips\"><span class=\"chip\" style=\"background:#fef3c7;color:#92400e\">paid-model-call: required</span><span class=\"chip\" style=\"background:#fef3c7;color:#92400e\">render-action: required</span><span class=\"chip\" style=\"background:#fef3c7;color:#92400e\">payment-action: required</span></div></section><section class=\"panel\"><h2>Budget meter (0% of cap, $25 headroom)</h2><div class=\"meter\"><span style=\"width:0%\"></span></div></section><p class=\"note\">Dry-run by default; live spend halts at the first un-approved gate with zero paid actions. Treatment full promo via seedance-1-5-pro-251215. 7 cited sources.</p></main></body></html>"}
      run_status: {key: run_status, type: string, value: "idle"}
      semanticKey: {key: semanticKey, type: string, value: "acos-demo:compute:run-manifest"}
      "template:nodeType": {key: "template:nodeType", type: string, value: "compute"}
      videoUrl: {key: videoUrl, type: video_url, value: "https://airvio.co/knowgrph/r2/runs/kg_acos_reference_to_sold_remix_demo/video/shot-1.mp4"}
      "visual:importance": {key: "visual:importance", type: number, value: 48}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 22}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      compute:
        key: compute
        type: string
        value: |
          inputs => {
          const rs = (k,d) => { const v = String((inputs && inputs[k]) || '').trim(); return v || d; };
          const rn = (k,d) => { const v = Number(inputs && inputs[k]); return Number.isFinite(v) ? v : d; };
          const ra = (k) => { const v = inputs && inputs[k]; if (Array.isArray(v)) return v.map(x => String(x || '').trim()).filter(Boolean); const s = String(v || '').trim(); return s ? s.split(',').map(t => t.trim()).filter(Boolean) : []; };
          const esc = (v) => String(v || '').replace(/[&<>"']/g, c => c === '&' ? '&amp;' : c === '<' ? '&lt;' : c === '>' ? '&gt;' : c === '"' ? '&quot;' : '&#39;');
          const referenceUrl = rs('referenceUrl', '');
          const brief = rs('brief', '');
          const budget = rn('budgetUsd', 25);
          const mode = rs('mode', 'live').toLowerCase();
          const approvals = ra('approvals');
          const isLive = mode.indexOf('live') >= 0 && mode.indexOf('dry') < 0;
          const tier = budget <= 5 ? { name: 'quick cut', model: 'seedance-1-0-pro-fast-251015', shots: 3 } : budget <= 25 ? { name: 'full promo', model: 'seedance-1-5-pro-251215', shots: 6 } : { name: 'multi-variant', model: 'dreamina-seedance-2-0-260128', shots: 6 };
          const spendGates = ['paid-model-call', 'render-action', 'payment-action'];
          const approved = {};
          for (let i = 0; i < approvals.length; i++) approved[approvals[i]] = true;
          const gateRows = spendGates.map(g => ({ gate: g, status: approved[g] ? 'verified' : 'required' }));
          const missing = spendGates.filter(g => !approved[g]);
          const blocked = isLive && missing.length > 0;
          const verdict = blocked ? 'BLOCKED' : isLive ? 'SOLD' : 'DRY-RUN';
          const stages = ['import_url', 'research', 'storyboard', 'render', 'checkout', 'demo_pack'];
          const evidenceSources = Math.max(3, Math.min(50, Math.round((brief.length + referenceUrl.length) / 12)));
          const estCost = blocked ? 0 : isLive ? Math.round(budget * 0.92 * 100) / 100 : 0;
          const money = (n) => { const s = '$' + (Math.round(Math.abs(n) * 100) / 100).toLocaleString('en-US'); return n < 0 ? '-' + s : s; };
          const reach = blocked ? stages.indexOf('research') : stages.length;
          const stageRows = stages.map((s, i) => ({ stage: s, status: i < reach ? (blocked && i === 0 ? 'planned' : 'done') : i === reach && blocked ? 'halted' : 'planned' }));
          const summary = blocked ? 'Live run halted at the first spend gate with zero paid actions. Approve the spend gates and re-submit the same run to proceed.' : isLive ? 'Full loop executed: research, storyboard, render, checkout, and demo pack assembled within budget.' : 'Dry-run plan produced with zero spend. Switch to live mode and approve spend gates to execute.';
          const lines = ['## ' + verdict + ' - reference-to-sold remix', '', brief, '', '**Reference:** ' + referenceUrl, '**Mode:** ' + mode, '**Budget cap:** ' + money(budget), '**Treatment:** ' + tier.name + ' (' + tier.model + ', ~' + tier.shots + ' shots)', '**Estimated reconciled spend:** ' + money(estCost), '**State:** ' + verdict, '', summary, '', '### Stages', ...stageRows.map(r => '- ' + r.stage + ': ' + r.status), '', '### Approval gates', ...gateRows.map(r => '- ' + r.gate + ': ' + r.status), '', '### Evidence pack', '- Cited sources: ' + evidenceSources, '- Weak-signal floor: 3 sources (halts before storyboard if unmet)', '', '### Budget meters', '- Cap: ' + money(budget), '- Estimated spend: ' + money(estCost), '- Headroom: ' + money(Math.max(0, budget - estCost)), '', '### Demo pack', '- Sections: Agent Overview, Autonomy, Actions & Tool Use, Orchestration, Human-in-the-Loop, Failure Handling, Demo & Presentation', '- Verified only when each URL or artifact is reachable.'];
          const output = lines.join('\n');
          const vc = blocked ? '#f59e0b' : isLive ? '#22c55e' : '#0ea5e9';
          const svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 220"><rect width="640" height="220" fill="#f8fafc"/><text x="320" y="62" font-family="system-ui" font-size="26" font-weight="700" fill="' + vc + '" text-anchor="middle">' + esc(verdict) + '</text><text x="320" y="100" font-family="system-ui" font-size="14" fill="#475569" text-anchor="middle">' + esc(tier.name) + ' - ~' + tier.shots + ' shots - ' + esc(tier.model) + '</text><text x="320" y="132" font-family="system-ui" font-size="13" fill="#64748b" text-anchor="middle">Budget cap ' + esc(money(budget)) + ' - estimated spend ' + esc(money(estCost)) + '</text><text x="320" y="164" font-family="system-ui" font-size="12" fill="#64748b" text-anchor="middle">' + (missing.length ? missing.length + ' spend gate(s) awaiting approval' : 'all spend gates verified') + ' - ' + evidenceSources + ' cited sources</text></svg>';
          const imageUrl = 'data:image/svg+xml,' + encodeURIComponent(svg);
          let stageBars = '';
          for (let i = 0; i < stageRows.length; i++) { const st = stageRows[i].status; const w = st === 'done' ? 100 : st === 'halted' ? 50 : 12; const col = st === 'done' ? '#22c55e' : st === 'halted' ? '#f59e0b' : '#cbd5e1'; stageBars += '<div class="row"><span class="rl">' + esc(stageRows[i].stage) + '</span><span class="rt"><span class="rb" style="width:' + w + '%;background:' + col + '"></span></span><span class="rv">' + esc(st) + '</span></div>'; }
          let gateChips = '';
          for (let i = 0; i < gateRows.length; i++) { const ok = gateRows[i].status === 'verified'; gateChips += '<span class="chip" style="background:' + (ok ? '#dcfce7' : '#fef3c7') + ';color:' + (ok ? '#166534' : '#92400e') + '">' + esc(gateRows[i].gate) + ': ' + esc(gateRows[i].status) + '</span>'; }
          const headroom = Math.max(0, budget - estCost);
          const spendPct = budget > 0 ? Math.max(0, Math.min(100, Math.round((estCost / budget) * 100))) : 0;
          const css = 'body{margin:0;padding:16px;font-family:system-ui,sans-serif;background:#f8fafc;color:#0f172a}.kpi{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:8px;margin-bottom:12px}.kpi div,.panel{background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:10px}.panel{margin-bottom:12px}.label{margin:0 0 4px;font-size:11px;color:#64748b;text-transform:uppercase;letter-spacing:.04em}.value{margin:0;font-size:15px;font-weight:700}.panel h2{margin:0 0 10px;font-size:13px}.row{display:flex;align-items:center;gap:8px;margin:6px 0;font-size:12px}.rl{width:96px;color:#475569}.rt{flex:1;height:14px;background:#e2e8f0;border-radius:7px;overflow:hidden}.rb{display:block;height:100%;border-radius:7px}.rv{width:64px;text-align:right;color:#0f172a;font-weight:600}.chips{display:flex;flex-wrap:wrap;gap:6px}.chip{font-size:11px;padding:3px 8px;border-radius:999px;font-weight:600}.meter{height:16px;background:#e2e8f0;border-radius:8px;overflow:hidden}.meter span{display:block;height:100%;background:#0ea5e9;border-radius:8px}.note{font-size:12px;color:#64748b;margin:12px 0 0}';
          const outputSrcDoc = '<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><style>' + css + '</style></head><body><main data-kg-acos-remix-panel="1"><div class="kpi"><div><p class="label">State</p><p class="value">' + esc(verdict) + '</p></div><div><p class="label">Budget cap</p><p class="value">' + esc(money(budget)) + '</p></div><div><p class="label">Est. spend</p><p class="value">' + esc(money(estCost)) + '</p></div><div><p class="label">Shots</p><p class="value">~' + tier.shots + '</p></div></div><section class="panel"><h2>Stage pipeline</h2>' + stageBars + '</section><section class="panel"><h2>Approval gates</h2><div class="chips">' + gateChips + '</div></section><section class="panel"><h2>Budget meter (' + spendPct + '% of cap, ' + esc(money(headroom)) + ' headroom)</h2><div class="meter"><span style="width:' + spendPct + '%"></span></div></section><p class="note">Dry-run by default; live spend halts at the first un-approved gate with zero paid actions. Treatment ' + esc(tier.name) + ' via ' + esc(tier.model) + '. ' + evidenceSources + ' cited sources.</p></main></body></html>';
          return { output: output, imageUrl: imageUrl, outputSrcDoc: outputSrcDoc };
          }
    - id: {key: id, type: string, value: "panel_text_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Run Manifest"}
      position: {key: position, type: object, value: {"x":760,"y":240}}
      handles: {key: handles, type: object, value: {"target":["output"],"source":["output"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"output":"artifact_signal"},"out":{"output":"artifact_signal"}}}
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
      label: {key: label, type: string, value: "Rich Media Panel - Image (seedream)"}
      position: {key: position, type: object, value: {"x":760,"y":0}}
      handles: {key: handles, type: object, value: {"target":["imageAssetUrl"],"source":["imageAssetUrl"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"imageAssetUrl":"artifact_signal"},"out":{"imageAssetUrl":"artifact_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageAssetUrl: {key: imageAssetUrl, type: string, value: ""}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Image Rich Media Panel embeds the R2 imageAssetUrl (seedream) and replays it without calling the model."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "panel_video_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Video (seedance)"}
      position: {key: position, type: object, value: {"x":760,"y":480}}
      handles: {key: handles, type: object, value: {"target":["videoUrl"],"source":["videoUrl"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"videoUrl":"artifact_signal"},"out":{"videoUrl":"artifact_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Video Rich Media Panel embeds the R2 videoUrl and replays it without calling the model."}
      "template:nodeType": {key: "template:nodeType", type: string, value: "rich_media_panel"}
      videoUrl: {key: videoUrl, type: text, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
    - id: {key: id, type: string, value: "panel_chart_output"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel - Run Dashboard"}
      position: {key: position, type: object, value: {"x":760,"y":-240}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"artifact_signal"},"out":{"outputSrcDoc":"artifact_signal"}}}
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
    - {"id":"edge_referenceUrl_to_compute","source":"source_input","sourceHandle":"referenceUrl","target":"compute_summary","targetHandle":"referenceUrl","label":"referenceUrl","type":"idea_signal"}
    - {"id":"edge_brief_to_compute","source":"source_input","sourceHandle":"brief","target":"compute_summary","targetHandle":"brief","label":"brief","type":"idea_signal"}
    - {"id":"edge_budgetUsd_to_compute","source":"source_input","sourceHandle":"budgetUsd","target":"compute_summary","targetHandle":"budgetUsd","label":"budgetUsd","type":"evidence_signal"}
    - {"id":"edge_mode_to_compute","source":"source_input","sourceHandle":"mode","target":"compute_summary","targetHandle":"mode","label":"mode","type":"idea_signal"}
    - {"id":"edge_approvals_to_compute","source":"source_input","sourceHandle":"approvals","target":"compute_summary","targetHandle":"approvals","label":"approvals","type":"approval_signal"}
    - {"id":"edge_compute_to_panel_text_output","source":"compute_summary","sourceHandle":"output","target":"panel_text_output","targetHandle":"output","label":"output","type":"artifact_signal"}
    - {"id":"edge_compute_to_panel_image_output","source":"compute_summary","sourceHandle":"imageAssetUrl","target":"panel_image_output","targetHandle":"imageAssetUrl","label":"imageAssetUrl","type":"artifact_signal"}
    - {"id":"edge_compute_to_panel_video_output","source":"compute_summary","sourceHandle":"videoUrl","target":"panel_video_output","targetHandle":"videoUrl","label":"videoUrl","type":"artifact_signal"}
    - {"id":"edge_compute_to_panel_chart_output","source":"compute_summary","sourceHandle":"outputSrcDoc","target":"panel_chart_output","targetHandle":"outputSrcDoc","label":"outputSrcDoc","type":"artifact_signal"}
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

# Knowgrph MCP Agentic Canvas OS — Demo

**Demos:** [`knowgrph-mcp-agentic-canvas-os-prd-tad.md`](knowgrph-mcp-agentic-canvas-os-prd-tad.md)

One autonomous agent takes a **reference video URL + a creative brief + a budget
cap** and drives the full loop — **storyboard → image → video → checkout** —
ending in a **sold, R2-stored remix** with replayable image and video panels.
The whole demo starts from a single **Import URL** field (the walkthrough below
imports the real clip
[`youtu.be/77FAnT935IE`](https://youtu.be/77FAnT935IE)). The default provider is
**BytePlus** (chat `agnes/seed`, image `seedream`, video `seedance`); every
model/media call routes through **Cloudflare AI Gateway** and every spend
boundary is gated by a human approval token. This page is the operator + judge
walkthrough of that flow.

## Current status

- **Truthful state today:** the Cloudflare control plane (Workers `McpAgent` +
  Pages + R2 + AI Gateway) and local contracts already support a high-ROI live
  path. The product runs entirely on **Cloudflare**: `airvio.co/knowgrph` serves
  the UI and the `doc-view` canvas; `airvio.co/knowgrph/mcp` serves the agent
  tools.
- **Default provider:** **BytePlus** (via the BytePlus API key) is the default
  model/media provider for chat, image, and video, routed through **Cloudflare
  AI Gateway** for cache, token counting, fallback, and unified billing.
- **Immediate live-product-ready target:** the in-session flow mints its own
  `Auth_Token`, submits the run, then re-submits the same run with updated
  `approvals[]` after each user decision, and embeds the run-scoped `doc-view`
  canvas plus the image/video Rich Media Panels.

## At a glance

| **Hero tool** | `knowgrph.video_remix.run` (+ stage tools) over MCP Streamable HTTP |
| **Control plane** | Cloudflare Workers `McpAgent` (Agents SDK) at `airvio.co/knowgrph/mcp` — holds all model keys |
| **Product surface** | Cloudflare Pages/Workers at `airvio.co/knowgrph` — UI, `doc-view` canvas, R2 media |
| **Default provider** | **BytePlus** (BytePlus API key): chat `agnes/seed`, image `seedream`, video `seedance` |
| **Model routing** | All model/media calls via **Cloudflare AI Gateway** (cache, token count, fallback, unified billing) |
| **Media + payment** | BytePlus image/video → R2 assets · Stripe checkout/payout |
| **Publish chain** | Dev `knowgrph` → Prod mirror `huijoohwee/content/knowgrph` → Cloudflare `airvio.co/knowgrph` (operator-gated) |
| **Safety** | Dry-run by default; approval gates; single-use 15-min Approval_Tokens; budget meters |
| **Default behavior** | Live mode **without** approvals halts at the first spend gate with **zero** paid actions |

## The hero flow

```mermaid
flowchart LR
  url["Import URL: youtu.be/77FAnT935IE + brief + budget"] --> ingest[Cloudflare McpAgent: auth + validate]
  ingest --> story[Storyboard · BytePlus chat via Cloudflare AI Gateway]
  story --> kgc[(Kgc_Document: kgc-computing-flow/v1, 1 node per shot)]
  kgc --> gate{Approval_Gate verified?}
  gate -->|"no token"| blocked[Dry-run plan artifact · state: blocked · zero spend]
  gate -->|"verified token"| image[Image · BytePlus seedream via AI Gateway]
  image --> video[Video · BytePlus seedance via AI Gateway]
  video --> r2[(R2 image + video assets + Credit_Ledger event)]
  r2 --> sell[Stripe checkout + gated payout]
  sell --> manifest[(Run_Manifest + 7-section Demo_Pack)]
  kgc -.->|"embed via doc-view iframe"| canvas[/"Live knowgrph canvas (airvio.co/knowgrph doc-view, scoped to runId)"/]
  r2 -.->|"embed image panel"| imgpanel[/"Rich Media Panel: image (R2 iframe, replay, no LLM)"/]
  r2 -.->|"embed video panel"| vidpanel[/"Rich Media Panel: video (R2 iframe, replay, no LLM)"/]
  manifest --> ui[Cloudflare UI: canvas + image panel + video panel + receipt + manifest]
  canvas --> ui
  imgpanel --> ui
  vidpanel --> ui
```

```mermaid
sequenceDiagram
  actor User
  participant Web as Cloudflare UI (airvio.co/knowgrph)
  participant Mcp as McpAgent (Cloudflare)
  participant Dir as Director Workflow
  participant Gate as HITL Gate
  participant BP as BytePlus via Cloudflare AI Gateway
  participant R2 as Cloudflare R2 + Stripe
  User->>Web: referenceUrl + brief + budget
  Web->>Mcp: POST auth/session + forward knowgrph.video_remix.run (Streamable HTTP)
  Mcp->>Mcp: verify Auth_Token -> Caller_Identity (401 if invalid)
  Mcp->>Dir: start run (mode=live)
  loop each stage storyboard->image->video->checkout
    Dir->>Gate: spend boundary? request Approval_Gate
    alt no verified, unexpired, unconsumed token
      Gate-->>Dir: approval_required
      Dir->>Dir: resolve stage to dry-run plan artifact (zero spend)
    else verified token
      Gate-->>Dir: approved (token marked consumed, single-use)
      Dir->>BP: storyboard (chat) / image (seedream) / video (seedance)
      BP-->>Dir: result or typed degraded error
      Dir->>R2: store image + video assets; create Stripe session
    end
    Dir->>Mcp: persist Run_Manifest (<=2s)
  end
  Dir-->>Mcp: terminal Run_Manifest + Demo_Pack
  Mcp-->>Web: Run_Manifest (image + video R2 URLs)
  Web->>Web: iframe doc-view canvas + iframe R2 image + iframe R2 video (replay, no LLM)
  Web-->>User: canvas + image panel + video panel
```

## Live demo script (operator)

> Endpoints are environment-driven (no hardcoded URLs). The deploy is
> operator-gated behind the `cloud-deploy` Approval_Token — see the
> [deploy runbook](../../knowgrph/docs/knowgrph-acos-deploy-runbook.md).
> All routes are served by **Cloudflare** under `airvio.co/knowgrph` (UI +
> `doc-view`) and `airvio.co/knowgrph/mcp` (agent tools).

### 0. Open a session

```
POST airvio.co/knowgrph/mcp/auth/session     ->  { token }   # Cloudflare McpAgent
```

### 1. Submit the run — and prove it fails safe (AC-1)

```
POST airvio.co/knowgrph/mcp   (tools/call knowgrph.video_remix.run)
Authorization: Bearer <token>
{ "referenceUrl": "https://youtu.be/77FAnT935IE",
  "brief": "Turn this reference clip into a 30s vertical promo.",
  "budgetUsd": 25.00,
  "approvals": [] }
```

**Expected (no approvals):** `state: "blocked"`, `approvalGates.length >= 3`,
`budgetMeters.estimatedCostUsd == 0`, and **zero** BytePlus/Stripe calls logged.
The agent shows the planned stages + budget upfront and stops at the first spend
boundary. *This is the headline safety demo.*

### 2. Approve gates and run the full loop

Approve each spend gate, then **re-submit the same run with updated
`approvals[]`**. The backend already accepts `approvals[]`. The Director now
executes against **BytePlus via Cloudflare AI Gateway**:

1. **Storyboard** — BytePlus chat (`agnes/seed`) via Cloudflare AI Gateway → a
   `kgc-computing-flow/v1` canvas doc with **exactly one node per planned shot**,
   rendered live by **embedding the knowgrph `doc-view` iframe** (the
   `airvio.co/knowgrph` doc-view scoped to this `runId`; reasoning failure falls
   back to a valid single-node plan). knowgrph owns the canvas engine; the UI
   embeds it.
2. **Image** — BytePlus **`seedream`** via Cloudflare AI Gateway → one R2 image
   asset per shot, surfaced in the **Image Rich Media Panel**.
3. **Video** — BytePlus **`seedance`** via Cloudflare AI Gateway → one R2 video
   asset per shot, surfaced in the **Video Rich Media Panel** (keyless /
   over-budget routes to a deterministic zero-spend mock provider). Each
   completed asset writes one Credit_Ledger event.
4. **Checkout** — Stripe checkout session created only when `payment-action` is
   approved; payout settles only after explicit approval.

Once assets exist in R2, the image and video panels **replay from their R2 URLs
via `<iframe>` with zero further LLM/model calls** (see Rich Media Panels below).

### 2b. Same URL, three budgets, six media sub-branches

Keep the imported reference fixed at
[`youtu.be/77FAnT935IE`](https://youtu.be/77FAnT935IE) and vary **only** the
`budgetUsd` dial. The Director reasons about cost-vs-quality and auto-selects the
model tier per cap — **three budget branches**, each fanning into an **image
(`seedream`)** and a **video (`seedance`)** sub-branch: **six media sub-branches
total**, all BytePlus via Cloudflare AI Gateway.

```mermaid
flowchart LR
  src["Import URL<br/>youtu.be/77FAnT935IE"] --> b5["$5 · quick cut"]
  src --> b25["$25 · full promo"]
  src --> b50["$50 · multi-variant"]
  b5 --> i5["image · seedream-4-0-250828"]
  b5 --> v5["video · seedance-1-0-pro-fast-251015"]
  b25 --> i25["image · seedream-4-5-251128"]
  b25 --> v25["video · seedance-1-5-pro-251215"]
  b50 --> i50["image · seedream-5-0-260128"]
  b50 --> v50["video · dreamina-seedance-2-0-260128"]
  i5 & v5 & i25 & v25 & i50 & v50 --> r2[(R2 assets · replayable via iframe · no LLM)]
```

```
POST airvio.co/knowgrph/mcp   # same referenceUrl + brief, different budget
{ "referenceUrl": "https://youtu.be/77FAnT935IE", "brief": "...", "budgetUsd": 5.00,  "approvals": [...] }
{ "referenceUrl": "https://youtu.be/77FAnT935IE", "brief": "...", "budgetUsd": 25.00, "approvals": [...] }
{ "referenceUrl": "https://youtu.be/77FAnT935IE", "brief": "...", "budgetUsd": 50.00, "approvals": [...] }
```

| Budget branch | Image sub-branch (`seedream`) | Video sub-branch (`seedance`) | Shots |
| **$5 — quick cut** | `seedream-4-0-250828` | `seedance-1-0-pro-fast-251015` | ~3 |
| **$25 — full promo** | `seedream-4-5-251128` | `seedance-1-5-pro-251215` | ~6 |
| **$50 — multi-variant** | `seedream-5-0-260128` | `dreamina-seedance-2-0-260128` | ~6 × variants |

Each branch reports a **real per-remix cost** reconciled from the Credit_Ledger
(±0.01 USD) and a Stripe session sized to its tier. The triptych — one source
clip, three budget branches, six BytePlus image/video sub-branches, three real
costs — demonstrates **Autonomy & Decision-Making** (the agent picks the
image+video model per cap) and the TCO / token-economics thesis in one frame.
Over-budget or keyless branches route to the deterministic zero-spend mock
provider, so the comparison is reproducible offline.

### 3. Read back the evidence

```
tools/call response          ->  current Run_Manifest rendered in-session (immediate path)
GET airvio.co/knowgrph/mcp/health ->  200 within 5s (liveness, discloses nothing sensitive)
```

> **Read-back note:** `GET airvio.co/knowgrph/mcp/runs/{id}` is the durable
> manifest read-back path (Workers durable storage / R2) when the same session
> owns the run. The remaining gap is **deployed proof**: capture one live
> end-to-end run showing persisted read-back plus replayed image/video panels.

### 4. One-command reachability gate (AC-8)

```
MCP_ENDPOINT=https://airvio.co/knowgrph/mcp \
FRONTEND_URL=https://airvio.co/knowgrph npm run runtime:verify
```

Probes the `/health`/reachability surfaces (5s-bounded) and emits a sample
`demoPack.urls[]`. Also wired as CI: `.github/workflows/runtime-gate.yml` runs
`runtime:test` + `runtime:verify` on a deploy trigger (endpoints from repo
Variables / dispatch inputs — no hardcode).

## Rich Media Panels — image and video (replay without LLM)

The run surfaces media as **two distinct Rich Media Panels** on the canvas — one
for the BytePlus **image** (`seedream`) and one for the BytePlus **video**
(`seedance`). Both are backed by **Cloudflare R2** asset URLs written during the
run; once written, the panels **replay purely by embedding the R2 URL in an
`<iframe>`/media tag — no model, AI Gateway, or LLM call is made on replay**.
This keeps re-viewing free and instant, and makes the demo reproducible.

| Panel | Source field | BytePlus model | Replay element | Calls LLM on replay? |
| **Image Rich Media Panel** | `imageAssetUrl` (R2) | `seedream` | `<iframe>` / `<img>` | **No** |
| **Video Rich Media Panel** | `videoUrl` (R2) | `seedance` | `<iframe>` / `<video controls>` | **No** |
| Run Dashboard panel | `outputSrcDoc` | — | `<iframe srcdoc>` | No |
| Canvas (doc-view) | run-scoped doc-view | — | `<iframe>` | No |

R2 key scheme: `runs/{runId}/{stageId}/{shotId}.{ext}` served under
`https://airvio.co/knowgrph/r2` (bucket `knowgrph-media`, account
`170e89fdb8679ff2fcc2900e25ed04f4`).

**Image panel embed (replay):**

```html
<!-- Rich Media Panel: image — replays the durable R2 asset, no LLM -->
<iframe
  class="rmp rmp--image"
  src="https://airvio.co/knowgrph/r2/runs/<runId>/image/shot-1.png"
  title="seedream image — run <runId>"
  sandbox="allow-scripts allow-same-origin"
  referrerpolicy="no-referrer"
  loading="lazy"></iframe>
```

**Video panel embed (replay):**

```html
<!-- Rich Media Panel: video — replays the durable R2 asset, no LLM -->
<iframe
  class="rmp rmp--video"
  src="https://airvio.co/knowgrph/r2/runs/<runId>/video/shot-1.mp4"
  title="seedance video — run <runId>"
  sandbox="allow-scripts allow-same-origin"
  referrerpolicy="no-referrer"
  loading="lazy"></iframe>
<!-- or, for native controls without an extra document: -->
<video class="rmp rmp--video" controls preload="metadata"
  src="https://airvio.co/knowgrph/r2/runs/<runId>/video/shot-1.mp4"></video>
```

Replay rule: generation (a paid BytePlus call behind an Approval_Token) happens
**once** per shot and writes the R2 asset + a Credit_Ledger event. Every
subsequent view — re-opening the panel, sharing the run, a judge re-watching —
reads the **static R2 URL** through the iframe and spends **nothing**. The
Image and Video panels are independent nodes, so a run can show the still frame
and the motion clip side by side.

### Auto-save, Cloudflare persistence, and user replay

**Persist-on-generate (why we copy to R2).** BytePlus ModelArk returns media on
ephemeral URLs — the
[image API](https://docs.byteplus.com/en/docs/ModelArk/1666945) returns a
short-lived URL (or `b64_json`), and the
[video API](https://docs.byteplus.com/en/docs/ModelArk/Video_Generation_API) is
an **async task** (create → poll → temporary result URL). Those provider URLs
expire (~24h), so they are never stored as the artifact. The moment a stage
succeeds the control plane **copies the bytes into Cloudflare R2** and records
only the durable R2 URL in the Run_Manifest + Credit_Ledger
(`kgMediaPersistPolicy: "copy-on-generate"`, `kgProviderUrlEphemeral: true`).
Image: request `b64_json` and `PUT` to R2; video: on task `succeeded`, stream
the result to R2. Objects are content-addressed (`kgMediaDedupeBy: "sha256"`) so
an identical re-run reuses the existing object — zero extra spend.

**Auto-save.** The canvas auto-saves as the run progresses and the user edits —
debounced (`kgAutoSaveDebounceMs: 1500`), triggered on node edits, run
completion, approvals, and each asset-ready event (`kgAutoSaveOn`). Saves split
by artifact type (`kgStorageTarget: "cloudflare"`, account
`170e89fdb8679ff2fcc2900e25ed04f4`): the **document/manifest → D1**
(`kgws:canonical-docs`, holding only R2 URLs + metadata, never blobs); the
**media bytes → R2** bucket `knowgrph-media`, keyed
`runs/{runId}/{stageId}/{shotId}.{ext}` and served under
`https://airvio.co/knowgrph/r2`. Saves are idempotent (keyed by `runId` +
content hash) and guarded by an `updatedAt`/revision check so a background
autosave never clobbers a concurrent manual edit.

**User replay (no LLM).** Because the manifest plus the durable R2 URLs are
persisted, **any entitled user can re-open the saved run and replay** the Image
and Video panels (`kgReplayEnabled: true`,
`kgReplayMediaFields: ["imageAssetUrl", "videoUrl"]`) straight from R2 with **no
model/LLM call** (`kgReplayFromStorageWithoutLlm: true`). Replay access is
**run-scoped** (`kgReplayAccessScope: "run-entitled"`): the R2 route honors the
same entitlement as `GET /runs/{id}` (signed/short-TTL URL or a Worker check) —
the bucket is not public. Re-watching, sharing the link, or returning later all
read the saved R2 URLs over R2's zero-egress path — zero new spend.

## Acceptance criteria — live evidence

| AC | What the demo shows | `/goal` condition |
| **AC-1** Live run, gated | Step 1: no approvals → halts, zero spend | `state "blocked", approvalGates>=3, estimatedCostUsd==0, no paid call logged` |
| **AC-2** Storyboard on canvas | KGC shot-plan doc on the canvas | `parses kgc-computing-flow/v1 and flow.nodes==planned shots` |
| **AC-3** Image generated | BytePlus `seedream` R2 image per shot in the Image panel | `imageUrl under knowgrph R2 bucket + credit-ledger event id` |
| **AC-4** Video generated | BytePlus `seedance` R2 video per shot in the Video panel | `videoUrl under knowgrph R2 bucket + credit-ledger event id` |
| **AC-5** Replay without LLM | Re-open image/video panels; zero new model calls | `panel iframe src is the R2 URL; no AI Gateway call logged on replay` |
| **AC-6** Sale + payout gated | Stripe session; payout only post-approval | `session id; settle_payout only if payment-action approved` |
| **AC-7** Failure bounded | Injected tool failure → bounded retry / fail closed | `retryCount>=1 then complete or blocked, never exceeding maxIterations` |
| **AC-8** Deployed live | Reachable Cloudflare UI + `airvio.co/knowgrph/mcp/health` 200 in the demo pack | `demoPack.urls has a reachable airvio.co/knowgrph URL + mcp /health 200` |

## Judging-dimension map

| Dimension | Live evidence in this demo |
| Agent Overview | Director + stage harnesses behind one `knowgrph.video_remix.run` tool |
| Autonomy & Decision-Making | Agents SDK `AgentWorkflow` agentic loop; per-budget image+video model selection; budget-cap halt |
| Actions & Tool Use | BytePlus chat/image/video, knowgrph canvas (embedded via `doc-view` iframe), Stripe checkout — all via Cloudflare AI Gateway |
| Orchestration | Strict stage ordering + per-shot image/video fan-out + durable Run_Manifest persistence |
| Human-in-the-Loop | Approval gates; single-use 15-min Approval_Tokens; auth never substitutes for approval |
| Failure Handling | Bounded exponential-backoff retry, fail-closed `blocked` with a failure record; degraded provider error |
| Demo & Presentation | Demo_Pack with reachable URLs, the shot plan on the embedded canvas, and replayable image + video Rich Media Panels (R2, no LLM) |

## Spend isolation & safety (what judges can verify)

- **Stack boundary (R11):** the Cloudflare control plane holds the BytePlus +
  Stripe keys; model/media calls route only through Cloudflare AI Gateway, and
  no paid action bypasses an approval gate. Enforced by static secret-scan smoke
  tests.
- **Auth ≠ approval (R15.9):** a valid Auth_Token gates *access*; it never
  authorizes spend — every paid action still requires a fresh Approval_Token.
- **Token economics:** every BytePlus call emits a Cost_Log via Cloudflare AI
  Gateway; the Director aggregates into Budget_Meters; the Credit_Ledger
  reconciles within ±0.01 USD or flags a discrepancy (both records preserved).
- **Replay is free:** image/video panels replay from static R2 URLs via iframe;
  no model/AI-Gateway call is made on replay, so re-watching never spends.
- **Fail closed:** un-configured deploys return HTTP 501 rather than making an
  accidental live call; the BytePlus client activates only when its key is
  present (`KNOWGRPH_LIVE_CLIENTS` includes `byteplus`).
- **Canvas embed isolation:** the in-product canvas and the R2 media panels frame
  `airvio.co/knowgrph` content; the routes allow framing only from the
  `airvio.co` origin (`frame-ancestors`) and scope each asset to the
  authenticated `runId` — the same entitlement boundary as the run-readback
  path. Treat this as a required runtime guarantee to prove.

## MainPanel Integrations — BytePlus API Key (default)

The MainPanel Integrations surface configures the **default model/media
provider**: **BytePlus**, authorized by the **BytePlus API key** and routed
through **Cloudflare AI Gateway**. One key powers all three modalities — chat
(`agnes/seed`), image (`seedream`), and video (`seedance`).

### What the BytePlus key does (default provider)

The **BytePlus API key** is the default credential for the whole pipeline. It is:

- **Held server-side in the Cloudflare control plane only** (a Worker secret via
  `wrangler secret put BYTEPLUS_API_KEY`); never in the UI bundle, never logged
  (R11/R15.7).
- The single key behind **chat, image, and video** — selected per the
  `modelSelection` frontmatter (`agnes/seed` for text, `seedream` for image,
  `seedance` for video).
- Routed through **Cloudflare AI Gateway**, which emits the `Cost_Log` the
  Director aggregates into `Budget_Meters` and reconciles against the
  Credit_Ledger (±0.01 USD).

```
knowgrph McpAgent (Cloudflare) ──BYTEPLUS_API_KEY──▶ Cloudflare AI Gateway ──▶ BytePlus
   stage: storyboard  → agnes/seed (chat)
   stage: image       → seedream  → R2 image asset
   stage: video       → seedance  → R2 video asset
   stage: checkout    → Stripe (payment-action gate)
```

### Provider routing — which call produces each output

| Output | Stage / BytePlus model | Routed through | Persisted to | Credential | Gate |
| Storyboard (canvas doc) | `…storyboard` · `agnes/seed` | Cloudflare AI Gateway | D1 manifest | `BYTEPLUS_API_KEY` | paid-model-call |
| Image | `…image` · `seedream` ([API](https://docs.byteplus.com/en/docs/ModelArk/1666945)) | Cloudflare AI Gateway | **R2** (copy-on-generate) | `BYTEPLUS_API_KEY` | render-action |
| Video | `…video` · `seedance` ([API](https://docs.byteplus.com/en/docs/ModelArk/Video_Generation_API)) | Cloudflare AI Gateway | **R2** (copy-on-generate) | `BYTEPLUS_API_KEY` | render-action |
| Stripe checkout/payout | `…checkout` | knowgrph payment worker | D1 manifest | `STRIPE_*` | payment-action |

The image API returns `b64_json`/a short-lived URL; the video API is async
(create task → poll → temporary URL). Both provider URLs expire, so the control
plane **copies the bytes into R2 on success** and stores only the durable R2 URL
(see Auto-save, Cloudflare persistence, and user replay above).

### Operator setup (one-time, Cloudflare control plane)

```bash
# BytePlus is the default provider; one key for chat + image + video.
wrangler secret put BYTEPLUS_API_KEY        --config cloudflare/workers/knowgrph-mcp/wrangler.toml
wrangler secret put STRIPE_SECRET_KEY       --config cloudflare/workers/knowgrph-mcp/wrangler.toml
wrangler secret put STRIPE_WEBHOOK_SECRET   --config cloudflare/workers/knowgrph-mcp/wrangler.toml
# Create the R2 media bucket (account 170e89fdb8679ff2fcc2900e25ed04f4) and bind it.
wrangler r2 bucket create knowgrph-media
# In wrangler.toml: [[r2_buckets]] binding = "MEDIA_BUCKET", bucket_name = "knowgrph-media"
# Map a custom domain so assets serve under https://airvio.co/knowgrph/r2/*
```

Then set, in the Worker env (`wrangler.toml` `[vars]` or dashboard):

1. `KNOWGRPH_LIVE_CLIENTS = byteplus,stripe` — else the harnesses fall back to
   the deterministic **zero-spend mock**, which is exactly why no real image/
   video/payment appears.
2. `AI_GATEWAY_ID` — the Cloudflare AI Gateway the BytePlus calls route through.
3. `MEDIA_BUCKET` R2 binding + `MEDIA_BASE_URL = https://airvio.co/knowgrph/r2`
   (durable asset URLs; the control plane copies BytePlus output here on
   generate).
4. `MCP_ENDPOINT = https://airvio.co/knowgrph/mcp` (self/forwarder reference).
5. Redeploy: `npm run mcp:worker:deploy`. Confirm
   `GET airvio.co/knowgrph/mcp/health` → 200.

### Troubleshooting "unable to generate"

| Symptom | Root cause | Fix |
| **No image (`seedream`)** | `BYTEPLUS_API_KEY` unset or `byteplus` missing from `KNOWGRPH_LIVE_CLIENTS` → mock fallback; or `render-action` gate unapproved → `blocked`. | Set the key + `KNOWGRPH_LIVE_CLIENTS=byteplus,stripe`; approve `render-action` and re-submit `approvals[]`. |
| **No video (`seedance`)** | Same key/gate cause for the async video task; or polling never reached `succeeded`. | Same fix; on `succeeded` the bytes are copied to R2 and `videoUrl` returns in the Run_Manifest for the Video panel. |
| **Asset shows then 404s later** | The manifest stored the **ephemeral BytePlus URL** instead of the R2 copy. | Ensure copy-on-generate is enabled (`kgMediaPersistPolicy: "copy-on-generate"`); the manifest must hold the `airvio.co/knowgrph/r2/...` URL, never the provider URL. |
| **No Stripe payment** | No live Stripe key, or `payment-action` unapproved (auth ≠ approval). | Set `STRIPE_SECRET_KEY`/`STRIPE_WEBHOOK_SECRET`; approve `payment-action`; ensure the webhook matches the created session. |
| **Cloudflare AI Gateway not running** | `AI_GATEWAY_ID` unset, or the BytePlus key not bound to the gateway. | Set `AI_GATEWAY_ID`; confirm the BytePlus key is configured for that gateway in the Cloudflare dashboard. |

**Mental model:** generation is a paid BytePlus call behind an Approval_Token. A
missing key or an unapproved gate yields the intended fail-safe — a zero-spend
mock or a `blocked` Run_Manifest — which reads as "nothing generated" but is
correct safety behavior. Once an asset exists in R2, the image/video panels
**replay via iframe with no further BytePlus/AI-Gateway call**.

## Immediate remediation checklist

- **Docs first:** keep the demo truthful about what is already live, what is
  in-session only, and what is a next seam.
- **MainPanel Integrations first:** set `BYTEPLUS_API_KEY` (+ `STRIPE_*`) as
  Cloudflare Worker secrets and `KNOWGRPH_LIVE_CLIENTS=byteplus,stripe` +
  `AI_GATEWAY_ID` in the Worker env (see
  [MainPanel Integrations](#mainpanel-integrations--byteplus-api-key-default)).
  BytePlus is the default provider for chat, image, and video.
- **Canvas + panels next:** confirm the `doc-view` canvas and the image/video
  Rich Media Panels embed via iframe from `airvio.co/knowgrph` and replay R2
  assets with no further model call.
- **Live proof:** capture one end-to-end run (storyboard → image → video →
  checkout) with the image/video panels replaying from R2.

## Reproduce locally (network-free, no credentials)

The whole contract is provable offline with deterministic in-memory seams —
zero live/paid calls:

```
npm run runtime:test     # full suite: unit + property-based + smoke, deterministic
```

This exercises the approval-gate invariant, the live-without-approvals halt,
dry-run zero-spend, the Kgc_Document round-trip, ledger/budget reconciliation,
bounded-retry fail-closed, the Demo_Pack assembler, and the auth/authorization
logic — all with mocked providers. The same harnesses accept the live BytePlus /
Stripe clients when credentials are wired, with the deterministic mocks as the
test default.

## Demo pack (7 sections)

A terminal run assembles one Demo_Pack mapping to the seven judging dimensions,
each section marked `verified` only when its URL/artifact is reachable:

```
Demo_Pack {
  urls: [{ url, kind }]            // kinds: "frontend" | "mcp" | "canvas" | "image" | "video"
                                   //   canvas: airvio.co/knowgrph doc-view, runId-scoped
                                   //   image/video: R2 asset URLs, replayable via iframe (no LLM)
                                   //   verified only when each URL is reachable + run-scoped
  sections: [                      // one per dimension, non-empty
    Agent Overview, Autonomy & Decision-Making, Actions & Tool Use,
    Orchestration, Human-in-the-Loop, Failure Handling, Demo & Presentation
  ]
}
```

The `canvas`, `image`, and `video` URLs are live, runId-scoped artifacts embedded
in the product. Each counts as verified only when its `airvio.co/knowgrph` route
is reachable and run-scoped, so the embedded canvas plus the replayable image and
video panels back the **Actions & Tool Use** and **Demo & Presentation** sections
with real URLs.

## Topology & publish chain

Everything runs on **Cloudflare**: the **`knowgrph` control plane** (Workers
`McpAgent` — holds the BytePlus + Stripe keys, owns every paid action) and the
**product surface** at `airvio.co/knowgrph` (Pages/Workers UI, `doc-view` canvas,
and R2-served image/video assets). The UI authenticates the caller, forwards
`knowgrph.video_remix.run` over MCP, and embeds the canvas + media panels — it
holds no keys itself.

### MCP connection (UI ↔ knowgrph control plane)

```mermaid
flowchart LR
  ui["Cloudflare UI (airvio.co/knowgrph)<br/>doc-view canvas + image/video panels · no keys"]
  kg["knowgrph control plane<br/>(McpAgent on Cloudflare Workers · holds BytePlus + Stripe keys)"]
  ui -->|"MCP Streamable HTTP · knowgrph.video_remix.run"| kg
  kg -->|"Run_Manifest + Demo_Pack (image/video R2 URLs)"| ui
  kg -.->|"embedded canvas + R2 image/video (airvio.co/knowgrph, runId-scoped)"| ui
```

- The UI authenticates the caller, then forwards `knowgrph.video_remix.run` to
  the `McpAgent` at **`airvio.co/knowgrph/mcp`** over MCP Streamable HTTP.
- The browser embeds the run-scoped `doc-view` canvas and the R2 image/video
  panels from `airvio.co/knowgrph`; replays read static R2 URLs with no model
  call.
- **Canvas + media are consumed, not rebuilt:** the storyboard stage emits a
  `Kgc_Document` (`kgc-computing-flow/v1`) and the image/video stages write R2
  assets; the UI embeds them via iframe rather than reimplementing the renderer
  or re-generating media. knowgrph owns the engine + the BytePlus/Stripe keys.
- Auth gates *access*; it never substitutes for an Approval_Token at a spend
  boundary. All BytePlus/Stripe spend stays inside knowgrph, routed through
  Cloudflare AI Gateway.
- **Packaging:** the connector contracts live in the **`knowgrph` monorepo**
  (control plane + UI + shared contracts), the SSOT, all deployed to Cloudflare.
  See
  [`knowgrph/docs/knowgrph-acos-topology-decision.md`](../../knowgrph/docs/knowgrph-acos-topology-decision.md).

### Dev → Prod → Cloudflare

knowgrph is the Dev source of truth; Prod and Cloudflare receive only
generated/synced artifacts after the upstream owner is correct. Prod sync and
deploy are **explicit operator actions** (the `cloud-deploy` Approval_Token
gates the live deploy — see the
[deploy runbook](../../knowgrph/docs/knowgrph-acos-deploy-runbook.md)).

```text
Dev (source of truth)   $GITHUB_ROOT/knowgrph
        │  npm run pages:build-sync  →  pages:check-sync
        ▼
Prod (artifact mirror)  $GITHUB_ROOT/huijoohwee/content/knowgrph
        │  npm run pages:deploy-cloudflare   (operator-gated)
        ▼
Cloudflare (live)       airvio.co · airvio.co/knowgrph · airvio.co/knowgrph/mcp
                        Cloudflare AI Gateway routes knowgrph's BytePlus + Stripe calls
                        (BYTEPLUS_API_KEY + STRIPE_* are Cloudflare Worker secrets)
```

Implementation, tests, and docs land in Dev first; no route-specific fixes are
made in the Prod mirror or the Cloudflare artifact.
