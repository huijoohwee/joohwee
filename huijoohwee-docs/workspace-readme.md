---
title: "Knowgrph Workspace README"
graphId: "md:workspace-readme"
doc_type: "Workspace README"
date: "2026-07-09"
lang: "en-US"
schema: "kgc-workspace-readme/v1"
source_reference: "docs/knowgrph-agentic-video-canvas-demo.md"
implementation_contract: "../../knowgrph/docs/documents/knowgrph-agentic-os-video-agent-prd-tad.companion.md"
validation_input_forbid_hardcode_in_repo: "true"
deployed_api_claim: "false"
publish_scope: "local-only"
publish_policy: "No Prod mirror, Cloudflare deploy, public release, fabricated provider IDs, generated asset URLs, transcript text, or credential material from this README."
workspace_topology:
  dev: "$GITHUB_ROOT/knowgrph"
  prod_mirror: "$GITHUB_ROOT/huijoohwee/content/knowgrph"
  cloudflare_routes: ["https://airvio.co", "https://airvio.co/knowgrph"]
  release_order: "Dev -> Prod -> Cloudflare"
  release_gate: "Prod and Cloudflare are blocked until the operator explicitly instructs that release lane."
docs_control_surface:
  operator_declared_path: "$GITHUB_ROOT/huijoohwee/agentic-os-docs"
  verified_path_status: "missing in this workspace on 2026-07-09"
  verified_fallback_path: "$GITHUB_ROOT/agentic-canvas-os"
  policy: "Use the verified docs-control surface only after local path verification; do not remap a missing path silently."
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: false
kgDocumentStructureBaselineLock: false
kgSharedRendererContract:
  version: "shared-renderer-contract/v1"
  semanticIdentity: "buildScopedGraphSemanticKey"
  cardPreview: "CardMediaPreview + CardMarkdownPreview"
  widgetCard: "canvas:widgetCard"
  richMediaPanel: "RichMediaPanel"
  storyboardDisplay: "2D Renderer: Storyboard Card (default) and Widget variants"
  storyboardSurfaces: ["Cards", "Widgets", "Rich Media Panels"]
  edgeModel: "active graph edges derive from frontmatter-owned flow.edges"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"
runtime_defaults:
  provider: "knowgrph-local-dry-run"
  status: "spec-complete"
  paid_call_count: 0
  runtime_proof_path: ""
  provider_job_id: ""
  stream_url: ""
  generated_asset_url: ""
agentic_os_invocation_grammar:
  slash:
    - "/source.normalize"
    - "/memory.seed"
    - "/harness.define"
    - "/mcp.capabilities"
    - "/cost.audit"
    - "/superagent.run"
    - "/tool.route"
    - "/canvas.project"
    - "/runtime-ready.check"
    - "/validation.run"
    - "/deploy.guard"
  semantic:
    - "#frontmatter"
    - "#harness"
    - "#token-economics"
    - "#tool-gateway"
    - "#tool-routing"
    - "#long-horizon-harness"
    - "#runtime-ready"
    - "#canvas"
    - "#human-in-loop"
    - "#approval-gate"
    - "#dev-only"
    - "#no-hardcode"
    - "#no-legacy"
  binding:
    - "@source.frontmatter"
    - "@source.body"
    - "@operator"
    - "@local-harness"
    - "@runtime-proof"
    - "@cost-log"
    - "@mcp-gateway"
    - "@tool-provider"
    - "@tool-policy"
    - "@orchestration-graph"
    - "@sandbox-workspace"
    - "@message-gateway"
    - "@human-review"
    - "@canvas"
    - "@approval-gate"
    - "@dev-only"
runtime_pipeline:
  version: "workspace-runtime-pipeline/v1"
  status: "spec-complete"
  source_docs:
    - "docs/knowgrph-agentic-video-canvas-demo.md"
    - "../../knowgrph/README.md"
    - "../../knowgrph/canvas/src/features/chat/chatStoryboardTemplateContract.ts"
    - "../../knowgrph/canvas/src/features/chat/chatStoryboardTemplateProjection.ts"
    - "../../knowgrph/docs/documents/knowgrph-strybldr-prd-tad.md"
  gates:
    hardcode: "Reject repo-stored generated outputs, provider IDs, credentials, stream URLs, and source-specific fixtures."
    cost: "Run /cost.audit before live provider or repeated generation work."
    recompute: "Reuse frontmatter, summaries, manifests, and timeline data before new model or media calls."
    prod_mirror: "Blocked by /deploy.guard and @dev-only until operator instruction."
    cloudflare: "Blocked by /deploy.guard and @dev-only until operator instruction."
  stages:
    - id: "source"
      lane: "Source"
      command: "/source.normalize"
      bindings: ["@source.frontmatter", "@source.body", "@operator"]
      semantics: ["#frontmatter", "#no-hardcode"]
      output: "operator-owned source brief and validation boundary"
      paid_call_count: 0
    - id: "scriptwriting"
      lane: "Scriptwriting"
      command: "/memory.seed"
      bindings: ["@source.frontmatter", "@source.body", "@cost-log"]
      semantics: ["#frontmatter", "#token-economics"]
      output: "source-backed premise, logline, scene outline, and script beats"
      paid_call_count: 0
    - id: "storyboard"
      lane: "Storyboard"
      command: "/canvas.project"
      bindings: ["@canvas", "@runtime-proof"]
      semantics: ["#canvas", "#runtime-ready"]
      output: "frontmatter-owned Storyboard cards and visible flow edges"
      paid_call_count: 0
    - id: "orchestration"
      lane: "Invocation"
      command: "/superagent.run"
      bindings: ["@local-harness", "@orchestration-graph", "@message-gateway", "@cost-log"]
      semantics: ["#harness", "#long-horizon-harness", "#approval-gate"]
      output: "bounded agent plan, tool routes, approvals, and stop conditions"
      paid_call_count: 0
    - id: "generation"
      lane: "Generation"
      command: "/tool.route"
      bindings: ["@tool-provider", "@tool-policy", "@approval-gate", "@runtime-proof"]
      semantics: ["#tool-gateway", "#tool-routing", "#token-economics"]
      output: "local dry-run packet by default; live provider evidence only after approval"
      paid_call_count: 0
    - id: "editing"
      lane: "Editing"
      command: "/runtime-ready.check"
      bindings: ["@runtime-proof", "@cost-log", "@human-review"]
      semantics: ["#runtime-ready", "#human-in-loop", "#token-economics"]
      output: "edit decision list, timeline proof, and review packet without redundant generation"
      paid_call_count: 0
    - id: "validation"
      lane: "Validation"
      command: "/validation.run"
      bindings: ["@runtime-proof", "@dev-only"]
      semantics: ["#runtime-ready", "#dev-only"]
      output: "focused local proof and explicit remaining gates"
      paid_call_count: 0
    - id: "deploy_guard"
      lane: "Publish"
      command: "/deploy.guard"
      bindings: ["@operator", "@dev-only"]
      semantics: ["#approval-gate", "#dev-only"]
      output: "local-only boundary unless Dev -> Prod -> Cloudflare is explicitly opened"
      paid_call_count: 0
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "workspace-source"}
      type: {key: type, type: string, value: "WorkspaceSourceWidget"}
      label: {key: label, type: string, value: "Source"}
      position: {key: position, type: object, value: {"x":-31.491652021089635,"y":-2095.9894002636197}}
      handles: {key: handles, type: object, value: {"source":["workspace_signal_out"]}}
      command: {key: command, type: string, value: "/source.normalize"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{},"out":{"workspace_signal_out":"workspace_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:workspace-source"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      lane: {key: lane, type: string, value: "Source"}
      summary:
        key: summary
        type: string
        value: |
          I and
          ![buddydrone.jpg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ) can ... #storyboard .. /soul.load #runtime, is it better in #storyboard
          
      "visual:height": {key: "visual:height", type: number, value: 758}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:width": {key: "visual:width", type: number, value: 948}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "workspace-runtime"}
      type: {key: type, type: string, value: "RuntimeGateWidget"}
      label: {key: label, type: string, value: "Runtime Gate"}
      position: {key: position, type: object, value: {"x":827.5208912823775,"y":-2486.5137640789203}}
      handles: {key: handles, type: object, value: {"target":["workspace_signal_in"],"source":["workspace_signal_out"]}}
      command: {key: command, type: string, value: "/runtime-ready.check"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"workspace_signal_in":"workspace_signal"},"out":{"workspace_signal_out":"workspace_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:workspace-runtime"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      lane: {key: lane, type: string, value: "Validation"}
      media: {key: media, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      summary:
        key: summary
        type: string
        value: |
          I, 567, 890,
          
          ![buddydrone.jpg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ)
          
          , 123
          
          ![1920s_Singapore_Malaya_202606190937.jpeg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ)
          
          589 and ![buddydrone.jpg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ) can 123 see that #storyboard is as #source interesting as /cost.audit
          
      thumbnailUrl: {key: thumbnailUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      "visual:height": {key: "visual:height", type: number, value: 356}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:width": {key: "visual:width", type: number, value: 701}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "workspace-publish"}
      type: {key: type, type: string, value: "DeployGuardWidget"}
      label: {key: label, type: string, value: "Publish Guard"}
      position: {key: position, type: object, value: {"x":1229.148140328956,"y":-1622.2397972973777}}
      handles: {key: handles, type: object, value: {"target":["workspace_signal_in"]}}
      command: {key: command, type: string, value: "/deploy.guard"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"workspace_signal_in":"workspace_signal"},"out":{}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:workspace-publish"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      lane: {key: lane, type: string, value: "Publish"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "n1"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel"}
      position: {key: position, type: object, value: {"x":1190.746550034281,"y":-2078.3863599146093}}
      audioUrl: {key: audioUrl, type: text, value: ""}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ"}
      imageUrl: {key: imageUrl, type: text, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ"}
      media: {key: media, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaSourceKey: {key: mediaSourceKey, type: string, value: "sha256:170a76238422bb27f5919405cee76d55a665fdb44e0933684872ca745bafbb93"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-170a76238422bb27/image/1920s_singapore_malaya_202606190937-170a76238422bb27.jpeg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0xNzBhNzYyMzg0MjJiYjI3IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ"}
      output: {key: output, type: textarea, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: ""}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "image"}
      videoUrl: {key: videoUrl, type: text, value: ""}
      "visual:height": {key: "visual:height", type: number, value: 769}
      "visual:width": {key: "visual:width", type: number, value: 1367}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
    - id: {key: id, type: string, value: "workspace-source-media-panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "buddydrone.jpg"}
      position: {key: position, type: object, value: {"x":-85.31115531472665,"y":-463.0106782207429}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      imageUrl: {key: imageUrl, type: text, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      media: {key: media, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaSource: {key: mediaSource, type: string, value: "storyboard-card-media-drop"}
      mediaSourceKey: {key: mediaSourceKey, type: string, value: "sha256:730fe6850f0fc26f74a39bfffd1e828c47fbb7086ea09c8118445ef7b943ce96"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      output: {key: output, type: textarea, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: ""}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "image"}
      storyboardCanvasRichMediaPanel: {key: storyboardCanvasRichMediaPanel, type: boolean, value: true}
      storyboardCardMediaSourceKind: {key: storyboardCardMediaSourceKind, type: string, value: "image"}
      storyboardCardMediaTargetId: {key: storyboardCardMediaTargetId, type: string, value: "workspace-source"}
      thumbnailUrl: {key: thumbnailUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
    - id: {key: id, type: string, value: "n7"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Text Widget"}
      position: {key: position, type: object, value: {"x":2339.1341899576832,"y":-2687.4928346756546}}
      chatAuthMode: {key: chatAuthMode, type: text, value: "serverManaged"}
      chatEndpointUrl: {key: chatEndpointUrl, type: text, value: "https://ark.ap-southeast.bytepluses.com/api/v3/chat/completions"}
      chatFrequencyPenalty: {key: chatFrequencyPenalty, type: number, value: 0}
      chatLogitBiasJson: {key: chatLogitBiasJson, type: json, value: ""}
      chatLogprobs: {key: chatLogprobs, type: boolean, value: false}
      chatMaxCompletionTokens: {key: chatMaxCompletionTokens, type: number, value: 1000}
      chatMessagesJson: {key: chatMessagesJson, type: json, value: ""}
      chatModel: {key: chatModel, type: select, value: "seed-2-0-mini-260215"}
      chatParallelToolCalls: {key: chatParallelToolCalls, type: boolean, value: true}
      chatPresencePenalty: {key: chatPresencePenalty, type: number, value: 0}
      chatProvider: {key: chatProvider, type: readonly, value: "byteplus-modelark"}
      chatReasoningEffort: {key: chatReasoningEffort, type: select, value: "medium"}
      chatResponseFormatJson: {key: chatResponseFormatJson, type: json, value: ""}
      chatServiceTier: {key: chatServiceTier, type: text, value: "auto"}
      chatStopJson: {key: chatStopJson, type: json, value: ""}
      chatStream: {key: chatStream, type: boolean, value: true}
      chatStreamOptionsJson: {key: chatStreamOptionsJson, type: json, value: ""}
      chatTemperature: {key: chatTemperature, type: number, value: 0.3}
      chatThinkingJson: {key: chatThinkingJson, type: json, value: ""}
      chatThinkingType: {key: chatThinkingType, type: select, value: "enabled"}
      chatToolChoiceJson: {key: chatToolChoiceJson, type: json, value: ""}
      chatToolsJson: {key: chatToolsJson, type: json, value: ""}
      chatTopLogprobs: {key: chatTopLogprobs, type: number, value: 0}
      chatTopP: {key: chatTopP, type: number, value: 0.7}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output: {key: output, type: textarea, value: ""}
      prompt: {key: prompt, type: textarea, value: "Generate a text response for the active request."}
      title: {key: title, type: string, value: "Text Widget"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "n8"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Text Widget"}
      position: {key: position, type: object, value: {"x":2915.713728494315,"y":-1926.165448820442}}
      chatAuthMode: {key: chatAuthMode, type: text, value: "serverManaged"}
      chatEndpointUrl: {key: chatEndpointUrl, type: text, value: "https://ark.ap-southeast.bytepluses.com/api/v3/chat/completions"}
      chatFrequencyPenalty: {key: chatFrequencyPenalty, type: number, value: 0}
      chatLogitBiasJson: {key: chatLogitBiasJson, type: json, value: ""}
      chatLogprobs: {key: chatLogprobs, type: boolean, value: false}
      chatMaxCompletionTokens: {key: chatMaxCompletionTokens, type: number, value: 1000}
      chatMessagesJson: {key: chatMessagesJson, type: json, value: ""}
      chatModel: {key: chatModel, type: select, value: "seed-2-0-mini-260215"}
      chatParallelToolCalls: {key: chatParallelToolCalls, type: boolean, value: true}
      chatPresencePenalty: {key: chatPresencePenalty, type: number, value: 0}
      chatProvider: {key: chatProvider, type: readonly, value: "byteplus-modelark"}
      chatReasoningEffort: {key: chatReasoningEffort, type: select, value: "medium"}
      chatResponseFormatJson: {key: chatResponseFormatJson, type: json, value: ""}
      chatServiceTier: {key: chatServiceTier, type: text, value: "auto"}
      chatStopJson: {key: chatStopJson, type: json, value: ""}
      chatStream: {key: chatStream, type: boolean, value: true}
      chatStreamOptionsJson: {key: chatStreamOptionsJson, type: json, value: ""}
      chatTemperature: {key: chatTemperature, type: number, value: 0.3}
      chatThinkingJson: {key: chatThinkingJson, type: json, value: ""}
      chatThinkingType: {key: chatThinkingType, type: select, value: "enabled"}
      chatToolChoiceJson: {key: chatToolChoiceJson, type: json, value: ""}
      chatToolsJson: {key: chatToolsJson, type: json, value: ""}
      chatTopLogprobs: {key: chatTopLogprobs, type: number, value: 0}
      chatTopP: {key: chatTopP, type: number, value: 0.7}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output: {key: output, type: textarea, value: ""}
      prompt: {key: prompt, type: textarea, value: "Generate a text response for the active request."}
      title: {key: title, type: string, value: "Text Widget"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
    - id: {key: id, type: string, value: "n9"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Text Widget"}
      position: {key: position, type: object, value: {"x":2241.1481403289563,"y":-428.23979729737766}}
      chatAuthMode: {key: chatAuthMode, type: text, value: "serverManaged"}
      chatEndpointUrl: {key: chatEndpointUrl, type: text, value: "https://ark.ap-southeast.bytepluses.com/api/v3/chat/completions"}
      chatFrequencyPenalty: {key: chatFrequencyPenalty, type: number, value: 0}
      chatLogitBiasJson: {key: chatLogitBiasJson, type: json, value: ""}
      chatLogprobs: {key: chatLogprobs, type: boolean, value: false}
      chatMaxCompletionTokens: {key: chatMaxCompletionTokens, type: number, value: 1000}
      chatMessagesJson: {key: chatMessagesJson, type: json, value: ""}
      chatModel: {key: chatModel, type: select, value: "seed-2-0-mini-260215"}
      chatParallelToolCalls: {key: chatParallelToolCalls, type: boolean, value: true}
      chatPresencePenalty: {key: chatPresencePenalty, type: number, value: 0}
      chatProvider: {key: chatProvider, type: readonly, value: "byteplus-modelark"}
      chatReasoningEffort: {key: chatReasoningEffort, type: select, value: "medium"}
      chatResponseFormatJson: {key: chatResponseFormatJson, type: json, value: ""}
      chatServiceTier: {key: chatServiceTier, type: text, value: "auto"}
      chatStopJson: {key: chatStopJson, type: json, value: ""}
      chatStream: {key: chatStream, type: boolean, value: true}
      chatStreamOptionsJson: {key: chatStreamOptionsJson, type: json, value: ""}
      chatTemperature: {key: chatTemperature, type: number, value: 0.3}
      chatThinkingJson: {key: chatThinkingJson, type: json, value: ""}
      chatThinkingType: {key: chatThinkingType, type: select, value: "enabled"}
      chatToolChoiceJson: {key: chatToolChoiceJson, type: json, value: ""}
      chatToolsJson: {key: chatToolsJson, type: json, value: ""}
      chatTopLogprobs: {key: chatTopLogprobs, type: number, value: 0}
      chatTopP: {key: chatTopP, type: number, value: 0.7}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output: {key: output, type: textarea, value: ""}
      prompt: {key: prompt, type: textarea, value: "Generate a text response for the active request."}
      title: {key: title, type: string, value: "Text Widget"}
      "visual:height": {key: "visual:height", type: number, value: 369}
      "visual:width": {key: "visual:width", type: number, value: 522}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
    - id: {key: id, type: string, value: "n10"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rich Media Panel"}
      position: {key: position, type: object, value: {"x":641.9883390114882,"y":-261.7778854118371}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      freezeConnectedOutput: {key: freezeConnectedOutput, type: boolean, value: true}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output:
        key: output
        type: textarea
        value: |
          i can see
          
          ![空武.jpg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQzfQ)
          
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      "visual:height": {key: "visual:height", type: number, value: 625}
      "visual:width": {key: "visual:width", type: number, value: 1111}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
    - id: {key: id, type: string, value: "workspace-runtime-media-panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "buddydrone.jpg"}
      position: {key: position, type: object, value: {"x":337.14814032895606,"y":-1385.2397972973777}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      imageUrl: {key: imageUrl, type: text, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      media: {key: media, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaSource: {key: mediaSource, type: string, value: "storyboard-card-media-drop"}
      mediaSourceKey: {key: mediaSourceKey, type: string, value: "sha256:730fe6850f0fc26f74a39bfffd1e828c47fbb7086ea09c8118445ef7b943ce96"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      output: {key: output, type: textarea, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: ""}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "image"}
      storyboardCanvasRichMediaPanel: {key: storyboardCanvasRichMediaPanel, type: boolean, value: true}
      storyboardCardMediaSourceKind: {key: storyboardCardMediaSourceKind, type: string, value: "image"}
      storyboardCardMediaTargetId: {key: storyboardCardMediaTargetId, type: string, value: "workspace-runtime"}
      thumbnailUrl: {key: thumbnailUrl, type: string, value: "http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -7}
    - id: {key: id, type: string, value: "n12"}
      type: {key: type, type: string, value: "WorkspaceSourceWidget"}
      label: {key: label, type: string, value: "Source Copy"}
      position: {key: position, type: object, value: {"x":-513.2850651479566,"y":-2675.9490377413813}}
      handles: {key: handles, type: object, value: {"source":["workspace_signal_out"]}}
      command: {key: command, type: string, value: "/source.normalize"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{},"out":{"workspace_signal_out":"workspace_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:workspace-source"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      lane: {key: lane, type: string, value: "Source"}
      summary:
        key: summary
        type: string
        value: |
          I and
          ![buddydrone.jpg](http://127.0.0.1:5174/api/storage/media/airvio/runs/upload-730fe6850f0fc26f/image/buddydrone-730fe6850f0fc26f.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC03MzBmZTY4NTBmMGZjMjZmIiwiZXhwaXJlc0F0IjoxNzg0NDUxMDgyNDQyfQ) can ... #storyboard .. /soul.load #runtime, is it better in #storyboard
          
      title: {key: title, type: string, value: "Source Copy"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "n26"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Widget Card"}
      position: {key: position, type: object, value: {"x":2400,"y":-2700}}
      chatAuthMode: {key: chatAuthMode, type: text, value: "byok"}
      chatEndpointUrl: {key: chatEndpointUrl, type: text, value: "http://127.0.0.1:5199/v1/chat/completions"}
      chatFrequencyPenalty: {key: chatFrequencyPenalty, type: number, value: 0}
      chatLogitBiasJson: {key: chatLogitBiasJson, type: json, value: ""}
      chatLogprobs: {key: chatLogprobs, type: boolean, value: false}
      chatMaxCompletionTokens: {key: chatMaxCompletionTokens, type: number, value: 1000}
      chatMessagesJson: {key: chatMessagesJson, type: json, value: ""}
      chatModel: {key: chatModel, type: select, value: "seed-1-8-251228"}
      chatParallelToolCalls: {key: chatParallelToolCalls, type: boolean, value: true}
      chatPresencePenalty: {key: chatPresencePenalty, type: number, value: 0}
      chatProvider: {key: chatProvider, type: readonly, value: "byteplus-modelark"}
      chatReasoningEffort: {key: chatReasoningEffort, type: select, value: "medium"}
      chatResponseFormatJson: {key: chatResponseFormatJson, type: json, value: ""}
      chatServiceTier: {key: chatServiceTier, type: text, value: "auto"}
      chatStopJson: {key: chatStopJson, type: json, value: ""}
      chatStream: {key: chatStream, type: boolean, value: true}
      chatStreamOptionsJson: {key: chatStreamOptionsJson, type: json, value: ""}
      chatTemperature: {key: chatTemperature, type: number, value: 0.3}
      chatThinkingJson: {key: chatThinkingJson, type: json, value: ""}
      chatThinkingType: {key: chatThinkingType, type: select, value: "enabled"}
      chatToolChoiceJson: {key: chatToolChoiceJson, type: json, value: ""}
      chatToolsJson: {key: chatToolsJson, type: json, value: ""}
      chatTopLogprobs: {key: chatTopLogprobs, type: number, value: 0}
      chatTopP: {key: chatTopP, type: number, value: 0.7}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      output:
        key: output
        type: textarea
        value: |
          # Generated Result

          Malaysia fruit-farm logistics plan with a RM100,000 budget.

          - Month 1 farm-gate setup: RM30,000
          - Monthly refrigerated transport: RM12,000
          - Base revenue: RM28,000 per month
          - Downside revenue: RM20,000 per month
          - Upside revenue: RM36,000 per month
          - Key risks: route disruption, spoilage, and seasonal volume.

      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "seed-1-8-251228"}
      outputPath: {key: outputPath, type: string, value: "/docs/workspace-readme-widget-card-text-output.md"}
      outputSavedName: {key: outputSavedName, type: string, value: "workspace-readme-widget-card-text-output.md"}
      prompt: {key: prompt, type: textarea, value: "Generate a text response for the active request."}
      title: {key: title, type: string, value: "Widget Card"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -9}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -34}
    - id: {key: id, type: string, value: "n27"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Deliverables Widget Card"}
      position: {key: position, type: object, value: {"x":4600,"y":-2700}}
      cardTypeLabel: {key: cardTypeLabel, type: string, value: "Deliverables Widget Card"}
      externalMcpCreateArtifacts: {key: externalMcpCreateArtifacts, type: boolean, value: true}
      externalMcpCreatedCount: {key: externalMcpCreatedCount, type: number, value: 2}
      externalMcpEnabled: {key: externalMcpEnabled, type: boolean, value: true}
      externalMcpErrors: {key: externalMcpErrors, type: array, value: []}
      externalMcpRequired: {key: externalMcpRequired, type: boolean, value: true}
      externalSheetsMcpCapability: {key: externalSheetsMcpCapability, type: string, value: "auto"}
      externalSlidesMcpCapability: {key: externalSlidesMcpCapability, type: string, value: "auto"}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      lastRunAt: {key: lastRunAt, type: string, value: "2026-07-19T01:51:57.408Z"}
      mcpInvocationTokens: {key: mcpInvocationTokens, type: array, value: ["/investment-research-agent","@source.body","#runtime-ready"]}
      mcpInvoked: {key: mcpInvoked, type: boolean, value: true}
      mcpTool: {key: mcpTool, type: string, value: "knowgrph.agentic_canvas_os.docs.invoke"}
      output: {key: output, type: textarea, value: "Generated Slide Deck, Markdown Financial Model, and XLSX workbook with MCP evidence; created 2 external MCP artifacts."}
      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "acceptance-model"}
      prompt:
        key: prompt
        type: textarea
        value: |
          /investment-research-agent @source.body #runtime-ready
          Use the connected Rich Media output as the source of truth.
          Generate a reusable Markdown slide deck and a Markdown financial-model spreadsheet with an XLSX companion workbook.
          Create external Slides and Sheets artifacts through the approved MCP capabilities.
          Keep assumptions explicit and do not invent source facts.

      richMediaDeliverablesMode: {key: richMediaDeliverablesMode, type: boolean, value: true}
      summary: {key: summary, type: string, value: "Connect a Rich Media output to prompt_in, then Run to publish two reusable Markdown panels."}
      tags: {key: tags, type: array, value: ["rich-media","slide-deck","financial-model","mcp"]}
      title: {key: title, type: string, value: "Deliverables Widget Card"}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -11}
      workbookPath: {key: workbookPath, type: string, value: "/docs/workspace-readme-financial-model.xlsx"}
      workbookSha256: {key: workbookSha256, type: string, value: "sha256:68daa7e3f68fe161dd79fd0bb4e821fd04e144e7cec8640f58e1079546a7a01c"}
    - id: {key: id, type: string, value: "n22"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Generated Result"}
      position: {key: position, type: object, value: {"x":3200,"y":-2700}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output:
        key: output
        type: textarea
        value: |
          # Generated Result

          Malaysia fruit-farm logistics plan with a RM100,000 budget.

          - Month 1 farm-gate setup: RM30,000
          - Monthly refrigerated transport: RM12,000
          - Base revenue: RM28,000 per month
          - Downside revenue: RM20,000 per month
          - Upside revenue: RM36,000 per month
          - Key risks: route disruption, spoilage, and seasonal volume.

      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "seed-1-8-251228"}
      outputPath: {key: outputPath, type: string, value: "/docs/workspace-readme-widget-card-text-output.md"}
      outputSavedName: {key: outputSavedName, type: string, value: "workspace-readme-widget-card-text-output.md"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      title: {key: title, type: string, value: "Generated Result"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: -8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -34}
      workflowOutputAnchorNodeId: {key: workflowOutputAnchorNodeId, type: string, value: "n26"}
      workflowOutputEdgeMode: {key: workflowOutputEdgeMode, type: string, value: "manual"}
      workflowOutputKey: {key: workflowOutputKey, type: string, value: "output"}
    - id: {key: id, type: string, value: "n23"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Slide Deck"}
      position: {key: position, type: object, value: {"x":5900,"y":-3300}}
      externalArtifactReceipt: {key: externalArtifactReceipt, type: object, value: {"capabilityId":"kgcap_80735419992395ada90619010e12ffa5","capabilityRevision":"799b4b3c148518c27e58281090a7f8c163015545618bd68f3906563f97c7ec07","artifactKind":"slide-deck","createdAt":"2026-07-19T01:51:54.761Z","externalId":"kg-28976e6da0e8639a3cc7943d4fd3808e6d2ae6717f5fd4de8ab25b217a0ca5de","url":"https://docs.example.com/decks/kg-28976e6da0e8639a3cc7943d4fd3808e6d2ae6717f5fd4de8ab25b217a0ca5de","fileName":"slide-deck.md","mimeType":"application/vnd.example.presentation","summary":"Slide Deck"}}
      externalMcpEnabled: {key: externalMcpEnabled, type: boolean, value: true}
      externalMcpErrors: {key: externalMcpErrors, type: array, value: []}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      freezeConnectedOutput: {key: freezeConnectedOutput, type: boolean, value: true}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      markdownPresentationMode: {key: markdownPresentationMode, type: boolean, value: true}
      mcpInvocationTokens: {key: mcpInvocationTokens, type: array, value: ["/investment-research-agent","@source.body","#runtime-ready"]}
      mcpInvoked: {key: mcpInvoked, type: boolean, value: true}
      mcpTool: {key: mcpTool, type: string, value: "knowgrph.agentic_canvas_os.docs.invoke"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      output:
        key: output
        type: textarea
        value: |
          # Malaysia Fruit-Farm Logistics Investment Case

          RM100,000 launch budget with RM30,000 farm-gate setup and RM12,000 monthly refrigerated transport.

          ---

          # Revenue Scenarios and Risks

          Base RM28,000/month; downside RM20,000/month; upside RM36,000/month. Key risks: route disruption, spoilage, and seasonal volume.
      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "acceptance-model"}
      outputSourceUrl: {key: outputSourceUrl, type: string, value: "https://docs.example.com/decks/kg-28976e6da0e8639a3cc7943d4fd3808e6d2ae6717f5fd4de8ab25b217a0ca5de"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      richMediaDeliverablesMode: {key: richMediaDeliverablesMode, type: boolean, value: true}
      richMediaDeliverablesSourceNodeId: {key: richMediaDeliverablesSourceNodeId, type: string, value: "n22"}
      richMediaDocumentKind: {key: richMediaDocumentKind, type: string, value: "markdown-slide-deck"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -11}
      workflowOutputAnchorNodeId: {key: workflowOutputAnchorNodeId, type: string, value: "n27"}
      workflowOutputKey: {key: workflowOutputKey, type: string, value: "markdown-slide-deck"}
    - id: {key: id, type: string, value: "n28"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Financial Model"}
      position: {key: position, type: object, value: {"x":5900,"y":-2100}}
      externalArtifactReceipt: {key: externalArtifactReceipt, type: object, value: {"capabilityId":"kgcap_14b9a99d50b46334d239af08dd637853","capabilityRevision":"2b02955bb31d061a6fcb55b1dfefd28d9d58b998c0e2070c62ed9bb1cc0c099f","artifactKind":"spreadsheet","createdAt":"2026-07-19T01:51:57.303Z","externalId":"kg-08dc286b8a3d899ff3ee9589e4d359a35e9a4bae1ddac1b1c8ac4c065e14f26d","url":"https://docs.example.com/sheets/kg-08dc286b8a3d899ff3ee9589e4d359a35e9a4bae1ddac1b1c8ac4c065e14f26d","fileName":"workspace-readme-financial-model.xlsx","mimeType":"application/vnd.example.spreadsheet","summary":"Financial Model"}}
      externalMcpEnabled: {key: externalMcpEnabled, type: boolean, value: true}
      externalMcpErrors: {key: externalMcpErrors, type: array, value: []}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      freezeConnectedOutput: {key: freezeConnectedOutput, type: boolean, value: true}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "markdown-table"}
      mcpInvocationTokens: {key: mcpInvocationTokens, type: array, value: ["/investment-research-agent","@source.body","#runtime-ready"]}
      mcpInvoked: {key: mcpInvoked, type: boolean, value: true}
      mcpTool: {key: mcpTool, type: string, value: "knowgrph.agentic_canvas_os.docs.invoke"}
      media_interactive: {key: media_interactive, type: boolean, value: false}
      output:
        key: output
        type: textarea
        value: |-
          | Metric | Base case | Downside | Upside | Source / assumption |
          | ------ | --------- | -------- | ------ | ------------ |
          | Launch budget | RM100,000 | RM100,000 | RM100,000 | Connected Generated Result |
          | Farm-gate setup | RM30,000 | RM30,000 | RM30,000 | Month 1 |
          | Monthly refrigerated transport | RM12,000 | RM12,000 | RM12,000 | Connected Generated Result |
          | Monthly revenue | RM28,000 | RM20,000 | RM36,000 | Connected Generated Result |
          | Key risks | Route disruption; spoilage; seasonal volume | Same | Same | Connected Generated Result |
      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "acceptance-model"}
      outputPath: {key: outputPath, type: string, value: "/docs/workspace-readme-financial-model.xlsx"}
      outputSavedName: {key: outputSavedName, type: string, value: "workspace-readme-financial-model.xlsx"}
      outputSourceUrl: {key: outputSourceUrl, type: string, value: "https://docs.example.com/sheets/kg-08dc286b8a3d899ff3ee9589e4d359a35e9a4bae1ddac1b1c8ac4c065e14f26d"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      richMediaDeliverablesMode: {key: richMediaDeliverablesMode, type: boolean, value: true}
      richMediaDeliverablesSourceNodeId: {key: richMediaDeliverablesSourceNodeId, type: string, value: "n22"}
      richMediaDocumentKind: {key: richMediaDocumentKind, type: string, value: "financial-model-spreadsheet"}
      tableFormat: {key: tableFormat, type: string, value: "markdown-pipe-table"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -11}
      workbookColumnCount: {key: workbookColumnCount, type: number, value: 5}
      workbookDownloadUrl: {key: workbookDownloadUrl, type: string, value: "/__kg_fs_artifact?path=%2Fdocs%2Fworkspace-readme-financial-model.xlsx"}
      workbookFileName: {key: workbookFileName, type: string, value: "workspace-readme-financial-model.xlsx"}
      workbookManifestPath: {key: workbookManifestPath, type: string, value: "/docs/workspace-readme-financial-model.xlsx.manifest.md"}
      workbookMimeType: {key: workbookMimeType, type: string, value: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"}
      workbookPath: {key: workbookPath, type: string, value: "/docs/workspace-readme-financial-model.xlsx"}
      workbookRowCount: {key: workbookRowCount, type: number, value: 5}
      workbookSha256: {key: workbookSha256, type: string, value: "sha256:68daa7e3f68fe161dd79fd0bb4e821fd04e144e7cec8640f58e1079546a7a01c"}
      workbookSheetName: {key: workbookSheetName, type: string, value: "Financial Model"}
      workbookSizeBytes: {key: workbookSizeBytes, type: number, value: 4049}
      workflowOutputAnchorNodeId: {key: workflowOutputAnchorNodeId, type: string, value: "n27"}
      workflowOutputKey: {key: workflowOutputKey, type: string, value: "financial-model-spreadsheet"}
  edges:
    - {"id":"edge_workspace_source_to_runtime","source":"workspace-source","sourceHandle":"workspace_signal_out","target":"workspace-runtime","targetHandle":"workspace_signal_in","type":"workspace_signal"}
    - {"id":"edge_workspace_runtime_to_publish","source":"workspace-runtime","sourceHandle":"workspace_signal_out","target":"workspace-publish","targetHandle":"workspace_signal_in","type":"workspace_signal"}
    - {"id":"e1","source":"workspace-source-media-panel","sourceHandle":"imageUrl","target":"workspace-source","targetHandle":"mediaUrl","label":"linksTo"}
    - {"id":"e3","source":"workspace-runtime-media-panel","sourceHandle":"imageUrl","target":"workspace-runtime","targetHandle":"mediaUrl","label":"linksTo"}
    - {"id":"e2","source":"n22","sourceHandle":"output","target":"n27","targetHandle":"prompt_in","label":"linksTo"}
    - {"id":"workflow-output-ws-caca068a-n27-markdown-slide-deck-n23","source":"n27","sourceHandle":"text_out","target":"n23","targetHandle":"output","label":"markdown-slide-deck"}
    - {"id":"workflow-output-ws-caca068a-n27-financial-model-spreadsheet-n28","source":"n27","sourceHandle":"text_out","target":"n28","targetHandle":"output","label":"financial-model-spreadsheet"}
---

# Knowgrph Workspace README

This README is the local workspace contract for the current Knowgrph lane. It replaces the previous generated Vite HTML capture with source-owned Markdown and YAML frontmatter that can be parsed, diffed, and audited.

The current work stays Dev-only:

- Dev source: `$GITHUB_ROOT/knowgrph`
- Docs target: `$GITHUB_ROOT/huijoohwee/docs`
- Prod mirror: `$GITHUB_ROOT/huijoohwee/content/knowgrph`
- Cloudflare: `airvio.co` and `airvio.co/knowgrph`

Do not deploy to Prod or Cloudflare from this document. Open that lane only after an explicit operator instruction that preserves `Dev -> Prod -> Cloudflare`.

## Source Contract

The source reference is `docs/knowgrph-agentic-video-canvas-demo.md`. That default video-agent seed keeps the imported script as a `workspace:` reference, exposes the editable `/`, `@`, and `#` invocation grammar, and projects provider-returned text, image, audio, and video artifacts through Cards, Widgets, Rich Media Panels, and compact Timeline lanes only after approval.

The active runtime shape is frontmatter-first:

- authored frontmatter and body prose are the SSOT;
- `flow.nodes`, `flow.edges`, and `socket_types` own graph structure;
- `2D Renderer: Storyboard` projects Cards, Widgets, Rich Media Panels, Gantt/Timeline views, and visible connectors from source data;
- runtime outputs stay blank until a returned local or approved live run provides evidence;
- `paid_call_count` remains `0` for the default local dry run;
- `buildScopedGraphSemanticKey`, `canvas:widgetCard`, `CardMediaPreview`, `CardMarkdownPreview`, and `RichMediaPanel` remain shared owners.

## Invocation Grammar

The shared grammar is query-visible and source-owned:

| Prefix | Role | Workspace routes |
|---|---|---|
| `/` | bounded action | `/source.normalize`, `/memory.seed`, `/harness.define`, `/mcp.capabilities`, `/cost.audit`, `/superagent.run`, `/tool.route`, `/canvas.project`, `/runtime-ready.check`, `/validation.run`, `/deploy.guard` |
| `#` | semantic scope | `#frontmatter`, `#harness`, `#token-economics`, `#tool-gateway`, `#tool-routing`, `#long-horizon-harness`, `#runtime-ready`, `#canvas`, `#human-in-loop`, `#approval-gate`, `#dev-only`, `#no-hardcode`, `#no-legacy` |
| `@` | binding surface | `@source.frontmatter`, `@source.body`, `@operator`, `@local-harness`, `@runtime-proof`, `@cost-log`, `@mcp-gateway`, `@tool-provider`, `@tool-policy`, `@orchestration-graph`, `@sandbox-workspace`, `@message-gateway`, `@human-review`, `@canvas`, `@approval-gate`, `@dev-only` |

Do not collapse these into hidden chips, stale aliases, or downstream remaps. Inline card editing, FloatingPanel Chat, Markdown Viewer, and graph-field tooling must preserve the raw `/`, `#`, and `@` query text through blur, rerender, parser reprojection, and Storyboard projection.

## Runtime-Ready Boundary

`spec-complete` means the contract, graph shape, gates, and local proof path are defined. `runtime-ready` requires returned local proof from `/validation.run` or an equivalent focused runtime gate.

Before claiming runtime-ready, verify:

- parser/frontmatter reads this file from byte-zero YAML through the closing fence;
- source routes resolve from the named template and `knowgrph` owners;
- no generated provider IDs, stream URLs, transcripts, data URIs, credentials, or output artifacts are committed;
- live provider calls are blocked until `@operator` approval;
- repeated generation is blocked when timeline edits, cached summaries, or existing manifests are enough;
- icon wrappers used by selectable controls remain visible to selection tooling and are not hidden as decorative `aria-hidden` surfaces;
- semantic HTML projections use `main`, `section`, `article`, `header`, `nav`, `aside`, `figure`, `figcaption`, and `table` before generic layout wrappers.

## Validation

Focused local checks for this README:

```bash
DOC=$GITHUB_ROOT/huijoohwee/docs/workspace-readme.md
ruby -e 'require "yaml"; text = File.read(ENV.fetch("DOC")); abort("missing byte-zero fence") unless text.start_with?("---\n"); YAML.safe_load(text.split(/^---\s*$/)[1], permitted_classes: [], aliases: true); puts "workspace-readme frontmatter ok"'
ruby -e 'text = File.read(ENV.fetch("DOC")); deny = ["data:" + "image", "<" + "script", "/@" + "vite", "VIDEODB" + "_API_KEY", "SENSENOVA" + "_API_KEY"]; deny += %w[provider_job_id stream_url generated_asset_url].map { |key| /#{key}: "[^"]+"/ }; hits = deny.flat_map { |item| item.is_a?(Regexp) ? text.scan(item).map(&:to_s) : (text.include?(item) ? [item] : []) }; abort(hits.uniq.join("\n")) unless hits.empty?; puts "workspace-readme hardcode scan ok"'
git -C $GITHUB_ROOT/huijoohwee diff --check -- docs/workspace-readme.md
```

The operator-declared docs-control path `$GITHUB_ROOT/huijoohwee/agentic-os-docs` was not present in this workspace on 2026-07-09. Verify the correct control-surface path before treating docs dictionaries as current runtime evidence.

## Cleanup Rules

- Remove stale generated captures at the source; do not stack aliases or compatibility shims.
- Keep generated `chat-log` or proof artifacts as evidence only; fix upstream routing or finalization instead of editing artifacts.
- Do not mirror to Prod, mutate Cloudflare, or publish external output from this README.
- Keep runtime-owned fields blank until returned evidence exists.
- Update sibling docs and API notes only when the shared owner changes, then prove the exact changed surface.

SMOKE_REMOTE_APPLY_MARKER_20260718T055931609Z

SMOKE_REMOTE_APPLY_MARKER_20260718T060126511Z

SMOKE_REMOTE_APPLY_MARKER_20260718T060509913Z

SMOKE_REMOTE_APPLY_MARKER_20260718T072055950Z

SMOKE_REMOTE_APPLY_MARKER_20260718T093559115Z

SMOKE_REMOTE_APPLY_MARKER_20260718T100938137Z

SMOKE_REMOTE_APPLY_MARKER_20260718T130246749Z

SMOKE_REMOTE_APPLY_MARKER_20260718T183328376Z

SMOKE_REMOTE_APPLY_MARKER_20260718T190001878Z
938137Z

SMOKE_REMOTE_APPLY_MARKER_20260718T130246749Z

SMOKE_REMOTE_APPLY_MARKER_20260718T183328376Z

SMOKE_REMOTE_APPLY_MARKER_20260718T190001878Z

SMOKE_REMOTE_APPLY_MARKER_20260719T074006893Z

SMOKE_REMOTE_APPLY_MARKER_20260719T083558412Z
