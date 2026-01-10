---
title: "eda-mlp-interview-session"
author: "joohwee"
tags: [EDA, MLP, Test]
date: 2026-01-10
mermaidAnchorsOnly: true
mermaid: |
  graph TB
    START([🎯 Business Problem:<br/>Phishing Detection<br/>$1.5M fraud exposure])
    
    %% ===== PHASE 0: DATA ACQUISITION =====
    subgraph P0["📥 PHASE 0: DATA ACQUISITION"]
        P0_LOAD[("DataLoader.load_from_sqlite<br/>→ DataFrame[11000×47]")]
        P0_VALIDATE[{"PipelineValidator.validate_schema<br/>46 features + 1 target?"}]
        P0_COUNT[{"DataLoader.check_row_count<br/>≥1000 rows?"}]
        P0_PARSE["DataLoader.parse_target_variable<br/>→ y ∈ {0,1}"]
        P0_LOG["DataLogger.log_load_summary<br/>→ pipeline.log"]
        P0_ARTIFACT[("📦 Artifact:<br/>raw_data.pkl<br/>11000×47, 4.2MB")]
    end
    
    START --> P0_LOAD
    P0_LOAD --> P0_VALIDATE
    P0_VALIDATE -->|"✅ Valid"| P0_COUNT
    P0_VALIDATE -->|"❌ Invalid"| ABORT1[/"⛔ ABORT:<br/>Schema mismatch"/]
    P0_COUNT -->|"✅ ≥1000"| P0_PARSE
    P0_COUNT -->|"❌ <1000"| ABORT2[/"⛔ ABORT:<br/>Insufficient data"/]
    P0_PARSE --> P0_LOG
    P0_LOG --> P0_ARTIFACT
    
    %% ===== PHASE 1: EXPLORATORY DATA ANALYSIS =====
    subgraph P1["📊 PHASE 1: EDA - UNIVARIATE & BIVARIATE"]
        P1_CLASS["UnivariateAnalyzer.compute_class_balance<br/>→ 55.04% phish, 44.96% legit"]
        P1_MISSING["UnivariateAnalyzer.analyze_missingness<br/>→ DomainAge: 21.5% missing"]
        P1_SKEW["UnivariateAnalyzer.compute_skewness<br/>→ 10 features |skew|>1"]
        P1_QQ["UnivariateAnalyzer.generate_qq_plots<br/>→ Heavy right tails confirmed"]
        P1_CORR["BivariateAnalyzer.compute_correlation_matrix<br/>→ CorrMatrix[46×46]"]
        P1_VIF["BivariateAnalyzer.compute_vif<br/>→ All VIF<5 (no severe collinearity)"]
        P1_MNAR_TEST["BivariateAnalyzer.test_missingness_independence<br/>→ DomainAge: χ²=42.3, p=0.003"]
        P1_ARTIFACT[("📦 Artifacts:<br/>eda_report.pdf<br/>qq_plots/")]
    end
    
    P0_ARTIFACT --> P1_CLASS
    P1_CLASS --> P1_MISSING
    P1_MISSING --> P1_SKEW
    P1_SKEW --> P1_QQ
    P1_QQ --> P1_CORR
    P1_CORR --> P1_VIF
    P1_VIF --> P1_MNAR_TEST
    P1_MNAR_TEST --> P1_ARTIFACT
    
    %% ===== PHASE 2: STATISTICAL HYPOTHESIS TESTING =====
    subgraph P2["🔬 PHASE 2: STATISTICAL HYPOTHESIS TESTING"]
        P2_BALANCE["HypothesisTester.test_class_balance_significance<br/>H₀: 50:50 | χ²=115.2, p<0.001 → REJECT"]
        P2_MNAR["HypothesisTester.test_mnar_hypothesis<br/>H₀: Independent | χ²=42.3, p=0.003 → MNAR"]
        P2_DECISION{{"MNAR Decision Tree:<br/>Create missing flag?"}}
        P2_STRAT["HypothesisTester.validate_stratified_splits<br/>(pre-validation for Phase 4)"]
        P2_NORM["HypothesisTester.test_normality_post_transform<br/>(pre-validation for Phase 3)"]
        P2_REPORT["StatisticalValidator.generate_hypothesis_test_report<br/>→ HypothesisTestReport.pdf"]
        P2_ARTIFACT[("📦 Artifact:<br/>hypothesis_results.json<br/>L1: Legal compliance")]
    end
    
    P1_ARTIFACT --> P2_BALANCE
    P2_BALANCE --> P2_MNAR
    P2_MNAR --> P2_DECISION
    P2_DECISION -->|"p<0.05 → MNAR"| P2_FLAG_YES["✅ Flag strategy:<br/>Create binary indicator"]
    P2_DECISION -->|"p≥0.05 → MCAR/MAR"| P2_FLAG_NO["❌ Simple imputation OK"]
    P2_FLAG_YES --> P2_STRAT
    P2_FLAG_NO --> P2_STRAT
    P2_STRAT --> P2_NORM
    P2_NORM --> P2_REPORT
    P2_REPORT --> P2_ARTIFACT
    
    %% ===== PHASE 3: FEATURE ENGINEERING & PREPROCESSING =====
    subgraph P3["⚙️ PHASE 3: FEATURE ENGINEERING & PREPROCESSING"]
        P3_MNAR_FLAG["MissingValueHandler.create_mnar_flags<br/>→ DomainAge_missing ∈ {0,1}"]
        P3_IMPUTE_NUM["MissingValueHandler.impute_numerical<br/>→ median=24.0 months"]
        P3_IMPUTE_CAT["MissingValueHandler.impute_categorical<br/>→ mode='present'"]
        P3_VALIDATE_MISS[{"MissingValueHandler.validate_no_missing<br/>Any NaN remaining?"}]
        P3_LOG_TRANSFORM["FeatureScaler.apply_log_transform<br/>→ log(x+1) for 10 features"]
        P3_VALIDATE_SKEW["FeatureScaler.validate_transform_effectiveness<br/>→ NoOfPopup: 8.1→0.3 skew"]
        P3_STANDARDIZE["FeatureScaler.standardize_features<br/>→ mean≈0, std≈1"]
        P3_DOMAIN_BINS["DomainFeatureEngineer.create_age_bins<br/>→ {new, medium, old}"]
        P3_RATIO["DomainFeatureEngineer.create_ratio_features<br/>→ SelfRef/ExternalRef"]
        P3_ENCODE["DomainFeatureEngineer.encode_categorical<br/>→ one-hot encoding"]
        P3_ARTIFACT[("📦 Artifacts:<br/>preprocessor.pkl<br/>51 final features")]
    end
    
    P2_ARTIFACT --> P3_MNAR_FLAG
    P3_MNAR_FLAG --> P3_IMPUTE_NUM
    P3_IMPUTE_NUM --> P3_IMPUTE_CAT
    P3_IMPUTE_CAT --> P3_VALIDATE_MISS
    P3_VALIDATE_MISS -->|"✅ No NaN"| P3_LOG_TRANSFORM
    P3_VALIDATE_MISS -->|"❌ NaN found"| ABORT3[/"⛔ ABORT:<br/>Imputation failed"/]
    P3_LOG_TRANSFORM --> P3_VALIDATE_SKEW
    P3_VALIDATE_SKEW --> P3_STANDARDIZE
    P3_STANDARDIZE --> P3_DOMAIN_BINS
    P3_DOMAIN_BINS --> P3_RATIO
    P3_RATIO --> P3_ENCODE
    P3_ENCODE --> P3_ARTIFACT
    
    %% ===== PHASE 4: DATA SPLITTING =====
    subgraph P4["🎲 PHASE 4: DATA SPLITTING & VALIDATION"]
        P4_SPLIT["DataSplitter.stratified_train_test_split<br/>→ 70-15-15, stratify=y"]
        P4_VALIDATE_STRAT["DataSplitter.validate_split_stratification<br/>→ χ²=0.82, p=0.89"]
        P4_CHECK_STRAT{{"Stratification valid?<br/>p>0.05?"}}
        P4_STATS["DataSplitter.compute_split_statistics<br/>→ Train[55.1,44.9], Val[54.9,45.1], Test[54.9,45.1]"]
        P4_LEAKAGE["DataSplitter.prevent_data_leakage<br/>→ Fit scaler/imputer on TRAIN only"]
        P4_LOG["DataLogger.log_split_metadata<br/>→ random_state=42, timestamp"]
        P4_ARTIFACT[("📦 Artifacts:<br/>X_train[7000×51]<br/>X_val[1500×51]<br/>X_test[2500×51]")]
    end
    
    P3_ARTIFACT --> P4_SPLIT
    P4_SPLIT --> P4_VALIDATE_STRAT
    P4_VALIDATE_STRAT --> P4_CHECK_STRAT
    P4_CHECK_STRAT -->|"✅ Valid"| P4_STATS
    P4_CHECK_STRAT -->|"❌ Invalid"| ABORT4[/"⛔ ABORT:<br/>Stratification failed"/]
    P4_STATS --> P4_LEAKAGE
    P4_LEAKAGE --> P4_LOG
    P4_LOG --> P4_ARTIFACT
    
    %% ===== PHASE 5: MODEL TRAINING =====
    subgraph P5["🤖 PHASE 5: MODEL TRAINING & SELECTION"]
        P5_LOGISTIC["LogisticRegressionModel.train<br/>→ Gradient descent, α=0.1, 120 epochs"]
        P5_LOG_VAL["LogisticRegressionModel.validate_against_sklearn<br/>→ AUC Δ=0.0016"]
        P5_KNN["KNNModel.train<br/>→ k=7, lazy learner"]
        P5_KNN_HYPO["KNNModel.evaluate_hypothesis<br/>→ Local patterns? AUC=0.809<0.888"]
        P5_XGB_GRID["XGBoostModel.grid_search_cv<br/>→ 54 configs × 5-fold = 270 fits"]
        P5_XGB_EARLY["XGBoostModel.train_with_early_stopping<br/>→ Best iteration: 68, val_auc=0.8912"]
        P5_XGB_IMPORT["XGBoostModel.extract_feature_importance<br/>→ NoOfPopup:18.4%, NoOfSelfRef:14.2%"]
        P5_COMPARE["ModelSelector.compare_validation_performance<br/>→ XGBoost AUC=0.891 (BEST)"]
        P5_SELECT["ModelSelector.select_production_model<br/>→ XGBoost selected"]
        P5_ARTIFACT[("📦 Artifacts:<br/>xgboost_v2.3.1.pkl (15MB)<br/>ModelComparisonReport.pdf")]
    end
    
    P4_ARTIFACT --> P5_LOGISTIC
    P5_LOGISTIC --> P5_LOG_VAL
    P5_LOG_VAL --> P5_KNN
    P5_KNN --> P5_KNN_HYPO
    P5_KNN_HYPO --> P5_XGB_GRID
    P5_XGB_GRID --> P5_XGB_EARLY
    P5_XGB_EARLY --> P5_XGB_IMPORT
    P5_XGB_IMPORT --> P5_COMPARE
    P5_COMPARE --> P5_SELECT
    P5_SELECT --> P5_ARTIFACT
    
    %% ===== PHASE 6: THRESHOLD TUNING =====
    subgraph P6["🎚️ PHASE 6: THRESHOLD TUNING & OPTIMIZATION"]
        P6_PROBS["ThresholdTuner.generate_probability_scores<br/>→ val_probs[1500] ∈ (0,1)"]
        P6_SWEEP["ThresholdTuner.sweep_thresholds<br/>→ 1000 thresholds from 0 to 1"]
        P6_CONSTRAINT["ThresholdTuner.apply_business_constraint<br/>→ Filter FPR≤0.05"]
        P6_OPTIMAL["ThresholdTuner.select_optimal_threshold<br/>→ argmax(recall) = 0.65"]
        P6_VAL_METRICS["Validation: Recall=75.2%, FPR=4.8%"]
        P6_TEST["ThresholdTuner.validate_on_test_set<br/>→ Test: Recall=73.8%, FPR=5.1%"]
        P6_GENERALIZE{{"Generalization OK?<br/>Δrecall<2pp, Δfpr<1pp?"}}
        P6_PARETO["ThresholdTuner.analyze_pareto_ceiling<br/>→ Can achieve targets with current features?"]
        P6_VIZ["ThresholdTuner.generate_pareto_visualization<br/>→ pareto_curve.png"]
        P6_ARTIFACT[("📦 Artifacts:<br/>threshold=0.65<br/>pareto_analysis.json")]
    end
    
    P5_ARTIFACT --> P6_PROBS
    P6_PROBS --> P6_SWEEP
    P6_SWEEP --> P6_CONSTRAINT
    P6_CONSTRAINT --> P6_OPTIMAL
    P6_OPTIMAL --> P6_VAL_METRICS
    P6_VAL_METRICS --> P6_TEST
    P6_TEST --> P6_GENERALIZE
    P6_GENERALIZE -->|"✅ Yes"| P6_PARETO
    P6_GENERALIZE -->|"❌ No"| RETUNE[/"⚠️ Re-tune or<br/>improve features"/]
    P6_PARETO --> P6_VIZ
    P6_VIZ --> P6_ARTIFACT
    
    %% ===== PHASE 7: EVALUATION =====
    subgraph P7["📈 PHASE 7: EVALUATION & METRICS"]
        P7_CONFUSION["MetricsCalculator.compute_confusion_matrix<br/>→ TP:1704, FN:605, FP:238, TN:4418"]
        P7_RECALL["MetricsCalculator.compute_recall<br/>→ 73.8% (Target: ≥70% ✅)"]
        P7_FPR["MetricsCalculator.compute_fpr<br/>→ 5.1% (Target: ≤5% ⚠️)"]
        P7_AUC["MetricsCalculator.compute_auc_roc<br/>→ 0.888"]
        P7_AUC_CUSTOM["MetricsCalculator.compute_auc_custom<br/>→ 0.8880 (validates sklearn)"]
        P7_FRAUD["BusinessImpactCalculator.quantify_fraud_exposure<br/>→ 605 FN × $500 = $302,500/month"]
        P7_SUPPORT["BusinessImpactCalculator.quantify_support_cost<br/>→ 238 FP → ~$12,000/day"]
        P7_SUMMARY["BusinessImpactCalculator.generate_executive_summary<br/>→ ExecutiveSummary.pdf"]
        P7_VALIDATE[{"PipelineValidator.validate_model_performance<br/>Meets KPIs?"}]
        P7_ARTIFACT[("📦 Artifacts:<br/>test_results.json<br/>confusion_matrix.png<br/>ExecutiveSummary.pdf")]
    end
    
    P6_ARTIFACT --> P7_CONFUSION
    P7_CONFUSION --> P7_RECALL
    P7_RECALL --> P7_FPR
    P7_FPR --> P7_AUC
    P7_AUC --> P7_AUC_CUSTOM
    P7_AUC_CUSTOM --> P7_FRAUD
    P7_FRAUD --> P7_SUPPORT
    P7_SUPPORT --> P7_SUMMARY
    P7_SUMMARY --> P7_VALIDATE
    P7_VALIDATE -->|"✅ KPIs met"| P7_ARTIFACT
    P7_VALIDATE -->|"❌ KPIs failed"| ABORT5[/"⛔ ABORT:<br/>Model inadequate"/]
    
    %% ===== PHASE 8: DEPLOYMENT & MONITORING =====
    subgraph P8["🚀 PHASE 8: DEPLOYMENT & MONITORING"]
        P8_PACKAGE["ModelPackager.serialize_model<br/>→ xgboost_v2.3.1.pkl + metadata"]
        P8_CARD["ModelPackager.create_model_card<br/>→ ModelCard.md (L1: Legal)"]
        P8_DOCKER["ModelPackager.containerize_model<br/>→ ml-phishing-detector:v2.3.1"]
        P8_SHADOW["BlueGreenDeployer.deploy_green_shadow_mode<br/>→ Week 1: 0% traffic, logs only"]
        P8_AB["BlueGreenDeployer.gradual_traffic_shift<br/>→ Week 2: 10%, Week 3: 50%, Week 4: 100%"]
        P8_MONITOR_SYS["SystemHealthMonitor.track_latency_percentiles<br/>→ p50=18ms, p99=87ms"]
        P8_MONITOR_DRIFT["FeatureDriftDetector.compute_kl_divergence<br/>→ Alert if D_KL>0.1"]
        P8_MONITOR_PERF["PerformanceMonitor.compute_weekly_recall_fpr<br/>→ n=200 sample, alert if recall<70%"]
        P8_MONITOR_BIZ["BusinessMetricsTracker.track_daily_blocks<br/>→ 18,234 blocks/day"]
        P8_ALERT["AlertManager.send_pagerduty_alert<br/>→ Critical: recall<65% or p99>150ms"]
        P8_DASHBOARD["DashboardGenerator.generate_grafana_dashboard<br/>→ PM/Legal/Eng visibility"]
        P8_ARTIFACT[("📦 Production Artifacts:<br/>Docker image<br/>Grafana dashboard<br/>Audit logs (90-day)")]
    end
    
    P7_ARTIFACT --> P8_PACKAGE
    P8_PACKAGE --> P8_CARD
    P8_CARD --> P8_DOCKER
    P8_DOCKER --> P8_SHADOW
    P8_SHADOW --> P8_AB
    P8_AB --> P8_MONITOR_SYS
    P8_MONITOR_SYS --> P8_MONITOR_DRIFT
    P8_MONITOR_DRIFT --> P8_MONITOR_PERF
    P8_MONITOR_PERF --> P8_MONITOR_BIZ
    P8_MONITOR_BIZ --> P8_ALERT
    P8_ALERT --> P8_DASHBOARD
    P8_DASHBOARD --> P8_ARTIFACT
    
    %% ===== FINAL OUTCOME =====
    P8_ARTIFACT --> SUCCESS{{"🎯 Production Model:<br/>Recall=73.8% (↓$1.31M fraud)<br/>FPR=5.1% (↓$701K/day support)<br/>AUC=0.888<br/>Latency p99=87ms"}}
    
    %% ===== CROSS-CUTTING CONCERNS =====
    subgraph CROSS["🔧 CROSS-CUTTING CONCERNS"]
        CROSS_LOG["PipelineLogger.log_pipeline_stage<br/>→ Audit trail for every phase"]
        CROSS_VALIDATE["PipelineValidator.validate_*<br/>→ Quality gates at each phase"]
        CROSS_ERROR["ErrorHandler.retry_with_backoff<br/>→ Resilience for DB/network"]
        CROSS_REPRO["ReproducibilityManager.set_random_seeds<br/>→ random_state=42 throughout"]
    end
    
    P0_LOG -.->|"Logs to"| CROSS_LOG
    P2_REPORT -.->|"Logs to"| CROSS_LOG
    P4_LOG -.->|"Logs to"| CROSS_LOG
    P8_DASHBOARD -.->|"Logs to"| CROSS_LOG
    
    P0_VALIDATE -.->|"Uses"| CROSS_VALIDATE
    P3_VALIDATE_MISS -.->|"Uses"| CROSS_VALIDATE
    P4_CHECK_STRAT -.->|"Uses"| CROSS_VALIDATE
    P7_VALIDATE -.->|"Uses"| CROSS_VALIDATE
    
    P0_LOAD -.->|"May use"| CROSS_ERROR
    P8_MONITOR_SYS -.->|"Uses"| CROSS_ERROR
    
    P4_SPLIT -.->|"Uses"| CROSS_REPRO
    P5_XGB_GRID -.->|"Uses"| CROSS_REPRO
    
    %% ===== INTERVIEW ASSESSMENT OVERLAY =====
    subgraph INTERVIEW["📝 INTERVIEW ASSESSMENT"]
        INT_POOR["❌ POOR: No MNAR test,<br/>default threshold,<br/>no business impact"]
        INT_QUAL["⚠️ QUALIFIED: Mentions concepts,<br/>basic implementation,<br/>some quantification"]
        INT_EXCEL["✅ EXCELLENT: Statistical rigor,<br/>empirical validation,<br/>full business quantification"]
    end
    
    P2_MNAR -.->|"Assessment point"| INT_EXCEL
    P6_OPTIMAL -.->|"Assessment point"| INT_EXCEL
    P7_FRAUD -.->|"Assessment point"| INT_EXCEL
    
    %% ===== TRAVERSAL PATHS =====
    TRAV1["🔄 Business→Technical:<br/>Fraud exposure → Recall → Threshold → Gradient descent"]
    TRAV2["🔄 Technical→Business:<br/>Gradient descent → Loss → Model → Recall → Fraud exposure"]
    
    SUCCESS -.->|"GraphRAG path"| TRAV1
    SUCCESS -.->|"GraphRAG path"| TRAV2
    
    %% ===== STYLING =====
    classDef phaseClass fill:#667eea,stroke:#333,stroke-width:2px,color:#fff
    classDef decisionClass fill:#f093fb,stroke:#333,stroke-width:2px,color:#000
    classDef artifactClass fill:#43e97b,stroke:#333,stroke-width:3px,color:#000
    classDef abortClass fill:#e03131,stroke:#333,stroke-width:2px,color:#fff
    classDef successClass fill:#38f9d7,stroke:#333,stroke-width:4px,color:#000
    classDef crossClass fill:#ffd43b,stroke:#333,stroke-width:2px,color:#000
    classDef interviewClass fill:#ff922b,stroke:#333,stroke-width:2px,color:#fff
    classDef traversalClass fill:#da77f2,stroke:#333,stroke-width:2px,color:#fff
    
    class P0_LOAD,P1_CLASS,P2_BALANCE,P3_MNAR_FLAG,P4_SPLIT,P5_LOGISTIC,P6_PROBS,P7_CONFUSION,P8_PACKAGE phaseClass
    class P0_VALIDATE,P0_COUNT,P2_DECISION,P3_VALIDATE_MISS,P4_CHECK_STRAT,P6_GENERALIZE,P7_VALIDATE decisionClass
    class P0_ARTIFACT,P1_ARTIFACT,P2_ARTIFACT,P3_ARTIFACT,P4_ARTIFACT,P5_ARTIFACT,P6_ARTIFACT,P7_ARTIFACT,P8_ARTIFACT artifactClass
    class ABORT1,ABORT2,ABORT3,ABORT4,ABORT5 abortClass
    class SUCCESS successClass
    class CROSS_LOG,CROSS_VALIDATE,CROSS_ERROR,CROSS_REPRO crossClass
    class INT_POOR,INT_QUAL,INT_EXCEL interviewClass
    class TRAV1,TRAV2 traversalClass
---

# EDA → MLP Interview Session: Maximum LOD Directory Table

**Version**: 1.0  
**Purpose**: Complete 7-Layer Coverage following zero-to-one EDA→MLP flow  
**Organization**: Module → Class/Object → Function/Method → Responsibility (S-V-O) → Dependencies → Artifacts

---

## Table of Contents

1. [Phase 0: Data Acquisition](#phase-0-data-acquisition)
2. [Phase 1: Exploratory Data Analysis](#phase-1-eda)
3. [Phase 2: Statistical Hypothesis Testing](#phase-2-statistical-testing)
4. [Phase 3: Feature Engineering & Preprocessing](#phase-3-feature-engineering)
5. [Phase 4: Data Splitting & Validation](#phase-4-data-splitting)
6. [Phase 5: Model Training & Selection](#phase-5-model-training)
7. [Phase 6: Threshold Tuning & Optimization](#phase-6-threshold-tuning)
8. [Phase 7: Evaluation & Metrics](#phase-7-evaluation)
9. [Phase 8: Deployment & Monitoring](#phase-8-deployment)
10. [Cross-Cutting Concerns](#cross-cutting-concerns)

---

## Phase 0: Data Acquisition {#phase-0-data-acquisition}

**Business Context**: Load raw phishing dataset (11,000 samples, 46 features) from SQLite database for fraud detection model.

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `data/loader.py` | `DataLoader` | `load_from_sqlite` | DataLoader loads raw dataset from SQLite database | `sqlite3`, `phishing.db` | `DataFrame[11000×47]` | **L5→L0**: Connects DB to business outcome (fraud exposure) |
| `data/loader.py` | `DataLoader` | `validate_schema` | DataLoader validates schema against expected columns | `schema_config.yaml` | `ValidationReport{missing_cols, extra_cols}` | Ensures 46 features + 1 target present |
| `data/loader.py` | `DataLoader` | `check_row_count` | DataLoader checks row count meets minimum threshold | `min_rows=1000` | `bool, actual_count` | Pipeline gate: <1000 rows → abort training |
| `data/loader.py` | `DataLoader` | `parse_target_variable` | DataLoader parses target variable to binary format | None | `y: Series[int]` with values {0,1} | 0=phishing, 1=legitimate |
| `data/logger.py` | `DataLogger` | `log_load_summary` | DataLogger logs dataset dimensions and basic stats | `DataFrame` | `log_entry{timestamp, rows, cols, memory_mb}` | Audit trail requirement (L1: Legal) |

**Interview Signal (Excellent)**: "Loaded 11,000 samples from SQLite (phishing.db). Schema validation: 46 features + target confirmed. Row count 11,000 > threshold 1,000 ✅. Memory footprint: 4.2MB. Logged to pipeline.log with timestamp for audit compliance."

---

## Phase 1: Exploratory Data Analysis {#phase-1-eda}

**Statistical Context**: Analyze feature distributions, class balance, missingness patterns to inform preprocessing strategy.

### 1.1 Univariate Analysis

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `eda/univariate.py` | `UnivariatAnalyzer` | `compute_class_balance` | UnivariateAnalyzer computes class distribution with statistical test | `scipy.stats.chisquare` | `ClassBalance{phish: 6050, legit: 4950, ratio: 55.04:44.96, chi2: 115.2, p: <0.001}` | **L3→L2**: Chi-square proves imbalance significant, informs stratified sampling |
| `eda/univariate.py` | `UnivariateAnalyzer` | `analyze_missingness` | UnivariateAnalyzer analyzes missing value patterns per feature | `DataFrame.isna()` | `MissingnessReport{feature: miss_rate}[]` | Key finding: DomainAge 21.5% missing overall |
| `eda/univariate.py` | `UnivariateAnalyzer` | `compute_skewness` | UnivariateAnalyzer computes skewness for numerical features | `scipy.stats.skew` | `SkewnessReport{feature: skew_value}[]` | |skew|>1 triggers log-transform (L3→L4) |
| `eda/univariate.py` | `UnivariateAnalyzer` | `generate_qq_plots` | UnivariateAnalyzer generates Q-Q plots for normality assessment | `scipy.stats.probplot` | `QQPlot[]` per feature | Visual validation of skewness findings |
| `eda/univariate.py` | `UnivariateAnalyzer` | `detect_outliers` | UnivariateAnalyzer detects outliers via IQR method | `Q1, Q3, IQR` | `OutlierReport{feature: outlier_count, outlier_indices}[]` | NoOfPopup: 234 outliers (>99th percentile) |

**Interview Signal (Excellent)**: "Class balance: 55.04% phishing, 44.96% legitimate. Chi-square test: χ²=115.2, p<0.001 → significant imbalance, NOT due to chance. Skewness analysis: 10 features with |skew|>1 (NoOfPopup: 8.1, NoOfImage: 5.2). Q-Q plots confirm heavy right tails. DomainAge: 21.5% missing (2,365 of 11,000 samples)—hypothesis: MNAR (phishing sites hide age)."

### 1.2 Bivariate Analysis

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `eda/bivariate.py` | `BivariateAnalyzer` | `compute_correlation_matrix` | BivariateAnalyzer computes Pearson correlation matrix | `DataFrame.corr()` | `CorrMatrix[46×46]` | Pairwise relationships (preliminary collinearity check) |
| `eda/bivariate.py` | `BivariateAnalyzer` | `compute_vif` | BivariateAnalyzer computes Variance Inflation Factor per feature | `statsmodels.stats.outliers_influence.variance_inflation_factor` | `VIF_Report{feature: vif_value}[]` | **L3**: VIF detects multicollinearity (VIF>10 problematic) |
| `eda/bivariate.py` | `BivariateAnalyzer` | `analyze_feature_target_relationship` | BivariateAnalyzer analyzes relationship between each feature and target | `scipy.stats` | `FeatureTargetStats{feature: mean_phish, mean_legit, t_stat, p_value}[]` | Identifies discriminative features |
| `eda/bivariate.py` | `BivariateAnalyzer` | `test_missingness_independence` | BivariateAnalyzer tests if missingness independent of target (MNAR test) | `scipy.stats.chi2_contingency` | `MNAR_Test{feature, chi2, p_value, is_mnar}[]` | **L3→L5**: DomainAge: χ²=42.3, p=0.003 → MNAR → create flag |

**Interview Signal (Excellent)**: "VIF analysis: All features VIF<5 (highest: NoOfSelfRef VIF=3.2 with NoOfExternalRef—expected for link counts). No severe multicollinearity. MNAR test for DomainAge: Contingency table [phishing: 35% missing, legitimate: 8% missing], χ²=42.3, df=1, p=0.003 < 0.05 → Reject H₀ → Missingness NOT independent → MNAR confirmed."

---

## Phase 2: Statistical Hypothesis Testing {#phase-2-statistical-testing}

**Purpose**: Rigorous hypothesis testing to validate EDA findings and inform preprocessing decisions.

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `stats/hypothesis_testing.py` | `HypothesisTester` | `test_class_balance_significance` | HypothesisTester tests if class imbalance significantly differs from 50:50 | `scipy.stats.chisquare` | `ChiSquareResult{observed: [6050,4950], expected: [5500,5500], chi2: 115.2, p: <0.001, reject_h0: True}` | **L3→L4**: Proves 55:45 split significant → use stratified sampling |
| `stats/hypothesis_testing.py` | `HypothesisTester` | `test_mnar_hypothesis` | HypothesisTester tests MNAR hypothesis for each feature with missingness | `scipy.stats.chi2_contingency` | `MNAR_Results{DomainAge: {chi2: 42.3, p: 0.003, mnar: True}, ...}` | **L3→L5**: Pipeline decision tree: MNAR → create flag before imputation |
| `stats/hypothesis_testing.py` | `HypothesisTester` | `validate_stratified_splits` | HypothesisTester validates train/val/test splits preserve class distribution | `scipy.stats.chisquare` | `StratificationValidation{train: [55.1,44.9], val: [54.9,45.1], test: [54.9,45.1], chi2: 0.82, p: 0.89, valid: True}` | **L3**: p>0.05 → splits NOT significantly different → stratification successful |
| `stats/hypothesis_testing.py` | `HypothesisTester` | `test_normality_post_transform` | HypothesisTester tests normality after log-transform via Shapiro-Wilk | `scipy.stats.shapiro` | `NormalityTest{feature, pre_transform_p, post_transform_p, improved: bool}` | Validates transformation effectiveness |
| `stats/validation.py` | `StatisticalValidator` | `generate_hypothesis_test_report` | StatisticalValidator generates comprehensive hypothesis testing report | All test results | `HypothesisTestReport.pdf` | **L1**: Legal compliance documentation |

**Interview Signal (Excellent)**: "Three chi-square applications: (1) Class imbalance: χ²=115.2, p<0.001 → 55:45 significantly different from 50:50. (2) MNAR test DomainAge: χ²=42.3, p=0.003 → missingness related to target. (3) Stratified split validation: train 55.1:44.9, val 54.9:45.1, test 54.9:45.1 vs original 55.0:45.0, χ²=0.82, p=0.89 → splits valid. All logged to pipeline_validation.json."

---

## Phase 3: Feature Engineering & Preprocessing {#phase-3-feature-engineering}

**Purpose**: Transform raw features into model-ready inputs based on EDA/statistical findings.

### 3.1 Missing Value Handling (MNAR-Aware)

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `preprocessing/missing_handler.py` | `MissingValueHandler` | `create_mnar_flags` | MissingValueHandler creates binary flags for MNAR features | `MNAR_Results` from Phase 2 | `DataFrame` with new columns `{feature}_missing` | **L3→L5**: DomainAge_missing = 1 if DomainAge is NaN, else 0 |
| `preprocessing/missing_handler.py` | `MissingValueHandler` | `impute_numerical` | MissingValueHandler imputes numerical features with median | `sklearn.impute.SimpleImputer(strategy='median')` | `Imputer` fitted on train, `DataFrame_imputed` | Applied AFTER flag creation to preserve MNAR signal |
| `preprocessing/missing_handler.py` | `MissingValueHandler` | `impute_categorical` | MissingValueHandler imputes categorical features with mode | `sklearn.impute.SimpleImputer(strategy='most_frequent')` | `Imputer`, `DataFrame_imputed` | Robots.txt: mode='present' |
| `preprocessing/missing_handler.py` | `MissingValueHandler` | `validate_no_missing` | MissingValueHandler validates no missing values remain post-imputation | `DataFrame.isna().sum()` | `ValidationResult{has_missing: False}` or raises `DataQualityError` | Pipeline gate: any NaN → abort |

**Interview Signal (Excellent)**: "Two-step missing value strategy based on MNAR test: (1) Created DomainAge_missing binary flag (1 if missing, 0 if present) capturing adversarial hiding pattern. (2) Then median imputation: DomainAge.fillna(median=24.0 months). A/B validation: with flag recall=73.8%, without flag recall=71.0% → +2.8pp improvement validates MNAR signal capture."

### 3.2 Feature Scaling & Transformation

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `preprocessing/scaling.py` | `FeatureScaler` | `apply_log_transform` | FeatureScaler applies log(x+1) transform to skewed features | `SkewnessReport` (|skew|>1) | `DataFrame` with transformed columns | **L3→L4**: 10 features transformed (NoOfPopup, NoOfImage, NoOfiFrame, etc.) |
| `preprocessing/scaling.py` | `FeatureScaler` | `validate_transform_effectiveness` | FeatureScaler validates skewness reduction post-transform | `scipy.stats.skew` | `TransformValidation{feature, pre_skew, post_skew, improvement_pct}[]` | NoOfPopup: 8.1 → 0.3 (96% reduction) |
| `preprocessing/scaling.py` | `FeatureScaler` | `standardize_features` | FeatureScaler standardizes features to mean=0, std=1 | `sklearn.preprocessing.StandardScaler` | `Scaler` fitted on train, `DataFrame_scaled` | Required for Logistic Regression, KNN |
| `preprocessing/scaling.py` | `FeatureScaler` | `validate_scaling` | FeatureScaler validates mean≈0, std≈1 post-scaling | `DataFrame.mean()`, `DataFrame.std()` | `ScalingValidation{feature, mean, std, valid: bool}` | Tolerance: |mean|<0.01, |std-1|<0.01 |

**Interview Signal (Excellent)**: "Log-transform for 10 features with |skew|>1. Pre-transform: NoOfPopup skew=8.1 (extreme right tail). Post-transform: log(NoOfPopup+1) skew=0.3 (near-normal). Convergence validation: without transform 512 epochs, with transform 120 epochs → 4.3× speedup. Q-Q plots confirm improved normality (points follow diagonal post-transform)."

### 3.3 Feature Engineering (Domain-Specific)

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `feature_engineering/domain_features.py` | `DomainFeatureEngineer` | `create_age_bins` | DomainFeatureEngineer creates categorical age bins from DomainAge | `pd.cut(bins=[0,6,24,∞])` | `DomainAge_bin: Series[category]` with levels {new, medium, old} | Business insight: <6mo high risk |
| `feature_engineering/domain_features.py` | `DomainFeatureEngineer` | `create_ratio_features` | DomainFeatureEngineer creates ratio features from counts | None | `SelfRef_to_ExternalRef_ratio: Series[float]` | Phishing sites: high internal/external ratio |
| `feature_engineering/domain_features.py` | `DomainFeatureEngineer` | `encode_categorical` | DomainFeatureEngineer encodes categorical features via one-hot | `pd.get_dummies` | `DataFrame` with binary columns | Robots.txt, DomainAge_bin → one-hot |
| `feature_engineering/domain_features.py` | `DomainFeatureEngineer` | `compute_feature_importance_proxy` | DomainFeatureEngineer computes mutual information for feature selection | `sklearn.feature_selection.mutual_info_classif` | `FeatureImportance{feature: mi_score}[]` | Pre-training feature ranking |

**Interview Signal (Excellent)**: "Domain-specific engineering: (1) DomainAge_missing binary flag (MNAR-aware). (2) DomainAge_bin categorical: <6mo='new' (high risk), 6-24mo='medium', >24mo='old' (low risk). (3) SelfRef_to_ExternalRef_ratio = NoOfSelfRef / (NoOfExternalRef+1). (4) Log-transforms for skewed counts. Final feature count: 46 original + 1 missing flag + 3 age bins + 1 ratio = 51 features."

---

## Phase 4: Data Splitting & Validation {#phase-4-data-splitting}

**Purpose**: Create train/val/test splits preserving class distribution for unbiased evaluation.

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `data/splitter.py` | `DataSplitter` | `stratified_train_test_split` | DataSplitter splits data into train/val/test with stratification | `sklearn.model_selection.train_test_split(stratify=y)` | `X_train[7000×51], y_train[7000], X_val[1500×51], y_val[1500], X_test[2500×51], y_test[2500]` | **L3**: 70-15-15 split, stratify=y preserves 55:45 ratio |
| `data/splitter.py` | `DataSplitter` | `validate_split_stratification` | DataSplitter validates splits via chi-square test | `HypothesisTester.validate_stratified_splits` | `StratificationValidation{chi2: 0.82, p: 0.89, valid: True}` | **L3**: p>0.05 → distributions not significantly different |
| `data/splitter.py` | `DataSplitter` | `compute_split_statistics` | DataSplitter computes class proportions per split | None | `SplitStats{train: [55.1,44.9], val: [54.9,45.1], test: [54.9,45.1]}` | Logged for audit trail |
| `data/splitter.py` | `DataSplitter` | `prevent_data_leakage` | DataSplitter ensures preprocessing fitted only on train set | Scaler, Imputer objects | `PreprocessingArtifacts{scaler, imputer, fitted_on: 'train'}` | **Critical**: fit on train, transform on val/test |
| `data/logger.py` | `DataLogger` | `log_split_metadata` | DataLogger logs split creation with timestamp and random seed | `random_state=42` | `split_metadata.json{timestamp, seed, train_size, val_size, test_size}` | Reproducibility requirement |

**Interview Signal (Excellent)**: "Stratified 70-15-15 split (train 7000, val 1500, test 2500) with random_state=42 for reproducibility. Validation: train [55.1% phish, 44.9% legit], val [54.9%, 45.1%], test [54.9%, 45.1%] vs original [55.0%, 45.0%]. Chi-square test: χ²=0.82, p=0.89 > 0.05 → Fail to reject H₀ → distributions not significantly different → stratification successful. Logged to pipeline_validation.json."

---

## Phase 5: Model Training & Selection {#phase-5-model-training}

**Purpose**: Train multiple models (Logistic, KNN, XGBoost) and select best based on validation performance.

### 5.1 Logistic Regression (Interpretable Baseline)

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `models/logistic_regression.py` | `LogisticRegressionModel` | `initialize_parameters` | LogisticRegressionModel initializes weights to zeros | None | `theta: ndarray[51]` with all 0s | 51 features (including engineered) |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `sigmoid` | LogisticRegressionModel applies sigmoid activation function | None | `predictions: ndarray` with values in (0,1) | **L6**: σ(z) = 1/(1+e^(-z)), maps ℝ→(0,1) |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `compute_loss` | LogisticRegressionModel computes binary cross-entropy with L2 regularization | `y_true, y_pred, theta, lambda` | `loss: float` | **L6**: L(θ)=-(1/m)Σ[y log(ŷ)+(1-y)log(1-ŷ)] + (λ/2m)||θ||² |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `compute_gradient` | LogisticRegressionModel computes gradient of loss w.r.t. parameters | `X, y, predictions, theta, lambda` | `gradient: ndarray[51]` | **L6**: ∇L=(1/m)Xᵀ(σ(Xθ)-y) + (λ/m)θ |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `gradient_descent` | LogisticRegressionModel optimizes parameters via batch gradient descent | `X_train, y_train, alpha=0.1, max_epochs=1000, tol=1e-4` | `theta_optimal, loss_history[]` | **L6**: θ_new = θ_old - α∇L(θ), converges at epoch 120 |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `train` | LogisticRegressionModel trains model on training set | `X_train, y_train` | `self.theta, self.training_metadata{epochs: 120, final_loss: 0.418}` | **L4→L2**: Baseline model, AUC=0.825 |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `predict_proba` | LogisticRegressionModel generates probability predictions | `X` | `probabilities: ndarray` in (0,1) | P(phishing|x) = σ(θᵀx) |
| `models/logistic_regression.py` | `LogisticRegressionModel` | `validate_against_sklearn` | LogisticRegressionModel validates custom implementation against sklearn | `sklearn.linear_model.LogisticRegression` | `ValidationResult{custom_auc: 0.8252, sklearn_auc: 0.8268, difference: 0.0016}` | **L6**: <0.2% difference validates correctness |

**Interview Signal (Excellent)**: "Implemented gradient descent from scratch. Derivation: L(θ)=-(1/m)Σ[y log(σ(Xθ))+(1-y)log(1-σ(Xθ))] + (λ/2m)||θ||². Gradient via chain rule: ∇L=(1/m)Xᵀ(σ(Xθ)-y)+(λ/m)θ. Learning rate α=0.1 (grid searched 0.01-0.5). Converged in 120 epochs (|Δloss|<1e-4), final loss=0.418. Validation: custom AUC=0.8252, sklearn AUC=0.8268, difference=0.0016 (<0.2%) validates implementation. Production would use sklearn for speed, but custom signals depth."

### 5.2 K-Nearest Neighbors (Hypothesis Test)

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `models/knn.py` | `KNNModel` | `tune_k_hyperparameter` | KNNModel tunes number of neighbors via cross-validation | `sklearn.model_selection.GridSearchCV` | `best_k: int`, `cv_results[]` | Tested k ∈ {3, 5, 7, 9, 11}, best k=7 |
| `models/knn.py` | `KNNModel` | `train` | KNNModel fits KNN classifier (lazy learner - stores training data) | `sklearn.neighbors.KNeighborsClassifier` | `self.model, self.X_train_stored, self.y_train_stored` | **L4**: No training, just stores data |
| `models/knn.py` | `KNNModel` | `predict_proba` | KNNModel generates predictions via k-nearest neighbor voting | `X` | `probabilities: ndarray` | O(n) inference per prediction |
| `models/knn.py` | `KNNModel` | `evaluate_hypothesis` | KNNModel evaluates if local patterns matter for phishing detection | Validation AUC | `HypothesisTestResult{knn_auc: 0.809, xgboost_auc: 0.888, local_patterns_matter: False}` | **L4**: KNN << XGBoost → local patterns NOT critical → simpler models suffice |

**Interview Signal (Excellent)**: "KNN hypothesis test: Does phishing form local clusters in feature space (suggesting need for complex models)? KNN k=7 achieves AUC=0.809 vs XGBoost 0.888. Conclusion: Local patterns NOT dominant (otherwise KNN would excel). Linear/tree boundaries sufficient → No need for deep learning. KNN O(n) inference (slow for 100K+ predictions/day) makes it production-unsuitable, but served diagnostic purpose."

### 5.3 XGBoost (Production Model)

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `models/xgboost_model.py` | `XGBoostModel` | `define_parameter_grid` | XGBoostModel defines hyperparameter search space | None | `param_grid{max_depth: [4,6,8], learning_rate: [0.05,0.1,0.2], n_estimators: [50,80,100], ...}` | 54 configurations total |
| `models/xgboost_model.py` | `XGBoostModel` | `grid_search_cv` | XGBoostModel performs 5-fold cross-validation over parameter grid | `sklearn.model_selection.GridSearchCV` | `best_params, cv_results[270 fits]` | 54 configs × 5 folds = 270 fits, 18 min runtime |
| `models/xgboost_model.py` | `XGBoostModel` | `configure_class_imbalance` | XGBoostModel sets scale_pos_weight for class imbalance | `sum(y==0) / sum(y==1)` | `scale_pos_weight: 1.22` | **L3→L4**: 55/45 ratio compensation |
| `models/xgboost_model.py` | `XGBoostModel` | `train_with_early_stopping` | XGBoostModel trains with validation-based early stopping | `X_train, y_train, X_val, y_val, early_stopping_rounds=20` | `model, best_iteration: 68, training_log[]` | Stops when val AUC plateaus |
| `models/xgboost_model.py` | `XGBoostModel` | `extract_feature_importance` | XGBoostModel extracts feature importance via gain metric | `model.get_score(importance_type='gain')` | `FeatureImportance{NoOfPopup: 0.184, NoOfSelfRef: 0.142, DomainAge: 0.134, ...}` | **L4→L0**: Top features align with fraud patterns |
| `models/xgboost_model.py` | `XGBoostModel` | `validate_no_overfitting` | XGBoostModel validates train vs validation performance gap | `train_auc, val_auc` | `OverfittingCheck{train_auc: 0.912, val_auc: 0.891, gap: 0.021, acceptable: True}` | Gap <0.05 acceptable |
| `models/xgboost_model.py` | `XGBoostModel` | `save_model_artifact` | XGBoostModel serializes trained model to disk | `pickle` | `xgboost_v2.3.1.pkl (15MB)` | **L5**: Production deployment artifact |

**Interview Signal (Excellent)**: "XGBoost hyperparameter tuning: Grid search 54 configs (depth ∈ {4,6,8}, LR ∈ {0.05,0.1,0.2}, n_est ∈ {50,80,100}) × 5-fold CV = 270 fits, 18 min. Best: depth=6 (not 8—depth 8 overfits, val AUC 0.894 but test 0.882; depth 6 generalizes better, val 0.891, test 0.888). scale_pos_weight=1.22 for 55:45 imbalance. Early stopping at iteration 68 (val AUC=0.8912). Feature importance: NoOfPopup 18.4%, NoOfSelfRef 14.2%, DomainAge 13.4%. Test performance: AUC=0.888 (best), Recall=73.8% @ threshold=0.65, FPR=5.1%."

### 5.4 Model Selection & Comparison

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `models/model_selector.py` | `ModelSelector` | `compare_validation_performance` | ModelSelector compares all models on validation set | Logistic, KNN, XGBoost predictions | `ComparisonTable{model: auc, recall, fpr, precision}[]` | **L4→L2**: XGBoost wins on all metrics |
| `models/model_selector.py` | `ModelSelector` | `select_production_model` | ModelSelector selects best model based on business criteria | `max_auc AND recall>=0.70 AND fpr<=0.05` | `selected_model: XGBoost, justification: str` | **L0→L4**: Business KPIs drive selection |
| `models/model_selector.py` | `ModelSelector` | `generate_model_comparison_report` | ModelSelector generates comprehensive comparison report | All model results | `ModelComparisonReport.pdf` | **L1**: Stakeholder documentation |

**Interview Signal (Excellent)**: "Model comparison (validation set): Logistic AUC=0.825, KNN AUC=0.809, XGBoost AUC=0.891. Selection criteria: (1) Max AUC for best discrimination, (2) Recall≥70%, (3) FPR≤5%. XGBoost selected: highest AUC, meets KPI constraints, feature importance for explainability. Logistic kept as interpretable backup for regulatory compliance."

---

## Phase 6: Threshold Tuning & Optimization {#phase-6-threshold-tuning}

**Purpose**: Optimize classification threshold to maximize recall subject to FPR≤5% business constraint.

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `generate_probability_scores` | ThresholdTuner generates predicted probabilities on validation set | `model.predict_proba(X_val)` | `val_probs: ndarray[1500]` in (0,1) | P(phishing|x) for each validation sample |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `sweep_thresholds` | ThresholdTuner sweeps thresholds from 0 to 1 computing metrics | `np.linspace(0, 1, 1000)` | `ThresholdSweepResults{threshold, recall, fpr, precision}[1000]` | **L2**: Generates Pareto frontier |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `apply_business_constraint` | ThresholdTuner filters thresholds satisfying FPR≤max_fpr | `max_fpr=0.05` | `feasible_thresholds[]` | **L0→L6**: Business constraint filters solution space |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `select_optimal_threshold` | ThresholdTuner selects threshold maximizing recall among feasible | `argmax(recall)` where `fpr <= 0.05` | `optimal_threshold: 0.65, achieved_recall: 0.752, achieved_fpr: 0.048` | **L6**: Constrained optimization solution |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `validate_on_test_set` | ThresholdTuner applies tuned threshold to test set | `X_test, y_test, threshold=0.65` | `TestResults{recall: 0.738, fpr: 0.051}` | Generalization check: -1.4pp recall, +0.3pp FPR (acceptable) |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `generate_pareto_visualization` | ThresholdTuner generates recall-FPR Pareto curve plot | `matplotlib` | `pareto_curve.png` with constraint lines | **L2→L1**: Stakeholder communication tool |
| `optimization/threshold_tuner.py` | `ThresholdTuner` | `analyze_pareto_ceiling` | ThresholdTuner analyzes if target KPIs achievable | Pareto curve data | `ParetoCeiling{can_achieve_targets: True, max_recall_at_fpr5: 0.752}` | If False → need better features |

**Interview Signal (Excellent)**: "Threshold tuning: Swept 1,000 thresholds on validation set. Default 0.5: recall=86.5%, FPR=18.2% (unacceptable). Objective: max recall s.t. FPR≤0.05. Found optimal at 0.65: val recall=75.2%, val FPR=4.8%. Test set generalization: recall=73.8% (-1.4pp), FPR=5.1% (+0.3pp), both within tolerance. Pareto curve shows ceiling: cannot achieve recall>80% AND FPR≤3% with current features. Next iteration: Add SSL, WHOIS to shift frontier."

---

## Phase 7: Evaluation & Metrics {#phase-7-evaluation}

**Purpose**: Comprehensive evaluation on held-out test set with business-relevant metrics.

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_confusion_matrix` | MetricsCalculator computes confusion matrix on test set | `sklearn.metrics.confusion_matrix` | `ConfusionMatrix{TP: 1704, FN: 605, FP: 238, TN: 4418}` | **L2**: Raw counts for all metrics |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_recall` | MetricsCalculator computes recall (TPR) | `TP/(TP+FN)` | `recall: 0.738 (73.8%)` | **L2→L0**: 73.8% > 70% target ✅ |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_fpr` | MetricsCalculator computes false positive rate | `FP/(FP+TN)` | `fpr: 0.051 (5.1%)` | **L2→L0**: 5.1% ≈ 5% target ⚠️ borderline |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_precision` | MetricsCalculator computes precision (PPV) | `TP/(TP+FP)` | `precision: 0.877 (87.7%)` | 87.7% of blocks are correct |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_auc_roc` | MetricsCalculator computes ROC AUC via sklearn | `sklearn.metrics.roc_auc_score` | `auc: 0.888` | **L6**: Probability model ranks phishing > legit 88.8% of time |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_auc_custom` | MetricsCalculator computes AUC via trapezoidal integration | Sort scores, integrate TPR over FPR | `auc_custom: 0.8880` | **L6**: Validates sklearn (match to 4 decimals) |
| `evaluation/metrics.py` | `MetricsCalculator` | `compute_f1_score` | MetricsCalculator computes F1 score | `2PR/(P+R)` | `f1: 0.802` | Secondary metric (not optimized for) |
| `evaluation/business_impact.py` | `BusinessImpactCalculator` | `quantify_fraud_exposure` | BusinessImpactCalculator quantifies monthly fraud exposure | `10000 × (1-recall) × 500` | `fraud_exposure: $1,310,000/month` | **L0**: 2,620 missed attacks × $500 |
| `evaluation/business_impact.py` | `BusinessImpactCalculator` | `quantify_support_cost` | BusinessImpactCalculator quantifies daily support cost | `275M × fpr × 0.01 × 5` | `support_cost: $701,250/day` | **L0**: 140,250 tickets × $5 |
| `evaluation/business_impact.py` | `BusinessImpactCalculator` | `generate_executive_summary` | BusinessImpactCalculator generates business-focused summary | All metrics + costs | `ExecutiveSummary.pdf` | **L1→L0**: PM/Legal/Eng dashboard |

**Interview Signal (Excellent)**: "Test set results (n=2,500, held-out): Confusion matrix: TP=1,704, FN=605, FP=238, TN=4,418. Metrics: Recall=73.8% (target ≥70% ✅), FPR=5.1% (target ≤5% ⚠️ borderline), Precision=87.7%, AUC=0.888. Business impact: 605 false negatives = $302,500 monthly fraud exposure (605×$500). 238 false positives = ~2,400 daily support tickets (238/2500 test ratio × 275M daily predictions × 1% escalation). Custom AUC via trapezoidal integration=0.8880 matches sklearn, validates implementation."

---

## Phase 8: Deployment & Monitoring {#phase-8-deployment}

**Purpose**: Production deployment with monitoring, rollback capability, and compliance.

### 8.1 Model Packaging & Deployment

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `deployment/model_packager.py` | `ModelPackager` | `serialize_model` | ModelPackager serializes trained model with metadata | `pickle`, model object | `xgboost_v2.3.1.pkl {model, threshold, scaler, metadata}` | **L5**: 15MB artifact |
| `deployment/model_packager.py` | `ModelPackager` | `create_model_card` | ModelPackager creates model card documentation | All training metadata | `ModelCard.md {version, metrics, training_date, features, known_limitations}` | **L1**: Legal compliance doc |
| `deployment/model_packager.py` | `ModelPackager` | `containerize_model` | ModelPackager builds Docker image with model | `Dockerfile`, dependencies | `ml-phishing-detector:v2.3.1 (Docker image)` | **L5**: Production artifact |
| `deployment/api.py` | `PredictionAPI` | `load_model_artifact` | PredictionAPI loads serialized model into memory | `xgboost_v2.3.1.pkl` | `self.model, self.threshold, self.scaler` | Startup: 2.3s cold start |
| `deployment/api.py` | `PredictionAPI` | `predict_endpoint` | PredictionAPI exposes HTTP endpoint for predictions | `Flask/FastAPI` | `POST /api/v1/predict → {prediction, confidence, latency_ms}` | **L5**: p50=18ms, p99=87ms |
| `deployment/api.py` | `PredictionAPI` | `generate_explanation` | PredictionAPI generates SHAP-based explanation | `shap.TreeExplainer` | `Explanation{top_features: [{name, value, contribution}]}` | **L1**: GDPR compliance |

**Interview Signal (Excellent)**: "Model packaging: Serialized XGBoost + threshold=0.65 + StandardScaler → 15MB pickle. Docker image: ml-phishing-detector:v2.3.1 with Python 3.9, XGBoost 1.5.1, dependencies. API: FastAPI endpoint POST /api/v1/predict. Performance: p50 latency=18ms, p99=87ms (target <100ms ✅). SHAP explainability: per-prediction top 3 features with contributions (e.g., 'DomainAge=2 months contributed -0.28 toward phishing')."

### 8.2 Blue-Green Deployment

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `deployment/blue_green.py` | `BlueGreenDeployer` | `deploy_green_shadow_mode` | BlueGreenDeployer deploys new model in shadow mode (logs only) | `Kubernetes`, green deployment manifest | `green_deployment (0% traffic, logs predictions)` | **L5**: Week 1—no user impact |
| `deployment/blue_green.py` | `BlueGreenDeployer` | `compare_blue_green_predictions` | BlueGreenDeployer compares blue vs green prediction disagreement | Prediction logs | `DisagreementReport{rate: 0.08, cases: []}` | 8% disagreement investigated |
| `deployment/blue_green.py` | `BlueGreenDeployer` | `gradual_traffic_shift` | BlueGreenDeployer incrementally routes traffic to green | `Kubernetes Service`, traffic weights | `traffic_split{blue: 90%, green: 10%}` → 50% → 100% | **L5**: Week 2-4 rollout |
| `deployment/blue_green.py` | `BlueGreenDeployer` | `monitor_rollout_metrics` | BlueGreenDeployer monitors recall/FPR during rollout | `Prometheus` queries | `RolloutMetrics{green_recall, green_fpr, anomaly_detected: bool}` | **L2→L5**: Real-time KPI tracking |
| `deployment/blue_green.py` | `BlueGreenDeployer` | `rollback_to_blue` | BlueGreenDeployer switches traffic back to blue if metrics degrade | `kubectl set image` | `traffic_split{blue: 100%, green: 0%}` | **L5**: <1 min rollback via load balancer |
| `deployment/blue_green.py` | `BlueGreenDeployer` | `finalize_deployment` | BlueGreenDeployer promotes green to blue after successful rollout | Rename deployments | `blue ← green, green deleted` | Green becomes new blue |

**Interview Signal (Excellent)**: "Blue-green deployment: Week 1—Shadow mode (green logs predictions, 0% traffic, compare to blue: 8% disagreement, investigated cases). Week 2—A/B test (10% traffic to green, monitor daily: recall=73.2%, FPR=5.4%, within tolerance). Week 3—50% traffic, stable metrics. Week 4—100% traffic, green finalized. Rollback protocol: if recall<65% or FPR>6% for 2 consecutive days, kubectl switches to blue in <1 min. Tested monthly: avg rollback=47 seconds."

### 8.3 Production Monitoring

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `monitoring/system_health.py` | `SystemHealthMonitor` | `track_latency_percentiles` | SystemHealthMonitor tracks p50/p95/p99 latency | `Prometheus histogram` | `latency_metrics{p50: 18ms, p95: 42ms, p99: 87ms}` | **L5→L1**: Eng SLA compliance |
| `monitoring/system_health.py` | `SystemHealthMonitor` | `track_error_rates` | SystemHealthMonitor tracks 4xx and 5xx error rates | `Prometheus counter` | `error_rate{4xx: 0.02%, 5xx: 0.01%}` | Target: <0.1% |
| `monitoring/system_health.py` | `SystemHealthMonitor` | `track_throughput` | SystemHealthMonitor tracks requests per second | `Prometheus counter` | `rps{current: 3200, peak: 5500}` | Capacity: 100K+ predictions/day |
| `monitoring/feature_drift.py` | `FeatureDriftDetector` | `compute_kl_divergence` | FeatureDriftDetector computes KL divergence vs training distribution | `scipy.stats.entropy` | `KL_Divergence{feature, d_kl}[]` | **L3→L5**: Alert if D_KL>0.1 |
| `monitoring/feature_drift.py` | `FeatureDriftDetector` | `detect_distribution_shift` | FeatureDriftDetector flags significant distribution changes | Daily batch | `DriftAlert{feature: 'NoOfPopup', d_kl: 0.12, timestamp}` | Triggers investigation |
| `monitoring/performance_decay.py` | `PerformanceMonitor` | `compute_weekly_recall_fpr` | PerformanceMonitor computes recall/FPR on labeled sample | Ground truth (n=200/week) | `WeeklyPerformance{recall: 0.728, fpr: 0.053}` | **L2→L5**: Early degradation detection |
| `monitoring/performance_decay.py` | `PerformanceMonitor` | `trigger_retraining_pipeline` | PerformanceMonitor triggers automated retraining if recall<70% | Performance thresholds | `RetrainingJob{triggered_by: 'recall_decay', timestamp}` | **L4**: Auto-remediation |
| `monitoring/business_metrics.py` | `BusinessMetricsTracker` | `track_daily_blocks` | BusinessMetricsTracker tracks phishing sites blocked per day | Prediction logs | `daily_blocks: 18234` | **L0**: Business value metric |
| `monitoring/business_metrics.py` | `BusinessMetricsTracker` | `track_appeal_rate` | BusinessMetricsTracker tracks user appeal rate (FPR proxy) | Support tickets | `appeal_rate: 0.049 (4.9%)` | **L0→L2**: FPR proxy metric |
| `monitoring/alerting.py` | `AlertManager` | `send_pagerduty_alert` | AlertManager sends critical alerts to on-call engineer | `PagerDuty API` | `Alert{severity: 'critical', message: 'Recall <65%'}` | **L5**: Incident response |
| `monitoring/dashboards.py` | `DashboardGenerator` | `generate_grafana_dashboard` | DashboardGenerator creates Grafana monitoring dashboard | `Grafana API` | `PhishingModelDashboard{panels: [latency, recall, fpr, drift]}` | **L1**: Stakeholder visibility |

**Interview Signal (Excellent)**: "Four-layer monitoring: (1) System health—Prometheus tracks p50=18ms, p95=42ms, p99=87ms (✅ <100ms target), RPS 3,200 sustained. (2) Feature drift—Daily KL divergence: NoOfPopup D_KL=0.08 (OK), alert if >0.1. (3) Performance decay—Weekly recall on n=200 labeled sample: 72.8% (✅ >70%), FPR=5.3% (✅ ≤6%). (4) Business metrics—Daily blocks 18,234 (↑3% vs last week), appeal rate 4.9% (proxy FPR). Alerting: PagerDuty if recall<65% or p99>150ms. Grafana dashboard for PM/Legal/Eng visibility."

---

## Cross-Cutting Concerns {#cross-cutting-concerns}

**Purpose**: Shared utilities, logging, validation, and compliance mechanisms across all phases.

### Logging & Audit Trail

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `utils/logger.py` | `PipelineLogger` | `log_pipeline_stage` | PipelineLogger logs each pipeline stage with timestamp | `logging` | `pipeline.log entry: [2026-01-10 14:32:18] PHASE_1_EDA COMPLETED` | **L1**: Audit trail for compliance |
| `utils/logger.py` | `PipelineLogger` | `log_data_quality_issue` | PipelineLogger logs data quality warnings | Issue details | `log entry: [WARNING] DomainAge: 21.5% missing` | **L5**: Debugging aid |
| `utils/logger.py` | `PipelineLogger` | `log_model_decision` | PipelineLogger logs every production prediction | `{timestamp, url_hash, model_v, prediction, features}` | `prediction_audit.log` (90-day retention) | **L1**: GDPR Article 22 compliance |
| `utils/logger.py` | `PipelineLogger` | `archive_logs_to_s3` | PipelineLogger archives logs after 90 days | `boto3`, S3 bucket | `s3://ml-audit-logs/2025/Q4/` | **L1**: 7-year retention requirement |

### Validation & Quality Gates

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `validation/pipeline_validator.py` | `PipelineValidator` | `validate_data_quality` | PipelineValidator checks data quality thresholds | Quality rules | `QualityReport{missing_rate_ok: True, outlier_rate_ok: True}` | Abort if thresholds exceeded |
| `validation/pipeline_validator.py` | `PipelineValidator` | `validate_feature_consistency` | PipelineValidator ensures feature set matches training | Expected features list | `FeatureConsistency{all_present: True}` | **L5**: Prevents feature mismatch bugs |
| `validation/pipeline_validator.py` | `PipelineValidator` | `validate_no_data_leakage` | PipelineValidator confirms preprocessing fitted only on train | Scaler, Imputer provenance | `LeakageCheck{train_only: True}` | **Critical**: Prevents optimistic bias |
| `validation/pipeline_validator.py` | `PipelineValidator` | `validate_model_performance` | PipelineValidator checks model meets minimum KPIs | `min_recall=0.70, max_fpr=0.05` | `PerformanceValidation{meets_requirements: True}` | **L2→L0**: Business gate |
| `validation/pipeline_validator.py` | `PipelineValidator` | `generate_validation_report` | PipelineValidator generates comprehensive validation report | All validation results | `pipeline_validation.json` | **L1**: Audit artifact |

### Error Handling & Resilience

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `utils/error_handler.py` | `ErrorHandler` | `retry_with_backoff` | ErrorHandler retries failed operations with exponential backoff | `time.sleep` | `result or raises Exception after 3 attempts` | **L5**: Database connection resilience |
| `utils/error_handler.py` | `ErrorHandler` | `handle_data_error` | ErrorHandler handles data-related errors gracefully | Exception details | `DataQualityError with diagnostic info` | **L5**: Informative error messages |
| `utils/error_handler.py` | `ErrorHandler` | `handle_model_error` | ErrorHandler handles model training/inference errors | Exception details | `ModelError with hyperparameters logged` | **L5**: Debugging context |
| `utils/error_handler.py` | `ErrorHandler` | `graceful_degradation` | ErrorHandler provides fallback when model unavailable | Fallback rules | `FallbackPrediction{source: 'rule_based', confidence: 'low'}` | **L5**: High availability |

### Reproducibility

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|
| `utils/reproducibility.py` | `ReproducibilityManager` | `set_random_seeds` | ReproducibilityManager sets all random seeds for reproducibility | `random.seed(42), np.random.seed(42)` | Deterministic behavior | **L5**: random_state=42 throughout |
| `utils/reproducibility.py` | `ReproducibilityManager` | `snapshot_environment` | ReproducibilityManager captures Python/library versions | `pip freeze` | `requirements.txt` | **L5**: Environment reproducibility |
| `utils/reproducibility.py` | `ReproducibilityManager` | `snapshot_configuration` | ReproducibilityManager saves all pipeline configuration | Config objects | `config_snapshot.yaml` | **L5**: Experiment tracking |
| `utils/reproducibility.py` | `ReproducibilityManager` | `version_artifacts` | ReproducibilityManager versions all pipeline artifacts | Git commit hash | `artifacts/run_20260110_143218/` | **L5**: Timestamped experiments |

---

## Interview Assessment Matrix

### Poor Candidate Signals

| Phase | Poor Signal | Example |
|-------|-------------|---------|
| EDA | "Filled missing values with mean" | No MNAR testing, mechanical imputation |
| Statistical | "Checked class balance" | No chi-square test, no quantification |
| Preprocessing | "Scaled features" | No skewness analysis, no transform validation |
| Training | "Trained XGBoost with default params" | No hyperparameter tuning justification |
| Threshold | "Used 0.5 threshold" | No threshold tuning, ignores business constraints |
| Evaluation | "Got 88% accuracy" | Reports accuracy (not recall/FPR), no business impact |
| Deployment | "Deployed model to server" | No monitoring, rollback, or compliance plan |

### Qualified Candidate Signals

| Phase | Qualified Signal | Example |
|-------|------------------|---------|
| EDA | "Tested MNAR, found DomainAge missing related to target" | Mentions MNAR concept, basic test |
| Statistical | "Class imbalance 55:45 is significant" | States finding, basic reasoning |
| Preprocessing | "Log-transformed skewed features" | Applies transform, basic justification |
| Training | "Tuned XGBoost max_depth and learning_rate" | Basic hyperparameter tuning |
| Threshold | "Tuned to 0.65 for better FPR" | Acknowledges tuning need |
| Evaluation | "Recall 73.8%, FPR 5.1%" | Reports relevant metrics |
| Deployment | "Deployed with monitoring" | Mentions monitoring concept |

### Excellent Candidate Signals

| Phase | Excellent Signal | Example |
|-------|------------------|---------|
| EDA | "Chi-square test: χ²=42.3, p=0.003 → MNAR. Created binary flag before imputation. A/B validation: +2.8pp recall." | Statistical rigor + quantification + validation |
| Statistical | "Three chi-square tests: (1) Class imbalance χ²=115.2, (2) MNAR χ²=42.3, (3) Stratification χ²=0.82, all logged." | Multiple applications, specific results |
| Preprocessing | "Log-transform for 10 features |skew|>1. Convergence validation: 4.3× speedup. Q-Q plots confirm normality." | Empirical validation, quantified impact |
| Training | "Grid search 54 configs × 5-fold. Best depth=6 (not 8—test AUC 0.888 vs 0.882). Early stopping at iter 68." | Comprehensive tuning with trade-off analysis |
| Threshold | "Swept 1,000 thresholds. Optimal 0.65: val recall=75.2%, FPR=4.8%. Test: 73.8%, 5.1% (within tolerance). Pareto ceiling analysis." | Full procedure + generalization check + strategic insight |
| Evaluation | "Test: TP=1,704, FN=605 → 605×$500=$302K monthly fraud exposure. FP=238 → 2,400 daily tickets×$5=$12K." | Business impact quantification |
| Deployment | "Blue-green: Shadow→10%→50%→100%. Monitoring: 4-layer (system/drift/perf/biz). Rollback <1 min if recall<65%." | Comprehensive deployment strategy |

---

## Traversal Paths for GraphRAG

### Business-Driven Query: "Why does recall matter?"

**Path**: `business_fraud_exposure` → `kpi_recall` → `model_threshold_tuning` → `mathematical_gradient_descent`

**Traversal**:
1. **L0 Business**: Fraud exposure = 10,000 attacks × (1-recall) × $500. At recall=70%, exposure=$1.5M/month.
2. **L2 KPI**: Recall = TP/(TP+FN) measures attack catch rate. Target ≥70% from cost-benefit analysis.
3. **L4 Model**: Threshold tuning maximizes recall subject to FPR≤5% constraint. Selected threshold=0.65.
4. **L6 Math**: Gradient descent minimizes loss L(θ) to optimize model parameters enabling high recall.

### Technical-Driven Query: "How does gradient descent improve fraud detection?"

**Path**: `mathematical_gradient_descent` → `mathematical_loss_function` → `model_logistic_regression` → `kpi_recall` → `business_fraud_exposure`

**Traversal**:
1. **L6 Math**: Gradient descent: θ_new = θ_old - α∇L(θ). Minimizes binary cross-entropy loss.
2. **L6 Math**: Loss L(θ) = -(1/m)Σ[y log(ŷ)+(1-y)log(1-ŷ)]. Lower loss = better predictions.
3. **L4 Model**: Logistic regression achieves AUC=0.825 via gradient descent convergence (120 epochs).
4. **L2 KPI**: Higher AUC enables better recall-FPR trade-off. Threshold tuning achieves recall=73.8%.
5. **L0 Business**: Recall=73.8% means catching 7,380 of 10,000 attacks, preventing $1.31M fraud monthly.

---

**End of Maximum LOD Directory Table**