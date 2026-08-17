---

title: "Knowgrph — Map it. Score it. Decide it."
id: md:knowgrph-readme-v4
author: joohwee
institution: "Knowgrph — airvio.co/knowgrph"
date: "2026-05-03"
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
      problem:   "#c0392b — red    — pain point / market gap / decision failure"
      insight:   "#d68910 — amber  — reframe / principle / scored signal"
      product:   "#1a6fa8 — blue   — tool / pipeline stage / canvas layer"
      actor:     "#1e8449 — green  — user segment / stakeholder / decision-maker"
      output:    "#7d3c98 — purple — artifact / scored report / data export"
      business:  "#117a65 — teal   — revenue line / model tier"
      milestone: "#5d6d7e — grey   — roadmap item"
      mcp:       "#0e4f6b — navy   — MCP tool / external API connector"
      signal:    "#1a7f5a — forest — ranked result / TOPSIS score / market signal"
    edges:
      user_flow:   "solid #2980b9  2px   — actor interacts with product surface"
      work_flow:   "dashed #d68910 2px   — pitch section narrative progression"
      data_flow:   "dotted #7d3c98 1.5px — artifact passes between pipeline stages"
      mcp_flow:    "solid #0e4f6b  1.5px — MCP tool call → collected data"
      signal_flow: "dotted #1a7f5a 1.5px — ranked signal feeds decision layer"
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
      classDef mcp       fill:#0e4f6b,color:#fff,stroke:#083444,stroke-width:1.5px
      classDef signal    fill:#1a7f5a,color:#fff,stroke:#125c40,stroke-width:1.5px

      subgraph S0["① Hook"]
        TAGLINE["Map it. Score it. Decide it."]:::insight
        POS["Geo data in · ranked decision out · no analyst required"]:::insight
      end

      subgraph S1["② Problem — Location Decisions Are Still Spreadsheets"]
        subgraph S1A["Too manual"]
          P_SHEET["Spreadsheet audits — hours of copy-paste per candidate"]:::problem
          P_STALE["Stale data — offline reports miss live POI density"]:::problem
        end
        subgraph S1B["Too opaque"]
          P_GUT["Gut-feel site picks — no reproducible scoring model"]:::problem
          P_SILO["Routing + competition + catchment analysed in separate tools"]:::problem
        end
        P_GAP["Decision-maker flying blind — no unified, live, scored view"]:::problem
      end

      subgraph S2["③ ICP — Local Market Decision-Makers"]
        subgraph S2A["Who"]
          ICP_FB["F&B operator — new outlet / expansion"]:::actor
          ICP_RET["Retailer / pop-up brand — site shortlisting"]:::actor
          ICP_DEV["Property developer — catchment due diligence"]:::actor
          ICP_CON["Management consultant — market entry advisory"]:::actor
        end
        subgraph S2B["Where — fragmented, data-poor markets"]
          MKT_SEA["Southeast Asia — SG MY TH ID PH VN"]:::actor
          MKT_MENA["MENA — AE SA EG"]:::actor
          MKT_SA["South Asia — IN BD PK"]:::actor
          MKT_LATAM["Latin America — MX BR CO"]:::actor
        end
        subgraph S2C["Situation"]
          SIT_CAND["Has 5–20 candidate locations · no time to survey all"]:::actor
          SIT_LOOP["Needs scored shortlist → site visit → final call"]:::insight
        end
      end

      subgraph S3["④ Insight — APIs Know More Than Any Analyst"]
        I_LIVE["Live POI density = real competition, not last year's survey"]:::insight
        I_MCP["MCP tools = maps APIs callable in a pipeline, not a browser tab"]:::insight
        I_TOPSIS["TOPSIS = transparent, weight-tunable, auditable scoring"]:::insight
        I_AUTO["Swap weight → all C* scores recompute in seconds"]:::insight
        I_POS["One pipeline. N candidates. One ranked output."]:::insight
      end

      subgraph S4["⑤ Product — Site Selection Canvas"]
        subgraph S4A["Discover — MCP Layer"]
          MCP_POI["POI Search — keyword · country · density"]:::mcp
          MCP_NEAR["Nearby Search — radius · rank_by=popularity"]:::mcp
          MCP_NAV["Routing ETA — walking · driving · cycling profiles"]:::mcp
        end
        subgraph S4B["Score — TOPSIS Engine"]
          SC_MAT["Decision Matrix — m candidates × n criteria"]:::product
          SC_NORM["Weighted Normalization — w_j × r_ij"]:::product
          SC_RANK["C* Ranking — D⁻ / (D⁺ + D⁻) per candidate"]:::signal
        end
        subgraph S4C["Report Layer"]
          OUT_RANK["Ranked Site Report — C* scores + sensitivity"]:::output
          OUT_MAP["Scored Map Canvas — visual heat overlay"]:::output
          OUT_MD["Markdown export — portable · version-controlled"]:::output
        end
      end

      subgraph S5["⑥ Demo — New Cafe · Singapore · 7 Candidates"]
        DM_BPJ["🥇 Bukit Panjang  C*=0.82 — zero competition · 16-sec MRT"]:::signal
        DM_PGL["🥈 Punggol        C*=0.78 — 22 residential POIs · young demo"]:::signal
        DM_WDL["🥉 Woodlands      C*=0.71 — zero competition · causeway traffic"]:::signal
        DM_SKG["✗  Sengkang       C*=0.22 — 6 cafes incl. 2 Starbucks"]:::problem
        DM_CBD["✗  CBD            C*=0.09 — baseline saturation"]:::problem
        DM_API["23 API calls · 5 MCP tools · 8 criteria · 1 ranked output"]:::product
      end

      subgraph S6["⑦ Architecture"]
        A_MCP["MCP Connectors — POI · nearby · navigation"]:::mcp
        A_SC["TOPSIS Engine — Python · NetworkX · DuckDB"]:::product
        A_FE["React 18 + TS + Vite — canvas + map overlay"]:::product
        A_DB["RxDB — offline-first · version-controlled reports"]:::product
        A_CF["Cloudflare Pages · Stripe"]:::product
      end

      subgraph S7["⑧ Business Model"]
        B_REP["Per-report — pay-per-scored-shortlist"]:::business
        B_SUB["Workspace subscription — unlimited scoring · saved canvases"]:::business
        B_API["API tier — embed scorer in existing tools"]:::business
        B_CON["Advisory — custom weight models per industry vertical"]:::business
      end

      subgraph S8["⑨ Roadmap"]
        R_NOW["Now — MCP pipeline · TOPSIS scorer · Markdown report · Stripe"]:::milestone
        R_NEXT["Next — scored map canvas · multi-provider geo adapter · batch candidates"]:::milestone
        R_LATER["Later — rent-index integration · real-time rescore · collab workspace"]:::milestone
      end

      subgraph S9["⑩ The Ask"]
        ASK_DP["Design partners — F&B / retail operators with live site decisions"]:::actor
        ASK_GEO["Geo API access — maps POI + routing connectors per market"]:::mcp
        ASK_DATA["Ground-truth datasets — site visits to validate C* predictions"]:::output
        ASK_DIST["Distribution — property consultants · franchise networks · VC portfolio ops"]:::actor
      end

      %% USER FLOW
      ICP_FB -->|"shortlists candidates"| MCP_POI
      ICP_RET -->|"scopes market"| MCP_NEAR
      ICP_CON -->|"advises on"| OUT_RANK
      SIT_CAND -->|"inputs to"| SC_MAT

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

      %% MCP FLOW
      MCP_POI -->|"poi_density"| SC_MAT
      MCP_NEAR -->|"competition_count"| SC_MAT
      MCP_NAV -->|"eta_minutes"| SC_MAT
      SC_MAT -->|"normalize · weight"| SC_NORM
      SC_NORM -->|"C* per candidate"| SC_RANK

      %% DATA FLOW
      SC_RANK -->|"ranked signal"| OUT_RANK
      SC_RANK -->|"heat scores"| OUT_MAP
      OUT_RANK -->|"export"| OUT_MD
      A_MCP -->|"live calls"| MCP_POI
      A_MCP -->|"live calls"| MCP_NEAR
      A_MCP -->|"live calls"| MCP_NAV
flow:
  edgeType: {key: "edgeType", type: string, value: "smoothstep"}
  balancedViewportPreset: {key: "balancedViewportPreset", type: string, value: "widgetFrontmatter"}
  computed: {key: "computed", type: boolean, value: true}
  snapToGrid: {key: "snapToGrid", type: boolean, value: true}
  direction: {key: direction, type: string, value: "LR"}
  nodes:
    - id: {key: id, type: string, value: "A_CF"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Cloudflare Pages · Stripe"}
      position: {key: position, type: object, value: {"x":0,"y":-7320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_CF"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "A_DB"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "RxDB — offline-first · version-controlled reports"}
      position: {key: position, type: object, value: {"x":0,"y":-7080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_DB"}
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
      label: {key: label, type: string, value: "React 18 + TS + Vite — canvas + map overlay"}
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
    - id: {key: id, type: string, value: "A_MCP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "MCP Connectors — POI · nearby · navigation"}
      position: {key: position, type: object, value: {"x":0,"y":-6600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_MCP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 3}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "A_SC"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "TOPSIS Engine — Python · NetworkX · DuckDB"}
      position: {key: position, type: object, value: {"x":0,"y":-6360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:A_SC"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DATA"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Ground-truth datasets — site visits to validate C* predictions"}
      position: {key: position, type: object, value: {"x":0,"y":-6120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DATA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DIST"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Distribution — property consultants · franchise networks · VC portfolio ops"}
      position: {key: position, type: object, value: {"x":0,"y":-5880}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DIST"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_DP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Design partners — F&B / retail operators with live site decisions"}
      position: {key: position, type: object, value: {"x":0,"y":-5640}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_DP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ASK_GEO"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Geo API access — maps POI + routing connectors per market"}
      position: {key: position, type: object, value: {"x":0,"y":-5400}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ASK_GEO"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_API"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "API tier — embed scorer in existing tools"}
      position: {key: position, type: object, value: {"x":0,"y":-5160}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_API"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_CON"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Advisory — custom weight models per industry vertical"}
      position: {key: position, type: object, value: {"x":0,"y":-4920}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_CON"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_REP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Per-report — pay-per-scored-shortlist"}
      position: {key: position, type: object, value: {"x":0,"y":-4680}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_REP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "B_SUB"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Workspace subscription — unlimited scoring · saved canvases"}
      position: {key: position, type: object, value: {"x":0,"y":-4440}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:B_SUB"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_API"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "23 API calls · 5 MCP tools · 8 criteria · 1 ranked output"}
      position: {key: position, type: object, value: {"x":0,"y":-4200}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_API"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_BPJ"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "🥇 Bukit Panjang  C*=0.82 — zero competition · 16-sec MRT"}
      position: {key: position, type: object, value: {"x":0,"y":-3960}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_BPJ"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_CBD"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "✗  CBD            C*=0.09 — baseline saturation"}
      position: {key: position, type: object, value: {"x":0,"y":-3720}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_CBD"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_PGL"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "🥈 Punggol        C*=0.78 — 22 residential POIs · young demo"}
      position: {key: position, type: object, value: {"x":0,"y":-3480}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_PGL"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_SKG"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "✗  Sengkang       C*=0.22 — 6 cafes incl. 2 Starbucks"}
      position: {key: position, type: object, value: {"x":0,"y":-3240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_SKG"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "DM_WDL"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "🥉 Woodlands      C*=0.71 — zero competition · causeway traffic"}
      position: {key: position, type: object, value: {"x":0,"y":-3000}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:DM_WDL"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_AUTO"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Swap weight → all C* scores recompute in seconds"}
      position: {key: position, type: object, value: {"x":0,"y":-2760}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_AUTO"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_LIVE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Live POI density = real competition, not last year's survey"}
      position: {key: position, type: object, value: {"x":0,"y":-2520}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_LIVE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_MCP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "MCP tools = maps APIs callable in a pipeline, not a browser tab"}
      position: {key: position, type: object, value: {"x":0,"y":-2280}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_MCP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_POS"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "One pipeline. N candidates. One ranked output."}
      position: {key: position, type: object, value: {"x":0,"y":-2040}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_POS"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "I_TOPSIS"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "TOPSIS = transparent, weight-tunable, auditable scoring"}
      position: {key: position, type: object, value: {"x":0,"y":-1800}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:I_TOPSIS"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_CON"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Management consultant — market entry advisory"}
      position: {key: position, type: object, value: {"x":0,"y":-1560}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_CON"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_DEV"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Property developer — catchment due diligence"}
      position: {key: position, type: object, value: {"x":0,"y":-1320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_DEV"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "ICP_FB"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "F&B operator — new outlet / expansion"}
      position: {key: position, type: object, value: {"x":0,"y":-1080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_FB"}
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
    - id: {key: id, type: string, value: "ICP_RET"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Retailer / pop-up brand — site shortlisting"}
      position: {key: position, type: object, value: {"x":0,"y":-840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:ICP_RET"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MKT_LATAM"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Latin America — MX BR CO"}
      position: {key: position, type: object, value: {"x":0,"y":-600}}
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
      label: {key: label, type: string, value: "MENA — AE SA EG"}
      position: {key: position, type: object, value: {"x":0,"y":-360}}
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
      position: {key: position, type: object, value: {"x":0,"y":-120}}
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
      label: {key: label, type: string, value: "Southeast Asia — SG MY TH ID PH VN"}
      position: {key: position, type: object, value: {"x":0,"y":120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MKT_SEA"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_GAP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Decision-maker flying blind — no unified, live, scored view"}
      position: {key: position, type: object, value: {"x":0,"y":360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_GAP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_GUT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Gut-feel site picks — no reproducible scoring model"}
      position: {key: position, type: object, value: {"x":0,"y":600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_GUT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_SHEET"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Spreadsheet audits — hours of copy-paste per candidate"}
      position: {key: position, type: object, value: {"x":0,"y":840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_SHEET"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_SILO"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Routing + competition + catchment analysed in separate tools"}
      position: {key: position, type: object, value: {"x":0,"y":1080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_SILO"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "P_STALE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Stale data — offline reports miss live POI density"}
      position: {key: position, type: object, value: {"x":0,"y":1320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:P_STALE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "POS"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Geo data in · ranked decision out · no analyst required"}
      position: {key: position, type: object, value: {"x":0,"y":1560}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:POS"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_LATER"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Later — rent-index integration · real-time rescore · collab workspace"}
      position: {key: position, type: object, value: {"x":0,"y":1800}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_LATER"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_NEXT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Next — scored map canvas · multi-provider geo adapter · batch candidates"}
      position: {key: position, type: object, value: {"x":0,"y":2040}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_NEXT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "R_NOW"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Now — MCP pipeline · TOPSIS scorer · Markdown report · Stripe"}
      position: {key: position, type: object, value: {"x":0,"y":2280}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:R_NOW"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S0"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "① Hook"}
      position: {key: position, type: object, value: {"x":0,"y":2520}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S0"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "② Problem — Location Decisions Are Still Spreadsheets"}
      position: {key: position, type: object, value: {"x":0,"y":2760}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Too manual"}
      position: {key: position, type: object, value: {"x":0,"y":3000}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S1B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Too opaque"}
      position: {key: position, type: object, value: {"x":0,"y":3240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S1B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "③ ICP — Local Market Decision-Makers"}
      position: {key: position, type: object, value: {"x":0,"y":3480}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Who"}
      position: {key: position, type: object, value: {"x":0,"y":3720}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Where — fragmented, data-poor markets"}
      position: {key: position, type: object, value: {"x":0,"y":3960}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S2C"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Situation"}
      position: {key: position, type: object, value: {"x":0,"y":4200}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S2C"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S3"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "④ Insight — APIs Know More Than Any Analyst"}
      position: {key: position, type: object, value: {"x":0,"y":4440}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S3"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑤ Product — Site Selection Canvas"}
      position: {key: position, type: object, value: {"x":0,"y":4680}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 7}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4A"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Discover — MCP Layer"}
      position: {key: position, type: object, value: {"x":0,"y":4920}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4A"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4B"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Score — TOPSIS Engine"}
      position: {key: position, type: object, value: {"x":0,"y":5160}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4B"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 8}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S4C"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Report Layer"}
      position: {key: position, type: object, value: {"x":0,"y":5400}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S4C"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -7}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S5"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑥ Demo — New Cafe · Singapore · 7 Candidates"}
      position: {key: position, type: object, value: {"x":0,"y":5640}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S5"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -6}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S6"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑦ Architecture"}
      position: {key: position, type: object, value: {"x":0,"y":5880}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S6"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -5}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S7"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑧ Business Model"}
      position: {key: position, type: object, value: {"x":0,"y":6120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S7"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S8"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑨ Roadmap"}
      position: {key: position, type: object, value: {"x":0,"y":6360}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S8"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "S9"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "⑩ The Ask"}
      position: {key: position, type: object, value: {"x":0,"y":6600}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:S9"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "SIT_CAND"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Has 5–20 candidate locations · no time to survey all"}
      position: {key: position, type: object, value: {"x":0,"y":6840}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:SIT_CAND"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "SIT_LOOP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Needs scored shortlist → site visit → final call"}
      position: {key: position, type: object, value: {"x":0,"y":7080}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:SIT_LOOP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "TAGLINE"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Map it. Score it. Decide it."}
      position: {key: position, type: object, value: {"x":0,"y":7320}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:TAGLINE"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "MCP_NAV"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Routing ETA — walking · driving · cycling profiles"}
      position: {key: position, type: object, value: {"x":380,"y":-240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MCP_NAV"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -4}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "MCP_NEAR"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Nearby Search — radius · rank_by=popularity"}
      position: {key: position, type: object, value: {"x":380,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MCP_NEAR"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "MCP_POI"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "POI Search — keyword · country · density"}
      position: {key: position, type: object, value: {"x":380,"y":240}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:MCP_POI"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 1}
    - id: {key: id, type: string, value: "SC_MAT"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Decision Matrix — m candidates × n criteria"}
      position: {key: position, type: object, value: {"x":760,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:SC_MAT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 5}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 4}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 32}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 18.94427190999916}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 2}
    - id: {key: id, type: string, value: "SC_NORM"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Weighted Normalization — w_j × r_ij"}
      position: {key: position, type: object, value: {"x":1140,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:SC_NORM"}
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
    - id: {key: id, type: string, value: "SC_RANK"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "C* Ranking — D⁻ / (D⁺ + D⁻) per candidate"}
      position: {key: position, type: object, value: {"x":1520,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:SC_RANK"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 8}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 4}
    - id: {key: id, type: string, value: "OUT_MAP"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Scored Map Canvas — visual heat overlay"}
      position: {key: position, type: object, value: {"x":1900,"y":-120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:OUT_MAP"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -3}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 5}
    - id: {key: id, type: string, value: "OUT_RANK"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Ranked Site Report — C* scores + sensitivity"}
      position: {key: position, type: object, value: {"x":1900,"y":120}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:OUT_RANK"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 24}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 16.928203230275507}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 5}
    - id: {key: id, type: string, value: "OUT_MD"}
      type: {key: type, type: string, value: "default"}
      label: {key: label, type: string, value: "Markdown export — portable · version-controlled"}
      position: {key: position, type: object, value: {"x":2280,"y":0}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:OUT_MD"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: -2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 6}
  edges:
    - {"id":"index-e01-4066605831","source":"ICP_FB","sourceHandle":"output","target":"MCP_POI","targetHandle":"input","label":"\"shortlists candidates\""}
    - {"id":"index-e02-1983666018","source":"ICP_RET","sourceHandle":"output","target":"MCP_NEAR","targetHandle":"input","label":"\"scopes market\""}
    - {"id":"index-e03-3024636150","source":"ICP_CON","sourceHandle":"output","target":"OUT_RANK","targetHandle":"input","label":"\"advises on\""}
    - {"id":"index-e04-2507280472","source":"SIT_CAND","sourceHandle":"output","target":"SC_MAT","targetHandle":"input","label":"\"inputs to\""}
    - {"id":"index-e05-2080970665","source":"MCP_POI","sourceHandle":"output","target":"SC_MAT","targetHandle":"input","label":"\"poi_density\""}
    - {"id":"index-e06-678798771","source":"MCP_NEAR","sourceHandle":"output","target":"SC_MAT","targetHandle":"input","label":"\"competition_count\""}
    - {"id":"index-e07-3100433483","source":"MCP_NAV","sourceHandle":"output","target":"SC_MAT","targetHandle":"input","label":"\"eta_minutes\""}
    - {"id":"index-e08-3816246444","source":"SC_MAT","sourceHandle":"output","target":"SC_NORM","targetHandle":"input","label":"\"normalize · weight\""}
    - {"id":"index-e09-1126820267","source":"SC_NORM","sourceHandle":"output","target":"SC_RANK","targetHandle":"input","label":"\"C* per candidate\""}
    - {"id":"index-e10-1068625777","source":"SC_RANK","sourceHandle":"output","target":"OUT_RANK","targetHandle":"input","label":"\"ranked signal\""}
    - {"id":"index-e11-995540405","source":"SC_RANK","sourceHandle":"output","target":"OUT_MAP","targetHandle":"input","label":"\"heat scores\""}
    - {"id":"index-e12-1614676189","source":"OUT_RANK","sourceHandle":"output","target":"OUT_MD","targetHandle":"input","label":"\"export\""}
    - {"id":"index-e13-2701065364","source":"A_MCP","sourceHandle":"output","target":"MCP_POI","targetHandle":"input","label":"\"live calls\""}
    - {"id":"index-e14-395334272","source":"A_MCP","sourceHandle":"output","target":"MCP_NEAR","targetHandle":"input","label":"\"live calls\""}
    - {"id":"index-e15-1514797407","source":"A_MCP","sourceHandle":"output","target":"MCP_NAV","targetHandle":"input","label":"\"live calls\""}
---
# Knowgrph

**Candidates in. Ranked decisions out.** A knowledge graph canvas that calls live map APIs via MCP tools, scores every candidate location through a TOPSIS multi-criteria engine, and delivers a portable, auditable site selection report — in minutes, not weeks.

> Not a dashboard. A decision pipeline.

---

## The problem — location decisions are still spreadsheets

Opening a cafe, placing a retail pop-up, entering a new market. The question is always the same: *which location?* The answer is almost always the same process: someone opens a spreadsheet, pastes in addresses, drives around, argues from gut feel, picks.

| | Status quo | Knowgrph |
|---|---|---|
| **Data freshness** | Offline reports, last-year surveys | Live POI density via MCP API calls |
| **Competition analysis** | Manual Google Maps tab-switching | `nearby_search` → competitor count per radius |
| **Routing / accessibility** | Estimated or ignored | `navigation` ETA — walking · driving · cycling |
| **Scoring model** | Gut feel, no audit trail | TOPSIS C* — weighted, normalized, reproducible |
| **Time per candidate** | 2–4 hours | Seconds per API call |
| **Output** | PowerPoint with vibes | Ranked Markdown report · scored map canvas |

The analyst time cost is real. The opacity is the bigger problem — a site pick that can't be interrogated can't be improved.

**Knowgrph makes location intelligence reproducible, live, and legible.**

---

## Who it's for

The ICP is not an industry. It's a decision type: **anyone shortlisting physical locations who needs scored, evidence-based output faster than a traditional market study allows.**

This person operates in:

- **F&B expansion** — franchise operators, independent restaurant groups, cloud kitchen networks opening outlet #2 to #10
- **Retail / pop-up brands** — DTC brands, seasonal activations, market stall operators choosing between 5–20 viable sites
- **Property development** — developers benchmarking commercial lots; landlords advising anchor tenant fit
- **Management consulting** — market entry advisory, retail network optimisation, competitor gap analysis across city districts

They share one bottleneck: **too many candidates, not enough scored data, not enough time.**

Markets where the gap is sharpest — Southeast Asia (SG MY TH ID PH VN), MENA (AE SA EG), South Asia (IN BD), Latin America (MX BR CO) — have high physical retail density, fragmented POI data, and no local equivalent of a mature market research platform.

---

## The insight — APIs already know

Maps platforms index millions of POIs, update in near-real-time, and expose everything needed for a rigorous site evaluation: competitor counts, category density, footfall proxies, transit ETAs across walking, driving, and cycling profiles.

None of that requires a field visit. It requires a pipeline.

```
candidate coordinates
→ MCP: POST nearby_search       → competitor count + F&B density
→ MCP: GET /place/v2/nearby     → residential + retail + commercial POI count
→ MCP: POST navigation          → walking ETA to transit · driving ETA to centre
→ TOPSIS: normalize · weight    → C* score per candidate
→ output: ranked report         → top 3 with sensitivity analysis
```

Swap a weight. All scores recompute. Same reproducibility as code.

---

## What it does

```mermaid
flowchart LR
  subgraph Discover["Discover — MCP Layer"]
    POI["POI Search\nkeyword · country · limit"]
    NEAR["Nearby Search\nradius · rank_by=popularity"]
    NAV["Routing ETA\nwalking · driving · cycling"]
  end
  subgraph Score["Score — TOPSIS Engine"]
    MAT["Decision Matrix\nm candidates × n criteria"]
    NORM["Weighted Normalization\nw_j × r_ij"]
    RANK["C* Ranking\nD⁻ / (D⁺ + D⁻)"]
  end
  subgraph Output["Output"]
    RPT["Ranked Report\nscored shortlist + sensitivity"]
    MAP["Scored Map Canvas\nheat overlay"]
    MD["Markdown export\nportable · auditable"]
  end

  POI --> MAT
  NEAR --> MAT
  NAV --> MAT
  MAT --> NORM --> RANK
  RANK --> RPT
  RANK --> MAP
  RPT --> MD
```

### Criteria the pipeline measures

| ID | Criterion | MCP Endpoint | Direction | Weight (default) |
|----|-----------|-------------|-----------|-----------------|
| C1 | Competitor density (2.5 km) | `POST nearby_search` | Lower = better | 0.25 |
| C2 | F&B / category saturation | `GET /place/v2/nearby` | Lower = better | 0.10 |
| C3 | Residential POI count | `GET /place/v2/nearby` | Higher = better | 0.15 |
| C4 | Retail / mall POI count | `GET /place/v2/nearby` | Higher = better | 0.10 |
| C5 | Walk-to-transit ETA (min) | `POST navigation profile=walking` | Lower = better | 0.15 |
| C6 | Drive-to-centre ETA (min) | `POST navigation profile=driving` | Target range | 0.05 |
| C7 | Total area POI density | `GET /poi/v1/search` | Higher = better | 0.10 |
| C8 | Commercial building count | `GET /place/v2/nearby` | Higher = better | 0.05 |

**Transport profiles:** `walking` · `driving` · `cycling` · `motorcycle` · `tricycle`

All weights are frontmatter fields. Swap one value, all C* scores recompute.

---

## Demo — New Cafe · Singapore · 7 Candidates · 23 API Calls

**Setup:** 7 candidate areas, radius 2.5 km (~30-min walk), ranked by `popularity`. 23 MCP calls total across POI search, nearby search, and routing profiles.

### TOPSIS results

| Rank | Location | C* | Decisive signal |
|------|----------|-----|----------------|
| 🥇 1 | **Bukit Panjang** | **0.82** | Zero cafe competitors · Bukit Panjang DTL MRT **16-second walk** · C8=18 commercial buildings (highest) |
| 🥈 2 | **Punggol** | **0.78** | C1=1 (one traditional coffeeshop only) · C3=22 HDB residential POIs · young growing demographic |
| 🥉 3 | **Woodlands** | **0.71** | C1=0 · causeway commuter flow · education/childcare ecosystem → family catchment |
| 4 | Yishun | 0.62 | Northpoint City mall anchor (C4=25) · C1=0 · high F&B saturation (C2=12) offsets |
| 5 | Jurong West | 0.41 | Major transport hub · C2=20 (worst saturation) · longest MRT walk (~14 min) |
| 6 | Sengkang | 0.22 | C1=6 cafes incl. 2 Starbucks · Compass One fully served — **do not enter** |
| — | CBD | 0.09 | Baseline saturation reference only |

### Sensitivity analysis — weight shifts change the winner

| Scenario | Weight change | New winner | Rationale |
|----------|-------------|-----------|-----------|
| Maximise foot traffic | C4 mall → 0.25 | **Yishun** | Northpoint City C4=25 becomes decisive |
| Minimise rent risk | Add C9 rent index → 0.10 | **Woodlands** | Northern areas ~30% below central band |
| Weekday lunch priority | C8 commercial → 0.20 | **Bukit Panjang** | C8=18 (highest) + DTL commuter lunch crowd |
| Family demographic focus | C3 residential → 0.30 | **Punggol** | C3=22 HDB precinct — dominant residential density |
| Hard filter C1 > 2 | Eliminate saturated | **BPJ · Woodlands · Yishun** 3-way tie | MRT access breaks tie → BPJ wins |

---

## Architecture

Server-light. MCP connectors call maps APIs directly. The TOPSIS engine runs in Python. The canvas renders in the browser.

```mermaid
flowchart LR
  CAND["Candidate\ncoordinates"] --> MCP
  subgraph MCP["MCP Connectors"]
    POI["POI search"]
    NEAR["Nearby search"]
    NAV["Routing ETA"]
  end
  MCP --> PY["TOPSIS Engine\nPython · NetworkX · DuckDB"]
  PY --> RANK["C* ranked signal"]
  RANK --> FC["Storyboard Canvas\nReact 18 + TS + Vite"]
  FC --> MAP["Scored Map\nheat overlay"]
  FC --> RPT["Ranked Report\nMarkdown export"]
```

| Layer | Technology |
|---|---|
| MCP connectors | Maps APIs — POI search · nearby · routing ETA (5 transport profiles) |
| Scoring engine | TOPSIS — Python 3.10+ · NetworkX · DuckDB · weighted normalization · C* ranking |
| Frontend canvas | React 18 + TypeScript + Vite 6 · D3.js · Mermaid |
| Map overlay | D3.js / Leaflet — heat scored candidates on base map |
| Local DB | RxDB — offline-first · report versioning |
| Payments | Stripe — per-report + subscription |
| Deployment | Cloudflare Pages (PWA) — airvio.co/knowgrph |

---

## Business model

**Per-report** — pay-per-scored shortlist. Input candidates, receive ranked Markdown report + scored canvas. No subscription required to start.

**Workspace subscription** — unlimited scoring runs, saved canvases, report history, weight model library.

**API tier** — embed the TOPSIS scorer into existing property, F&B, or retail tools via REST. Bring your own geo API keys; Knowgrph handles the scoring logic.

**Advisory** — custom weight models per vertical (F&B vs. retail vs. logistics), calibrated against ground-truth site performance data.

---

## Roadmap

**Now** — MCP pipeline (POI + nearby + routing), TOPSIS scorer, ranked Markdown report, Stripe per-report gating

**Next** — scored map canvas (heat overlay), multi-provider geo adapter (swap maps API without re-wiring scorer), batch candidate import (CSV → N runs), sensitivity dashboard

**Later** — rent-index integration (URA / third-party property data), real-time rescore on candidate edit, collaborative workspace, mobile shortlisting UI

---

## The ask

**Design partners** — F&B operators, retail brands, or property consultants with live site decisions in the next 90 days. We run your shortlist through the pipeline; you validate the C* output against what you know on the ground.

**Geo API access** — teams with maps platform API keys (POI search, nearby, routing ETA) across SEA, MENA, or South Asia markets. Knowgrph is provider-agnostic; the adapter layer handles normalization.

**Ground-truth datasets** — post-opening performance data (revenue, footfall) from sites already chosen by gut feel. We back-test C* predictions against actuals to calibrate weights.

**Distribution intros** — franchise networks, VC portfolio ops teams, property consultancies, and retail expansion advisors who run multiple site decisions per quarter.

If you believe location intelligence should be as reproducible as code — scored, auditable, and re-runnable — let us build it together.

---

**Product:** airvio.co/knowgrph

**Docs:** see `docs/conflict-resolution.md` for repo sync policy.

> *"Map it. Score it. Decide it."*