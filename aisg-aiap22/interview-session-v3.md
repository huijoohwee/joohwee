---
title: "eda-mlp-interview-session"
author: "joohwee"
tags: [EDA, MLP, Test]
date: 2026-01-10
mermaidAnchorsOnly: true
mermaid: |
  flowchart TD
    %% ================================================================================
    %% AIAP Batch 22 Technical Assessment - End-to-End ML Pipeline Flow
    %% Maximum Level of Detail (LOD) - Interview Session Reference
    %% ================================================================================
    
    %% Entry Point
    START([Interview Start:<br/>Pipeline Execution]) --> LOAD_CONFIG
    
    %% ================================================================================
    %% CONFIGURATION LOADING
    %% ================================================================================
    subgraph CONFIG["🔧 Configuration Loading (src/main.py)"]
        LOAD_CONFIG[Load config.yaml] --> PARSE_CONFIG{Parse Configuration}
        PARSE_CONFIG --> CONFIG_DATA[Data Config:<br/>db_path, table]
        PARSE_CONFIG --> CONFIG_MODELS[Model Config:<br/>enabled, hyperparams]
        PARSE_CONFIG --> CONFIG_EVAL[Evaluation Config:<br/>max_fpr, threshold_grid]
        PARSE_CONFIG --> CONFIG_PREP[Preprocessing Config:<br/>scale_method, clip_quantile]
    end
    
    %% ================================================================================
    %% STEP 1: DATA LOADING
    %% ================================================================================
    subgraph STEP1["📊 STEP 1: Data Loading (src/data_loader.py)"]
        direction TB
        
        DL_INIT[DataLoader.__init__:<br/>db_path, table] --> DL_CHECK{Database<br/>Exists?}
        DL_CHECK -->|No| DL_ERROR[Raise FileNotFoundError:<br/>Download from assessment URL]
        DL_CHECK -->|Yes| DL_CONNECT[sqlite3.connect]
        
        DL_CONNECT --> DL_QUERY[Execute:<br/>SELECT * FROM table]
        DL_QUERY --> DL_DF[pd.read_sql_query:<br/>→ DataFrame]
        
        DL_DF --> DL_VALIDATE{Validate Schema:<br/>15 expected columns?}
        DL_VALIDATE -->|Missing Cols| DL_SCHEMA_ERROR[Raise ValueError:<br/>Missing columns]
        DL_VALIDATE -->|Valid| DL_SHAPE[Log Shape:<br/>11,430 rows × 15 cols]
        
        DL_SHAPE --> DL_OUTPUT[Output: df<br/>Target: label<br/>Features: 14 cols]
    end
    
    CONFIG_DATA --> DL_INIT
    DL_OUTPUT --> FE_INIT
    
    %% ================================================================================
    %% STEP 2: FEATURE ENGINEERING
    %% ================================================================================
    subgraph STEP2["🔨 STEP 2: Feature Engineering (src/feature_engineering.py)"]
        direction TB
        
        FE_INIT[FeatureEngineer.__init__:<br/>config] --> FE_START{fit or transform?}
        
        %% FIT PATH (Training Data)
        FE_START -->|fit_transform| FE_FIT_FLAGS[create_missing_flags:<br/>DomainAge_missing,<br/>Robots_missing,<br/>IsResponsive_missing]
        FE_FIT_FLAGS --> FE_FIT_BINS[bin_domain_age:<br/>bins=[0,6,12,24,inf]<br/>labels=['<6mo','6-12mo',<br/>'12-24mo','>24mo']]
        FE_FIT_BINS --> FE_FIT_RATIO[create_ratio_features:<br/>Ext_Self_Ratio =<br/>NoOfExternalRef/(NoOfSelfRef+1)]
        FE_FIT_RATIO --> FE_FIT_FREQ{config.enable_<br/>frequency_encoding?}
        FE_FIT_FREQ -->|Yes| FE_FREQ[Frequency Encoding:<br/>Industry, HostingProvider]
        FE_FIT_FREQ -->|No| FE_FIT_DONE
        FE_FREQ --> FE_FIT_DONE[Mark fitted=True]
        
        %% TRANSFORM PATH (Test Data)
        FE_START -->|transform| FE_CHECK{fitted?}
        FE_CHECK -->|No| FE_NOT_FITTED[Raise ValueError:<br/>Must fit before transform]
        FE_CHECK -->|Yes| FE_TRANS_FLAGS[Apply same transformations:<br/>No re-learning]
        FE_TRANS_FLAGS --> FE_TRANS_DONE
        
        FE_FIT_DONE --> FE_OUTPUT[Output: df_engineered<br/>+3 missing flags<br/>+1 DomainAgeBin<br/>+1 Ext_Self_Ratio]
        FE_TRANS_DONE --> FE_OUTPUT
    end
    
    FE_OUTPUT --> PREP_INIT
    
    %% ================================================================================
    %% STEP 3: PREPROCESSING PIPELINE
    %% ================================================================================
    subgraph STEP3["🧹 STEP 3: Preprocessing (src/preprocessing.py)"]
        direction TB
        
        PREP_INIT[Preprocessor.__init__:<br/>scale_method, config] --> PREP_START{fit or transform?}
        
        %% FIT PATH
        PREP_START -->|fit_transform| PREP_CLIP[clip_invalid_values:<br/>NoOfImage.clip(lower=0)]
        PREP_CLIP --> PREP_DETECT_SKEW{Detect Skewed:<br/>|skew| > 1?}
        PREP_DETECT_SKEW -->|Yes, 10 features| PREP_LOG[log_transform:<br/>np.log1p(x)]
        PREP_LOG --> PREP_OUTLIER[clip_outliers:<br/>99th percentile]
        PREP_OUTLIER --> PREP_IMPUTE_NUM[impute_missing:<br/>Median for numeric]
        PREP_IMPUTE_NUM --> PREP_IMPUTE_CAT[Mode for categorical<br/>Store values for test]
        PREP_IMPUTE_CAT --> PREP_ENCODE[encode_categorical:<br/>OneHotEncoder(handle_unknown='ignore')]
        PREP_ENCODE --> PREP_SCALE{scale_method?}
        PREP_SCALE -->|standard| PREP_STD[StandardScaler:<br/>(x-mean)/std]
        PREP_SCALE -->|robust| PREP_ROBUST[RobustScaler:<br/>(x-median)/IQR]
        PREP_STD --> PREP_FIT_DONE[fitted=True<br/>Store scalers/encoders]
        PREP_ROBUST --> PREP_FIT_DONE
        
        %% TRANSFORM PATH
        PREP_START -->|transform| PREP_TRANS_CHECK{fitted?}
        PREP_TRANS_CHECK -->|No| PREP_NOT_FITTED[Raise ValueError:<br/>Preprocessor not fitted]
        PREP_TRANS_CHECK -->|Yes| PREP_TRANS_APPLY[Apply learned params:<br/>Use stored scalers/encoders]
        PREP_TRANS_APPLY --> PREP_TRANS_DONE
        
        PREP_FIT_DONE --> PREP_OUTPUT[Output: X_preprocessed<br/>Scaled, Encoded<br/>Artifact: preprocessor.pkl]
        PREP_TRANS_DONE --> PREP_OUTPUT
    end
    
    CONFIG_PREP --> PREP_INIT
    PREP_OUTPUT --> SPLIT_INIT
    
    %% ================================================================================
    %% STEP 4: DATA SPLITTING
    %% ================================================================================
    subgraph STEP4["✂️ STEP 4: Stratified Splitting (src/data_splitter.py)"]
        direction TB
        
        SPLIT_INIT[DataSplitter.__init__:<br/>train=0.7, val=0.15, test=0.15<br/>random_state=42] --> SPLIT_VALIDATE{Ratios<br/>sum to 1.0?}
        SPLIT_VALIDATE -->|No| SPLIT_ERROR[Raise ValueError]
        SPLIT_VALIDATE -->|Yes| SPLIT_FIRST[train_test_split:<br/>stratify=y<br/>test_size=0.15]
        
        SPLIT_FIRST --> SPLIT_TEMP[X_temp 85%<br/>X_test 15%]
        SPLIT_TEMP --> SPLIT_SECOND[train_test_split:<br/>stratify=y_temp<br/>test_size=0.176]
        
        SPLIT_SECOND --> SPLIT_FINAL[X_train 70%<br/>X_val 15%<br/>X_test 15%]
        
        SPLIT_FINAL --> SPLIT_VAL_INIT[PipelineValidator.<br/>validate_split]
        SPLIT_VAL_INIT --> SPLIT_VAL_CHECK{Class distribution<br/>preserved?}
        SPLIT_VAL_CHECK -->|Drift > 2%| SPLIT_WARNING[Log Warning:<br/>Imbalance detected]
        SPLIT_VAL_CHECK -->|Valid| SPLIT_VAL_SAVE[Save to:<br/>data/processed/<br/>pipeline_validation.json]
        
        SPLIT_WARNING --> SPLIT_OUTPUT
        SPLIT_VAL_SAVE --> SPLIT_OUTPUT[Output:<br/>X_train, y_train<br/>X_val, y_val<br/>X_test, y_test]
    end
    
    SPLIT_OUTPUT --> MODEL_TRAIN_INIT
    
    %% ================================================================================
    %% STEP 5: MODEL TRAINING
    %% ================================================================================
    subgraph STEP5["🤖 STEP 5: Model Training (src/models/)"]
        direction TB
        
        MODEL_TRAIN_INIT{Which models<br/>enabled in config?} --> MODEL_LR_CHECK{logistic<br/>enabled?}
        MODEL_TRAIN_INIT --> MODEL_KNN_CHECK{knn<br/>enabled?}
        MODEL_TRAIN_INIT --> MODEL_XGB_CHECK{xgboost<br/>enabled?}
        
        %% LOGISTIC REGRESSION
        MODEL_LR_CHECK -->|Yes| MODEL_LR_INIT[LogisticRegressionModel:<br/>lr=0.1, epochs=120, l2=0.0]
        MODEL_LR_INIT --> MODEL_LR_FIT_START[fit: Initialize θ=zeros]
        MODEL_LR_FIT_START --> MODEL_LR_EPOCH{epoch < 120?}
        MODEL_LR_EPOCH -->|Yes| MODEL_LR_FORWARD[Forward Pass:<br/>z = Xθ<br/>ŷ = σ(z)]
        MODEL_LR_FORWARD --> MODEL_LR_GRAD[Compute Gradient:<br/>∇L = (1/m)X^T(ŷ-y) + (λ/m)θ]
        MODEL_LR_GRAD --> MODEL_LR_UPDATE[Update Weights:<br/>θ = θ - α∇L]
        MODEL_LR_UPDATE --> MODEL_LR_LOSS{Loss change<br/>< 1e-6?}
        MODEL_LR_LOSS -->|Yes| MODEL_LR_DONE
        MODEL_LR_LOSS -->|No| MODEL_LR_EPOCH
        MODEL_LR_EPOCH -->|No| MODEL_LR_DONE[Save model:<br/>models/logistic_regression.pkl]
        
        %% KNN
        MODEL_KNN_CHECK -->|Yes| MODEL_KNN_INIT[KNNModel:<br/>k=5]
        MODEL_KNN_INIT --> MODEL_KNN_FIT[fit: Store X_train, y_train<br/>Lazy learner - no training]
        MODEL_KNN_FIT --> MODEL_KNN_DONE[Model ready:<br/>In-memory only]
        
        %% XGBOOST
        MODEL_XGB_CHECK -->|Yes| MODEL_XGB_INIT[XGBoostModel:<br/>max_depth=6, lr=0.2<br/>n_estimators=80]
        MODEL_XGB_INIT --> MODEL_XGB_WEIGHT[Compute scale_pos_weight:<br/>n_neg / n_pos ≈ 1.22]
        MODEL_XGB_WEIGHT --> MODEL_XGB_FIT[XGBClassifier.fit:<br/>eval_set=(X_val, y_val)<br/>early_stopping_rounds=20]
        MODEL_XGB_FIT --> MODEL_XGB_MONITOR{Validation loss<br/>improves?}
        MODEL_XGB_MONITOR -->|Yes| MODEL_XGB_CONTINUE[Continue training]
        MODEL_XGB_MONITOR -->|No for 20 rounds| MODEL_XGB_STOP[Early Stop]
        MODEL_XGB_CONTINUE --> MODEL_XGB_MONITOR
        MODEL_XGB_STOP --> MODEL_XGB_DONE[Save model:<br/>models/xgboost.pkl]
        
        MODEL_LR_DONE --> MODEL_COLLECT
        MODEL_KNN_DONE --> MODEL_COLLECT
        MODEL_XGB_DONE --> MODEL_COLLECT[Collect Trained Models]
    end
    
    CONFIG_MODELS --> MODEL_TRAIN_INIT
    MODEL_COLLECT --> EVAL_INIT
    
    %% ================================================================================
    %% STEP 6: EVALUATION & THRESHOLD TUNING
    %% ================================================================================
    subgraph STEP6["📈 STEP 6: Evaluation (src/evaluation.py)"]
        direction TB
        
        EVAL_INIT[Evaluator.__init__:<br/>model, X_val, y_val<br/>X_test, y_test] --> EVAL_LOOP{For each<br/>trained model}
        
        %% Baseline Evaluation (Threshold = 0.5)
        EVAL_LOOP --> EVAL_BASELINE_PRED[predict_proba(X_val):<br/>Get probability scores]
        EVAL_BASELINE_PRED --> EVAL_BASELINE_THRESH[Apply threshold=0.5:<br/>y_pred = (scores >= 0.5)]
        EVAL_BASELINE_THRESH --> EVAL_CM[compute_confusion_matrix:<br/>[[TN, FP],<br/> [FN, TP]]]
        EVAL_CM --> EVAL_METRICS[compute_metrics:<br/>Precision, Recall, F1, FPR]
        EVAL_METRICS --> EVAL_ROC[compute_roc_auc:<br/>Rank-based method]
        
        %% Threshold Tuning
        EVAL_ROC --> EVAL_TUNE_START[tune_threshold:<br/>max_fpr from config]
        EVAL_TUNE_START --> EVAL_SWEEP{Sweep thresholds:<br/>0.0 to 1.0<br/>step=0.001}
        EVAL_SWEEP --> EVAL_SWEEP_PRED[Predict at threshold_i]
        EVAL_SWEEP_PRED --> EVAL_SWEEP_FPR{FPR ≤ max_fpr?}
        EVAL_SWEEP_FPR -->|No| EVAL_SWEEP_NEXT[Try next threshold]
        EVAL_SWEEP_FPR -->|Yes| EVAL_SWEEP_RECALL{Recall ><br/>best_recall?}
        EVAL_SWEEP_RECALL -->|Yes| EVAL_SWEEP_UPDATE[Update:<br/>best_threshold<br/>best_recall]
        EVAL_SWEEP_RECALL -->|No| EVAL_SWEEP_NEXT
        EVAL_SWEEP_UPDATE --> EVAL_SWEEP_NEXT
        EVAL_SWEEP_NEXT --> EVAL_SWEEP_DONE{All thresholds<br/>tested?}
        EVAL_SWEEP_DONE -->|No| EVAL_SWEEP
        EVAL_SWEEP_DONE -->|Yes| EVAL_TUNED[Tuned Metrics:<br/>threshold, recall, FPR]
        
        %% Test Set Evaluation
        EVAL_TUNED --> EVAL_TEST[evaluate_test_set:<br/>Apply tuned threshold]
        EVAL_TEST --> EVAL_TEST_CM[Compute test metrics:<br/>Final performance]
        
        EVAL_TEST_CM --> EVAL_SAVE[Save to:<br/>results/baseline_metrics.json]
        EVAL_SAVE --> EVAL_PLOTS{Generate<br/>plots?}
        EVAL_PLOTS -->|Yes| EVAL_ROC_PLOT[Save ROC curve:<br/>results/model_roc.png]
        EVAL_PLOTS -->|Yes| EVAL_PR_PLOT[Save PR curve:<br/>results/model_pr.png]
        EVAL_ROC_PLOT --> EVAL_OUTPUT
        EVAL_PR_PLOT --> EVAL_OUTPUT
        EVAL_PLOTS -->|No| EVAL_OUTPUT
        
        EVAL_OUTPUT[Output per model:<br/>baseline + tuned metrics<br/>confusion matrices]
    end
    
    CONFIG_EVAL --> EVAL_INIT
    EVAL_OUTPUT --> SELECT_INIT
    
    %% ================================================================================
    %% STEP 7: MODEL SELECTION
    %% ================================================================================
    subgraph STEP7["🏆 STEP 7: Model Selection (src/model_selector.py)"]
        direction TB
        
        SELECT_INIT[ModelSelector.select_best:<br/>Load baseline_metrics.json] --> SELECT_FILTER{Filter models:<br/>Recall >= 0.7?}
        SELECT_FILTER -->|None qualify| SELECT_RELAX[Relax constraint:<br/>Recall >= 0.6]
        SELECT_FILTER -->|Some qualify| SELECT_FPR{FPR <= max_fpr?}
        SELECT_RELAX --> SELECT_FPR
        SELECT_FPR -->|Multiple qualify| SELECT_ROC[Sort by ROC AUC<br/>descending]
        SELECT_FPR -->|One qualifies| SELECT_SINGLE
        SELECT_ROC --> SELECT_BEST[Select highest ROC AUC]
        SELECT_BEST --> SELECT_SINGLE[Best Model Identified]
        
        SELECT_SINGLE --> SELECT_SAVE[Save to:<br/>results/best_model.json<br/>{model, threshold, metrics}]
    end
    
    SELECT_SAVE --> ORCHESTRATE
    
    %% ================================================================================
    %% STEP 8: ORCHESTRATION & ARTIFACTS
    %% ================================================================================
    subgraph STEP8["🎯 STEP 8: Orchestration (src/main.py)"]
        direction TB
        
        ORCHESTRATE[main.py:<br/>Orchestrate pipeline] --> ORCH_LOG[Setup logging:<br/>pipeline.log]
        ORCH_LOG --> ORCH_TIMESTAMP[Create experiment dir:<br/>experiments/run_YYYYMMDD_HHMMSS/]
        ORCH_TIMESTAMP --> ORCH_EXEC[Execute Steps 1-7]
        ORCH_EXEC --> ORCH_SAVE[Save artifacts:<br/>models/*.pkl<br/>results/*.json<br/>results/*.png]
        
        ORCH_SAVE --> ORCH_COMPLIANCE[Run compliance_check.py:<br/>Validate Task 2 requirements]
        ORCH_COMPLIANCE --> ORCH_RESULT{Compliance<br/>check passed?}
        ORCH_RESULT -->|No| ORCH_WARNING[Log warnings:<br/>Missing requirements]
        ORCH_RESULT -->|Yes| ORCH_SUCCESS[Exit code 0:<br/>Pipeline complete]
        
        ORCH_WARNING --> ORCH_EXIT
        ORCH_SUCCESS --> ORCH_EXIT[END: Artifacts ready<br/>for submission]
    end
    
    ORCH_EXIT --> INTERVIEW_QA
    
    %% ================================================================================
    %% INTERVIEW Q&A DECISION TREE
    %% ================================================================================
    subgraph INTERVIEW["💬 Interview Q&A Decision Points"]
        direction TB
        
        INTERVIEW_QA{Panel Question<br/>Category?} --> QA_EDA[EDA Competency:<br/>Q3, Q4, Q5]
        INTERVIEW_QA --> QA_PREP[Preprocessing:<br/>Q6, Q7, Q8]
        INTERVIEW_QA --> QA_MODEL[Model Selection:<br/>Q9, Q10, Q11]
        INTERVIEW_QA --> QA_EVAL[Evaluation:<br/>Q12, Q13, Q14]
        
        QA_EDA --> QA_EDA_ANS{Can explain:<br/>stratified split,<br/>MNAR, skewness?}
        QA_EDA_ANS -->|No| SCORE_POOR_EDA[Score: Poor 0-8]
        QA_EDA_ANS -->|Partially| SCORE_QUAL_EDA[Score: Qualified 9-17]
        QA_EDA_ANS -->|Yes + Business| SCORE_EXC_EDA[Score: Excellent 18-25]
        
        QA_PREP --> QA_PREP_ANS{Can explain:<br/>fit vs transform,<br/>edge cases?}
        QA_PREP_ANS -->|No| SCORE_POOR_PREP[Score: Poor 0-6]
        QA_PREP_ANS -->|Partially| SCORE_QUAL_PREP[Score: Qualified 7-13]
        QA_PREP_ANS -->|Yes + Rationale| SCORE_EXC_PREP[Score: Excellent 14-20]
        
        QA_MODEL --> QA_MODEL_ANS{Can explain:<br/>gradient descent,<br/>hyperparams?}
        QA_MODEL_ANS -->|No| SCORE_POOR_MODEL[Score: Poor 0-8]
        QA_MODEL_ANS -->|Partially| SCORE_QUAL_MODEL[Score: Qualified 9-17]
        QA_MODEL_ANS -->|Yes + Trade-offs| SCORE_EXC_MODEL[Score: Excellent 18-25]
        
        QA_EVAL --> QA_EVAL_ANS{Can explain:<br/>ROC AUC calc,<br/>business impact?}
        QA_EVAL_ANS -->|No| SCORE_POOR_EVAL[Score: Poor 0-6]
        QA_EVAL_ANS -->|Partially| SCORE_QUAL_EVAL[Score: Qualified 7-13]
        QA_EVAL_ANS -->|Yes + CEO pitch| SCORE_EXC_EVAL[Score: Excellent 14-20]
        
        SCORE_POOR_EDA --> FINAL_SCORE
        SCORE_QUAL_EDA --> FINAL_SCORE
        SCORE_EXC_EDA --> FINAL_SCORE
        SCORE_POOR_PREP --> FINAL_SCORE
        SCORE_QUAL_PREP --> FINAL_SCORE
        SCORE_EXC_PREP --> FINAL_SCORE
        SCORE_POOR_MODEL --> FINAL_SCORE
        SCORE_QUAL_MODEL --> FINAL_SCORE
        SCORE_EXC_MODEL --> FINAL_SCORE
        SCORE_POOR_EVAL --> FINAL_SCORE
        SCORE_QUAL_EVAL --> FINAL_SCORE
        SCORE_EXC_EVAL --> FINAL_SCORE
        
        FINAL_SCORE[Calculate Total Score:<br/>EDA×0.25 + Prep×0.2 + Model×0.25<br/>+ Eval×0.2 + Code×0.1]
    end
    
    FINAL_SCORE --> DECISION
    
    %% ================================================================================
    %% FINAL DECISION
    %% ================================================================================
    DECISION{Total Score?}
    DECISION -->|0-59| REJECT[❌ REJECT:<br/>Lacks fundamentals]
    DECISION -->|60-74| WAITLIST[⏸️ WAITLIST:<br/>Needs mentorship]
    DECISION -->|75-89| ACCEPT[✅ ACCEPT:<br/>AIAP-ready]
    DECISION -->|90-100| STRONG_ACCEPT[🌟 STRONG ACCEPT:<br/>Exceptional candidate]
    
    %% ================================================================================
    %% STYLING
    %% ================================================================================
    classDef configStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef stepStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef errorStyle fill:#ffebee,stroke:#c62828,stroke-width:2px
    classDef successStyle fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
    classDef decisionStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef interviewStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    
    class LOAD_CONFIG,PARSE_CONFIG,CONFIG_DATA,CONFIG_MODELS,CONFIG_EVAL,CONFIG_PREP configStyle
    class DL_INIT,DL_CONNECT,DL_QUERY,DL_DF,DL_SHAPE,DL_OUTPUT stepStyle
    class FE_INIT,FE_FIT_FLAGS,FE_FIT_BINS,FE_FIT_RATIO,FE_FIT_DONE,FE_OUTPUT stepStyle
    class PREP_INIT,PREP_CLIP,PREP_LOG,PREP_OUTLIER,PREP_IMPUTE_NUM,PREP_ENCODE,PREP_FIT_DONE,PREP_OUTPUT stepStyle
    class SPLIT_INIT,SPLIT_FIRST,SPLIT_TEMP,SPLIT_SECOND,SPLIT_FINAL,SPLIT_OUTPUT stepStyle
    class MODEL_LR_INIT,MODEL_LR_FIT_START,MODEL_LR_DONE,MODEL_KNN_INIT,MODEL_KNN_DONE,MODEL_XGB_INIT,MODEL_XGB_DONE,MODEL_COLLECT stepStyle
    class EVAL_INIT,EVAL_BASELINE_PRED,EVAL_CM,EVAL_METRICS,EVAL_ROC,EVAL_TUNED,EVAL_TEST_CM,EVAL_SAVE,EVAL_OUTPUT stepStyle
    class SELECT_INIT,SELECT_BEST,SELECT_SAVE stepStyle
    class ORCHESTRATE,ORCH_LOG,ORCH_TIMESTAMP,ORCH_EXEC,ORCH_SAVE,ORCH_SUCCESS stepStyle
    
    class DL_ERROR,DL_SCHEMA_ERROR,PREP_NOT_FITTED,FE_NOT_FITTED,SPLIT_ERROR,SPLIT_WARNING,ORCH_WARNING errorStyle
    class ORCH_SUCCESS,SPLIT_VAL_SAVE,EVAL_SAVE,SELECT_SAVE successStyle
    class DL_CHECK,DL_VALIDATE,FE_START,PREP_START,SPLIT_VALIDATE,MODEL_TRAIN_INIT,EVAL_LOOP,SELECT_FILTER,ORCH_RESULT,INTERVIEW_QA,DECISION decisionStyle
    class QA_EDA,QA_PREP,QA_MODEL,QA_EVAL,QA_EDA_ANS,QA_PREP_ANS,QA_MODEL_ANS,QA_EVAL_ANS,FINAL_SCORE interviewStyle
    class REJECT,WAITLIST,ACCEPT,STRONG_ACCEPT successStyle
---

# interview-session-v3

## Maximum LOD Interview Session Guide

### How to Use This Diagram in the Interview

**Presentation Phase (10 minutes)**:
1. **Start at CONFIG**: "Pipeline begins by loading `config.yaml` for reproducibility"
2. **Trace main path**: CONFIG → STEP1 → STEP2 → ... → STEP8 → INTERVIEW
3. **Highlight decision points** (yellow diamonds): "Notice stratified split validation—this prevents class imbalance drift"
4. **Point to error handling** (red nodes): "Error paths ensure defensive programming"

**Q&A Phase (50 minutes)**:
- **When asked about specific module**: Navigate to corresponding subgraph
  - Q6 (fit vs transform): Point to STEP3 → PREP_START decision
  - Q9 (gradient descent): Point to STEP5 → MODEL_LR_EPOCH loop
  - Q12 (ROC AUC): Point to STEP6 → EVAL_ROC node

**Pro Tip**: Print this diagram or display on tablet during interview—shows preparation and systems thinking.

---

## Mermaid Rendering Instructions

**To render this diagram**:

1. **GitHub**: Commit as `interview-session.mmd` → View in repository
2. **VS Code**: Install "Markdown Preview Mermaid Support" extension
3. **Online**: Paste into https://mermaid.live
4. **Export**: Save as PNG/SVG for presentation slides

**Troubleshooting**:
- If diagram too large: Use browser zoom (Ctrl+Scroll) or split into 3 diagrams (Steps 1-3, Steps 4-6, Steps 7-8)
- If text overlaps: Increase `direction TB` spacing or use `LR` (left-right) orientation

---

## Key Interview Talking Points (Mapped to Diagram Nodes)

| Diagram Node | Interview Question | Your Answer (30 seconds) |
|--------------|-------------------|--------------------------|
| `DL_CHECK` | Q: What if database missing? | "Node `DL_ERROR` raises `FileNotFoundError` with clear message: 'Download from assessment URL'. This prevents cryptic crashes and guides user." |
| `FE_START` | Q: Difference fit vs transform? | "Decision node shows two paths: `fit_transform` learns from training data, `transform` applies learned rules. No re-learning on test → prevents data leakage." |
| `PREP_DETECT_SKEW` | Q: Why log-transform 10 features? | "EDA found \|skew\|>1 → heavy tails. Decision node checks skewness, then applies `np.log1p(x)` to stabilize variance for gradient descent." |
| `SPLIT_VALIDATE` | Q: Why stratified split? | "Validation node checks class distribution preserved (55:45). Random split risks drift → biased evaluation. Stratification ensures consistency." |
| `MODEL_LR_EPOCH` | Q: How does gradient descent work? | "Loop node shows 120 iterations: compute gradient `∇L = (1/m)X^T(ŷ-y)`, update `θ = θ - α∇L`, monitor loss convergence. Stops when change <1e-6." |
| `EVAL_SWEEP` | Q: Explain threshold tuning | "Loop sweeps 1001 thresholds (0.0→1.0). For each, check FPR≤3%. Among valid, select threshold maximizing recall. Avoids test set leakage by using validation set." |
| `SELECT_FILTER` | Q: How select best model? | "Decision tree: Filter Recall≥70% → Filter FPR≤3% → Sort by ROC AUC. If no model qualifies, relax constraints and document trade-offs." |

---

## Zoom-In: Critical Subgraphs for Deep Dives

### Subgraph 1: Gradient Descent Loop (STEP5 - Logistic Regression)

```mermaid
flowchart TD
    GD_START[Initialize θ=zeros] --> GD_EPOCH{epoch < 120?}
    GD_EPOCH -->|Yes| GD_FORWARD[z = Xθ<br/>ŷ = σ(z)]
    GD_FORWARD --> GD_LOSS[L = -mean(y*log(ŷ) + (1-y)*log(1-ŷ))]
    GD_LOSS --> GD_GRAD[∇L = (1/m)X^T(ŷ-y) + (λ/m)θ]
    GD_GRAD --> GD_UPDATE[θ = θ - α*∇L]
    GD_UPDATE --> GD_CHECK{|ΔL| < 1e-6?}
    GD_CHECK -->|Yes| GD_CONVERGED[Converged]
    GD_CHECK -->|No| GD_EPOCH
    GD_EPOCH -->|No| GD_MAX[Max epochs reached]
    GD_CONVERGED --> GD_DONE[θ optimized]
    GD_MAX --> GD_DONE
```

**Interview Usage**: "When asked Q9, draw this on whiteboard to demonstrate understanding of optimization."

---

### Subgraph 2: Threshold Tuning Logic (STEP6 - Evaluation)

```mermaid
flowchart TD
    TT_START[Get y_scores from model.predict_proba] --> TT_INIT[best_threshold=0.5<br/>best_recall=0]
    TT_INIT --> TT_LOOP{For t in linspace(0,1,1001)}
    TT_LOOP --> TT_PRED[y_pred = (y_scores >= t)]
    TT_PRED --> TT_CM[Compute confusion matrix]
    TT_CM --> TT_FPR{FPR(t) <= 0.03?}
    TT_FPR -->|No| TT_NEXT[Continue to next t]
    TT_FPR -->|Yes| TT_RECALL{Recall(t) > best_recall?}
    TT_RECALL -->|Yes| TT_UPDATE[best_threshold = t<br/>best_recall = Recall(t)]
    TT_RECALL -->|No| TT_NEXT
    TT_UPDATE --> TT_NEXT
    TT_NEXT --> TT_DONE{All t tested?}
    TT_DONE -->|No| TT_LOOP
    TT_DONE -->|Yes| TT_RESULT[Return best_threshold, best_recall]
```

**Interview Usage**: "When asked Q13, show this to explain why Recall=12% at FPR≤3% (very restrictive constraint)."

---

## Interview Cheat Sheet (Diagram Navigation)

**If panel asks...**

| Question Topic | Navigate to Node | Key Insight |
|---------------|------------------|-------------|
| "Explain your pipeline flow" | START → CONFIG → STEP1-8 | "8-step evidence-based design from EDA findings" |
| "What if data missing?" | DL_CHECK → DL_ERROR | "Defensive programming with clear error messages" |
| "Why missing-value flags?" | FE_FIT_FLAGS | "MNAR pattern: fraud sites hide metadata → flag as feature" |
| "Difference fit and transform?" | PREP_START decision | "fit learns, transform applies → prevents test leakage" |
| "Why stratified split?" | SPLIT_VALIDATE | "Preserves 55:45 class balance → consistent evaluation" |
| "Gradient descent explained?" | MODEL_LR_EPOCH loop | "120 iterations: ∇L → θ update → loss convergence" |
| "ROC AUC vs FPR difference?" | EVAL_ROC vs EVAL_SWEEP_FPR | "AUC=discrimination, FPR=operating point at threshold" |
| "How choose best model?" | SELECT_FILTER → SELECT_ROC | "Recall≥70% → FPR≤3% → max ROC AUC hierarchy" |

---

**Final Note**: This diagram is your **mental model** of the pipeline. During the interview, you can:
1. Navigate it verbally ("Let me walk you through the preprocessing subgraph...")
2. Draw portions on whiteboard (e.g., gradient descent loop)
3. Reference it for edge cases ("Node PREP_TRANS_CHECK prevents unfitted transform error")

**Practice**: Explain the entire pipeline in <5 minutes using only this diagram. Record yourself and iterate until smooth. Good luck! 🚀