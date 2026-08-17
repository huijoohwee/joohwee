---
title: "Knowgrph Vdeoxpln Demo - Interactive Visual Explanation"
schema: "kgc-computing-flow/v1"
graphId: "md:knowgrph-vdeoxpln-demo-interactive-visual-explanation"
doc_type: "Knowgrph Vdeoxpln Demo"
date: "2026-05-31"
lang: "en-US"
implementation_contract: "docs/documents/knowgrph-vdeoxpln-prd-tad.md"
source_truth: "canvas/src/features/agent-ready/knowgrphVdeoxplnContract.mjs"
validation_input_forbid_hardcode_in_repo: true
copyhardcode_forbid: true
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgVideoSequenceTimeline: true
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgAutoSaveEnabled: true
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
kgMultiDimTableModeEnabled: false
kgDocumentStructureBaselineLock: false
canvasWorkspacePreset:
  canvasSurfaceMode: "2d"
  canvasRenderMode: "2d"
  canvas2dRenderer: "storyboard"
  documentSemanticMode: "document"
  frontmatterModeEnabled: true
  multiDimTableModeEnabled: false
  documentStructureBaselineLock: false
  videoSequenceTimelineEnabled: true
local_file_import_contract:
  - "Toolbar -> Launch -> Import local files"
  - "Select this Markdown document as validation input"
  - "Local import opens the 2D Storyboard renderer"
  - "Canvas View Mode reports Storyboard"
  - "AI Showrunner dry-run brief is runnable through local MCP start_run with zero paid calls"
  - "AI Showrunner artifacts include run state, cost log, narration manifest, and artifact manifest"
  - "Storyboard Widget exposes a dependency-free video-agent Render_Spec for the YouTube test URL set while the primary rendered validation URL remains https://youtu.be/8NkwH29Ou1o"
  - "The video-agent graph demonstrates ingest, parse, annotate, dataset load/split/merge/save, real-time zone counting, search, edit, compile, generate, and stream stages without copying external code or depending on Roboflow/supervision"
  - "Storyboard Widget exposes an HTML Video Renderer node with a complete animated HTML/CSS/data Render_Spec"
  - "HTML Video Renderer uses engine_hint=canvas-2d for browser-native MP4 smoke rendering without a system FFmpeg install"
  - "Run all writes a video/mp4 artifact and manifest through shared rich-media output owners when the selected runtime can encode video"
  - "Run all publishes the same parsed HTML/CSS/data as an inline preview when the browser lacks MediaRecorder, canvas captureStream, or WebCodecs"
  - "Video agent frame-by-frame bounding-box analysis is visible in both the streamed Rich Media preview and a separate Rich Media analysis panel"
  - "Video agent frame boxes load into a native visual annotation dataset that supports deterministic split, merge, save, and frame-ordered zone counting"
  - "BottomPanel Timeline FBF clips show frame-by-frame image thumbnails synchronized with video-agent bounding-box tracks"
  - "Toolbar -> Launch -> Import URL exposes user-configurable video-agent validation document path, test URL set controls, and per-URL selection"
  - "Rich Media Panel exposes the generated HTML-to-MP4 artifact or inline preview without stale runtime state in this source document"
  - "FloatingPanel Media exposes image/video ingestion, parsed media metadata, annotation JSON, and rendered preview outputs from the same source-owned flow"
  - "Visual Annotation Engine nodes validate Annotation_Spec input, resolve registered model identifiers at runtime, and materialize LLM-ready JSON through shared rich-media output owners"
  - "Image object_detection output renders labelled normalized bounding boxes over the source image preview in FloatingPanel Media"
  - "Design FloatingPanel Video exposes workspace files, compositions, assets, timeline lanes, and Render MP4"
  - "Design BottomPanel Timeline exposes source-derived design video tracks instead of the generic empty Mermaid prompt"
aiShowrunnerRuntimeContract:
  schema: "knowgrph-showrunner-brief/v1"
  localMcpTool: "knowgrph.showrunner.start_run"
  mode: "dry-run"
  paidCallCount: 0
  sourceTruth:
    - "canvas/src/features/ai-showrunner"
    - "mcp/showrunner-runtime.js"
    - "mcp/local-tool-contract.js"
    - "canvas/src/features/agent-ready/knowgrphVdeoxplnContract.mjs"
  artifactPaths:
    - "showrunner/briefs/<run_id>/brief.md"
    - "showrunner/runs/<run_id>/state.json"
    - "showrunner/runs/<run_id>/cost-log.jsonl"
    - "showrunner/runs/<run_id>/narration-manifest.md"
    - "showrunner/runs/<run_id>/manifest.md"
htmlVideoRendererRuntimeContract:
  schema: "knowgrph-html-video-renderer/v1"
  nodeTypeId: "HtmlVideoRenderer"
  formId: "htmlVideoRenderer"
  localMcpTool: "knowgrph.html_video.render"
  recommendedDevProdEngine: "canvas-2d"
  noSystemFfmpegRequired: true
  outputMimeType: "video/mp4"
  sourceTruth:
    - "canvas/src/features/html-video-renderer/htmlVideoRendererSsot.ts"
    - "canvas/src/features/html-video-renderer/htmlVideoRendererSpec.ts"
    - "canvas/src/features/html-video-renderer/htmlVideoEngineRegistry.ts"
    - "canvas/src/features/html-video-renderer/htmlVideoFlowNode.ts"
    - "canvas/src/features/html-video-renderer/htmlVideoWidget.ts"
    - "canvas/src/features/html-video-renderer/engines/canvas2dAdapter.ts"
    - "canvas/src/features/chat/richMediaRun.ts"
  renderSpec:
    html: "properties.html"
    css: "properties.css"
    data: "properties.data_json"
    durationMs: "properties.duration_ms"
    fps: "properties.fps"
    width: "properties.width"
    height: "properties.height"
    engineHint: "properties.engine_hint"
  acceptance:
    - "engine adapters are independent loadable modules"
    - "no hardcoded fallback engine is used when the selected engine is missing"
    - "canvas-2d produces a real MP4 in browser runtimes without installing ffmpeg"
    - "headless-browser remains available for operator-provided FFmpeg runtimes"
    - "unsupported browser encoders publish a runnable HTML preview through outputSrcDoc instead of leaving the panel empty"
videoAgentRuntimeContract:
  schema: "knowgrph-video-agent/v1"
  inspiration: "Roboflow/supervision-inspired visual annotation, dataset, and zone-counting workflow"
  operatorConfig:
    validationDocPathSource: "Toolbar Launch Import URL video-agent validation config"
    validationUrlsSource: "Toolbar Launch Import URL video-agent validation config"
    storageKey: "knowgrph:video-agent:validation-config:v1"
    envDocPathKey: "VITE_KNOWGRPH_VIDEO_AGENT_VALIDATION_DOC_PATH"
    envUrlsKey: "VITE_KNOWGRPH_VIDEO_AGENT_VALIDATION_URLS"
  referenceBoundary:
    kind: "inspiration-only"
    implementation: "native-knowgrph"
    copyPolicy: "no-external-code-copy"
    dependencyPolicy: "no-external-video-agent-runtime"
    runtimeDependency: false
  dependencyPolicy:
    - "no copied external annotation code"
    - "no Roboflow/supervision runtime dependency"
    - "no external API key requirement"
    - "test URL is source-owned validation input only"
  testUrl: "https://youtu.be/8NkwH29Ou1o"
  testUrls:
    - "https://youtu.be/8NkwH29Ou1o"
    - "https://youtu.be/77FAnT935IE"
  sourceId: "youtube:8NkwH29Ou1o"
  sourceIds:
    - "youtube:8NkwH29Ou1o"
    - "youtube:77FAnT935IE"
  capabilities:
    - "ingest"
    - "parse"
    - "annotate"
    - "dataset"
    - "zone_count"
    - "search"
    - "edit"
    - "compile"
    - "generate"
    - "stream"
  pipelinePhases:
    - "ingestion"
    - "parsing"
    - "rendering"
  agentStages:
    - "source_intake"
    - "video_parser"
    - "frame_annotator"
    - "dataset_builder"
    - "zone_counter"
    - "moment_searcher"
    - "edit_planner"
    - "timeline_compiler"
    - "generation_router"
    - "stream_publisher"
  reasoningArtifacts:
    - "search evidence windows"
    - "edit decision plan"
    - "compiled timeline manifest"
    - "visual annotation dataset artifact"
    - "real-time zone counting timeline"
    - "generation placeholder manifest"
    - "instant stream manifest"
  datasetOperations:
    - "load"
    - "split"
    - "merge"
    - "save"
    - "count_zones"
  streamPanels:
    - "Rendered MP4 Artifact"
    - "Video Agent Frame Analysis"
    - "FloatingPanel Media Annotation Outputs"
  frameBoundingBoxes:
    - {frameIndex: 0, timestampMs: 0, label: "tracked subject", bbox: [0.13, 0.18, 0.34, 0.30], confidence: 0.82}
    - {frameIndex: 1, timestampMs: 700, label: "context object", bbox: [0.15, 0.23, 0.334, 0.304], confidence: 0.83}
    - {frameIndex: 2, timestampMs: 1400, label: "tracked subject", bbox: [0.17, 0.18, 0.329, 0.309], confidence: 0.84}
    - {frameIndex: 3, timestampMs: 2100, label: "context object", bbox: [0.19, 0.23, 0.323, 0.313], confidence: 0.85}
    - {frameIndex: 4, timestampMs: 2800, label: "tracked subject", bbox: [0.21, 0.18, 0.318, 0.318], confidence: 0.86}
    - {frameIndex: 5, timestampMs: 3500, label: "context object", bbox: [0.23, 0.23, 0.312, 0.322], confidence: 0.86}
    - {frameIndex: 6, timestampMs: 4200, label: "tracked subject", bbox: [0.25, 0.18, 0.307, 0.327], confidence: 0.87}
    - {frameIndex: 7, timestampMs: 4900, label: "context object", bbox: [0.27, 0.23, 0.301, 0.331], confidence: 0.88}
    - {frameIndex: 8, timestampMs: 5600, label: "tracked subject", bbox: [0.29, 0.18, 0.296, 0.336], confidence: 0.89}
    - {frameIndex: 9, timestampMs: 6300, label: "context object", bbox: [0.31, 0.23, 0.29, 0.34], confidence: 0.90}
  sourceTruth:
    - "canvas/src/features/video-agent/videoAgentPipeline.ts"
    - "canvas/src/features/video-agent/videoAgentDatasetRuntime.ts"
    - "canvas/src/features/video-agent/videoAgentDatasetProjection.ts"
    - "canvas/src/features/video-agent/VideoAgentValidationImportControls.tsx"
    - "canvas/src/features/html-video-renderer/htmlVideoRendererSpec.ts"
    - "canvas/src/features/html-video-renderer/htmlVideoFlowNode.ts"
    - "canvas/src/features/visual-annotation-engine/annotationDataset.ts"
    - "canvas/src/features/visual-annotation-engine/annotationFlowNode.ts"
    - "canvas/src/features/chat/richMediaRun.ts"
    - "canvas/src/lib/graph/semanticKey.ts"
  outputBoundary:
    - "HTML/CSS/data Render_Spec is the source-owned program"
    - "video/mp4, outputSrcDoc, renderJobId, and manifests are runtime outputs"
    - "RichMediaPanel receives streamable artifact output through explicit frontmatter-flow edges"
    - "frame-by-frame bounding boxes are routed to multiple RichMediaPanel surfaces as visible overlays"
    - "frameByFrameSamples expose sample ids, annotation counts, per-frame zone counts, and cumulative zone counts derived from frameBoundingBoxes"
    - "richMediaPanels expose stream, frame-analysis, and floatingpanel-annotation routes from the same Render_Spec timeline clock"
    - "visualDataset, mergedVisualDataset, datasetSplitSummary, datasetOperationSummary, savedDatasetArtifact, and zoneCounting are Render_Spec data outputs derived from frameBoundingBoxes"
    - "BottomPanel Timeline FBF lane renders frame-by-frame-image thumbnails from /__video_frame source-frame evidence derived from the runtime source URL"
    - "source document stores no generated blob URLs, output paths, or run identifiers"
visualAnnotationRuntimeContract:
  schema: "knowgrph-annotation/v1"
  nodeTypeId: "AnnotationEngine"
  formId: "annotationEngine"
  localMcpTools:
    - "knowgrph.annotate.image"
    - "knowgrph.annotate.video_frame"
  annotationTasks:
    - "caption"
    - "object_detection"
    - "dense_region_caption"
  runtimeBoundary:
    - "Annotation_Spec validation happens before worker dispatch"
    - "modelHint overrides KNOWGRPH_ANNOTATION_MODEL only when it resolves to ANNOTATION_MODEL_IDS"
    - "image and video-frame annotation outputs use buildScopedGraphSemanticKey with assetUrl, modelId, and sortedTasks"
    - "annotation JSON is routed through writeRichMediaWidgetRunOutputArtifact; no parallel storage or canvas-apply path is introduced"
    - "annotation datasets load from Annotation_Result or frame-box arrays, then split, merge, save, and count zones through annotationDataset.ts"
  boundingBoxProjection:
    sourcePath: "tasks.object_detection.objects"
    boxFormat: "[x, y, width, height]"
    coordinateSpace: "normalized-0-to-1"
    clampToMediaBounds: true
    fields:
      - "label"
      - "bbox"
      - "confidence"
    rendering:
      - "project boxes against the image content rectangle after object-fit layout"
      - "preserve source coordinates during panel resize and zoom"
      - "render semantic labels without mutating annotation JSON"
  floatingPanelMedia:
    tab: "Media"
    accepts:
      - "image asset preview"
      - "video asset preview"
      - "annotation result JSON"
      - "image bounding-box overlay"
      - "rendered preview artifact"
  sourceTruth:
    - "canvas/src/features/visual-annotation-engine/annotationEngineSsot.ts"
    - "canvas/src/features/visual-annotation-engine/annotationDataset.ts"
    - "canvas/src/features/visual-annotation-engine/annotationSpec.ts"
    - "canvas/src/features/visual-annotation-engine/annotationOrchestrator.ts"
    - "canvas/src/features/visual-annotation-engine/annotationSerializers.ts"
    - "canvas/src/features/visual-annotation-engine/annotationFlowNode.ts"
    - "canvas/src/features/visual-annotation-engine/annotationMcpTools.ts"
    - "canvas/src/features/chat/richMediaRun.ts"
designAgentVideoWorkspaceContract:
  schema: "knowgrph-design-agent-video/v1"
  floatingPanel:
    - "Workspace files"
    - "Compositions"
    - "Assets"
    - "Timeline lanes"
    - "Render MP4"
  bottomPanel:
    tab: "timeline"
    view: "designTimeline"
    trackSource: "active Design graph through designAgentVideoSpec"
  artifactShape:
    - "semantic HTML with data-composition-id"
    - "per-track data-start data-duration data-track-index markers"
    - "virtual workspace files"
    - "composition rows"
    - "source-derived assets"
    - "timeline lanes and ticks"
kgCanvas2dRenderer: "storyboard"
kgWorkflowManagerModeEnabled: true
socket_types:
  html_video_spec: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [html_video_spec]}
  html_video_artifact: {color: "#0ea5e9", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [html_video_artifact]}
  visual_media_asset: {color: "#22c55e", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [visual_media_asset]}
  annotation_json: {color: "#a855f7", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [annotation_json]}
  rich_media_inline_html: {color: "#f59e0b", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [rich_media_inline_html, html_video_artifact]}
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "html_video_source_spec"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "Programmatic Video Agent Render Spec"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      handles: {key: handles, type: object, value: {"source":["html","css","data_json","frameBoundingBoxes"]}}
      css:
        key: css
        type: css
        value: |
          main{width:100%;height:100%;box-sizing:border-box;display:grid;grid-template-rows:auto 1fr auto;gap:14px;padding:18px;font-family:Inter,system-ui,sans-serif;background:#07111f;color:#f8fafc;overflow:hidden}p,h1,h2,h3{margin:0}.hero{display:grid;grid-template-columns:1fr auto;gap:12px;align-items:start}.eyebrow{color:#5eead4;font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.08em}.hero h1{font-size:30px;line-height:1.05;letter-spacing:0}.lede{max-width:740px;color:#cbd5e1;font-size:13px;line-height:1.45}.chip{border:1px solid #334155;background:#0f172a;color:#e2e8f0;border-radius:8px;padding:8px 10px;font:12px ui-monospace,SFMono-Regular,Menlo,monospace}.stage{display:grid;grid-template-columns:1.08fr 1fr;gap:12px;min-height:0}.source,.reasoning,.stream{min-width:0;border:1px solid #334155;border-radius:8px;background:#0f172a;box-shadow:0 18px 40px rgba(0,0,0,.28);overflow:hidden}.source{display:grid;grid-template-rows:auto 1fr}.bar{display:grid;grid-template-columns:auto 1fr auto;gap:8px;align-items:center;padding:8px 10px;border-bottom:1px solid #334155;background:#111827}.dot{width:8px;height:8px;border-radius:50%;background:#06b6d4;box-shadow:14px 0 #22c55e,28px 0 #f59e0b}.url{font:12px ui-monospace,SFMono-Regular,Menlo,monospace;color:#cbd5e1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.badge{font-size:11px;color:#5eead4}.video-card{display:grid;gap:12px;padding:14px}.thumbnail{position:relative;aspect-ratio:16/9;border:1px solid #334155;border-radius:8px;background:linear-gradient(135deg,#123456,#0b1220 55%,#0f766e);overflow:hidden}.thumbnail::before{content:"";position:absolute;inset:14% 18%;border:2px solid rgba(94,234,212,.72);border-radius:8px}.thumbnail::after{content:"";position:absolute;left:12%;right:12%;bottom:16%;height:6px;border-radius:999px;background:#5eead4;transform-origin:left;animation:kgProgress 7s linear infinite}.thumbnail-source{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.72}.frame-boxes{position:absolute;inset:0;pointer-events:none}.frame-box{position:absolute;border:2px solid #fbbf24;border-radius:6px;background:rgba(251,191,36,.08);box-shadow:0 0 0 1px rgba(15,23,42,.7);animation:kgFrameBox 7s steps(5,end) infinite both}.frame-box span{position:absolute;left:0;top:-18px;border-radius:4px;background:#fbbf24;color:#1f2937;padding:2px 5px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;white-space:nowrap}.video-card h2{font-size:20px}.video-card p{color:#cbd5e1;font-size:12px;line-height:1.45}.tasks{display:grid;grid-template-columns:repeat(5,1fr);gap:7px}.tasks li{list-style:none;border:1px solid #334155;border-radius:8px;padding:8px;background:#111827;color:#e2e8f0;font-size:11px;text-align:center}.reasoning{display:grid;grid-template-rows:auto 1fr}.reasoning header{padding:12px;border-bottom:1px solid #334155}.reasoning h2{font-size:18px}.agents{display:grid;gap:8px;padding:12px}.agents li{list-style:none;display:grid;grid-template-columns:auto 1fr auto;gap:9px;align-items:center;border:1px solid #334155;border-radius:8px;padding:9px;background:#0b1220;transform:translateX(18px);opacity:.18;animation:kgStep .7s ease-out both}.agents li:nth-child(1){animation-delay:.1s}.agents li:nth-child(2){animation-delay:.28s}.agents li:nth-child(3){animation-delay:.46s}.agents li:nth-child(4){animation-delay:.64s}.agents li:nth-child(5){animation-delay:.82s}.agents li:nth-child(6){animation-delay:1s}.num{display:grid;place-items:center;width:26px;height:26px;border-radius:50%;background:#5eead4;color:#042f2e;font-weight:800;font-size:12px}.agents span{font-size:12px;color:#e2e8f0}.agents output{font:11px ui-monospace,SFMono-Regular,Menlo,monospace;color:#93c5fd}.timeline{display:grid;gap:8px;border-top:1px solid #334155;padding-top:10px}.rail{height:8px;border-radius:999px;background:#1f2937;overflow:hidden}.rail::before{content:"";display:block;height:100%;width:100%;background:#5eead4;transform-origin:left;animation:kgProgress 7s linear infinite}.ticks{display:grid;grid-template-columns:repeat(7,1fr);gap:7px}.ticks li{list-style:none;color:#94a3b8;font-size:10px}.ticks strong{display:block;color:#f8fafc;font-size:11px}.stream{display:grid;grid-template-columns:auto 1fr;gap:10px;align-items:center;padding:10px}.stream strong{font-size:13px}.stream p{color:#cbd5e1;font-size:12px;line-height:1.4}.trace{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:8px;min-height:0}.trace article{border:1px solid #334155;border-radius:8px;background:#111827;padding:9px;min-width:0}.trace h3{font-size:12px;color:#5eead4}.trace p{font-size:11px;color:#cbd5e1;line-height:1.35}.trace output{display:block;margin-top:6px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;color:#93c5fd;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}@keyframes kgStep{to{opacity:1;transform:translateX(0)}}@keyframes kgProgress{from{transform:scaleX(0)}to{transform:scaleX(1)}}@keyframes kgFrameBox{0%,19%{opacity:1}20%,100%{opacity:.22}}
          
      data_json: {key: data_json, type: json, value: "{\"title\":\"Knowgrph Video Agent Demo\",\"engine\":\"canvas-2d\",\"rasterizer\":\"html2canvas\",\"output\":\"video/mp4\",\"referencePattern\":\"visual-annotation-inspired video workflow; no copied code and no external dependency\",\"composition\":{\"id\":\"knowgrph-video-agent-youtube-demo\",\"durationMs\":7000,\"fps\":24,\"width\":1280,\"height\":720},\"sourceVideo\":{\"url\":\"https://youtu.be/8NkwH29Ou1o\",\"testUrls\":[\"https://youtu.be/8NkwH29Ou1o\",\"https://youtu.be/77FAnT935IE\"],\"sourceId\":\"youtube:8NkwH29Ou1o\",\"sourceIds\":[\"youtube:8NkwH29Ou1o\",\"youtube:77FAnT935IE\"],\"ingestMode\":\"operator-supplied-test-url\",\"externalDependency\":false},\"agentIntent\":\"reason through complex video tasks: search, editing, compilation, generation, and streaming\",\"capabilities\":[\"ingest\",\"parse\",\"annotate\",\"dataset\",\"zone_count\",\"search\",\"edit\",\"compile\",\"generate\",\"stream\"],\"agents\":[{\"id\":\"source_intake\",\"role\":\"ingest\",\"output\":\"source key and media manifest\"},{\"id\":\"video_parser\",\"role\":\"parse\",\"output\":\"transcript, frame labels, annotation tasks\"},{\"id\":\"moment_searcher\",\"role\":\"search\",\"output\":\"ranked evidence windows\"},{\"id\":\"edit_planner\",\"role\":\"edit\",\"output\":\"clip ranges, overlays, subtitles, pacing\"},{\"id\":\"timeline_compiler\",\"role\":\"compile\",\"output\":\"timeline manifest and render spec\"},{\"id\":\"generation_router\",\"role\":\"generate\",\"output\":\"generated overlay or narration placeholders\"},{\"id\":\"stream_publisher\",\"role\":\"stream\",\"output\":\"videoUrl or outputSrcDoc rich-media payload\"}],\"reasoningArtifacts\":[{\"capability\":\"search\",\"task\":\"Search transcript, frame, and annotation evidence\",\"decision\":\"Rank reusable evidence windows without a provider-specific search API\",\"outputArtifact\":\"video-agent/moments.json\",\"streamSignal\":\"moments-ready\"},{\"capability\":\"edit\",\"task\":\"Plan clips, overlays, subtitles, and pacing\",\"decision\":\"Store edit decisions as timeline data\",\"outputArtifact\":\"video-agent/edit-plan.json\",\"streamSignal\":\"edit-ready\"},{\"capability\":\"compile\",\"task\":\"Compile the selected moments into Render_Spec output\",\"decision\":\"Reuse the existing HTML Video Renderer path\",\"outputArtifact\":\"video-agent/render.html\",\"streamSignal\":\"render-spec-ready\"},{\"capability\":\"generate\",\"task\":\"Plan generated overlays and narration placeholders\",\"decision\":\"Defer live generation to optional local tools\",\"outputArtifact\":\"video-agent/generated-assets.json\",\"streamSignal\":\"generation-plan-ready\"},{\"capability\":\"stream\",\"task\":\"Publish the compiled result immediately\",\"decision\":\"Prefer video/mp4 and preserve outputSrcDoc fallback\",\"outputArtifact\":\"video-agent/stream-manifest.json\",\"streamSignal\":\"stream-ready\"}],\"workspaceFiles\":[{\"path\":\"video-agent/source.json\",\"kind\":\"json\",\"role\":\"source-manifest\"},{\"path\":\"video-agent/parse.json\",\"kind\":\"json\",\"role\":\"parse-output\"},{\"path\":\"video-agent/moments.json\",\"kind\":\"json\",\"role\":\"search-index\"},{\"path\":\"video-agent/timeline.json\",\"kind\":\"json\",\"role\":\"edit-plan\"},{\"path\":\"video-agent/generated-assets.json\",\"kind\":\"json\",\"role\":\"generation-plan\"},{\"path\":\"video-agent/frame-boxes.json\",\"kind\":\"json\",\"role\":\"frame-bounding-boxes\"},{\"path\":\"video-agent/render.html\",\"kind\":\"html\",\"role\":\"composition\"},{\"path\":\"video-agent/stream-manifest.json\",\"kind\":\"json\",\"role\":\"stream-output\"}],\"timelineTracks\":[{\"id\":\"ingest\",\"label\":\"Ingest test URL\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":900,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"parse\",\"label\":\"Parse multimodal context\",\"trackIndex\":1,\"startMs\":900,\"durationMs\":1100,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"search\",\"label\":\"Search relevant moments\",\"trackIndex\":2,\"startMs\":2000,\"durationMs\":1000,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"edit\",\"label\":\"Plan clips and overlays\",\"trackIndex\":3,\"startMs\":3000,\"durationMs\":1200,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"compile\",\"label\":\"Compile timeline\",\"trackIndex\":4,\"startMs\":4200,\"durationMs\":1200,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"generate\",\"label\":\"Generate assets\",\"trackIndex\":5,\"startMs\":5400,\"durationMs\":1000,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"stream\",\"label\":\"Publish stream\",\"trackIndex\":6,\"startMs\":6400,\"durationMs\":600,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"frame_box_0_fbf\",\"label\":\"Frame-by-frame bbox 0.0s tracked subject\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.82 [0.13, 0.18, 0.34, 0.3]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82,\"frameIndex\":0},{\"id\":\"frame_box_1_fbf\",\"label\":\"Frame-by-frame bbox 0.7s context object\",\"trackIndex\":1,\"startMs\":700,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.83 [0.15, 0.23, 0.334, 0.304]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83,\"frameIndex\":1},{\"id\":\"frame_box_2_fbf\",\"label\":\"Frame-by-frame bbox 1.4s tracked subject\",\"trackIndex\":2,\"startMs\":1400,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.84 [0.17, 0.18, 0.329, 0.309]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84,\"frameIndex\":2},{\"id\":\"frame_box_3_fbf\",\"label\":\"Frame-by-frame bbox 2.1s context object\",\"trackIndex\":3,\"startMs\":2100,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.85 [0.19, 0.23, 0.323, 0.313]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85,\"frameIndex\":3},{\"id\":\"frame_box_4_fbf\",\"label\":\"Frame-by-frame bbox 2.8s tracked subject\",\"trackIndex\":4,\"startMs\":2800,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.86 [0.21, 0.18, 0.318, 0.318]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86,\"frameIndex\":4},{\"id\":\"frame_box_5_fbf\",\"label\":\"Frame-by-frame bbox 3.5s context object\",\"trackIndex\":5,\"startMs\":3500,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.86 [0.23, 0.23, 0.312, 0.322]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86,\"frameIndex\":5},{\"id\":\"frame_box_6_fbf\",\"label\":\"Frame-by-frame bbox 4.2s tracked subject\",\"trackIndex\":6,\"startMs\":4200,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.87 [0.25, 0.18, 0.307, 0.327]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87,\"frameIndex\":6},{\"id\":\"frame_box_7_fbf\",\"label\":\"Frame-by-frame bbox 4.9s context object\",\"trackIndex\":7,\"startMs\":4900,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.88 [0.27, 0.23, 0.301, 0.331]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88,\"frameIndex\":7},{\"id\":\"frame_box_8_fbf\",\"label\":\"Frame-by-frame bbox 5.6s tracked subject\",\"trackIndex\":8,\"startMs\":5600,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.89 [0.29, 0.18, 0.296, 0.336]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89,\"frameIndex\":8},{\"id\":\"frame_box_9_fbf\",\"label\":\"Frame-by-frame bbox 6.3s context object\",\"trackIndex\":9,\"startMs\":6300,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.90 [0.31, 0.23, 0.29, 0.34]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9,\"frameIndex\":9}],\"streaming\":{\"primary\":\"video/mp4\",\"fallback\":\"outputSrcDoc\",\"panel\":\"RichMediaPanel\",\"panels\":[\"RichMediaPanel:stream\",\"RichMediaPanel:frame-analysis\",\"RichMediaPanel:floatingpanel-annotation\"]},\"safeguards\":[\"no copied external annotation code\",\"no Roboflow/supervision runtime dependency\",\"no API key requirement\",\"source document stores no generated blob URLs\"],\"frameBoundingBoxes\":[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}],\"frameBoundingBoxTimelineTracks\":[{\"id\":\"frame_box_0_fbf\",\"label\":\"Frame-by-frame bbox 0.0s tracked subject\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.82 [0.13, 0.18, 0.34, 0.3]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82,\"frameIndex\":0},{\"id\":\"frame_box_1_fbf\",\"label\":\"Frame-by-frame bbox 0.7s context object\",\"trackIndex\":1,\"startMs\":700,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.83 [0.15, 0.23, 0.334, 0.304]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83,\"frameIndex\":1},{\"id\":\"frame_box_2_fbf\",\"label\":\"Frame-by-frame bbox 1.4s tracked subject\",\"trackIndex\":2,\"startMs\":1400,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.84 [0.17, 0.18, 0.329, 0.309]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84,\"frameIndex\":2},{\"id\":\"frame_box_3_fbf\",\"label\":\"Frame-by-frame bbox 2.1s context object\",\"trackIndex\":3,\"startMs\":2100,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.85 [0.19, 0.23, 0.323, 0.313]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85,\"frameIndex\":3},{\"id\":\"frame_box_4_fbf\",\"label\":\"Frame-by-frame bbox 2.8s tracked subject\",\"trackIndex\":4,\"startMs\":2800,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.86 [0.21, 0.18, 0.318, 0.318]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86,\"frameIndex\":4},{\"id\":\"frame_box_5_fbf\",\"label\":\"Frame-by-frame bbox 3.5s context object\",\"trackIndex\":5,\"startMs\":3500,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.86 [0.23, 0.23, 0.312, 0.322]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86,\"frameIndex\":5},{\"id\":\"frame_box_6_fbf\",\"label\":\"Frame-by-frame bbox 4.2s tracked subject\",\"trackIndex\":6,\"startMs\":4200,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.87 [0.25, 0.18, 0.307, 0.327]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87,\"frameIndex\":6},{\"id\":\"frame_box_7_fbf\",\"label\":\"Frame-by-frame bbox 4.9s context object\",\"trackIndex\":7,\"startMs\":4900,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.88 [0.27, 0.23, 0.301, 0.331]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88,\"frameIndex\":7},{\"id\":\"frame_box_8_fbf\",\"label\":\"Frame-by-frame bbox 5.6s tracked subject\",\"trackIndex\":8,\"startMs\":5600,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.89 [0.29, 0.18, 0.296, 0.336]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89,\"frameIndex\":8},{\"id\":\"frame_box_9_fbf\",\"label\":\"Frame-by-frame bbox 6.3s context object\",\"trackIndex\":9,\"startMs\":6300,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.90 [0.31, 0.23, 0.29, 0.34]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9,\"frameIndex\":9}],\"timelineLanes\":[{\"id\":\"video-agent-stages\",\"label\":\"Video agent stages\",\"tracks\":[\"ingest\",\"parse\",\"search\",\"edit\",\"compile\",\"generate\",\"stream\"]},{\"id\":\"frame-by-frame-boxes\",\"label\":\"Frame-by-frame boxes\",\"tracks\":[\"frame_box_0_fbf\",\"frame_box_1_fbf\",\"frame_box_2_fbf\",\"frame_box_3_fbf\",\"frame_box_4_fbf\",\"frame_box_5_fbf\",\"frame_box_6_fbf\",\"frame_box_7_fbf\",\"frame_box_8_fbf\",\"frame_box_9_fbf\"]}],\"bottomPanelTimelineSync\":{\"surface\":\"BottomPanel Timeline\",\"source\":\"frameBoundingBoxes\",\"lane\":\"fbf\",\"thumbnailMode\":\"frame-by-frame-image\",\"trackIds\":[\"frame_box_0_fbf\",\"frame_box_1_fbf\",\"frame_box_2_fbf\",\"frame_box_3_fbf\",\"frame_box_4_fbf\",\"frame_box_5_fbf\",\"frame_box_6_fbf\",\"frame_box_7_fbf\",\"frame_box_8_fbf\",\"frame_box_9_fbf\"]},\"frameByFrameSamples\":[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"confidence\":0.82,\"bbox\":[0.13,0.18,0.34,0.3],\"sampleId\":\"frame-sample-0\",\"annotationCount\":1,\"zoneCounts\":{\"zone-a\":1},\"cumulativeZoneCounts\":{\"zone-a\":1,\"zone-b\":0,\"zone-c\":0}},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"confidence\":0.83,\"bbox\":[0.15,0.23,0.334,0.304],\"sampleId\":\"frame-sample-1\",\"annotationCount\":1,\"zoneCounts\":{\"zone-a\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":0,\"zone-c\":0}},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"confidence\":0.84,\"bbox\":[0.17,0.18,0.329,0.309],\"sampleId\":\"frame-sample-2\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":1,\"zone-c\":0}},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"confidence\":0.85,\"bbox\":[0.19,0.23,0.323,0.313],\"sampleId\":\"frame-sample-3\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":2,\"zone-c\":0}},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"confidence\":0.86,\"bbox\":[0.21,0.18,0.318,0.318],\"sampleId\":\"frame-sample-4\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":3,\"zone-c\":0}},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"confidence\":0.86,\"bbox\":[0.23,0.23,0.312,0.322],\"sampleId\":\"frame-sample-5\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":4,\"zone-c\":0}},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"confidence\":0.87,\"bbox\":[0.25,0.18,0.307,0.327],\"sampleId\":\"frame-sample-6\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":5,\"zone-c\":0}},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"confidence\":0.88,\"bbox\":[0.27,0.23,0.301,0.331],\"sampleId\":\"frame-sample-7\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":6,\"zone-c\":0}},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"confidence\":0.89,\"bbox\":[0.29,0.18,0.296,0.336],\"sampleId\":\"frame-sample-8\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":7,\"zone-c\":0}},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"confidence\":0.9,\"bbox\":[0.31,0.23,0.29,0.34],\"sampleId\":\"frame-sample-9\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":8,\"zone-c\":0}}],\"richMediaPanels\":[{\"route\":\"RichMediaPanel:stream\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"stream-output\",\"inputs\":[\"videoUrl\",\"outputSrcDoc\",\"frameBoundingBoxes\"]},{\"route\":\"RichMediaPanel:frame-analysis\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"frame-analysis\",\"inputs\":[\"outputSrcDoc\",\"frameBoundingBoxes\",\"zoneCounting\"]},{\"route\":\"RichMediaPanel:floatingpanel-annotation\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"visual-annotation-dataset\",\"inputs\":[\"visualDataset\",\"mergedVisualDataset\",\"zoneCounting\"]}],\"datasetOperationSummary\":{\"loadedSamples\":10,\"mergedSamples\":10,\"savedSamples\":10,\"zoneCountedFrames\":10}}"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"html":"html_video_spec","css":"html_video_spec","data_json":"html_video_spec","frameBoundingBoxes":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "htmlVideoRenderSpecInput"}
      frameBoundingBoxes: {key: frameBoundingBoxes, type: json, value: "[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}]"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 4}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 4}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      html:
        key: html
        type: html
        value: |
          <main data-composition-id="knowgrph-video-agent-youtube-demo" data-start="0" data-duration="7.000" aria-label="Knowgrph video agent render"><header class="hero"><section><p class="eyebrow">Knowgrph video agent</p><h1>Reason through video, then stream the result</h1><p class="lede">A visual-annotation-inspired, dependency-free knowgrph graph ingests the operator supplied YouTube test URL, parses source context, searches moments, plans edits, compiles a timeline, generates overlays, and streams the result through Rich Media output.</p></section><p class="chip">test-url=https://youtu.be/8NkwH29Ou1o</p></header><section class="stage" aria-label="Video agent orchestration"><article class="source" data-start="0.000" data-duration="2.000" data-track-index="0"><header class="bar"><span class="dot" aria-hidden="true"></span><span class="url">https://youtu.be/8NkwH29Ou1o</span><span class="badge">ingested</span></header><section class="video-card"><figure><section class="thumbnail" aria-label="Frame-by-frame bounding box preview"><img class="thumbnail-source" src="/__video_frame?url=https%3A%2F%2Fyoutu.be%2F8NkwH29Ou1o&amp;time=0&amp;format=png" alt="" loading="lazy" decoding="async"><section class="frame-boxes" aria-label="Frame-by-frame bounding boxes"><mark class="frame-box" style="left:13%;top:18%;width:34%;height:30%"><span>0.0s tracked subject</span></mark><mark class="frame-box" style="left:15%;top:23%;width:33.4%;height:30.4%"><span>0.7s context object</span></mark><mark class="frame-box" style="left:17%;top:18%;width:32.9%;height:30.9%"><span>1.4s tracked subject</span></mark><mark class="frame-box" style="left:19%;top:23%;width:32.300000000000004%;height:31.3%"><span>2.1s context object</span></mark><mark class="frame-box" style="left:21%;top:18%;width:31.8%;height:31.8%"><span>2.8s tracked subject</span></mark><mark class="frame-box" style="left:23%;top:23%;width:31.2%;height:32.2%"><span>3.5s context object</span></mark><mark class="frame-box" style="left:25%;top:18%;width:30.7%;height:32.7%"><span>4.2s tracked subject</span></mark><mark class="frame-box" style="left:27%;top:23%;width:30.099999999999998%;height:33.1%"><span>4.9s context object</span></mark><mark class="frame-box" style="left:28.999999999999996%;top:18%;width:29.599999999999998%;height:33.6%"><span>5.6s tracked subject</span></mark><mark class="frame-box" style="left:31%;top:23%;width:28.999999999999996%;height:34%"><span>6.3s context object</span></mark></section></section><figcaption>Frame-by-frame bounding boxes are normalized validation data; rendering stays native to knowgrph.</figcaption></figure><h2>Search, edit, compile, generate</h2><p>The graph records source metadata, frame tasks, annotation targets, timeline decisions, and stream-ready artifact routes as typed data.</p><ol class="tasks"><li>search</li><li>edit</li><li>compile</li><li>generate</li><li>stream</li></ol></section></article><article class="reasoning" data-start="1.200" data-duration="4.800" data-track-index="1"><header><p class="eyebrow">Agent plan</p><h2>Modular orchestration without external dependency</h2></header><ol class="agents"><li><strong class="num">1</strong><span>Ingest video URL and normalize source key</span><output>source-ready</output></li><li><strong class="num">2</strong><span>Parse transcript, frames, labels, and searchable moments</span><output>parse-ready</output></li><li><strong class="num">3</strong><span>Search for task-relevant shots and evidence windows</span><output>moments-ready</output></li><li><strong class="num">4</strong><span>Edit clips, overlays, subtitles, and pacing decisions</span><output>edit-ready</output></li><li><strong class="num">5</strong><span>Compile a timeline manifest with generation placeholders</span><output>render-spec-ready</output></li><li><strong class="num">6</strong><span>Stream MP4 or inline preview through Rich Media output</span><output>stream-ready</output></li></ol></article></section><section class="trace" aria-label="Video agent reasoning trace"><article><h3>search</h3><p>Rank source moments as reusable evidence windows before edit planning.</p><output>moments-ready</output></article><article><h3>edit</h3><p>Convert selected evidence into clip ranges, overlays, subtitles, and pacing.</p><output>edit-ready</output></article><article><h3>compile</h3><p>Compile a deterministic HTML/CSS/data Render_Spec for the selected timeline.</p><output>render-spec-ready</output></article><article><h3>generate</h3><p>Keep generated overlays and narration as optional local-tool placeholders.</p><output>generation-plan-ready</output></article><article><h3>stream</h3><p>Publish video/mp4 when encoding succeeds, while preserving outputSrcDoc fallback.</p><output>stream-ready</output></article></section><footer class="timeline" aria-label="Video agent timeline"><section class="rail" aria-label="Instant stream progress"></section><ol class="ticks"><li><strong>0.0s</strong>ingest</li><li><strong>1.0s</strong>parse</li><li><strong>2.0s</strong>search</li><li><strong>3.0s</strong>edit</li><li><strong>4.2s</strong>compile</li><li><strong>5.4s</strong>generate</li><li><strong>6.4s</strong>stream</li></ol><section class="stream" aria-label="Stream output contract"><strong>Instant stream</strong><p>Rich Media Panel receives a playable video artifact when encoding is available, or an inline srcdoc preview from the same Render_Spec when browser encoding is unavailable.</p></section></footer></main>
          
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Source-owned HTML, CSS, and JSON data for a dependency-free video-agent renderer over the YouTube test URL."}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "html_video_renderer_node"}
      type: {key: type, type: string, value: "HtmlVideoRenderer"}
      label: {key: label, type: string, value: "Video Agent HTML Stream Renderer"}
      position: {key: position, type: object, value: {"x":420,"y":0}}
      handles: {key: handles, type: object, value: {"target":["html_in","css_in","data_json_in","frameBoundingBoxes_in"],"source":["videoUrl","outputSrcDoc","outputPath","renderJobId","frameBoundingBoxes"]}}
      css:
        key: css
        type: textarea
        value: |
          main{width:100%;height:100%;box-sizing:border-box;display:grid;grid-template-rows:auto 1fr auto;gap:14px;padding:18px;font-family:Inter,system-ui,sans-serif;background:#07111f;color:#f8fafc;overflow:hidden}p,h1,h2,h3{margin:0}.hero{display:grid;grid-template-columns:1fr auto;gap:12px;align-items:start}.eyebrow{color:#5eead4;font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.08em}.hero h1{font-size:30px;line-height:1.05;letter-spacing:0}.lede{max-width:740px;color:#cbd5e1;font-size:13px;line-height:1.45}.chip{border:1px solid #334155;background:#0f172a;color:#e2e8f0;border-radius:8px;padding:8px 10px;font:12px ui-monospace,SFMono-Regular,Menlo,monospace}.stage{display:grid;grid-template-columns:1.08fr 1fr;gap:12px;min-height:0}.source,.reasoning,.stream{min-width:0;border:1px solid #334155;border-radius:8px;background:#0f172a;box-shadow:0 18px 40px rgba(0,0,0,.28);overflow:hidden}.source{display:grid;grid-template-rows:auto 1fr}.bar{display:grid;grid-template-columns:auto 1fr auto;gap:8px;align-items:center;padding:8px 10px;border-bottom:1px solid #334155;background:#111827}.dot{width:8px;height:8px;border-radius:50%;background:#06b6d4;box-shadow:14px 0 #22c55e,28px 0 #f59e0b}.url{font:12px ui-monospace,SFMono-Regular,Menlo,monospace;color:#cbd5e1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.badge{font-size:11px;color:#5eead4}.video-card{display:grid;gap:12px;padding:14px}.thumbnail{position:relative;aspect-ratio:16/9;border:1px solid #334155;border-radius:8px;background:linear-gradient(135deg,#123456,#0b1220 55%,#0f766e);overflow:hidden}.thumbnail::before{content:"";position:absolute;inset:14% 18%;border:2px solid rgba(94,234,212,.72);border-radius:8px}.thumbnail::after{content:"";position:absolute;left:12%;right:12%;bottom:16%;height:6px;border-radius:999px;background:#5eead4;transform-origin:left;animation:kgProgress 7s linear infinite}.thumbnail-source{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.72}.frame-boxes{position:absolute;inset:0;pointer-events:none}.frame-box{position:absolute;border:2px solid #fbbf24;border-radius:6px;background:rgba(251,191,36,.08);box-shadow:0 0 0 1px rgba(15,23,42,.7);animation:kgFrameBox 7s steps(5,end) infinite both}.frame-box span{position:absolute;left:0;top:-18px;border-radius:4px;background:#fbbf24;color:#1f2937;padding:2px 5px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;white-space:nowrap}.video-card h2{font-size:20px}.video-card p{color:#cbd5e1;font-size:12px;line-height:1.45}.tasks{display:grid;grid-template-columns:repeat(5,1fr);gap:7px}.tasks li{list-style:none;border:1px solid #334155;border-radius:8px;padding:8px;background:#111827;color:#e2e8f0;font-size:11px;text-align:center}.reasoning{display:grid;grid-template-rows:auto 1fr}.reasoning header{padding:12px;border-bottom:1px solid #334155}.reasoning h2{font-size:18px}.agents{display:grid;gap:8px;padding:12px}.agents li{list-style:none;display:grid;grid-template-columns:auto 1fr auto;gap:9px;align-items:center;border:1px solid #334155;border-radius:8px;padding:9px;background:#0b1220;transform:translateX(18px);opacity:.18;animation:kgStep .7s ease-out both}.agents li:nth-child(1){animation-delay:.1s}.agents li:nth-child(2){animation-delay:.28s}.agents li:nth-child(3){animation-delay:.46s}.agents li:nth-child(4){animation-delay:.64s}.agents li:nth-child(5){animation-delay:.82s}.agents li:nth-child(6){animation-delay:1s}.num{display:grid;place-items:center;width:26px;height:26px;border-radius:50%;background:#5eead4;color:#042f2e;font-weight:800;font-size:12px}.agents span{font-size:12px;color:#e2e8f0}.agents output{font:11px ui-monospace,SFMono-Regular,Menlo,monospace;color:#93c5fd}.timeline{display:grid;gap:8px;border-top:1px solid #334155;padding-top:10px}.rail{height:8px;border-radius:999px;background:#1f2937;overflow:hidden}.rail::before{content:"";display:block;height:100%;width:100%;background:#5eead4;transform-origin:left;animation:kgProgress 7s linear infinite}.ticks{display:grid;grid-template-columns:repeat(7,1fr);gap:7px}.ticks li{list-style:none;color:#94a3b8;font-size:10px}.ticks strong{display:block;color:#f8fafc;font-size:11px}.stream{display:grid;grid-template-columns:auto 1fr;gap:10px;align-items:center;padding:10px}.stream strong{font-size:13px}.stream p{color:#cbd5e1;font-size:12px;line-height:1.4}.trace{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:8px;min-height:0}.trace article{border:1px solid #334155;border-radius:8px;background:#111827;padding:9px;min-width:0}.trace h3{font-size:12px;color:#5eead4}.trace p{font-size:11px;color:#cbd5e1;line-height:1.35}.trace output{display:block;margin-top:6px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;color:#93c5fd;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}@keyframes kgStep{to{opacity:1;transform:translateX(0)}}@keyframes kgProgress{from{transform:scaleX(0)}to{transform:scaleX(1)}}@keyframes kgFrameBox{0%,19%{opacity:1}20%,100%{opacity:.22}}
          
      data_json: {key: data_json, type: textarea, value: "{\"title\":\"Knowgrph Video Agent Demo\",\"engine\":\"canvas-2d\",\"rasterizer\":\"html2canvas\",\"output\":\"video/mp4\",\"referencePattern\":\"visual-annotation-inspired video workflow; no copied code and no external dependency\",\"composition\":{\"id\":\"knowgrph-video-agent-youtube-demo\",\"durationMs\":7000,\"fps\":24,\"width\":1280,\"height\":720},\"sourceVideo\":{\"url\":\"https://youtu.be/8NkwH29Ou1o\",\"testUrls\":[\"https://youtu.be/8NkwH29Ou1o\",\"https://youtu.be/77FAnT935IE\"],\"sourceId\":\"youtube:8NkwH29Ou1o\",\"sourceIds\":[\"youtube:8NkwH29Ou1o\",\"youtube:77FAnT935IE\"],\"ingestMode\":\"operator-supplied-test-url\",\"externalDependency\":false},\"agentIntent\":\"reason through complex video tasks: search, editing, compilation, generation, and streaming\",\"capabilities\":[\"ingest\",\"parse\",\"annotate\",\"dataset\",\"zone_count\",\"search\",\"edit\",\"compile\",\"generate\",\"stream\"],\"agents\":[{\"id\":\"source_intake\",\"role\":\"ingest\",\"output\":\"source key and media manifest\"},{\"id\":\"video_parser\",\"role\":\"parse\",\"output\":\"transcript, frame labels, annotation tasks\"},{\"id\":\"moment_searcher\",\"role\":\"search\",\"output\":\"ranked evidence windows\"},{\"id\":\"edit_planner\",\"role\":\"edit\",\"output\":\"clip ranges, overlays, subtitles, pacing\"},{\"id\":\"timeline_compiler\",\"role\":\"compile\",\"output\":\"timeline manifest and render spec\"},{\"id\":\"generation_router\",\"role\":\"generate\",\"output\":\"generated overlay or narration placeholders\"},{\"id\":\"stream_publisher\",\"role\":\"stream\",\"output\":\"videoUrl or outputSrcDoc rich-media payload\"}],\"reasoningArtifacts\":[{\"capability\":\"search\",\"task\":\"Search transcript, frame, and annotation evidence\",\"decision\":\"Rank reusable evidence windows without a provider-specific search API\",\"outputArtifact\":\"video-agent/moments.json\",\"streamSignal\":\"moments-ready\"},{\"capability\":\"edit\",\"task\":\"Plan clips, overlays, subtitles, and pacing\",\"decision\":\"Store edit decisions as timeline data\",\"outputArtifact\":\"video-agent/edit-plan.json\",\"streamSignal\":\"edit-ready\"},{\"capability\":\"compile\",\"task\":\"Compile the selected moments into Render_Spec output\",\"decision\":\"Reuse the existing HTML Video Renderer path\",\"outputArtifact\":\"video-agent/render.html\",\"streamSignal\":\"render-spec-ready\"},{\"capability\":\"generate\",\"task\":\"Plan generated overlays and narration placeholders\",\"decision\":\"Defer live generation to optional local tools\",\"outputArtifact\":\"video-agent/generated-assets.json\",\"streamSignal\":\"generation-plan-ready\"},{\"capability\":\"stream\",\"task\":\"Publish the compiled result immediately\",\"decision\":\"Prefer video/mp4 and preserve outputSrcDoc fallback\",\"outputArtifact\":\"video-agent/stream-manifest.json\",\"streamSignal\":\"stream-ready\"}],\"workspaceFiles\":[{\"path\":\"video-agent/source.json\",\"kind\":\"json\",\"role\":\"source-manifest\"},{\"path\":\"video-agent/parse.json\",\"kind\":\"json\",\"role\":\"parse-output\"},{\"path\":\"video-agent/moments.json\",\"kind\":\"json\",\"role\":\"search-index\"},{\"path\":\"video-agent/timeline.json\",\"kind\":\"json\",\"role\":\"edit-plan\"},{\"path\":\"video-agent/generated-assets.json\",\"kind\":\"json\",\"role\":\"generation-plan\"},{\"path\":\"video-agent/frame-boxes.json\",\"kind\":\"json\",\"role\":\"frame-bounding-boxes\"},{\"path\":\"video-agent/render.html\",\"kind\":\"html\",\"role\":\"composition\"},{\"path\":\"video-agent/stream-manifest.json\",\"kind\":\"json\",\"role\":\"stream-output\"}],\"timelineTracks\":[{\"id\":\"ingest\",\"label\":\"Ingest test URL\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":900,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"parse\",\"label\":\"Parse multimodal context\",\"trackIndex\":1,\"startMs\":900,\"durationMs\":1100,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"search\",\"label\":\"Search relevant moments\",\"trackIndex\":2,\"startMs\":2000,\"durationMs\":1000,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"edit\",\"label\":\"Plan clips and overlays\",\"trackIndex\":3,\"startMs\":3000,\"durationMs\":1200,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"compile\",\"label\":\"Compile timeline\",\"trackIndex\":4,\"startMs\":4200,\"durationMs\":1200,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"generate\",\"label\":\"Generate assets\",\"trackIndex\":5,\"startMs\":5400,\"durationMs\":1000,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"stream\",\"label\":\"Publish stream\",\"trackIndex\":6,\"startMs\":6400,\"durationMs\":600,\"timelineLane\":\"video\",\"source\":\"agent-stage\"},{\"id\":\"frame_box_0_fbf\",\"label\":\"Frame-by-frame bbox 0.0s tracked subject\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.82 [0.13, 0.18, 0.34, 0.3]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82,\"frameIndex\":0},{\"id\":\"frame_box_1_fbf\",\"label\":\"Frame-by-frame bbox 0.7s context object\",\"trackIndex\":1,\"startMs\":700,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.83 [0.15, 0.23, 0.334, 0.304]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83,\"frameIndex\":1},{\"id\":\"frame_box_2_fbf\",\"label\":\"Frame-by-frame bbox 1.4s tracked subject\",\"trackIndex\":2,\"startMs\":1400,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.84 [0.17, 0.18, 0.329, 0.309]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84,\"frameIndex\":2},{\"id\":\"frame_box_3_fbf\",\"label\":\"Frame-by-frame bbox 2.1s context object\",\"trackIndex\":3,\"startMs\":2100,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.85 [0.19, 0.23, 0.323, 0.313]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85,\"frameIndex\":3},{\"id\":\"frame_box_4_fbf\",\"label\":\"Frame-by-frame bbox 2.8s tracked subject\",\"trackIndex\":4,\"startMs\":2800,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.86 [0.21, 0.18, 0.318, 0.318]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86,\"frameIndex\":4},{\"id\":\"frame_box_5_fbf\",\"label\":\"Frame-by-frame bbox 3.5s context object\",\"trackIndex\":5,\"startMs\":3500,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.86 [0.23, 0.23, 0.312, 0.322]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86,\"frameIndex\":5},{\"id\":\"frame_box_6_fbf\",\"label\":\"Frame-by-frame bbox 4.2s tracked subject\",\"trackIndex\":6,\"startMs\":4200,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.87 [0.25, 0.18, 0.307, 0.327]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87,\"frameIndex\":6},{\"id\":\"frame_box_7_fbf\",\"label\":\"Frame-by-frame bbox 4.9s context object\",\"trackIndex\":7,\"startMs\":4900,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.88 [0.27, 0.23, 0.301, 0.331]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88,\"frameIndex\":7},{\"id\":\"frame_box_8_fbf\",\"label\":\"Frame-by-frame bbox 5.6s tracked subject\",\"trackIndex\":8,\"startMs\":5600,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.89 [0.29, 0.18, 0.296, 0.336]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89,\"frameIndex\":8},{\"id\":\"frame_box_9_fbf\",\"label\":\"Frame-by-frame bbox 6.3s context object\",\"trackIndex\":9,\"startMs\":6300,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.90 [0.31, 0.23, 0.29, 0.34]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9,\"frameIndex\":9}],\"streaming\":{\"primary\":\"video/mp4\",\"fallback\":\"outputSrcDoc\",\"panel\":\"RichMediaPanel\",\"panels\":[\"RichMediaPanel:stream\",\"RichMediaPanel:frame-analysis\",\"RichMediaPanel:floatingpanel-annotation\"]},\"safeguards\":[\"no copied external annotation code\",\"no Roboflow/supervision runtime dependency\",\"no API key requirement\",\"source document stores no generated blob URLs\"],\"frameBoundingBoxes\":[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}],\"frameBoundingBoxTimelineTracks\":[{\"id\":\"frame_box_0_fbf\",\"label\":\"Frame-by-frame bbox 0.0s tracked subject\",\"trackIndex\":0,\"startMs\":0,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.82 [0.13, 0.18, 0.34, 0.3]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82,\"frameIndex\":0},{\"id\":\"frame_box_1_fbf\",\"label\":\"Frame-by-frame bbox 0.7s context object\",\"trackIndex\":1,\"startMs\":700,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.83 [0.15, 0.23, 0.334, 0.304]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83,\"frameIndex\":1},{\"id\":\"frame_box_2_fbf\",\"label\":\"Frame-by-frame bbox 1.4s tracked subject\",\"trackIndex\":2,\"startMs\":1400,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.84 [0.17, 0.18, 0.329, 0.309]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84,\"frameIndex\":2},{\"id\":\"frame_box_3_fbf\",\"label\":\"Frame-by-frame bbox 2.1s context object\",\"trackIndex\":3,\"startMs\":2100,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.85 [0.19, 0.23, 0.323, 0.313]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85,\"frameIndex\":3},{\"id\":\"frame_box_4_fbf\",\"label\":\"Frame-by-frame bbox 2.8s tracked subject\",\"trackIndex\":4,\"startMs\":2800,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.86 [0.21, 0.18, 0.318, 0.318]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86,\"frameIndex\":4},{\"id\":\"frame_box_5_fbf\",\"label\":\"Frame-by-frame bbox 3.5s context object\",\"trackIndex\":5,\"startMs\":3500,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.86 [0.23, 0.23, 0.312, 0.322]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86,\"frameIndex\":5},{\"id\":\"frame_box_6_fbf\",\"label\":\"Frame-by-frame bbox 4.2s tracked subject\",\"trackIndex\":6,\"startMs\":4200,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.87 [0.25, 0.18, 0.307, 0.327]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87,\"frameIndex\":6},{\"id\":\"frame_box_7_fbf\",\"label\":\"Frame-by-frame bbox 4.9s context object\",\"trackIndex\":7,\"startMs\":4900,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.88 [0.27, 0.23, 0.301, 0.331]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88,\"frameIndex\":7},{\"id\":\"frame_box_8_fbf\",\"label\":\"Frame-by-frame bbox 5.6s tracked subject\",\"trackIndex\":8,\"startMs\":5600,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"tracked subject 0.89 [0.29, 0.18, 0.296, 0.336]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89,\"frameIndex\":8},{\"id\":\"frame_box_9_fbf\",\"label\":\"Frame-by-frame bbox 6.3s context object\",\"trackIndex\":9,\"startMs\":6300,\"durationMs\":700,\"phase\":\"parsing\",\"output\":\"context object 0.90 [0.31, 0.23, 0.29, 0.34]\",\"timelineLane\":\"fbf\",\"source\":\"frameBoundingBox\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9,\"frameIndex\":9}],\"timelineLanes\":[{\"id\":\"video-agent-stages\",\"label\":\"Video agent stages\",\"tracks\":[\"ingest\",\"parse\",\"search\",\"edit\",\"compile\",\"generate\",\"stream\"]},{\"id\":\"frame-by-frame-boxes\",\"label\":\"Frame-by-frame boxes\",\"tracks\":[\"frame_box_0_fbf\",\"frame_box_1_fbf\",\"frame_box_2_fbf\",\"frame_box_3_fbf\",\"frame_box_4_fbf\",\"frame_box_5_fbf\",\"frame_box_6_fbf\",\"frame_box_7_fbf\",\"frame_box_8_fbf\",\"frame_box_9_fbf\"]}],\"bottomPanelTimelineSync\":{\"surface\":\"BottomPanel Timeline\",\"source\":\"frameBoundingBoxes\",\"lane\":\"fbf\",\"thumbnailMode\":\"frame-by-frame-image\",\"trackIds\":[\"frame_box_0_fbf\",\"frame_box_1_fbf\",\"frame_box_2_fbf\",\"frame_box_3_fbf\",\"frame_box_4_fbf\",\"frame_box_5_fbf\",\"frame_box_6_fbf\",\"frame_box_7_fbf\",\"frame_box_8_fbf\",\"frame_box_9_fbf\"]},\"frameByFrameSamples\":[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"confidence\":0.82,\"bbox\":[0.13,0.18,0.34,0.3],\"sampleId\":\"frame-sample-0\",\"annotationCount\":1,\"zoneCounts\":{\"zone-a\":1},\"cumulativeZoneCounts\":{\"zone-a\":1,\"zone-b\":0,\"zone-c\":0}},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"confidence\":0.83,\"bbox\":[0.15,0.23,0.334,0.304],\"sampleId\":\"frame-sample-1\",\"annotationCount\":1,\"zoneCounts\":{\"zone-a\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":0,\"zone-c\":0}},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"confidence\":0.84,\"bbox\":[0.17,0.18,0.329,0.309],\"sampleId\":\"frame-sample-2\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":1,\"zone-c\":0}},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"confidence\":0.85,\"bbox\":[0.19,0.23,0.323,0.313],\"sampleId\":\"frame-sample-3\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":2,\"zone-c\":0}},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"confidence\":0.86,\"bbox\":[0.21,0.18,0.318,0.318],\"sampleId\":\"frame-sample-4\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":3,\"zone-c\":0}},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"confidence\":0.86,\"bbox\":[0.23,0.23,0.312,0.322],\"sampleId\":\"frame-sample-5\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":4,\"zone-c\":0}},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"confidence\":0.87,\"bbox\":[0.25,0.18,0.307,0.327],\"sampleId\":\"frame-sample-6\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":5,\"zone-c\":0}},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"confidence\":0.88,\"bbox\":[0.27,0.23,0.301,0.331],\"sampleId\":\"frame-sample-7\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":6,\"zone-c\":0}},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"confidence\":0.89,\"bbox\":[0.29,0.18,0.296,0.336],\"sampleId\":\"frame-sample-8\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":7,\"zone-c\":0}},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"confidence\":0.9,\"bbox\":[0.31,0.23,0.29,0.34],\"sampleId\":\"frame-sample-9\",\"annotationCount\":1,\"zoneCounts\":{\"zone-b\":1},\"cumulativeZoneCounts\":{\"zone-a\":2,\"zone-b\":8,\"zone-c\":0}}],\"richMediaPanels\":[{\"route\":\"RichMediaPanel:stream\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"stream-output\",\"inputs\":[\"videoUrl\",\"outputSrcDoc\",\"frameBoundingBoxes\"]},{\"route\":\"RichMediaPanel:frame-analysis\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"frame-analysis\",\"inputs\":[\"outputSrcDoc\",\"frameBoundingBoxes\",\"zoneCounting\"]},{\"route\":\"RichMediaPanel:floatingpanel-annotation\",\"timelineSync\":\"knowgrph:render-frame\",\"role\":\"visual-annotation-dataset\",\"inputs\":[\"visualDataset\",\"mergedVisualDataset\",\"zoneCounting\"]}],\"datasetOperationSummary\":{\"loadedSamples\":10,\"mergedSamples\":10,\"savedSamples\":10,\"zoneCountedFrames\":10}}"}
      duration_ms: {key: duration_ms, type: number, value: 7000}
      engine_hint: {key: engine_hint, type: text, value: "canvas-2d"}
      engineId: {key: engineId, type: string, value: "canvas-2d"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"html_in":"html_video_spec","css_in":"html_video_spec","data_json_in":"html_video_spec","frameBoundingBoxes_in":"annotation_json"},"out":{"videoUrl":"html_video_artifact","outputSrcDoc":"html_video_artifact","outputPath":"html_video_artifact","renderJobId":"html_video_artifact","frameBoundingBoxes":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "htmlVideoRenderer"}
      fps: {key: fps, type: number, value: 24}
      frameBoundingBoxes: {key: frameBoundingBoxes, type: string, value: "[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}]"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 10}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 6}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      height: {key: height, type: number, value: 720}
      html:
        key: html
        type: textarea
        value: |
          <main data-composition-id="knowgrph-video-agent-youtube-demo" data-start="0" data-duration="7.000" aria-label="Knowgrph video agent render"><header class="hero"><section><p class="eyebrow">Knowgrph video agent</p><h1>Reason through video, then stream the result</h1><p class="lede">A visual-annotation-inspired, dependency-free knowgrph graph ingests the operator supplied YouTube test URL, parses source context, searches moments, plans edits, compiles a timeline, generates overlays, and streams the result through Rich Media output.</p></section><p class="chip">test-url=https://youtu.be/8NkwH29Ou1o</p></header><section class="stage" aria-label="Video agent orchestration"><article class="source" data-start="0.000" data-duration="2.000" data-track-index="0"><header class="bar"><span class="dot" aria-hidden="true"></span><span class="url">https://youtu.be/8NkwH29Ou1o</span><span class="badge">ingested</span></header><section class="video-card"><figure><section class="thumbnail" aria-label="Frame-by-frame bounding box preview"><img class="thumbnail-source" src="/__video_frame?url=https%3A%2F%2Fyoutu.be%2F8NkwH29Ou1o&amp;time=0&amp;format=png" alt="" loading="lazy" decoding="async"><section class="frame-boxes" aria-label="Frame-by-frame bounding boxes"><mark class="frame-box" style="left:13%;top:18%;width:34%;height:30%"><span>0.0s tracked subject</span></mark><mark class="frame-box" style="left:15%;top:23%;width:33.4%;height:30.4%"><span>0.7s context object</span></mark><mark class="frame-box" style="left:17%;top:18%;width:32.9%;height:30.9%"><span>1.4s tracked subject</span></mark><mark class="frame-box" style="left:19%;top:23%;width:32.300000000000004%;height:31.3%"><span>2.1s context object</span></mark><mark class="frame-box" style="left:21%;top:18%;width:31.8%;height:31.8%"><span>2.8s tracked subject</span></mark><mark class="frame-box" style="left:23%;top:23%;width:31.2%;height:32.2%"><span>3.5s context object</span></mark><mark class="frame-box" style="left:25%;top:18%;width:30.7%;height:32.7%"><span>4.2s tracked subject</span></mark><mark class="frame-box" style="left:27%;top:23%;width:30.099999999999998%;height:33.1%"><span>4.9s context object</span></mark><mark class="frame-box" style="left:28.999999999999996%;top:18%;width:29.599999999999998%;height:33.6%"><span>5.6s tracked subject</span></mark><mark class="frame-box" style="left:31%;top:23%;width:28.999999999999996%;height:34%"><span>6.3s context object</span></mark></section></section><figcaption>Frame-by-frame bounding boxes are normalized validation data; rendering stays native to knowgrph.</figcaption></figure><h2>Search, edit, compile, generate</h2><p>The graph records source metadata, frame tasks, annotation targets, timeline decisions, and stream-ready artifact routes as typed data.</p><ol class="tasks"><li>search</li><li>edit</li><li>compile</li><li>generate</li><li>stream</li></ol></section></article><article class="reasoning" data-start="1.200" data-duration="4.800" data-track-index="1"><header><p class="eyebrow">Agent plan</p><h2>Modular orchestration without external dependency</h2></header><ol class="agents"><li><strong class="num">1</strong><span>Ingest video URL and normalize source key</span><output>source-ready</output></li><li><strong class="num">2</strong><span>Parse transcript, frames, labels, and searchable moments</span><output>parse-ready</output></li><li><strong class="num">3</strong><span>Search for task-relevant shots and evidence windows</span><output>moments-ready</output></li><li><strong class="num">4</strong><span>Edit clips, overlays, subtitles, and pacing decisions</span><output>edit-ready</output></li><li><strong class="num">5</strong><span>Compile a timeline manifest with generation placeholders</span><output>render-spec-ready</output></li><li><strong class="num">6</strong><span>Stream MP4 or inline preview through Rich Media output</span><output>stream-ready</output></li></ol></article></section><section class="trace" aria-label="Video agent reasoning trace"><article><h3>search</h3><p>Rank source moments as reusable evidence windows before edit planning.</p><output>moments-ready</output></article><article><h3>edit</h3><p>Convert selected evidence into clip ranges, overlays, subtitles, and pacing.</p><output>edit-ready</output></article><article><h3>compile</h3><p>Compile a deterministic HTML/CSS/data Render_Spec for the selected timeline.</p><output>render-spec-ready</output></article><article><h3>generate</h3><p>Keep generated overlays and narration as optional local-tool placeholders.</p><output>generation-plan-ready</output></article><article><h3>stream</h3><p>Publish video/mp4 when encoding succeeds, while preserving outputSrcDoc fallback.</p><output>stream-ready</output></article></section><footer class="timeline" aria-label="Video agent timeline"><section class="rail" aria-label="Instant stream progress"></section><ol class="ticks"><li><strong>0.0s</strong>ingest</li><li><strong>1.0s</strong>parse</li><li><strong>2.0s</strong>search</li><li><strong>3.0s</strong>edit</li><li><strong>4.2s</strong>compile</li><li><strong>5.4s</strong>generate</li><li><strong>6.4s</strong>stream</li></ol><section class="stream" aria-label="Stream output contract"><strong>Instant stream</strong><p>Rich Media Panel receives a playable video artifact when encoding is available, or an inline srcdoc preview from the same Render_Spec when browser encoding is unavailable.</p></section></footer></main>
          
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Runtime-selected HTML-to-MP4 renderer for the video-agent stream. The canvas-2d engine path is browser-native and does not require a system FFmpeg install."}
      "visual:importance": {key: "visual:importance", type: number, value: 28}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      width: {key: width, type: number, value: 1280}
    - id: {key: id, type: string, value: "html_video_mp4_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Rendered MP4 Artifact"}
      position: {key: position, type: object, value: {"x":860,"y":0}}
      handles: {key: handles, type: object, value: {"target":["videoUrl","outputSrcDoc","frameBoundingBoxes"],"source":["videoUrl","outputSrcDoc","frameBoundingBoxes"]}}
      engineId: {key: engineId, type: string, value: "canvas-2d"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"videoUrl":"html_video_artifact","outputSrcDoc":"html_video_artifact","frameBoundingBoxes":"annotation_json"},"out":{"videoUrl":"html_video_artifact","outputSrcDoc":"html_video_artifact","frameBoundingBoxes":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      frameBoundingBoxes: {key: frameBoundingBoxes, type: string, value: "[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}]"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 3}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Rich Media Panel receives the video/mp4 artifact or inline srcdoc stream, plus routed frame-by-frame bounding boxes from the video-agent renderer."}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "auto"}
      srcDoc:
        key: srcDoc
        type: string
        value: |
          <style>body{margin:0;background:#07111f}main{box-sizing:border-box;width:100%;min-height:100%;display:grid;gap:12px;padding:14px;font-family:Inter,system-ui,sans-serif;background:#07111f;color:#f8fafc}p,h1,h2,h3{margin:0}.eyebrow{color:#5eead4;font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.08em}header{display:grid;gap:5px}.lede{color:#cbd5e1;font-size:12px;line-height:1.45}.analysis-layout{display:grid;grid-template-columns:minmax(260px,1.2fr) minmax(220px,.8fr);gap:12px}.preview{margin:0}.thumbnail{position:relative;aspect-ratio:16/9;border:1px solid #334155;border-radius:8px;background:linear-gradient(135deg,#123456,#0b1220 55%,#0f766e);overflow:hidden}.thumbnail::before{content:"";position:absolute;inset:14% 18%;border:2px solid rgba(94,234,212,.72);border-radius:8px}.thumbnail-source{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.72}.frame-boxes{position:absolute;inset:0;pointer-events:none}.frame-box{position:absolute;border:2px solid #fbbf24;border-radius:6px;background:rgba(251,191,36,.1);box-shadow:0 0 0 1px rgba(15,23,42,.7)}.frame-box span{position:absolute;left:0;top:-18px;border-radius:4px;background:#fbbf24;color:#1f2937;padding:2px 5px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;white-space:nowrap}figcaption{margin-top:8px;color:#cbd5e1;font-size:11px;line-height:1.35}.frame-list{display:grid;gap:7px;margin:0;padding:0}.frame-list li{list-style:none;display:grid;grid-template-columns:auto 1fr;gap:7px;border:1px solid #334155;border-radius:8px;background:#0f172a;padding:8px}.frame-list strong{color:#5eead4;font-size:12px}.frame-list span{font-size:12px}.frame-list output{grid-column:1/-1;color:#93c5fd;font:10px ui-monospace,SFMono-Regular,Menlo,monospace}footer{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}.phase{border:1px solid #334155;border-radius:8px;background:#111827;color:#e2e8f0;padding:7px;text-align:center;font-size:11px}</style><main data-composition-id="knowgrph-video-agent-frame-analysis" aria-label="Video agent frame-by-frame bounding box analysis"><header><p class="eyebrow">Frame-by-frame bounding box analysis</p><h2>Video agent analysis for https://youtu.be/8NkwH29Ou1o</h2><p class="lede">The same parsed frame evidence is streamed as a Rich Media preview and as an inspection panel, so search, editing, compilation, generation, and stream decisions stay visible.</p></header><section class="analysis-layout" aria-label="Frame evidence and coordinates"><figure class="preview"><section class="thumbnail" aria-label="Frame-by-frame bounding box preview"><img class="thumbnail-source" src="/__video_frame?url=https%3A%2F%2Fyoutu.be%2F8NkwH29Ou1o&amp;time=0&amp;format=png" alt="" loading="lazy" decoding="async"><section class="frame-boxes" aria-label="Frame-by-frame bounding boxes"><mark class="frame-box" style="left:13%;top:18%;width:34%;height:30%"><span>0.0s tracked subject</span></mark><mark class="frame-box" style="left:15%;top:23%;width:33.4%;height:30.4%"><span>0.7s context object</span></mark><mark class="frame-box" style="left:17%;top:18%;width:32.9%;height:30.9%"><span>1.4s tracked subject</span></mark><mark class="frame-box" style="left:19%;top:23%;width:32.300000000000004%;height:31.3%"><span>2.1s context object</span></mark><mark class="frame-box" style="left:21%;top:18%;width:31.8%;height:31.8%"><span>2.8s tracked subject</span></mark><mark class="frame-box" style="left:23%;top:23%;width:31.2%;height:32.2%"><span>3.5s context object</span></mark><mark class="frame-box" style="left:25%;top:18%;width:30.7%;height:32.7%"><span>4.2s tracked subject</span></mark><mark class="frame-box" style="left:27%;top:23%;width:30.099999999999998%;height:33.1%"><span>4.9s context object</span></mark><mark class="frame-box" style="left:28.999999999999996%;top:18%;width:29.599999999999998%;height:33.6%"><span>5.6s tracked subject</span></mark><mark class="frame-box" style="left:31%;top:23%;width:28.999999999999996%;height:34%"><span>6.3s context object</span></mark></section></section><figcaption>Normalized xywh boxes are projected against the preview frame; the source URL remains validation input rather than repo source code.</figcaption></figure><ol class="frame-list" aria-label="Frame bounding box coordinates"><li><strong>0.0s</strong><span>tracked subject confidence 0.82</span><output>[0.13, 0.18, 0.34, 0.3]</output></li><li><strong>0.7s</strong><span>context object confidence 0.83</span><output>[0.15, 0.23, 0.334, 0.304]</output></li><li><strong>1.4s</strong><span>tracked subject confidence 0.84</span><output>[0.17, 0.18, 0.329, 0.309]</output></li><li><strong>2.1s</strong><span>context object confidence 0.85</span><output>[0.19, 0.23, 0.323, 0.313]</output></li><li><strong>2.8s</strong><span>tracked subject confidence 0.86</span><output>[0.21, 0.18, 0.318, 0.318]</output></li><li><strong>3.5s</strong><span>context object confidence 0.86</span><output>[0.23, 0.23, 0.312, 0.322]</output></li><li><strong>4.2s</strong><span>tracked subject confidence 0.87</span><output>[0.25, 0.18, 0.307, 0.327]</output></li><li><strong>4.9s</strong><span>context object confidence 0.88</span><output>[0.27, 0.23, 0.301, 0.331]</output></li><li><strong>5.6s</strong><span>tracked subject confidence 0.89</span><output>[0.29, 0.18, 0.296, 0.336]</output></li><li><strong>6.3s</strong><span>context object confidence 0.90</span><output>[0.31, 0.23, 0.29, 0.34]</output></li></ol></section><footer aria-label="Video agent reasoning phases"><span class="phase">search</span><span class="phase">edit</span><span class="phase">compile</span><span class="phase">generate</span><span class="phase">stream</span></footer></main>
          
      "visual:height": {key: "visual:height", type: number, value: 472}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:width": {key: "visual:width", type: number, value: 839}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "video_agent_frame_analysis_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Video Agent Frame Analysis"}
      position: {key: position, type: object, value: {"x":860,"y":390}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc","frameBoundingBoxes"],"source":["outputSrcDoc","frameBoundingBoxes"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"outputSrcDoc":"rich_media_inline_html","frameBoundingBoxes":"annotation_json"},"out":{"outputSrcDoc":"rich_media_inline_html","frameBoundingBoxes":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      frameBoundingBoxes: {key: frameBoundingBoxes, type: string, value: "[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}]"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Rich Media analysis panel renders frame-by-frame normalized xywh bounding boxes for the runtime-supplied validation video."}
      kind: {key: kind, type: string, value: "video-agent-frame-analysis"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "auto"}
      srcDoc:
        key: srcDoc
        type: string
        value: |
          <style>body{margin:0;background:#07111f}main{box-sizing:border-box;width:100%;min-height:100%;display:grid;gap:12px;padding:14px;font-family:Inter,system-ui,sans-serif;background:#07111f;color:#f8fafc}p,h1,h2,h3{margin:0}.eyebrow{color:#5eead4;font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.08em}header{display:grid;gap:5px}.lede{color:#cbd5e1;font-size:12px;line-height:1.45}.analysis-layout{display:grid;grid-template-columns:minmax(260px,1.2fr) minmax(220px,.8fr);gap:12px}.preview{margin:0}.thumbnail{position:relative;aspect-ratio:16/9;border:1px solid #334155;border-radius:8px;background:linear-gradient(135deg,#123456,#0b1220 55%,#0f766e);overflow:hidden}.thumbnail::before{content:"";position:absolute;inset:14% 18%;border:2px solid rgba(94,234,212,.72);border-radius:8px}.thumbnail-source{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.72}.frame-boxes{position:absolute;inset:0;pointer-events:none}.frame-box{position:absolute;border:2px solid #fbbf24;border-radius:6px;background:rgba(251,191,36,.1);box-shadow:0 0 0 1px rgba(15,23,42,.7)}.frame-box span{position:absolute;left:0;top:-18px;border-radius:4px;background:#fbbf24;color:#1f2937;padding:2px 5px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;white-space:nowrap}figcaption{margin-top:8px;color:#cbd5e1;font-size:11px;line-height:1.35}.frame-list{display:grid;gap:7px;margin:0;padding:0}.frame-list li{list-style:none;display:grid;grid-template-columns:auto 1fr;gap:7px;border:1px solid #334155;border-radius:8px;background:#0f172a;padding:8px}.frame-list strong{color:#5eead4;font-size:12px}.frame-list span{font-size:12px}.frame-list output{grid-column:1/-1;color:#93c5fd;font:10px ui-monospace,SFMono-Regular,Menlo,monospace}footer{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}.phase{border:1px solid #334155;border-radius:8px;background:#111827;color:#e2e8f0;padding:7px;text-align:center;font-size:11px}</style><main data-composition-id="knowgrph-video-agent-frame-analysis" aria-label="Video agent frame-by-frame bounding box analysis"><header><p class="eyebrow">Frame-by-frame bounding box analysis</p><h2>Video agent analysis for https://youtu.be/8NkwH29Ou1o</h2><p class="lede">The same parsed frame evidence is streamed as a Rich Media preview and as an inspection panel, so search, editing, compilation, generation, and stream decisions stay visible.</p></header><section class="analysis-layout" aria-label="Frame evidence and coordinates"><figure class="preview"><section class="thumbnail" aria-label="Frame-by-frame bounding box preview"><img class="thumbnail-source" src="/__video_frame?url=https%3A%2F%2Fyoutu.be%2F8NkwH29Ou1o&amp;time=0&amp;format=png" alt="" loading="lazy" decoding="async"><section class="frame-boxes" aria-label="Frame-by-frame bounding boxes"><mark class="frame-box" style="left:13%;top:18%;width:34%;height:30%"><span>0.0s tracked subject</span></mark><mark class="frame-box" style="left:15%;top:23%;width:33.4%;height:30.4%"><span>0.7s context object</span></mark><mark class="frame-box" style="left:17%;top:18%;width:32.9%;height:30.9%"><span>1.4s tracked subject</span></mark><mark class="frame-box" style="left:19%;top:23%;width:32.300000000000004%;height:31.3%"><span>2.1s context object</span></mark><mark class="frame-box" style="left:21%;top:18%;width:31.8%;height:31.8%"><span>2.8s tracked subject</span></mark><mark class="frame-box" style="left:23%;top:23%;width:31.2%;height:32.2%"><span>3.5s context object</span></mark><mark class="frame-box" style="left:25%;top:18%;width:30.7%;height:32.7%"><span>4.2s tracked subject</span></mark><mark class="frame-box" style="left:27%;top:23%;width:30.099999999999998%;height:33.1%"><span>4.9s context object</span></mark><mark class="frame-box" style="left:28.999999999999996%;top:18%;width:29.599999999999998%;height:33.6%"><span>5.6s tracked subject</span></mark><mark class="frame-box" style="left:31%;top:23%;width:28.999999999999996%;height:34%"><span>6.3s context object</span></mark></section></section><figcaption>Normalized xywh boxes are projected against the preview frame; the source URL remains validation input rather than repo source code.</figcaption></figure><ol class="frame-list" aria-label="Frame bounding box coordinates"><li><strong>0.0s</strong><span>tracked subject confidence 0.82</span><output>[0.13, 0.18, 0.34, 0.3]</output></li><li><strong>0.7s</strong><span>context object confidence 0.83</span><output>[0.15, 0.23, 0.334, 0.304]</output></li><li><strong>1.4s</strong><span>tracked subject confidence 0.84</span><output>[0.17, 0.18, 0.329, 0.309]</output></li><li><strong>2.1s</strong><span>context object confidence 0.85</span><output>[0.19, 0.23, 0.323, 0.313]</output></li><li><strong>2.8s</strong><span>tracked subject confidence 0.86</span><output>[0.21, 0.18, 0.318, 0.318]</output></li><li><strong>3.5s</strong><span>context object confidence 0.86</span><output>[0.23, 0.23, 0.312, 0.322]</output></li><li><strong>4.2s</strong><span>tracked subject confidence 0.87</span><output>[0.25, 0.18, 0.307, 0.327]</output></li><li><strong>4.9s</strong><span>context object confidence 0.88</span><output>[0.27, 0.23, 0.301, 0.331]</output></li><li><strong>5.6s</strong><span>tracked subject confidence 0.89</span><output>[0.29, 0.18, 0.296, 0.336]</output></li><li><strong>6.3s</strong><span>context object confidence 0.90</span><output>[0.31, 0.23, 0.29, 0.34]</output></li></ol></section><footer aria-label="Video agent reasoning phases"><span class="phase">search</span><span class="phase">edit</span><span class="phase">compile</span><span class="phase">generate</span><span class="phase">stream</span></footer></main>
          
      "visual:height": {key: "visual:height", type: number, value: 602}
      "visual:importance": {key: "visual:importance", type: number, value: 17}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15}
      "visual:width": {key: "visual:width", type: number, value: 1071}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "floating_media_ingestion_source"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "FloatingPanel Media Source"}
      position: {key: position, type: object, value: {"x":0,"y":420}}
      handles: {key: handles, type: object, value: {"source":["image_asset_url","video_frame_asset_url","image_tasks","video_tasks","frame_timestamp_ms"]}}
      assetCatalog: {key: assetCatalog, type: json, value: "{\"schema\":\"knowgrph-media-ingestion/v1\",\"surface\":\"FloatingPanel Media\",\"assets\":[{\"id\":\"media:image:demo\",\"assetType\":\"image\",\"assetUrl\":\"/image/knowgrph/video-frame/frame-c0a158fe-t0.png\",\"roles\":[\"preview\",\"annotation-source\",\"bounding-box-overlay-source\"]},{\"id\":\"media:video-frame:demo\",\"assetType\":\"video_frame\",\"assetUrl\":\"/image/knowgrph/video-frame/frame-c0a158fe-t0.png\",\"frameTimestampMs\":1200,\"roles\":[\"preview\",\"video-frame-annotation-source\",\"bounding-box-overlay-source\"]}],\"parseOutputs\":[\"mime family\",\"asset type\",\"semantic source key\",\"preview role\",\"annotation task set\"],\"renderOutputs\":[\"media preview\",\"annotation JSON\",\"image bounding-box overlay\",\"video-frame bounding-box overlay\",\"LLM-ready payload\"]}"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"image_asset_url":"visual_media_asset","video_frame_asset_url":"visual_media_asset","image_tasks":"annotation_json","video_tasks":"annotation_json","frame_timestamp_ms":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "mediaIngestionSource"}
      frame_timestamp_ms: {key: frame_timestamp_ms, type: number, value: 1200}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 5}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image_asset_url: {key: image_asset_url, type: string, value: "/image/knowgrph/video-frame/frame-c0a158fe-t0.png"}
      image_tasks: {key: image_tasks, type: string, value: "caption,object_detection,dense_region_caption"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "FloatingPanel Media source describes image/video assets and parsed annotation task inputs without generated runtime artifacts."}
      video_frame_asset_url: {key: video_frame_asset_url, type: string, value: "/image/knowgrph/video-frame/frame-c0a158fe-t0.png"}
      video_tasks: {key: video_tasks, type: string, value: "caption,object_detection"}
      "visual:importance": {key: "visual:importance", type: number, value: 22}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "image_annotation_engine_node"}
      type: {key: type, type: string, value: "AnnotationEngine"}
      label: {key: label, type: string, value: "Image Annotation Engine"}
      position: {key: position, type: object, value: {"x":420,"y":360}}
      handles: {key: handles, type: object, value: {"target":["asset_url","tasks"],"source":["annotation_json","outputSrcDoc","annotationId","outputPath"]}}
      asset_type: {key: asset_type, type: string, value: "image"}
      asset_url: {key: asset_url, type: string, value: "/image/knowgrph/video-frame/frame-c0a158fe-t0.png"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"asset_url":"visual_media_asset","tasks":"annotation_json"},"out":{"annotation_json":"annotation_json","outputSrcDoc":"rich_media_inline_html","annotationId":"annotation_json","outputPath":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "annotationEngine"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Image Annotation Engine validates Annotation_Spec and emits captions, object_detection bounding boxes, dense-region captions, and LLM-ready JSON through shared rich-media artifact owners."}
      model_hint: {key: model_hint, type: string, value: ""}
      tasks: {key: tasks, type: string, value: "caption,object_detection,dense_region_caption"}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 17}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "video_frame_annotation_engine_node"}
      type: {key: type, type: string, value: "AnnotationEngine"}
      label: {key: label, type: string, value: "Video Frame Annotation Engine"}
      position: {key: position, type: object, value: {"x":420,"y":580}}
      handles: {key: handles, type: object, value: {"target":["asset_url","tasks","frame_timestamp_ms"],"source":["annotation_json","outputSrcDoc","annotationId","outputPath"]}}
      asset_type: {key: asset_type, type: string, value: "video_frame"}
      asset_url: {key: asset_url, type: string, value: "/image/knowgrph/video-frame/frame-c0a158fe-t0.png"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"asset_url":"visual_media_asset","tasks":"annotation_json","frame_timestamp_ms":"annotation_json"},"out":{"annotation_json":"annotation_json","outputSrcDoc":"rich_media_inline_html","annotationId":"annotation_json","outputPath":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "annotationEngine"}
      frame_timestamp_ms: {key: frame_timestamp_ms, type: number, value: 1200}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 3}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Video frame annotation reuses the same AnnotationEngine contract and records frame_timestamp_ms as runtime input."}
      model_hint: {key: model_hint, type: string, value: ""}
      tasks: {key: tasks, type: string, value: "caption,object_detection"}
      "visual:importance": {key: "visual:importance", type: number, value: 23}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 17}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
    - id: {key: id, type: string, value: "floating_panel_media_annotation_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "FloatingPanel Media Annotation Outputs"}
      position: {key: position, type: object, value: {"x":860,"y":770}}
      handles: {key: handles, type: object, value: {"target":["imageAnnotationJson","videoFrameAnnotationJson","outputSrcDoc","frameBoundingBoxes"],"source":["annotation_json","mediaUrl","outputSrcDoc","frameBoundingBoxes"]}}
      annotationBoxFormat: {key: annotationBoxFormat, type: string, value: "xywh"}
      annotationCoordinateSpace: {key: annotationCoordinateSpace, type: string, value: "normalized-0-to-1"}
      annotationOverlayEnabled: {key: annotationOverlayEnabled, type: boolean, value: true}
      annotationOverlaySource: {key: annotationOverlaySource, type: string, value: "source-owned-outputSrcDoc-runtime-ready"}
      annotationSchemaVersion: {key: annotationSchemaVersion, type: string, value: "knowgrph-annotation/v1"}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"imageAnnotationJson":"annotation_json","videoFrameAnnotationJson":"annotation_json","outputSrcDoc":"rich_media_inline_html","frameBoundingBoxes":"annotation_json"},"out":{"annotation_json":"annotation_json","mediaUrl":"visual_media_asset","outputSrcDoc":"rich_media_inline_html","frameBoundingBoxes":"annotation_json"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      frameBoundingBoxes: {key: frameBoundingBoxes, type: string, value: "[{\"frameIndex\":0,\"timestampMs\":0,\"label\":\"tracked subject\",\"bbox\":[0.13,0.18,0.34,0.3],\"confidence\":0.82},{\"frameIndex\":1,\"timestampMs\":700,\"label\":\"context object\",\"bbox\":[0.15,0.23,0.334,0.304],\"confidence\":0.83},{\"frameIndex\":2,\"timestampMs\":1400,\"label\":\"tracked subject\",\"bbox\":[0.17,0.18,0.329,0.309],\"confidence\":0.84},{\"frameIndex\":3,\"timestampMs\":2100,\"label\":\"context object\",\"bbox\":[0.19,0.23,0.323,0.313],\"confidence\":0.85},{\"frameIndex\":4,\"timestampMs\":2800,\"label\":\"tracked subject\",\"bbox\":[0.21,0.18,0.318,0.318],\"confidence\":0.86},{\"frameIndex\":5,\"timestampMs\":3500,\"label\":\"context object\",\"bbox\":[0.23,0.23,0.312,0.322],\"confidence\":0.86},{\"frameIndex\":6,\"timestampMs\":4200,\"label\":\"tracked subject\",\"bbox\":[0.25,0.18,0.307,0.327],\"confidence\":0.87},{\"frameIndex\":7,\"timestampMs\":4900,\"label\":\"context object\",\"bbox\":[0.27,0.23,0.301,0.331],\"confidence\":0.88},{\"frameIndex\":8,\"timestampMs\":5600,\"label\":\"tracked subject\",\"bbox\":[0.29,0.18,0.296,0.336],\"confidence\":0.89},{\"frameIndex\":9,\"timestampMs\":6300,\"label\":\"context object\",\"bbox\":[0.31,0.23,0.29,0.34],\"confidence\":0.9}]"}
      freezeConnectedOutput: {key: freezeConnectedOutput, type: boolean, value: true}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 4}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "FloatingPanel Media projects runtime image or video-frame object_detection results and the video-agent frame-by-frame bounding boxes as visible Rich Media overlays without storing generated output in this document."}
      kind: {key: kind, type: string, value: "annotation"}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "auto"}
      srcDoc:
        key: srcDoc
        type: string
        value: |
          <style>body{margin:0;background:#07111f}main{box-sizing:border-box;width:100%;min-height:100%;display:grid;gap:12px;padding:14px;font-family:Inter,system-ui,sans-serif;background:#07111f;color:#f8fafc}p,h1,h2,h3{margin:0}.eyebrow{color:#5eead4;font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.08em}header{display:grid;gap:5px}.lede{color:#cbd5e1;font-size:12px;line-height:1.45}.analysis-layout{display:grid;grid-template-columns:minmax(260px,1.2fr) minmax(220px,.8fr);gap:12px}.preview{margin:0}.thumbnail{position:relative;aspect-ratio:16/9;border:1px solid #334155;border-radius:8px;background:linear-gradient(135deg,#123456,#0b1220 55%,#0f766e);overflow:hidden}.thumbnail::before{content:"";position:absolute;inset:14% 18%;border:2px solid rgba(94,234,212,.72);border-radius:8px}.thumbnail-source{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.72}.frame-boxes{position:absolute;inset:0;pointer-events:none}.frame-box{position:absolute;border:2px solid #fbbf24;border-radius:6px;background:rgba(251,191,36,.1);box-shadow:0 0 0 1px rgba(15,23,42,.7)}.frame-box span{position:absolute;left:0;top:-18px;border-radius:4px;background:#fbbf24;color:#1f2937;padding:2px 5px;font:10px ui-monospace,SFMono-Regular,Menlo,monospace;white-space:nowrap}figcaption{margin-top:8px;color:#cbd5e1;font-size:11px;line-height:1.35}.frame-list{display:grid;gap:7px;margin:0;padding:0}.frame-list li{list-style:none;display:grid;grid-template-columns:auto 1fr;gap:7px;border:1px solid #334155;border-radius:8px;background:#0f172a;padding:8px}.frame-list strong{color:#5eead4;font-size:12px}.frame-list span{font-size:12px}.frame-list output{grid-column:1/-1;color:#93c5fd;font:10px ui-monospace,SFMono-Regular,Menlo,monospace}footer{display:grid;grid-template-columns:repeat(5,1fr);gap:6px}.phase{border:1px solid #334155;border-radius:8px;background:#111827;color:#e2e8f0;padding:7px;text-align:center;font-size:11px}</style><main data-composition-id="knowgrph-video-agent-floatingpanel-frame-analysis" aria-label="FloatingPanel video frame-by-frame bounding box analysis"><header><p class="eyebrow">FloatingPanel frame-by-frame bounding box analysis</p><h2>FloatingPanel analysis for https://youtu.be/8NkwH29Ou1o</h2><p class="lede">The FloatingPanel Media output renders the same frame evidence as the stream and analysis panels, keeping search, editing, compilation, generation, and stream reasoning visible without waiting for a runtime artifact.</p></header><section class="analysis-layout" aria-label="FloatingPanel frame evidence and coordinates"><figure class="preview"><section class="thumbnail" aria-label="FloatingPanel frame-by-frame bounding box preview"><img class="thumbnail-source" src="/__video_frame?url=https%3A%2F%2Fyoutu.be%2F8NkwH29Ou1o&amp;time=0&amp;format=png" alt="" loading="lazy" decoding="async"><section class="frame-boxes" aria-label="Frame-by-frame bounding boxes"><mark class="frame-box" style="left:13%;top:18%;width:34%;height:30%"><span>0.0s tracked subject</span></mark><mark class="frame-box" style="left:15%;top:23%;width:33.4%;height:30.4%"><span>0.7s context object</span></mark><mark class="frame-box" style="left:17%;top:18%;width:32.9%;height:30.9%"><span>1.4s tracked subject</span></mark><mark class="frame-box" style="left:19%;top:23%;width:32.300000000000004%;height:31.3%"><span>2.1s context object</span></mark><mark class="frame-box" style="left:21%;top:18%;width:31.8%;height:31.8%"><span>2.8s tracked subject</span></mark><mark class="frame-box" style="left:23%;top:23%;width:31.2%;height:32.2%"><span>3.5s context object</span></mark><mark class="frame-box" style="left:25%;top:18%;width:30.7%;height:32.7%"><span>4.2s tracked subject</span></mark><mark class="frame-box" style="left:27%;top:23%;width:30.099999999999998%;height:33.1%"><span>4.9s context object</span></mark><mark class="frame-box" style="left:28.999999999999996%;top:18%;width:29.599999999999998%;height:33.6%"><span>5.6s tracked subject</span></mark><mark class="frame-box" style="left:31%;top:23%;width:28.999999999999996%;height:34%"><span>6.3s context object</span></mark></section></section><figcaption>Normalized xywh boxes are projected against the preview frame; the source URL remains validation input rather than repo source code.</figcaption></figure><ol class="frame-list" aria-label="FloatingPanel frame bounding box coordinates"><li><strong>0.0s</strong><span>tracked subject confidence 0.82</span><output>[0.13, 0.18, 0.34, 0.3]</output></li><li><strong>0.7s</strong><span>context object confidence 0.83</span><output>[0.15, 0.23, 0.334, 0.304]</output></li><li><strong>1.4s</strong><span>tracked subject confidence 0.84</span><output>[0.17, 0.18, 0.329, 0.309]</output></li><li><strong>2.1s</strong><span>context object confidence 0.85</span><output>[0.19, 0.23, 0.323, 0.313]</output></li><li><strong>2.8s</strong><span>tracked subject confidence 0.86</span><output>[0.21, 0.18, 0.318, 0.318]</output></li><li><strong>3.5s</strong><span>context object confidence 0.86</span><output>[0.23, 0.23, 0.312, 0.322]</output></li><li><strong>4.2s</strong><span>tracked subject confidence 0.87</span><output>[0.25, 0.18, 0.307, 0.327]</output></li><li><strong>4.9s</strong><span>context object confidence 0.88</span><output>[0.27, 0.23, 0.301, 0.331]</output></li><li><strong>5.6s</strong><span>tracked subject confidence 0.89</span><output>[0.29, 0.18, 0.296, 0.336]</output></li><li><strong>6.3s</strong><span>context object confidence 0.90</span><output>[0.31, 0.23, 0.29, 0.34]</output></li></ol></section><footer aria-label="FloatingPanel video agent reasoning phases"><span class="phase">search</span><span class="phase">edit</span><span class="phase">compile</span><span class="phase">generate</span><span class="phase">stream</span></footer></main>
          <aside data-kg-frame-sequence-strip="floating-panel" class="frame-sequence-strip" aria-label="FloatingPanel visible frame-by-frame sequence"><strong>FRAME-BY-FRAME</strong><output>0.0s | 0.7s | 1.4s | 2.1s | 2.8s | 3.5s | 4.2s | 4.9s | 5.6s | 6.3s</output><span>https://youtu.be/8NkwH29Ou1o</span></aside><style>main[data-composition-id="knowgrph-video-agent-floatingpanel-frame-analysis"]{padding-top:46px}.frame-sequence-strip{position:fixed;z-index:5;left:8px;right:8px;top:28px;display:grid;grid-template-columns:auto 1fr auto;gap:8px;align-items:center;border:1px solid #334155;border-radius:8px;background:rgba(15,23,42,.94);color:#e2e8f0;padding:6px 8px;font:11px ui-monospace,SFMono-Regular,Menlo,monospace;box-shadow:0 10px 24px rgba(0,0,0,.28)}.frame-sequence-strip strong{color:#5eead4}.frame-sequence-strip output{color:#fbbf24}.frame-sequence-strip span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;color:#93c5fd}</style>
          
      "visual:height": {key: "visual:height", type: number, value: 550}
      "visual:importance": {key: "visual:importance", type: number, value: 18}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15}
      "visual:width": {key: "visual:width", type: number, value: 978}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
  edges:
    - {"id":"flow-e01","source":"html_video_source_spec","sourceHandle":"html","target":"html_video_renderer_node","targetHandle":"html_in"}
    - {"id":"flow-e02","source":"html_video_source_spec","sourceHandle":"css","target":"html_video_renderer_node","targetHandle":"css_in"}
    - {"id":"flow-e03","source":"html_video_source_spec","sourceHandle":"data_json","target":"html_video_renderer_node","targetHandle":"data_json_in"}
    - {"id":"flow-e04","source":"html_video_renderer_node","sourceHandle":"videoUrl","target":"html_video_mp4_panel","targetHandle":"videoUrl"}
    - {"id":"flow-e05","source":"html_video_renderer_node","sourceHandle":"outputSrcDoc","target":"html_video_mp4_panel","targetHandle":"outputSrcDoc"}
    - {"id":"flow-e14","source":"html_video_source_spec","sourceHandle":"frameBoundingBoxes","target":"html_video_renderer_node","targetHandle":"frameBoundingBoxes_in"}
    - {"id":"flow-e15","source":"html_video_renderer_node","sourceHandle":"frameBoundingBoxes","target":"html_video_mp4_panel","targetHandle":"frameBoundingBoxes"}
    - {"id":"flow-e16","source":"html_video_renderer_node","sourceHandle":"outputSrcDoc","target":"video_agent_frame_analysis_panel","targetHandle":"outputSrcDoc"}
    - {"id":"flow-e17","source":"html_video_renderer_node","sourceHandle":"frameBoundingBoxes","target":"video_agent_frame_analysis_panel","targetHandle":"frameBoundingBoxes"}
    - {"id":"flow-e18","source":"html_video_renderer_node","sourceHandle":"frameBoundingBoxes","target":"floating_panel_media_annotation_panel","targetHandle":"frameBoundingBoxes"}
    - {"id":"flow-e06","source":"floating_media_ingestion_source","sourceHandle":"image_asset_url","target":"image_annotation_engine_node","targetHandle":"asset_url"}
    - {"id":"flow-e07","source":"floating_media_ingestion_source","sourceHandle":"image_tasks","target":"image_annotation_engine_node","targetHandle":"tasks"}
    - {"id":"flow-e08","source":"floating_media_ingestion_source","sourceHandle":"video_frame_asset_url","target":"video_frame_annotation_engine_node","targetHandle":"asset_url"}
    - {"id":"flow-e09","source":"floating_media_ingestion_source","sourceHandle":"video_tasks","target":"video_frame_annotation_engine_node","targetHandle":"tasks"}
    - {"id":"flow-e10","source":"floating_media_ingestion_source","sourceHandle":"frame_timestamp_ms","target":"video_frame_annotation_engine_node","targetHandle":"frame_timestamp_ms"}
    - {"id":"flow-e11","source":"image_annotation_engine_node","sourceHandle":"annotation_json","target":"floating_panel_media_annotation_panel","targetHandle":"imageAnnotationJson"}
    - {"id":"flow-e12","source":"video_frame_annotation_engine_node","sourceHandle":"annotation_json","target":"floating_panel_media_annotation_panel","targetHandle":"videoFrameAnnotationJson"}
    - {"id":"flow-e13","source":"video_frame_annotation_engine_node","sourceHandle":"outputSrcDoc","target":"floating_panel_media_annotation_panel","targetHandle":"outputSrcDoc"}
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
  diagramKinds:
    - "mermaid_flowchart"
    - "mermaid_gitgraph"
    - "mermaid_architecture"
    - "mermaid_eventmodeling"
    - "mermaid_gantt"
    - "frontmatter_flow"
  surfaces:
    - "2D Renderer: Storyboard"
    - "BottomPanel/FloatingPanel Mermaid panels"
  edgePolicy: "explicit graphData.edges, flow.edges, workflow.edges, and diagram edges are source-owned SSOT; renderers project visible connectors only"
---

# Knowgrph Vdeoxpln Demo - Interactive Visual Explanation

This validation input turns the vdeoxpln contract into an inspectable visual
explanation. Import it into Knowgrph to verify that semantic HTML, CSS, and
data become a real MP4 through shared Storyboard Widget and Rich Media owners without
relying on copied reference strings, route names, demo filenames, provider keys,
or mirror-only patches.

## What The Demo Must Prove

| Stage | Required behavior | Shared owner |
|---|---|---|
| Import | The Markdown file is imported as a workspace document. | `workspaceFs.ts` |
| Parse | Frontmatter `flow.nodes` and `flow.edges` become runnable graph data. | frontmatter-flow parser |
| Source | Contract, registry, chat, and renderer owners remain source-backed records. | Source Files owners |
| Visualize | The vdeoxpln workflow appears as editable Storyboard widgets and Rich Media panels. | shared Storyboard widget surface |
| Interact | The Render_Spec source feeds the HTML Video Renderer through explicit flow edges. | shared frontmatter-flow dataflow owners |
| Render MP4 | The Storyboard Widget `HtmlVideoRenderer` node turns semantic HTML, CSS, and data into a real `video/mp4` artifact through `engine_hint=canvas-2d`. | `html-video-renderer/*` + `richMediaRun.ts` |
| Ingest Media | FloatingPanel Media receives source-owned image and video asset references without generated blob URLs in the validation input. | Rich Media / Media catalog owners |
| Annotate | `AnnotationEngine` nodes validate image and video-frame Annotation_Spec inputs and emit LLM-ready JSON. | `visual-annotation-engine/*` |
| Dataset | Frame annotations load once, split deterministically, merge without duplicate samples, and serialize as a saved dataset artifact. | `annotationDataset.ts` + `videoAgentDatasetRuntime.ts` |
| Count Zones | Each frame updates per-zone and cumulative counts on the shared render-frame clock. | `videoAgentDatasetProjection.ts` + Rich Media timeline bridge |
| Render Annotation | Annotation JSON, semantic ids, media previews, and image object-detection bounding boxes flow into the FloatingPanel Media Rich Media target through explicit edges. | `richMediaRun.ts` + shared frontmatter-flow dataflow |
| Project Bounding Boxes | The image preview projects `tasks.object_detection.objects[].bbox` from normalized `[x,y,width,height]` coordinates into its fitted media rectangle with labels and optional confidence. | FloatingPanel Media annotation overlay owner |
| Execute | Toolbar Run all runs the flow and publishes the output to the downstream Rich Media Panel. | Storyboard workflow run action |
| Guard | Repo code consumes this document by input path and must not copy this payload into fixtures or runtime branches. | policy tests |

## Runnable Video Agent HTML-to-MP4 Demo

This document includes a frontmatter-flow graph with three runnable
nodes:

1. `Programmatic Video Agent Render Spec` provides semantic HTML, CSS, and JSON
   data for the YouTube test URL set, with `https://youtu.be/8NkwH29Ou1o`
   as the primary rendered validation URL and `https://youtu.be/77FAnT935IE`
   covered by the shared Import URL validation path.
2. `Video Agent HTML Stream Renderer` consumes the Render_Spec and sets
   `engine_hint` to `canvas-2d`.
3. `Rendered MP4 Artifact` receives the emitted `videoUrl` in a Rich Media
   Panel video tab.

For the executable URL path, open Storyboard Widget video-agent validation import
controls, enter the operator-supplied URL set, and choose `Import set`. Imports
run sequentially through the shared workspace bridge so concurrent writes
cannot overwrite one another. Each imported URL materializes three distinct
Rich Media routes: stream output, frame analysis, and dataset/zone counts. The
dataset panel reads the already-computed visual dataset artifacts and follows
the same `knowgrph:render-frame` clock; it does not recalculate annotations.

The video-agent branch is inspired by Roboflow/supervision-style visual
annotation workflows at the product-pattern level only: the source graph models
ingest, parse, annotate, dataset load/split/merge/save, real-time zone counting,
search, edit, compile, generate, and stream stages as typed Render_Spec data. It
does not copy external annotation code, import Roboflow/supervision, require
external service credentials, or treat the YouTube URL as a runtime dependency.
The URL is validation input; runtime owners decide how to resolve, annotate,
count, render, or stream it.

The `canvas-2d` engine is the no-install Dev/Prod smoke path. It rasterizes
HTML with `html2canvas` and uses browser-native recording capabilities when the
runtime exposes them. If the browser cannot encode video, Run all publishes the
same parsed HTML/CSS/data as an inline `outputSrcDoc` preview rather than
leaving the Rich Media Panel empty. The `headless-browser` adapter remains an
independent runtime option for operators who deliberately register an FFmpeg
runtime.

Run path:

- Import this Markdown file through `Toolbar -> Launch -> Import local files`.
- Switch to the Storyboard widget surface if it is not already selected.
- Run `Video Agent HTML Stream Renderer`, or run the whole flow from Toolbar
  Run all.
- Verify that the downstream Rich Media Panel has either a playable `video/mp4`
  artifact or the inline HTML preview generated from the same Render_Spec, and
  that the render manifest records the selected `engineHint=canvas-2d` when an
  MP4 is produced.
- Confirm the source document remains free of generated blob URLs, run IDs, and
  output paths; those fields are runtime artifacts, not validation input.

The embedded Render_Spec is source-owned in frontmatter under
`flow.nodes[].{html,css,data_json,duration_ms,fps,width,height,engine_hint}`.
It models a video-agent pipeline with source intake, multimodal parsing, moment
search, edit planning, timeline compilation, generated overlay placeholders,
seekable CSS keyframes, timeline lanes, and stream artifact publication. Do not
duplicate the payload into fixture files; tests must ingest this document by
path.

## Runnable FloatingPanel Media Annotation Demo

The same frontmatter graph also includes a FloatingPanel Media branch for
image/video ingestion, parsing, annotation, and rendering:

1. `FloatingPanel Media Source` declares image and video asset references, parsed
   media roles, task sets, and a video frame timestamp as source-owned inputs.
2. `Image Annotation Engine` consumes the image asset and task set with
   `asset_type=image`.
3. `Video Frame Annotation Engine` consumes the video asset, task set, and
   `frame_timestamp_ms` with `asset_type=video_frame`.
4. `FloatingPanel Media Annotation Outputs` receives annotation JSON through
   explicit frontmatter-flow edges. The runtime projection owns the source media and
   labelled `object_detection` boxes as one atomic `outputSrcDoc` render channel.

The branch is intentionally runtime-ready but source-neutral. The validation
input stores a document-relative, browser-resolvable media reference, task
names, and frame timestamp only. It does not store generated blob URLs, output
paths,
annotation ids, model cache state, or worker progress. At runtime, the
Annotation Engine must build ids through the shared semantic-key helper and
route successful JSON through `writeRichMediaWidgetRunOutputArtifact`. The Dev
runtime uses dependency-free heuristic worker output for both image and
video-frame tasks; validation/runtime failures remain structured
(`invalid_spec`, `model_not_configured`, `worker_not_supported`, or
`inference_failed`) rather than branching into a demo-only fallback.

Image bounding-box projection contract:

- read detections from `tasks.object_detection.objects[]`
- require each detection to expose `label` and `bbox`, with optional
  `confidence`
- interpret `bbox` as normalized `[x, y, width, height]` values
- clamp projected rectangles to the fitted image content bounds
- recompute screen rectangles from source coordinates when the panel resizes or
  zoom changes; do not mutate or duplicate the annotation JSON
- hide only malformed detections while preserving other valid annotations

Run path:

- Import this Markdown file through `Toolbar -> Launch -> Import local files`.
- Open FloatingPanel Media and verify that the media branch exposes image/video
  source rows, parsed annotation task sets, and the downstream annotation panel.
- Run the image annotation node, the video-frame annotation node, or Toolbar Run
  all.
- Verify that successful outputs are LLM-ready `knowgrph-annotation/v1` JSON
  and that the FloatingPanel Media target shows the media preview alongside the
  annotation payload.
- Verify that the image preview shows at least one labelled bounding rectangle
  when `object_detection` returns objects, and that the rectangle remains
  aligned with the image while resizing or zooming the panel.
- Confirm the source document remains unchanged after execution; generated
  annotation ids, output paths, worker progress, and cached model state belong
  to runtime artifacts only.

## Runnable AI Showrunner Dry-Run

Use this section to prove the AI Showrunner capability without a provider call.
The embedded Creative_Brief is a valid `knowgrph-showrunner-brief/v1` document.
The local MCP payload below runs it in dry-run mode and should return a
`run_id`, `run_status=complete`, `paid_call_count=0`, and a manifest path.

```yaml knowgrph-showrunner-brief
---
schema: "knowgrph-showrunner-brief/v1"
run_type: "podcast"
title: "Vdeoxpln AI Showrunner Demo"
run_id: "vdeoxpln-ai-showrunner-demo"
token_budget: 1200
max_retries: 2
max_memory_tokens: 300
dry_run: true
agent_pipeline: ["researcher","scriptwriter","director","narrator_router"]
agent_roles:
  - role: "researcher"
  - role: "scriptwriter"
  - role: "director"
  - role: "narrator_router"
narrator_voice_map:
  - speaker: "host"
    voice_endpoint_env_key: "SHOWRUNNER_HOST_VOICE_URL"
acceptance_criteria:
  - "research_pack entry is appended before scriptwriter runs"
  - "script_draft conforms to knowgrph-script/v1"
  - "narration-manifest.md is written before any TTS call"
  - "paid_call_count remains 0 in dry-run mode"
---

# Vdeoxpln AI Showrunner Demo

Run a provider-neutral podcast pipeline that explains how vdeoxpln turns an
abstract capability registry into source-backed visual workflows, review gates,
and artifact manifests.
```

```json mcp-call
{
  "tool": "knowgrph.showrunner.start_run",
  "arguments": {
    "dry_run": true,
    "brief_markdown": "---\nschema: \"knowgrph-showrunner-brief/v1\"\nrun_type: \"podcast\"\ntitle: \"Vdeoxpln AI Showrunner Demo\"\nrun_id: \"vdeoxpln-ai-showrunner-demo\"\ntoken_budget: 1200\nmax_retries: 2\nmax_memory_tokens: 300\ndry_run: true\nagent_pipeline: [\"researcher\",\"scriptwriter\",\"director\",\"narrator_router\"]\nagent_roles:\n  - role: \"researcher\"\n  - role: \"scriptwriter\"\n  - role: \"director\"\n  - role: \"narrator_router\"\nnarrator_voice_map:\n  - speaker: \"host\"\n    voice_endpoint_env_key: \"SHOWRUNNER_HOST_VOICE_URL\"\nacceptance_criteria:\n  - \"research_pack entry is appended before scriptwriter runs\"\n  - \"script_draft conforms to knowgrph-script/v1\"\n  - \"narration-manifest.md is written before any TTS call\"\n  - \"paid_call_count remains 0 in dry-run mode\"\n---\n\n# Vdeoxpln AI Showrunner Demo\n\nRun a provider-neutral podcast pipeline that explains how vdeoxpln turns an abstract capability registry into source-backed visual workflows, review gates, and artifact manifests.\n"
  }
}
```

Expected local MCP artifact shape:

- `showrunner/briefs/<run_id>/brief.md`
- `showrunner/runs/<run_id>/state.json`
- `showrunner/runs/<run_id>/cost-log.jsonl`
- `showrunner/runs/<run_id>/narration-manifest.md`
- `showrunner/runs/<run_id>/manifest.md`

## Expected Inspection Result

After import, the parsed graph should expose:

- `kgCanvasSurfaceMode=2d`
- `kgCanvasRenderMode=2d`
- `kgCanvas2dRenderer=storyboard`
- one frontmatter-flow graph containing the Render_Spec source, HTML Video Renderer, and Rich Media Panel
- one dependency-free `knowgrph-video-agent/v1` branch for the test URL set
  (`https://youtu.be/8NkwH29Ou1o`, `https://youtu.be/77FAnT935IE`)
- one video-agent Render_Spec with ingest, parse, search, edit, compile, generate, and stream stages
- one AI Showrunner branch showing the dry-run role pipeline, token budget, artifact manifest, and zero paid calls
- one Storyboard Widget HTML Video Renderer branch with `HtmlVideoRenderer -> RichMediaPanel`, `engine_hint=canvas-2d`, and a real `video/mp4` artifact or inline stream preview
- one FloatingPanel Media branch with `InputWidget -> AnnotationEngine -> RichMediaPanel` for both image annotation and video-frame annotation
- one Annotation Engine result path using `knowgrph-annotation/v1`, sorted task semantic-key inputs, and the shared rich-media artifact writer
- one image annotation projection reading normalized object-detection boxes from `tasks.object_detection.objects[]` and rendering labelled overlays in FloatingPanel Media
- one Design FloatingPanel Video workspace showing files, compositions, assets, timeline lanes, and the same runtime-registered Render MP4 action
- one Design BottomPanel Timeline view showing source-derived design video tracks when `kgCanvas2dRenderer=design` and the bottom tab is Timeline
- one Run all execution path that uses source-owned flow edges and publishes only the generated MP4 artifact

The repo must treat this file as external validation input. Runtime code and
tests may read it by caller-supplied path, but must not copy its node ids,
titles, prompts, source hashes, showrunner brief, MCP payload, HTML video
Render_Spec, video-agent stages, test URL, media asset references, annotation
task sets, Annotation_Spec payloads, or output payload into implementation
fixtures.
