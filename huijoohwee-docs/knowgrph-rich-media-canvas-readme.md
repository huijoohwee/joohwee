---

title: "Knowgrph — Write it. See it. Ship it."
id: md:knowgrph-readme-v3
author: joohwee
institution: "Knowgrph — airvio.co/knowgrph"
date: "2026-05-01"
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "d3"
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
  edgeModel: "active graph edges from the selected source graph"
  timelineSurface: "TimelineTransportControls + shared bottom-panel surface"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"
index:
  legend:
    nodes:
      problem:   "#c0392b — red    — pain point / competitor gap"
      insight:   "#d68910 — amber  — reframe / principle / tagline"
      product:   "#1a6fa8 — blue   — widget / layer / tech component"
      actor:     "#1e8449 — green  — user segment / stakeholder / market"
      output:    "#7d3c98 — purple — artifact / export / data store"
      business:  "#117a65 — teal   — revenue line / model tier"
      milestone: "#5d6d7e — grey   — roadmap item"
    edges:
      user_flow: "solid #2980b9  2px  — actor interacts with product surface"
      work_flow: "dashed #d68910 2px  — pitch section narrative progression"
      data_flow: "dotted #7d3c98 1.5px — artifact passes between pipeline nodes"
  mermaid: |
    %%{init:{
      "theme":"base",
      "themeVariables":{
        "primaryColor":"#1a1a2e","primaryTextColor":"#f0f0f0",
        "primaryBorderColor":"#444","lineColor":"#888",
        "secondaryColor":"#16213e","tertiaryColor":"#0f3460",
        "edgeLabelBackground":"#1a1a2e"
      }
    }}%%
    flowchart TD

      classDef problem   fill:#c0392b,color:#fff,stroke:#922b21,stroke-width:1.5px
      classDef insight   fill:#d68910,color:#fff,stroke:#9a6301,stroke-width:1.5px
      classDef product   fill:#1a6fa8,color:#fff,stroke:#154f7a,stroke-width:1.5px
      classDef actor     fill:#1e8449,color:#fff,stroke:#145a32,stroke-width:1.5px
      classDef output    fill:#7d3c98,color:#fff,stroke:#5b2c6f,stroke-width:1.5px
      classDef business  fill:#117a65,color:#fff,stroke:#0e6655,stroke-width:1.5px
      classDef milestone fill:#5d6d7e,color:#fff,stroke:#424f5c,stroke-width:1.5px

      subgraph S0["① Hook"]
        TAGLINE["Write it. See it. Ship it."]:::insight
        POS["Extends CapCut · bridges to Higgsfield · no learning curve"]:::insight
      end

      subgraph S1["② Problem — The Middle Is Empty"]
        subgraph S1A["Too much"]
          P_STEEP["Node-graph tools — too steep, hours to learn"]:::problem
          P_BLIND["Higgsfield — powerful but context-blind"]:::problem
        end
        subgraph S1B["Too little"]
          P_ONE["CapCut — fast for one · breaks at variants"]:::problem
          P_MEMORY["No brand memory · no locale context · manual re-edit"]:::problem
        end
        P_GAP["Solopreneur stuck in the middle — no tool fits"]:::problem
      end

      subgraph S2["③ ICP — Global Emerging Market Creator"]
        subgraph S2A["Who"]
          ICP_SOLO["Solopreneur / one-person company"]:::actor
          ICP_FREE["Freelancer / independent creator"]:::actor
          ICP_INFL["Influencer / content creator"]:::actor
          ICP_ECOM["E-commerce seller (TikTok Shop, Shopee, Mercado)"]:::actor
        end
        subgraph S2B["Where — fragmented, local-context markets"]
          MKT_SEA["Southeast Asia — ID PH TH VN SG MY"]:::actor
          MKT_LATAM["Latin America — MX BR CO AR"]:::actor
          MKT_MENA["MENA — EG SA AE NG"]:::actor
          MKT_SA["South Asia — IN BD PK"]:::actor
          MKT_US["US — Wild West frontier creators"]:::actor
          MKT_CAR["Caribbean — island creators"]:::actor
        end
        subgraph S2C["Behaviour"]
          GTM_CC["Already on CapCut · hits variant ceiling"]:::actor
          GTM_LOOP["Gets template · runs once · ships N · shares forward"]:::insight
        end
      end

      subgraph S3["④ Insight — Extend, Don't Replace"]
        I_EXT["Knowgrph augments CapCut — not a replacement"]:::insight
        I_MD["Markdown brief = brand memory + local context"]:::insight
        I_AI["AI = orchestrator across text → image → video"]:::insight
        I_AUTO["Upstream change → all variants recompute"]:::insight
        I_POS["CapCut for one video · Knowgrph for sixty"]:::insight
      end

      subgraph S4["⑤ Product — Widget Canvas"]
        subgraph S4A["Core Pipeline"]
          W_TEXT["Text Gen — scene plan + captions"]:::product
          W_IMG["Image Gen — local keyframes"]:::product
          W_VID["Video Gen — 9:16 clip"]:::product
          W_PANEL["Rich Media Panel — preview + export"]:::product
        end
        subgraph S4B["Brief Layers"]
          BR_BRAND["Brand memory — palette · font · tone"]:::output
          BR_LOCALE["Locale — language · cultural context · format"]:::output
          BR_VARIANT["Variant field — swap → full recompute"]:::output
        end
      end

      subgraph S5["⑥ Demo — RoboDrone X1 · Three Skies"]
        DM_US["US · Wild West mesa → ghost mustang stampede"]:::output
        DM_CAR["Caribbean · island tempest → mermaid queen cathedral"]:::output
        DM_SG["SG · Marina Bay → RoboTown AI sentinel"]:::output
        DM_PAR["Parent — safety · flight time · crash-proof"]:::actor
        DM_KID["Child — multiverse portal opens at the horizon"]:::actor
        DM_NODE["Three worlds as canvas nodes · one brief"]:::product
      end

      subgraph S6["⑦ Architecture"]
        A_FE["React 18 + TS + Vite — client-first PWA"]:::product
        A_BP["BytePlus OpenArk + Seed — text · image · video"]:::product
        A_PY["Python parser — NetworkX · DuckDB"]:::product
        A_CF["Cloudflare Pages · Stripe · RxDB"]:::product
      end

      subgraph S7["⑧ Business Model"]
        B_SUB["Workspace subscription"]:::business
        B_USE["Usage-based compute"]:::business
        B_MKT["Template marketplace — locale pipelines"]:::business
      end

      subgraph S8["⑨ Roadmap"]
        R_NOW["Now — brief→video pipeline · BytePlus · Stripe"]:::milestone
        R_NEXT["Next — batch variants · eval harness · templates"]:::milestone
        R_LATER["Later — collab · mobile brief editor · plugins"]:::milestone
      end

      subgraph S9["⑩ The Ask"]
        ASK_DP["Design partners — creators at variant ceiling"]:::actor
        ASK_DIST["Distribution — creator community intros"]:::actor
        ASK_DATA["Real-world locale briefs + templates"]:::output
      end

      %% USER FLOW
      GTM_CC -->|"hits ceiling"| W_PANEL
      ICP_SOLO -->|"writes brief"| W_TEXT
      ICP_ECOM -->|"authors campaign"| W_TEXT
      DM_PAR -->|"buys via"| W_PANEL
      DM_KID -->|"enters world in"| DM_NODE

      %% WORK FLOW
      S0 -.->|"frames"| S1
      S1 -.->|"scopes ICP"| S2
      S2 -.->|"motivates"| S3
      S3 -.->|"enables"| S4
      S4 -.->|"shown by"| S5
      S5 -.->|"runs on"| S6
      S6 -.->|"monetised via"| S7
      S7 -.->|"delivered by"| S8
      S8 -.->|"closes"| S9

      %% DATA FLOW
      BR_BRAND -->|"locked context"| W_TEXT
      BR_LOCALE -->|"locale context"| W_TEXT
      BR_VARIANT -->|"swap → recompute"| W_TEXT
      W_TEXT -->|"text_out"| W_IMG
      W_IMG -->|"imageUrl"| W_VID
      W_VID -->|"videoUrl"| W_PANEL
      A_BP -->|"completions · generations · renders"| W_TEXT
flow:
  edgeType: {key: "edgeType", type: string, value: "smoothstep"}
  balancedViewportPreset: {key: "balancedViewportPreset", type: string, value: "widgetFrontmatter"}
  computed: {key: "computed", type: boolean, value: true}
  snapToGrid: {key: "snapToGrid", type: boolean, value: true}
  direction: {key: direction, type: string, value: "LR"}
  nodes:
    - id: {key: id, type: string, value: "A_BP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "BytePlus OpenArk + Seed — text · image · video"}
      position: {key: position, type: object, value: {"x":0,"y":-7320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_BP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "A_CF"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Cloudflare Pages · Stripe · RxDB"}
      position: {key: position, type: object, value: {"x":0,"y":-7080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_CF"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "A_FE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "React 18 + TS + Vite — client-first PWA"}
      position: {key: position, type: object, value: {"x":0,"y":-6840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_FE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "A_PY"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Python parser — NetworkX · DuckDB"}
      position: {key: position, type: object, value: {"x":0,"y":-6600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_PY"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DATA"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Real-world locale briefs + templates"}
      position: {key: position, type: object, value: {"x":0,"y":-6360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DATA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DIST"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Distribution — creator community intros"}
      position: {key: position, type: object, value: {"x":0,"y":-6120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DIST"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Design partners — creators at variant ceiling"}
      position: {key: position, type: object, value: {"x":0,"y":-5880}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_MKT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Template marketplace — locale pipelines"}
      position: {key: position, type: object, value: {"x":0,"y":-5640}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_MKT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_SUB"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Workspace subscription"}
      position: {key: position, type: object, value: {"x":0,"y":-5400}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_SUB"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_USE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Usage-based compute"}
      position: {key: position, type: object, value: {"x":0,"y":-5160}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_USE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "BR_BRAND"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Brand memory — palette · font · tone"}
      position: {key: position, type: object, value: {"x":0,"y":-4920}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:BR_BRAND"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "BR_LOCALE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Locale — language · cultural context · format"}
      position: {key: position, type: object, value: {"x":0,"y":-4680}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:BR_LOCALE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "BR_VARIANT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Variant field — swap → full recompute"}
      position: {key: position, type: object, value: {"x":0,"y":-4440}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:BR_VARIANT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_CAR"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Caribbean · island tempest → mermaid queen cathedral"}
      position: {key: position, type: object, value: {"x":0,"y":-4200}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_CAR"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_KID"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Child — multiverse portal opens at the horizon"}
      position: {key: position, type: object, value: {"x":0,"y":-3960}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_KID"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_PAR"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Parent — safety · flight time · crash-proof"}
      position: {key: position, type: object, value: {"x":0,"y":-3720}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_PAR"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_SG"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "SG · Marina Bay → RoboTown AI sentinel"}
      position: {key: position, type: object, value: {"x":0,"y":-3480}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_SG"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_US"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "US · Wild West mesa → ghost mustang stampede"}
      position: {key: position, type: object, value: {"x":0,"y":-3240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_US"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "GTM_CC"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Already on CapCut · hits variant ceiling"}
      position: {key: position, type: object, value: {"x":0,"y":-3000}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:GTM_CC"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "GTM_LOOP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Gets template · runs once · ships N · shares forward"}
      position: {key: position, type: object, value: {"x":0,"y":-2760}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:GTM_LOOP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_AI"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "AI = orchestrator across text → image → video"}
      position: {key: position, type: object, value: {"x":0,"y":-2520}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_AI"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_AUTO"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Upstream change → all variants recompute"}
      position: {key: position, type: object, value: {"x":0,"y":-2280}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_AUTO"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_EXT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Knowgrph augments CapCut — not a replacement"}
      position: {key: position, type: object, value: {"x":0,"y":-2040}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_EXT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_MD"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Markdown brief = brand memory + local context"}
      position: {key: position, type: object, value: {"x":0,"y":-1800}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_MD"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_POS"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "CapCut for one video · Knowgrph for sixty"}
      position: {key: position, type: object, value: {"x":0,"y":-1560}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_POS"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_ECOM"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "E-commerce seller (TikTok Shop, Shopee, Mercado)"}
      position: {key: position, type: object, value: {"x":0,"y":-1320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_ECOM"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_FREE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Freelancer / independent creator"}
      position: {key: position, type: object, value: {"x":0,"y":-1080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_FREE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_INFL"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Influencer / content creator"}
      position: {key: position, type: object, value: {"x":0,"y":-840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_INFL"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_SOLO"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Solopreneur / one-person company"}
      position: {key: position, type: object, value: {"x":0,"y":-600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_SOLO"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_CAR"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Caribbean — island creators"}
      position: {key: position, type: object, value: {"x":0,"y":-360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_CAR"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_LATAM"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Latin America — MX BR CO AR"}
      position: {key: position, type: object, value: {"x":0,"y":-120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_LATAM"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_MENA"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "MENA — EG SA AE NG"}
      position: {key: position, type: object, value: {"x":0,"y":120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_MENA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_SA"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "South Asia — IN BD PK"}
      position: {key: position, type: object, value: {"x":0,"y":360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_SA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_SEA"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Southeast Asia — ID PH TH VN SG MY"}
      position: {key: position, type: object, value: {"x":0,"y":600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_SEA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_US"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "US — Wild West frontier creators"}
      position: {key: position, type: object, value: {"x":0,"y":840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_US"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_BLIND"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Higgsfield — powerful but context-blind"}
      position: {key: position, type: object, value: {"x":0,"y":1080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_BLIND"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_GAP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Solopreneur stuck in the middle — no tool fits"}
      position: {key: position, type: object, value: {"x":0,"y":1320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_GAP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_MEMORY"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "No brand memory · no locale context · manual re-edit"}
      position: {key: position, type: object, value: {"x":0,"y":1560}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_MEMORY"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_ONE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "CapCut — fast for one · breaks at variants"}
      position: {key: position, type: object, value: {"x":0,"y":1800}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_ONE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_STEEP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Node-graph tools — too steep, hours to learn"}
      position: {key: position, type: object, value: {"x":0,"y":2040}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_STEEP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "POS"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Extends CapCut · bridges to Higgsfield · no learning curve"}
      position: {key: position, type: object, value: {"x":0,"y":2280}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:POS"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_LATER"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Later — collab · mobile brief editor · plugins"}
      position: {key: position, type: object, value: {"x":0,"y":2520}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_LATER"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_NEXT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Next — batch variants · eval harness · templates"}
      position: {key: position, type: object, value: {"x":0,"y":2760}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_NEXT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_NOW"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Now — brief→video pipeline · BytePlus · Stripe"}
      position: {key: position, type: object, value: {"x":0,"y":3000}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_NOW"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S0"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "① Hook"}
      position: {key: position, type: object, value: {"x":0,"y":3240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S0"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "② Problem — The Middle Is Empty"}
      position: {key: position, type: object, value: {"x":0,"y":3480}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Too much"}
      position: {key: position, type: object, value: {"x":0,"y":3720}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Too little"}
      position: {key: position, type: object, value: {"x":0,"y":3960}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "③ ICP — Global Emerging Market Creator"}
      position: {key: position, type: object, value: {"x":0,"y":4200}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Who"}
      position: {key: position, type: object, value: {"x":0,"y":4440}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Where — fragmented, local-context markets"}
      position: {key: position, type: object, value: {"x":0,"y":4680}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2C"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Behaviour"}
      position: {key: position, type: object, value: {"x":0,"y":4920}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2C"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S3"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "④ Insight — Extend, Don't Replace"}
      position: {key: position, type: object, value: {"x":0,"y":5160}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S3"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑤ Product — Widget Canvas"}
      position: {key: position, type: object, value: {"x":0,"y":5400}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Core Pipeline"}
      position: {key: position, type: object, value: {"x":0,"y":5640}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Brief Layers"}
      position: {key: position, type: object, value: {"x":0,"y":5880}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S5"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑥ Demo — RoboDrone X1 · Three Skies"}
      position: {key: position, type: object, value: {"x":0,"y":6120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S5"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S6"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑦ Architecture"}
      position: {key: position, type: object, value: {"x":0,"y":6360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S6"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 8}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S7"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑧ Business Model"}
      position: {key: position, type: object, value: {"x":0,"y":6600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S7"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S8"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑨ Roadmap"}
      position: {key: position, type: object, value: {"x":0,"y":6840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S8"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S9"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑩ The Ask"}
      position: {key: position, type: object, value: {"x":0,"y":7080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S9"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "TAGLINE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Write it. See it. Ship it."}
      position: {key: position, type: object, value: {"x":0,"y":7320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:TAGLINE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_NODE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Three worlds as canvas nodes · one brief"}
      position: {key: position, type: object, value: {"x":380,"y":-120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_NODE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "W_TEXT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Text Gen — scene plan + captions"}
      position: {key: position, type: object, value: {"x":380,"y":120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:W_TEXT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 7}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 6}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 40}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 20.583005244258363}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "W_IMG"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Image Gen — local keyframes"}
      position: {key: position, type: object, value: {"x":760,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:W_IMG"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 2}
    - id: {key: id, type: string, value: "W_VID"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Video Gen — 9:16 clip"}
      position: {key: position, type: object, value: {"x":1140,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:W_VID"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 3}
    - id: {key: id, type: string, value: "W_PANEL"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Rich Media Panel — preview + export"}
      position: {key: position, type: object, value: {"x":1520,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:W_PANEL"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 3}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 4}
  edges:
    - {"id":"index-e01-2689650164","source":"GTM_CC","sourceHandle":"output","target":"W_PANEL","targetHandle":"input","label":"\"hits ceiling\""}
    - {"id":"index-e02-3015591615","source":"ICP_SOLO","sourceHandle":"output","target":"W_TEXT","targetHandle":"input","label":"\"writes brief\""}
    - {"id":"index-e03-532712988","source":"ICP_ECOM","sourceHandle":"output","target":"W_TEXT","targetHandle":"input","label":"\"authors campaign\""}
    - {"id":"index-e04-2931045366","source":"DM_PAR","sourceHandle":"output","target":"W_PANEL","targetHandle":"input","label":"\"buys via\""}
    - {"id":"index-e05-1163237476","source":"DM_KID","sourceHandle":"output","target":"DM_NODE","targetHandle":"input","label":"\"enters world in\""}
    - {"id":"index-e06-1345375168","source":"BR_BRAND","sourceHandle":"output","target":"W_TEXT","targetHandle":"input","label":"\"locked context\""}
    - {"id":"index-e07-3097728689","source":"BR_LOCALE","sourceHandle":"output","target":"W_TEXT","targetHandle":"input","label":"\"locale context\""}
    - {"id":"index-e08-15022114","source":"BR_VARIANT","sourceHandle":"\"swap","target":"W_TEXT","targetHandle":"recompute\"","label":"\"swap → recompute\""}
    - {"id":"index-e09-4256426980","source":"W_TEXT","sourceHandle":"output","target":"W_IMG","targetHandle":"input","label":"\"text_out\""}
    - {"id":"index-e10-2555313008","source":"W_IMG","sourceHandle":"output","target":"W_VID","targetHandle":"input","label":"\"imageUrl\""}
    - {"id":"index-e11-2689692277","source":"W_VID","sourceHandle":"output","target":"W_PANEL","targetHandle":"input","label":"\"videoUrl\""}
    - {"id":"index-e12-1056658522","source":"A_BP","sourceHandle":"output","target":"W_TEXT","targetHandle":"input","label":"\"completions · generations · renders\""}
---
# Knowgrph

## Authoring Contract

- The opening YAML frontmatter block remains the first-block machine SSOT for renderer activation, graph metadata, and reusable product narrative inputs.
- This document is a canonical authored product/readme demo, not a typed normalization fixture.
- Frontmatter stays in plain YAML so the file demonstrates the default authoring path for product, architecture, and demo overview docs.
- If typed `{key, type, value}` envelopes are needed for ingestion-regression coverage, that validation should live in a dedicated fixture doc rather than replacing the canonical readme-style authoring example.
- Runtime behavior must still be derived from parsed frontmatter and graph content only, never from file path assumptions or hardcoded demo fallbacks.

**Brief in. Campaign out.** A node canvas where Markdown becomes images — and images become video — orchestrated by AI. Built for solo creators who already know CapCut and need to go further without starting over.

> Not a replacement. An extension.

Watch on YouTube: [airvio | rich media canvas for global emerging market creators](https://youtu.be/RkPzWb4Bi8w)

[![airvio | rich media canvas for global emerging market creators](https://raw.githubusercontent.com/huijoohwee/huijoohwee/main/docs_/airvio-knowgrph.png)](https://youtu.be/RkPzWb4Bi8w)

---

## The problem — the middle is empty

Every creator eventually hits a ceiling. The tool that got them here can't take them further.

| | Too sophisticated | Just right | Too simple |
|---|---|---|---|
| **Tool** | Node-graph editors · Higgsfield | **← Knowgrph fits here →** | CapCut |
| **Learning curve** | Hours to days | Minutes | Seconds |
| **Local context** | Possible but manual | Built-in to the brief | None |
| **Variants** | Manual wiring | Swap one field, N exports | Full re-edit |
| **Who it's for** | Technical users | **Solopreneurs · freelancers · creators** | Anyone |

CapCut is fast for one video. It breaks when a creator needs ten — same brand, three markets, two formats. Every variant is a full manual re-edit. No brand memory. No locale context. No pipeline.

Node-graph editors are too steep. Higgsfield is powerful but context-blind — it doesn't know that Eid gifting is not Christmas gifting, that a Wild West frontier aesthetic needs a different energy than a Caribbean island, or that your brand font is not the default.

**Knowgrph is the middle path** — structured enough to scale, simple enough to start in minutes.

---

## Who it's for — global emerging market creators

The ICP is not a geography. It's a situation: **a solo creator, freelancer, or one-person business in a fragmented emerging market who makes content for a local audience and needs local context baked in.**

This person exists in:
- Southeast Asia (Jakarta, Manila, Bangkok, Ho Chi Minh City, Singapore)
- Latin America (Mexico City, São Paulo, Bogotá, Buenos Aires)
- MENA (Cairo, Riyadh, Lagos, Dubai)
- South Asia (Mumbai, Dhaka, Karachi)
- Frontier markets everywhere — including the US creator economy's long tail and the Caribbean

What they share: they already use CapCut. They've hit a ceiling. They want to ship more, faster, without a learning curve. They want a tool that knows their market, their language, their cultural moment — without having to explain it every time.

**They don't want to replace CapCut. They want something that picks up where CapCut stops.**

---

## The insight — extend, don't replace

Knowgrph augments the CapCut workflow. It doesn't compete with it.

A CapCut creator already knows what good video looks like. Knowgrph handles the part that kills them: re-editing the same brief six times by hand for six markets.

If you can write a scene plan as structured Markdown, then:
- **AI becomes the orchestrator** — text node produces localised scene plans, image node renders culturally-grounded keyframes, video node composes the clip
- **The brief becomes brand memory** — palette, font, tone, cultural context, locale — locked once, inherited by every downstream node
- **Upstream change → downstream recompute** — swap one field, every variant updates automatically

```
CapCut creator → hits variant ceiling
→ gets Knowgrph template from a creator group
→ runs once → ships 6 variants
→ shares template forward → new creator joins
```

Template sharing is the distribution loop, same as CapCut templates spread today. Every share is a distribution event.

---

## What it does

One Markdown brief. Three pipeline stages. N variants.

```mermaid
flowchart LR
  subgraph Brief
    MD["Markdown brief\nbrand + locale + shots"]
  end
  subgraph Produce
    MD --> SA["Knowgrph SuperAgent\nresearch + tools"]
    SA --> TG["Text Gen\nscene plan + captions"]
    TG --> IG["Image Gen\nlocal keyframes"]
    IG --> VG["Video Gen\n9:16 clip"]
  end
  subgraph Reuse
    VG --> RMP["Rich Media Panel\npreview + export"]
    SWAP["swap variant field"] --> SA
  end
```

The brief carries three locked layers:

```markdown
## Campaign brief · variant: US-WEST
Brand: SkyKids · Palette: amber, sand · Tone: frontier · adventurous
Product: RoboDrone X1 · Age: 8–14 · Price: $49
— parent layer —
Trust: obstacle-sense / 20-min flight / crash-proof shell
— child adventure layer —
Shot 1: boy on mesa cliff, sunrise, drone launches
Shot 2: ghost mustang herd charges across sky-plain above canyon
Shot 3: drone banks through cathedral arch light beams
CTA: "Ship it before school break!" · Format: 9:16 · Platform: TikTok US
```

Swap `variant: US-WEST` → `variant: CARIBBEAN`. Hook rewrites. Keyframes change. Video recomposes. **Zero manual re-edit.**

---

## Demo — RoboDrone X1 · Three Skies

Same drone. Three worlds. Three completely different children. Three completely different reasons a parent buys it.

**US · Wild West frontier mesa**
- Real scene: boy on sandstone cliff at sunrise, canyon below
- Multiverse: ghost mustang herd charges silver across a sky-plain above the canyon; spectral frontier town hangs inverted from the clouds; drone leads the stampede through cathedral light arches
- Parent trust: crash-proof shell, obstacle-sense, 20-min flight
- Hook: *"Lead the ghost herd. Own the frontier."*

**Caribbean · island tempest**
- Real scene: girl on white-sand beach, tropical storm rolling in off turquoise water
- Multiverse: drone punches through the rain wall; mermaid queen rises from the deep — coral crown, bioluminescent scales; drone descends as her herald through a cathedral of lightning-lit coral spires
- Parent trust: waterproof-rated, obstacle-sense, crash-proof shell
- Hook: *"Fly the tempest. Serve the queen."*

**Singapore · Marina Bay → RoboTown**
- Real scene: girl on Marina Bay promenade at blue-hour dusk
- Multiverse: Merlion morphs to 100m chrome AI sentinel with amber scanning eyes; city becomes RoboTown — sensor arrays, drone corridors, neural grid bay; girl's drone ascends to command position
- Parent trust: precision sensors, 20-min flight, crash-proof shell
- Hook: *"Command the future. Your city. Your drone."*

**Canvas reveal:** pull-back from SG command position — three locale scenes materialise as glowing nodes on a dark canvas, connected by luminous bezier threads. Three parent silhouettes at each node base. A cursor hovers. One brief. Three multiverses.

---

## Architecture

Client-first. The browser handles parsing, rendering, and canvas orchestration. Long-horizon research/code/create work runs through Knowgrph's native SuperAgent harness and can optionally call a DeerFlow local gateway as a provider. DeerFlow is a conceptual reference and optional gateway, not copied architecture and not the required renderer/parser owner.

```mermaid
flowchart LR
  MD[Markdown brief] --> FC[Storyboard Canvas]
  FC --> SA["Knowgrph SuperAgent Harness\nmessage gateway · memory · tools · sandbox"]
  SA -->|"shared provider adapters"| LLM["Multi-provider LLM\nOpenAI · Claude · Gemini · BytePlus"]
  SA -->|"image tool/provider"| IMG["Image outputs\nimageUrl"]
  SA -->|"video tool/provider"| VID["Video outputs\nvideoUrl"]
  SA -->|"creation tool"| PPT["Slide deck\n.pptx export"]
  SA --> RMP[Rich Media Panel]
  FC --> RMP
  RMP --> EXP["Export: MP4 / PNG / JSON / PPTX"]
```

### SuperAgent and DeerFlow Boundary

Knowgrph's canvas provides the **visual pipeline**: nodes, edges, panels, variant switching, and shared Rich Media Panel previews. The native SuperAgent harness provides bounded long-horizon coordination for research, tools, memory, subagents, sandboxed workspace artifacts, and verification. DeerFlow can inform concepts or serve as an optional gateway provider, but it must not replace Knowgrph's markdown/frontmatter, Storyboard Widget, or Rich Media Panel owners.

| Canvas concern | Knowgrph owner | Optional provider/inspiration |
|---|---|---|
| Pipeline layout | Storyboard Widget DAG | — |
| Variant switching | Brief layer swap | — |
| Artifact rendering | Rich Media Panel | — |
| Prompt engineering | SuperAgent planner/tool lane | Optional DeerFlow gateway |
| Image generation | Shared image tool writes `imageUrl` | Optional provider |
| Video generation | Shared video tool writes `videoUrl` | Optional provider |
| Multi-provider routing | Settings + provider adapters | Optional DeerFlow config |
| Multi-locale parallelism | Role-scoped subagent contracts | Conceptual reference only |
| PPT composition | Creation tool writes workspace artifact | Optional provider |
| Retry / error handling | Bounded run state + verifier | Conceptual reference only |

**Direct API works for simple cases.** The native harness adds value when the run needs minutes-to-hours reasoning before generation, multi-step pipelines (text -> image -> video -> PPT), provider flexibility, or parallel execution across variants.

| Layer | Technology |
|---|---|
| Frontend | React 18 + TypeScript + Vite 6 |
| 2D / 3D | D3.js · Three.js + R3F |
| Markdown | markdown-it + Mermaid + KaTeX |
| Agent orchestrator | Knowgrph native SuperAgent harness — message gateway · memory · tools · skills · sandbox |
| AI runtime | Shared provider adapters — OpenAI · Claude · Gemini · BytePlus · optional DeerFlow gateway |
| Image generation | Shared image tool output — `imageUrl` |
| Video generation | Shared video tool output — `videoUrl` |
| Local DB | RxDB — offline-first |
| Parsers | Python 3.10+ — NetworkX · DuckDB |
| Payments | Stripe — subscription + usage |
| Deployment | Cloudflare Pages (PWA) — airvio.co/knowgrph |

Shell: ~248 KB gzip. Monaco, Mermaid, Three.js lazy-loaded.

---

## Business model

**Workspace subscription** — canvas, collaboration, storage, template library.  
**Usage-based compute** — per-image and per-second pricing with explicit budget caps. No surprise bills.  
**Template marketplace** — creators sell locale-aware pipeline templates; buyers get a proven brief-to-video workflow, not just a prompt.

---

## Roadmap

**Now** — brief→video pipeline, native SuperAgent harness (research + tools + sandbox), Storyboard Canvas, Stripe gating
**Next** — batch variant generation via role-scoped subagents, eval harness, scene template library, MCP server
**Later** — mobile-first brief editor (form UI over Markdown), real-time collaboration, plugin system

---

## The ask

**Design partners** — solo creators and freelancers who've hit the CapCut ceiling and are shipping content across 2+ markets or languages.  
**Distribution intros** — creator community leads, influencer networks, TikTok Shop / Shopee seller communities in any emerging market.  
**Locale briefs** — real-world campaign specs to encode as Markdown pipelines and seed the template marketplace.

If you believe video creation should be as reusable as code — declarative, local-aware, automatable — let us build it together.

---

**Demo:** airvio.co/knowgrph  

**Docs:** see `docs/conflict-resolution.md` for the repo conflict-resolution and sync policy.  

> *"Write it. See it. Ship it."*
