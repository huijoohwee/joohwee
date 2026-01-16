---
title: "interview-session-implementation-guide"
author: "joohwee"
tags: [EDA, MLP, Test]
date: 2026-01-12
mermaidAnchorsOnly: true
mermaid: |
  flowchart TD
    Start([Start Implementation<br/>From Clean Slate]) --> Phase0_Start

    %% ===================================================================
    %% Phase 0: Setup & Data Acquisition (30 min)
    %% ===================================================================
    subgraph Phase0["Phase 0: Setup & Data Acquisition (30 min)"]
        Phase0_Start[0.1.0 Download phishing.db<br/>to data/ folder]
        Phase0_Start --> P0_2_0[0.2.0 Create project structure]
        P0_2_0 --> P0_2_1[0.2.1 Create src/ folder]
        P0_2_1 --> P0_2_2[0.2.2 Create results/ folder]
        P0_2_2 --> P0_2_3[0.2.3 Create .gitignore<br/>data/, results/, __pycache__]
        
        P0_2_3 --> P0_3_0[0.3.0 Implement DataLoader]
        P0_3_0 --> P0_3_1[0.3.1 Create DataLoader class]
        P0_3_1 --> P0_3_2[0.3.2 Implement load_from_sqlite<br/>SQLite → DataFrame + ValidationReport]
        P0_3_2 --> P0_3_3[0.3.3 Implement validate_schema<br/>Check 46+1 columns, dtypes]
        P0_3_3 --> P0_3_4[0.3.4 Implement check_row_count<br/>Ensure ≥1000 samples]
        P0_3_4 --> P0_3_5[0.3.5 Implement parse_target_variable<br/>Validate labels ∈ {0,1}]
        P0_3_5 --> P0_3_6[0.3.6 Add S-V-O docstrings]
        
        P0_3_6 --> P0_4_0[0.4.0 Create requirements.txt<br/>Pin versions: pandas, numpy, sklearn, xgboost]
        P0_4_0 --> P0_5_0[0.5.0 Create run.sh<br/>#!/bin/bash, set -e, python src/main.py]
        P0_5_0 --> P0_6_0{0.6.0 Test Setup<br/>bash run.sh succeeds?}
    end

    P0_6_0 -->|✓ Yes| Phase1_Start
    P0_6_0 -->|✗ No| P0_Fix[Debug: Check imports,<br/>data path, permissions]
    P0_Fix --> P0_6_0

    %% ===================================================================
    %% Phase 1: Exploratory Data Analysis (3-4 hours)
    %% ===================================================================
    subgraph Phase1["Phase 1: Exploratory Data Analysis (3-4 hours)"]
        Phase1_Start[1.1.0 Create eda.ipynb<br/>Markdown header with TOC]
        Phase1_Start --> P1_2_0[1.2.0 Section 1: Data Overview]
        P1_2_0 --> P1_2_1[1.2.1 Load with DataLoader<br/>df.shape, df.info, df.describe]
        P1_2_1 --> P1_2_2[1.2.2 Target distribution<br/>55% legit, 45% phishing]
        P1_2_2 --> P1_2_3[1.2.3 State baseline accuracy<br/>55% naive predictor]
        
        P1_2_3 --> P1_3_0[1.3.0 Section 2: Missing Values]
        P1_3_0 --> P1_3_1[1.3.1 Compute missing rates<br/>per column, sort descending]
        P1_3_1 --> P1_3_2[1.3.2 Create heatmap<br/>seaborn missing pattern]
        P1_3_2 --> P1_3_3[1.3.3 Categorize by severity<br/>Severe >70%, Moderate 20-70%, Low <20%]
        P1_3_3 --> P1_3_4[1.3.4 MNAR Test: DomainAge<br/>χ²=450, p<0.001<br/>Contingency: missing × target]
        P1_3_4 --> P1_3_5[1.3.5 Document imputation<br/>DomainAge: flag + median<br/>Numeric: median, Categorical: mode]
        
        P1_3_5 --> P1_4_0[1.4.0 Section 3: Univariate]
        P1_4_0 --> P1_4_1[1.4.1 Compute skewness<br/>10 features |skew|>2]
        P1_4_1 --> P1_4_2[1.4.2 Detect outliers IQR<br/>Q1-1.5×IQR, Q3+1.5×IQR]
        P1_4_2 --> P1_4_3[1.4.3 Histograms for numeric<br/>Grid with Q1/median/Q3 lines]
        P1_4_3 --> P1_4_4[1.4.4 Bar charts for categorical<br/>Industry 8 unique, HostingProvider 15]
        P1_4_4 --> P1_4_5[1.4.5 Document preprocessing<br/>LineOfCode: clip at 99th + log1p]
        
        P1_4_5 --> P1_5_0[1.5.0 Section 4: Bivariate]
        P1_5_0 --> P1_5_1[1.5.1 Correlation matrix<br/>Pearson r, heatmap]
        P1_5_1 --> P1_5_2[1.5.2 Rank by |r| with target<br/>Top 5 features]
        P1_5_2 --> P1_5_3[1.5.3 T-tests for numerics<br/>ExternalSelfRatio: t=12.4, p<0.001]
        P1_5_3 --> P1_5_4[1.5.4 Scatter plots vs target<br/>Box plots by class]
        P1_5_4 --> P1_5_5[1.5.5 Chi-square for categoricals<br/>Industry χ²=87, p<0.001]
        
        P1_5_5 --> P1_6_0[1.6.0 Section 5: Multivariate]
        P1_6_0 --> P1_6_1[1.6.1 PCA 2D visualization<br/>PC1=23%, PC2=12%<br/>Partial class separation]
        P1_6_1 --> P1_6_2[1.6.2 Identify interactions<br/>High ExtRef × Low DomainAge = phishing]
        
        P1_6_2 --> P1_7_0[1.7.0 Section 6: Summary]
        P1_7_0 --> P1_7_1[1.7.1 Create EDA→MLP table<br/>Finding | Evidence | Decision | Impact]
        P1_7_1 --> P1_7_2[1.7.2 Hypothesis for models<br/>XGBoost will outperform due to interactions]
        P1_7_2 --> P1_7_3[1.7.3 Document validation plan<br/>List chi-square tests to run]
        
        P1_7_3 --> P1_8_0[1.8.0 Polish notebook<br/>Restart & Run All, proofread]
    end

    P1_8_0 --> Phase2_Start

    %% ===================================================================
    %% Phase 2: Statistical Hypothesis Testing (1-2 hours)
    %% ===================================================================
    subgraph Phase2["Phase 2: Statistical Hypothesis Testing (1-2 hours)"]
        Phase2_Start[2.1.0 Create hypothesis_tester.py<br/>HypothesisTester class, α=0.05]
        Phase2_Start --> P2_2_0[2.2.0 Test 1: Class Balance]
        P2_2_0 --> P2_2_1[2.2.1 Implement test_class_balance_significance<br/>H₀: P(phishing)=0.5<br/>Observed [6050,4950] vs Expected [5500,5500]<br/>χ²=110, p<0.001 → Reject H₀]
        P2_2_1 --> P2_2_2[2.2.2 Add to eda.ipynb Section 1<br/>Display test result, interpretation]
        
        P2_2_2 --> P2_3_0[2.3.0 Test 2: MNAR Hypothesis]
        P2_3_0 --> P2_3_1[2.3.1 Implement test_mnar_hypothesis<br/>Contingency: [missing × target]<br/>chi2_contingency → χ², p-value]
        P2_3_1 --> P2_3_2[2.3.2 Test DomainAge, Robots, IsResponsive<br/>DomainAge: MNAR (p<0.001)<br/>Robots: borderline (p=0.04)]
        P2_3_2 --> P2_3_3[2.3.3 Add to eda.ipynb Section 2<br/>Table: feature, χ², p, conclusion]
        
        P2_3_3 --> P2_4_0[2.4.0 Test 3: Stratification<br/>After split in pipeline]
        P2_4_0 --> P2_4_1[2.4.1 Implement validate_stratified_splits<br/>Chi-square per split vs full dist<br/>Train p=0.08, Val p=0.76, Test p=0.82]
        P2_4_1 --> P2_4_2[2.4.2 Integrate into pipeline<br/>Call after split, log results]
        
        P2_4_2 --> P2_5_0[2.5.0 Save all tests<br/>results/hypothesis_tests.json<br/>Include: test, H₀, χ², p, reject_h0, timestamp]
        P2_5_0 --> P2_6_0[2.6.0 Document in README<br/>Table: Test | H₀ | χ² | p | Conclusion | Impact]
    end

    P2_6_0 --> Phase3_Start

    %% ===================================================================
    %% Phase 3: Feature Engineering & Preprocessing (2-3 hours) 🔴 CRITICAL
    %% ===================================================================
    subgraph Phase3["Phase 3: Feature Engineering & Preprocessing (2-3 hours) 🔴 CRITICAL"]
        Phase3_Start[3.1.0 ⚠️ SPLIT FIRST PARADIGM<br/>Mental model: Never test influences preprocessing]
        
        Phase3_Start --> P3_2_0[3.2.0 Create FeatureEngineer class]
        P3_2_0 --> P3_2_1[3.2.1 Implement __init__<br/>enable_flags, enable_bins, enable_ratios<br/>quantile_bins=None, freq_maps=None]
        P3_2_1 --> P3_2_2[3.2.2 Implement fit method<br/>Learn quantile_bins from train<br/>Learn freq_maps from train<br/>Return self]
        P3_2_2 --> P3_2_3[3.2.3 Implement transform method<br/>Apply stored quantile_bins<br/>Apply stored freq_maps<br/>Never recompute]
        
        P3_2_3 --> P3_3_0[3.3.0 Create missing flags]
        P3_3_0 --> P3_3_1[3.3.1 create_missing_flags helper<br/>DomainAge_missing = df.isna.astype int<br/>Robots_missing, IsResponsive_missing]
        
        P3_3_1 --> P3_4_0[3.4.0 Create domain ratios]
        P3_4_0 --> P3_4_1[3.4.1 create_external_self_ratio<br/>Ext / (Self+1)<br/>Prevents division by zero]
        
        P3_4_1 --> P3_5_0[3.5.0 Create Preprocessor class]
        P3_5_0 --> P3_5_1[3.5.1 Implement __init__<br/>clip_quantile=0.99<br/>impute_strategy='median'<br/>scale_method='standard']
        P3_5_1 --> P3_5_2[3.5.2 Implement fit_transform<br/>TRAINING DATA ONLY<br/>Learn: clip_values, imputers,<br/>scaler_params, columns<br/>Apply: log-clip, impute, encode, scale]
        P3_5_2 --> P3_5_3[3.5.3 Implement transform<br/>VAL/TEST DATA<br/>Apply TRAIN-LEARNED params<br/>NO RECOMPUTATION<br/>reindex for column alignment]
        
        P3_5_3 --> P3_6_0[3.6.0 Log-clipping helper]
        P3_6_0 --> P3_6_1[3.6.1 _log_clip method<br/>Clip at stored 99th percentile<br/>Apply log1p]
        
        P3_6_1 --> P3_7_0[3.7.0 Imputation helper]
        P3_7_0 --> P3_7_1[3.7.1 _impute method<br/>Numeric: fillna with stored median<br/>Categorical: fillna with stored mode<br/>Fallback to 'unknown' if all missing]
        
        P3_7_1 --> P3_8_0[3.8.0 Encoding + alignment]
        P3_8_0 --> P3_8_1[3.8.1 One-hot encode<br/>pd.get_dummies]
        P3_8_1 --> P3_8_2[3.8.2 Column alignment<br/>df.reindex columns=self.columns_<br/>fill_value=0 for unseen categories]
        
        P3_8_2 --> P3_9_0[3.9.0 Scaling helper]
        P3_9_0 --> P3_9_1[3.9.1 _scale method<br/>(df - stored_mean) / stored_std]
        
        P3_9_1 --> P3_10_0[3.10.0 main.py orchestration]
        P3_10_0 --> P3_10_1[3.10.1 Load data]
        P3_10_1 --> P3_10_2[3.10.2 SPLIT FIRST<br/>stratified_split 70/15/15]
        P3_10_2 --> P3_10_3[3.10.3 engineer.fit df_train]
        P3_10_3 --> P3_10_4[3.10.4 engineer.transform<br/>train, val, test]
        P3_10_4 --> P3_10_5[3.10.5 preprocessor.fit_transform<br/>df_train only]
        P3_10_5 --> P3_10_6[3.10.6 preprocessor.transform<br/>val, test]
        P3_10_6 --> P3_10_7[3.10.7 Save preprocessor.pkl]
        
        P3_10_7 --> P3_11_0[3.11.0 Add S-V-O docstrings<br/>All methods documented]
        P3_11_0 --> P3_12_0{3.12.0 Validate output<br/>No missing? No inf?<br/>Shapes correct?}
    end

    P3_12_0 -->|✓ Yes| Phase4_Start
    P3_12_0 -->|✗ No| P3_Debug[Debug:<br/>Check assertions,<br/>print intermediate shapes]
    P3_Debug --> P3_5_2

    %% ===================================================================
    %% Phase 4: Data Splitting & Validation (30 min)
    %% ===================================================================
    subgraph Phase4["Phase 4: Data Splitting & Validation (30 min)"]
        Phase4_Start[4.1.0 Create data_splitter.py]
        Phase4_Start --> P4_2_0[4.2.0 Implement stratified_split]
        P4_2_0 --> P4_2_1[4.2.1 Set random_state=42<br/>np.random.default_rng]
        P4_2_1 --> P4_2_2[4.2.2 Per-class indices<br/>Shuffle within class<br/>Split 70/15/15]
        P4_2_2 --> P4_2_3[4.2.3 Verify split sizes<br/>Log sample counts]
        
        P4_2_3 --> P4_3_0[4.3.0 Create pipeline_validator.py]
        P4_3_0 --> P4_4_0[4.4.0 Implement validate_stratification]
        P4_4_0 --> P4_4_1[4.4.1 Chi-square per split<br/>Observed vs Expected from full dist<br/>Train p=0.08, Val p=0.76, Test p=0.82]
        P4_4_1 --> P4_4_2[4.4.2 Save validation results<br/>results/stratification_validation.json]
        
        P4_4_2 --> P4_5_0[4.5.0 Implement validate_processed]
        P4_5_0 --> P4_5_1[4.5.1 Assert no missing values<br/>not X.isna.any.any]
        P4_5_1 --> P4_5_2[4.5.2 Assert no infinities<br/>not np.isinf X.any]
        P4_5_2 --> P4_5_3[4.5.3 Check label proportions<br/>Compute per split]
        P4_5_3 --> P4_5_4[4.5.4 Validate sample sizes<br/>Test ≥150 per class]
        
        P4_5_4 --> P4_6_0[4.6.0 Compute CI for test set]
        P4_6_0 --> P4_6_1[4.6.1 Calculate CI<br/>742 phishing → recall CI ±3.6%<br/>Formula: ±1.96 × sqrt p(1-p)/n]
        
        P4_6_1 --> P4_7_0[4.7.0 Integrate into pipeline<br/>Call after preprocessing<br/>Log to results/]
    end

    P4_7_0 --> Phase5_Start

    %% ===================================================================
    %% Phase 5: Model Training & Selection (2-3 hours)
    %% ===================================================================
    subgraph Phase5["Phase 5: Model Training & Selection (2-3 hours)"]
        Phase5_Start[5.1.0 Create models.py<br/>Three model classes with fit/predict_proba]
        
        Phase5_Start --> P5_2_0[5.2.0 LogisticRegressionModel]
        P5_2_0 --> P5_2_1[5.2.1 __init__<br/>lr=0.01, epochs=1000, L2_lambda=0.1]
        P5_2_1 --> P5_2_2[5.2.2 fit method<br/>Gradient descent with L2<br/>Store weights, bias]
        P5_2_2 --> P5_2_3[5.2.3 predict_proba<br/>sigmoid X @ w + b<br/>Return (n,2) array]
        
        P5_2_3 --> P5_3_0[5.3.0 KNNModel]
        P5_3_0 --> P5_3_1[5.3.1 fit method<br/>Store X_train, y_train<br/>Lazy learning]
        P5_3_1 --> P5_3_2[5.3.2 predict_proba<br/>k=15 nearest neighbors<br/>Distance-based voting]
        
        P5_3_2 --> P5_4_0[5.4.0 XGBoostModel]
        P5_4_0 --> P5_4_1[5.4.1 Configure hyperparams<br/>max_depth=6, n_estimators=100<br/>learning_rate=0.1<br/>scale_pos_weight=1.22]
        P5_4_1 --> P5_4_2[5.4.2 Optional: Grid search<br/>Cross-validation tuning]
        
        P5_4_2 --> P5_5_0[5.5.0 Create ModelSelector]
        P5_5_0 --> P5_5_1[5.5.1 compare_models<br/>Sort by: -tuned_recall, fpr, -roc_auc<br/>Metric hierarchy]
        P5_5_1 --> P5_5_2[5.5.2 select_best<br/>Return top-ranked model]
        
        P5_5_2 --> P5_6_0[5.6.0 Train all three models]
        P5_6_0 --> P5_6_1[5.6.1 Initialize with hyperparams]
        P5_6_1 --> P5_6_2[5.6.2 Fit on X_train, y_train]
        P5_6_2 --> P5_6_3[5.6.3 Predict on validation set]
        P5_6_3 --> P5_6_4[5.6.4 Save models as .pkl]
        P5_6_4 --> P5_6_5[5.6.5 Log training times]
        
        P5_6_5 --> P5_7_0[5.7.0 Document in README<br/>Table: Model | Type | Hyperparams | Results<br/>Logistic: 71.2% recall @ 4.8% FPR<br/>KNN: 68.5% recall @ 4.9% FPR<br/>XGBoost: 74.1% recall @ 4.9% FPR]
    end

    P5_7_0 --> Phase6_Start

    %% ===================================================================
    %% Phase 6: Threshold Tuning & Optimization (1-2 hours) 🔴 REDEMPTION
    %% ===================================================================
    subgraph Phase6["Phase 6: Threshold Tuning & Optimization (1-2 hours) 🔴 REDEMPTION"]
        Phase6_Start[6.1.0 ⚠️ THIS IS YOUR REDEMPTION<br/>Acknowledge: max_fpr=0.03 ERROR<br/>caused 12% recall]
        
        Phase6_Start --> P6_2_0[6.2.0 Create config.yaml]
        P6_2_0 --> P6_2_1[6.2.1 Set max_fpr: 0.05<br/>✓ NOT 0.03 ✗<br/>Business constraint: FPR≤5%]
        
        P6_2_1 --> P6_3_0[6.3.0 Implement evaluate_tuned]
        P6_3_0 --> P6_3_1[6.3.1 Generate threshold grid<br/>np.linspace 1.0, 0.0, 1001<br/>Fine granularity 0.001]
        P6_3_1 --> P6_3_2[6.3.2 Compute metrics per threshold<br/>y_pred = y_proba >= t<br/>For each: FPR, recall, precision, F1]
        P6_3_2 --> P6_3_3[6.3.3 Filter by constraint<br/>acceptable = sweep_df[FPR <= max_fpr]<br/>Enforce business rule]
        P6_3_3 --> P6_3_4[6.3.4 Select max recall<br/>best_threshold = acceptable.recall.idxmax<br/>threshold=0.78 → 74.1% recall @ 4.9% FPR]
        P6_3_4 --> P6_3_5[6.3.5 Save threshold_sweep.csv<br/>All t, recall, FPR, F1 for audit]
        
        P6_3_5 --> P6_4_0[6.4.0 Optional: Pareto analysis]
        P6_4_0 --> P6_4_1[6.4.1 compute_pareto_frontier<br/>Sort by FPR, keep if recall > max_seen<br/>Non-dominated points]
        P6_4_1 --> P6_4_2[6.4.2 plot_pareto_curve<br/>Scatter all gray, frontier red<br/>Chosen threshold green star<br/>Constraint line blue vertical]
        
        P6_4_2 --> P6_5_0[6.5.0 Calculate business impact]
        P6_5_0 --> P6_5_1[6.5.1 OLD scenario<br/>max_fpr=0.03, recall=12%<br/>54K/450K caught, $198M fraud]
        P6_5_1 --> P6_5_2[6.5.2 NEW scenario<br/>max_fpr=0.05, recall=74%<br/>333K/450K caught, $58.5M fraud]
        P6_5_2 --> P6_5_3[6.5.3 Compute delta<br/>261 more attacks/day<br/>15 more FP/day<br/>SAVINGS: $139.5M monthly<br/>ROI: 116:1]
        
        P6_5_3 --> P6_6_0[6.6.0 Integrate into pipeline<br/>Apply to all models]
        P6_6_0 --> P6_6_1[6.6.1 Get y_proba_val]
        P6_6_1 --> P6_6_2[6.6.2 Call evaluate_tuned per model]
        P6_6_2 --> P6_6_3[6.6.3 Store tuned_metrics<br/>Use tuned_recall for selection]
        
        P6_6_3 --> P6_7_0[6.7.0 Document in README<br/>Section: Threshold Tuning<br/>OLD vs NEW comparison<br/>$139.5M savings highlighted]
    end

    P6_7_0 --> Phase7_Start

    %% ===================================================================
    %% Phase 7: Evaluation & Metrics (1 hour)
    %% ===================================================================
    subgraph Phase7["Phase 7: Evaluation & Metrics (1 hour)"]
        Phase7_Start[7.1.0 Implement evaluate function]
        Phase7_Start --> P7_1_1[7.1.1 Compute confusion matrix<br/>sklearn.metrics.confusion_matrix<br/>Extract TN, FP, FN, TP]
        P7_1_1 --> P7_1_2[7.1.2 Derive rates<br/>FPR = FP/(FP+TN)<br/>Recall = TP/(TP+FN)<br/>Precision, Specificity]
        P7_1_2 --> P7_1_3[7.1.3 Threshold-independent<br/>ROC AUC, PR AUC, Brier score]
        
        P7_1_3 --> P7_2_0[7.2.0 BusinessImpactCalculator]
        P7_2_0 --> P7_2_1[7.2.1 Implement calculate<br/>Scale to monthly volume<br/>monthly_phishing = 1M × 0.45 = 450K<br/>scale_factor = 450K / (TP+FN)<br/>monthly_FN = FN × scale_factor]
        P7_2_1 --> P7_2_2[7.2.2 Compute costs<br/>fraud_exposure = monthly_FN × $500<br/>support_cost = monthly_FP × $5<br/>total_cost = sum]
        P7_2_2 --> P7_2_3[7.2.3 Implement compare_thresholds<br/>Calculate OLD and NEW<br/>Compute delta savings]
        
        P7_2_3 --> P7_3_0[7.3.0 Create comparison table<br/>Model | ROC AUC | Tuned Recall | Tuned FPR<br/>Business Value column]
        P7_3_0 --> P7_4_0[7.4.0 Interpret confusion matrix<br/>XGBoost @ threshold=0.78:<br/>TN=616, FP=41, FN=258, TP=735<br/>74% recall, 6.2% FPR]
        P7_4_0 --> P7_5_0[7.5.0 Document metrics<br/>Section: Evaluation Metrics Explained<br/>Definition | Why | Business | Limitations]
        P7_5_0 --> P7_6_0{7.6.0 Evaluate test set<br/>ONCE with final model<br/>No further tuning}
        P7_6_0 --> P7_7_0[7.7.0 Create results summary<br/>README section with:<br/>Confusion matrix viz<br/>Metrics table<br/>Business impact<br/>Comparison to original]
    end

    P7_7_0 --> Phase8_Start

    %% ===================================================================
    %% Phase 8: Deployment & Monitoring (1 hour README)
    %% ===================================================================
    subgraph Phase8["Phase 8: Deployment & Monitoring (1 hour README)"]
        Phase8_Start[8.1.0 Document deployment]
        Phase8_Start --> P8_1_1[8.1.1 Client-side architecture<br/>Browser extension, WASM<br/><10ms latency, privacy]
        P8_1_1 --> P8_1_2[8.1.2 Server-side architecture<br/>FastAPI + Kubernetes<br/>p99 <100ms, scalable]
        
        P8_1_2 --> P8_2_0[8.2.0 Monitoring strategy]
        P8_2_0 --> P8_2_1[8.2.1 Layer 1: System Health<br/>Prometheus + Grafana<br/>p99 latency, error rate<br/>Alert: p99>500ms → PagerDuty]
        P8_2_1 --> P8_2_2[8.2.2 Layer 2: Feature Drift<br/>Weekly KL divergence<br/>Alert: KL>0.5 → investigate<br/>Example: LineOfCode 850→1500]
        P8_2_2 --> P8_2_3[8.2.3 Layer 3: Performance<br/>Weekly recall/FPR vs baseline<br/>Recall degrades >5% → retrain<br/>FPR increases >2% → escalate]
        P8_2_3 --> P8_2_4[8.2.4 Layer 4: Business Metrics<br/>Attacks blocked/day<br/>Fraud prevented USD/month<br/>Dashboard with trends]
        
        P8_2_4 --> P8_3_0[8.3.0 Model update strategy]
        P8_3_0 --> P8_3_1[8.3.1 Phase 1: Shadow Mode<br/>0% traffic, log predictions<br/>Compare agreement >95%<br/>Duration: 3 days]
        P8_3_1 --> P8_3_2[8.3.2 Phase 2: Canary<br/>5% traffic to new model<br/>Monitor metrics ≥ v1.0<br/>Duration: 3 days]
        P8_3_2 --> P8_3_3[8.3.3 Phase 3: Gradual Rollout<br/>25→50→100% traffic<br/>Circuit breaker:<br/>error_rate>1% OR FPR>baseline×1.2<br/>→ Auto-rollback]
        
        P8_3_3 --> P8_4_0[8.4.0 Document limitations]
        P8_4_0 --> P8_4_1[8.4.1 Temporal drift<br/>Phishing evolves quarterly<br/>Mitigation: retraining schedule]
        P8_4_1 --> P8_4_2[8.4.2 Adversarial attacks<br/>Feature engineering risk<br/>Mitigation: ensemble + anomaly layer]
        P8_4_2 --> P8_4_3[8.4.3 Missing data<br/>DomainAge lookup fails<br/>Mitigation: graceful degradation]
        
        P8_4_3 --> P8_5_0[8.5.0 Future improvements<br/>1. Online learning<br/>2. Ensemble approach<br/>3. Deep learning on screenshots<br/>4. Graph analysis<br/>5. Explainability layer]
        P8_5_0 --> P8_6_0[8.6.0 Finalize README<br/>Proofread, check links<br/>Verify instructions<br/>All 9 sections complete]
    end

    P8_6_0 --> Phase9_Start

    %% ===================================================================
    %% Phase 9: Final Pre-Interview Checklist (24 hours before)
    %% ===================================================================
    subgraph Phase9["Phase 9: Final Checklist (24 hours before)"]
        Phase9_Start[9.1.0 Code Functionality]
        Phase9_Start --> P9_1_1{9.1.1 bash run.sh<br/>works end-to-end?}
        P9_1_1 -->|✓ Yes| P9_1_2[9.1.2 Data loads<br/>Verify row count]
        P9_1_1 -->|✗ No| P9_Fix[Debug: Check imports,<br/>paths, data file]
        P9_Fix --> P9_1_1
        
        P9_1_2 --> P9_1_3[9.1.3 Preprocessing valid<br/>Verify: split → fit → transform]
        P9_1_3 --> P9_1_4[9.1.4 Training succeeds<br/>3 models in models/]
        P9_1_4 --> P9_1_5[9.1.5 Evaluation complete<br/>results/test_evaluation.json<br/>XGBoost recall ≥70%]
        
        P9_1_5 --> P9_2_0[9.2.0 Documentation]
        P9_2_0 --> P9_2_1[9.2.1 README identity<br/>Name, email present]
        P9_2_1 --> P9_2_2[9.2.2 EDA→MLP table<br/>Finding | Evidence | Decision]
        P9_2_2 --> P9_2_3[9.2.3 Feature table<br/>15+ features with processing]
        P9_2_3 --> P9_2_4[9.2.4 Model comparison<br/>3+ models with metrics]
        P9_2_4 --> P9_2_5[9.2.5 Business impact<br/>$139.5M savings documented]
        
        P9_2_5 --> P9_3_0[9.3.0 Statistical Validation]
        P9_3_0 --> P9_3_1["9.3.1 Class balance test<br/>χ²=110, p&lt;0.001"]
        P9_3_1 --> P9_3_2["9.3.2 MNAR tests<br/>DomainAge χ²=450, p&lt;0.001"]
        P9_3_2 --> P9_3_3[9.3.3 Stratification<br/>All splits p>0.05]
        
        P9_3_3 --> P9_4_0[9.4.0 Threshold Tuning]
        P9_4_0 --> P9_4_1[9.4.1 Config correct<br/>max_fpr: 0.05 ✓]
        P9_4_1 --> P9_4_2[9.4.2 Results achieved<br/>Recall ≥70% ✓]
        P9_4_2 --> P9_4_3[9.4.3 Comparison documented<br/>OLD 12% vs NEW 74%]
        
        P9_4_3 --> P9_5_0[9.5.0 EDA Notebook]
        P9_5_0 --> P9_5_1[9.5.1 Reproducibility<br/>Restart & Run All succeeds]
        P9_5_1 --> P9_5_2[9.5.2 Explanations present<br/>Every viz has interpretation]
        P9_5_2 --> P9_5_3[9.5.3 MNAR test visible<br/>Section 2 chi-square]
        
        P9_5_3 --> P9_6_0[9.6.0 Presentation Prep]
        P9_6_0 --> P9_6_1[9.6.1 Opening scripted<br/>"I made 3 critical mistakes..."]
        P9_6_1 --> P9_6_2[9.6.2 OLD vs NEW ready<br/>Side-by-side comparison]
        P9_6_2 --> P9_6_3[9.6.3 Business impact stated<br/>"$139.5M monthly savings"]
        P9_6_3 --> P9_6_4[9.6.4 Timing checked<br/>Fits in 9:30 with buffer]
        
        P9_6_4 --> P9_7_0[9.7.0 Q&A Prep]
        P9_7_0 --> P9_7_1[9.7.1 Data leakage<br/>Can explain fit vs transform<br/>2-min answer no notes]
        P9_7_1 --> P9_7_2[9.7.2 MNAR explanation<br/>"H₀, contingency, χ²=450..."]
        P9_7_2 --> P9_7_3[9.7.3 Threshold explanation<br/>Cost-benefit $139.5M]
        P9_7_3 --> P9_7_4[9.7.4 Business calculation<br/>scale_factor formula]
        
        P9_7_4 --> P9_8_0[9.8.0 Group Exercise Prep]
        P9_8_0 --> P9_8_1[9.8.1 Mindset: collaborate<br/>Help teammates, share findings]
        P9_8_1 --> P9_8_2[9.8.2 Priority: no leakage<br/>Memorize: split → fit → transform]
        P9_8_2 --> P9_8_3[9.8.3 Template ready<br/>Quick EDA checklist]
        P9_8_3 --> P9_8_4[9.8.4 Speed principle<br/>Simple working > complex broken]
    end

    P9_8_4 --> Success

    Success([🎯 SUCCESS<br/>Ready for Interview<br/><br/>✓ Technical Competence<br/>✓ Professional Communication<br/>✓ Production Thinking<br/>✓ Learning Demonstration])

    %% Critical Path Styling
    style Phase3_Start fill:#ff6b6b,stroke:#c92a2a,stroke-width:4px,color:#fff
    style P3_10_2 fill:#ffd43b,stroke:#f59f00,stroke-width:3px
    style Phase6_Start fill:#ff6b6b,stroke:#c92a2a,stroke-width:4px,color:#fff
    style P6_2_1 fill:#ffd43b,stroke:#f59f00,stroke-width:3px
    style P6_5_3 fill:#51cf66,stroke:#2f9e44,stroke-width:3px
    style P7_6_0 fill:#ffd43b,stroke:#f59f00,stroke-width:3px
    style Success fill:#51cf66,stroke:#2f9e44,stroke-width:4px,color:#fff

    %% Phase Styling
    style Phase0 fill:#e7f5ff,stroke:#339af0,stroke-width:2px
    style Phase1 fill:#f3f0ff,stroke:#7950f2,stroke-width:2px
    style Phase2 fill:#fff3bf,stroke:#f59f00,stroke-width:2px
    style Phase3 fill:#ffe0e0,stroke:#fa5252,stroke-width:3px
    style Phase4 fill:#e7f5ff,stroke:#339af0,stroke-width:2px
    style Phase5 fill:#f3f0ff,stroke:#7950f2,stroke-width:2px
    style Phase6 fill:#ffe0e0,stroke:#fa5252,stroke-width:3px
    style Phase7 fill:#d3f9d8,stroke:#37b24d,stroke-width:2px
    style Phase8 fill:#fff3bf,stroke:#f59f00,stroke-width:2px
    style Phase9 fill:#d3f9d8,stroke:#37b24d,stroke-width:2px
---

# AIAP22 Interview Session: Phase-by-Phase Implementation Guide

**Version**: 1.0  
**Purpose**: Step-by-step implementation roadmap with LOD patterns for zero-experience candidates  
**Format**: Hierarchical tasks (m.n.o) with reasoning, outcomes, and excellent practices  
**Context**: Last-chance interview redemption from failed technical assessment

---

## How to Use This Guide

**Numbering System**:
- **m**: Phase number (0-8)
- **n**: Step number within phase
- **o**: Sub-step number within step (0 = main step)

**Example**: 3.2.1 = Phase 3 (Preprocessing), Step 2 (Feature Engineering), Sub-step 1 (Create MNAR flags)

**Priority Levels**:
- 🔴 **CRITICAL**: Will cause failure if wrong (data leakage, wrong KPI)
- 🟡 **HIGH**: Significantly impacts score (statistical validation, business impact)
- 🟢 **MEDIUM**: Improves professionalism (documentation, organization)
- ⚪ **LOW**: Nice to have (advanced visualizations, extra features)

**Work in Order**: Complete each phase before moving to next. Don't skip steps.

---

## Phase 0: Setup & Data Acquisition (30 minutes)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **0.1.0** | **Download phishing.db to data/ folder** | Data source acquisition, local storage, gitignore compliance | phishing.db in data/ directory, NOT in git repo | ✅ DO: Create data/ folder in repository root, download from provided URL, add data/ to .gitignore<br>❌ DON'T: Upload database to GitHub (violates instructions), hardcode absolute paths | 🟡 |
| **0.2.0** | **Create project structure** | Separation of concerns, module organization, professional layout | Organized repository matching required structure | ✅ DO: Create folders: src/ for code modules, results/ for outputs, tests/ for unit tests. Use descriptive module names: data_loader.py, preprocessing.py, models.py, evaluation.py, business_impact.py, hypothesis_tester.py<br>❌ DON'T: Put all code in one file, use vague names like utils.py or helpers.py | 🟢 |
| 0.2.1 | Create src/ folder | Module organization | Empty src/ directory | ✅ DO: Keep Python modules here, one class per file for clarity | 🟢 |
| 0.2.2 | Create results/ folder | Output artifact storage, audit trail | Empty results/ directory for JSON/CSV outputs | ✅ DO: Store baseline_metrics.json, threshold_sweep.csv, hypothesis_tests.json here<br>❌ DON'T: Commit large output files if >10MB | 🟢 |
| 0.2.3 | Create .gitignore | Prevent accidental uploads | .gitignore with data/, results/, __pycache__, *.pkl | ✅ DO: Add data/, results/, .ipynb_checkpoints, __pycache__, *.pyc, *.pkl, .DS_Store<br>❌ DON'T: Forget data/ entry (will upload database by mistake) | 🟡 |
| **0.3.0** | **Implement data_loader.py** | Database access, schema validation, quality gates | Working DataLoader class that enforces data contracts | ✅ DO: Use sqlite3.connect, implement validation before returning data, raise clear exceptions<br>❌ DON'T: Use pandas.read_csv (wrong tool), skip validation (silent failures) | 🟡 |
| 0.3.1 | Create DataLoader class | Encapsulation, reusability | Class skeleton with __init__ method | ✅ DO: Store expected_schema as class attribute, use type hints<br>❌ DON'T: Use module-level functions (harder to test) | 🟢 |
| 0.3.2 | Implement load_from_sqlite method | Database querying, DataFrame creation | Method that returns DataFrame and ValidationReport | ✅ DO: Connect to SQLite, detect table name automatically via sqlite_master, use pandas.read_sql for query, validate schema before returning, log row count<br>❌ DON'T: Hardcode table name (fragile), return unvalidated data, ignore connection cleanup | 🟡 |
| 0.3.3 | Implement validate_schema method | Data contracts, type safety, defensive programming | Method that checks columns and dtypes, returns ValidationReport | ✅ DO: Assert 46+1 columns exist, check dtype matches (int64, float64, object), return structured dict with is_valid, errors list, columns_found, row_count<br>❌ DON'T: Only check column count (miss type mismatches), print errors instead of returning structured output | 🟡 |
| 0.3.4 | Implement check_row_count method | Sample size adequacy, statistical power | Method that validates minimum 1000 rows | ✅ DO: Check len(df) >= MIN_ROWS (1000), compute confidence interval for test set (±3.6% acceptable), raise DataQualityError if insufficient with clear message: "Only 800 rows, need ≥1000 for reliable 70/15/15 split"<br>❌ DON'T: Accept any dataset size (unreliable metrics), silently return false (no context) | 🟢 |
| 0.3.5 | Implement parse_target_variable method | Label encoding validation, class balance check | Method that validates target column | ✅ DO: Assert unique labels == {0, 1}, compute class counts [legit, phishing], log distribution for imbalance detection, raise ValueError if encoding wrong: "Expected {0,1}, found {-1,1}"<br>❌ DON'T: Assume labels are correct (silent failure if {legit, phish} strings), skip class count (miss imbalance) | 🟢 |
| 0.3.6 | Add Responsibility S-V-O docstrings | Documentation pattern, clear contracts | Every method has Subject-Verb-Object docstring | ✅ DO: "DataLoader loads data and enforces schema contract", "validate_schema checks columns and types against contract", include Parameters, Returns, Raises sections<br>❌ DON'T: Skip docstrings, write vague descriptions like "validates data" | 🟢 |
| **0.4.0** | **Create requirements.txt** | Dependency management, reproducibility | requirements.txt with pinned versions | ✅ DO: Pin versions: pandas==2.0.3, numpy==1.24.3, scikit-learn==1.3.0, xgboost==2.0.0, scipy==1.11.1, matplotlib==3.7.2, seaborn==0.12.2. Use pip freeze > requirements.txt after installing in clean environment<br>❌ DON'T: Omit versions (reproducibility issues), include unnecessary packages, use conda format in pip file | 🟡 |
| **0.5.0** | **Create run.sh** | Pipeline automation, executable script | Bash script that runs entire pipeline | ✅ DO: Start with #!/bin/bash, add set -e to fail on errors, run: python src/main.py, make executable: chmod +x run.sh, test from clean state<br>❌ DON'T: Install dependencies in run.sh (violates instructions), use Windows batch file, hardcode paths | 🟡 |
| **0.6.0** | **Test setup** | Validation before proceeding | Successful pipeline dry run | ✅ DO: Run bash run.sh from repository root, verify no import errors, check data/ folder exists<br>❌ DON'T: Skip testing, proceed with broken setup | 🟢 |

---

## Phase 1: Exploratory Data Analysis (3-4 hours for Task 1)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **1.1.0** | **Create eda.ipynb** | Interactive analysis, presentation format, Task 1 deliverable | Jupyter notebook with proper structure | ✅ DO: Start with markdown cell: title, your name, date, table of contents. Use h1 for phases, h2 for sections, h3 for sub-analyses<br>❌ DON'T: Start coding immediately, use generic notebook name like Untitled.ipynb | 🟢 |
| **1.2.0** | **Section 1: Data Overview** | First look at data, understand structure, identify issues | Comprehensive data summary with statistics | ✅ DO: Display df.shape with interpretation ("11,000 samples, 46 features + 1 target"), df.info() with dtype commentary, df.describe() with observations, show first 5 rows with df.head()<br>❌ DON'T: Just dump outputs without explanation, skip data quality assessment | 🟡 |
| 1.2.1 | Load data using DataLoader | Reuse validation logic, ensure consistency with pipeline | DataFrame loaded with schema validated | ✅ DO: Import from src.data_loader, call load_from_sqlite, display validation report<br>❌ DON'T: Use pandas.read_sql directly (bypass validation), load different way than pipeline | 🟡 |
| 1.2.2 | Compute and display target distribution | Class balance understanding, baseline metrics | Bar chart + percentages showing 55% legit, 45% phishing | ✅ DO: Use value_counts(normalize=True), create bar chart with percentages annotated, add text: "55% legitimate (6050), 45% phishing (4950). Mild imbalance—not severe but requires stratified splits and class weights."<br>❌ DON'T: Show only counts without percentages, ignore implications for modeling | 🟡 |
| 1.2.3 | State baseline accuracy | Naive predictor benchmark, metric sanity check | Baseline accuracy = 55% documented | ✅ DO: Explain: "If we always predict 'legitimate', we'd achieve 55% accuracy. This immediately shows accuracy is misleading for this problem—we need to focus on recall (catching phishing attacks) and confusion matrix breakdown."<br>❌ DON'T: Skip this insight, treat 55% as low when it's actually the naive baseline | 🟢 |
| **1.3.0** | **Section 2: Missing Value Analysis** | Data quality assessment, MNAR detection, imputation strategy | Complete missing value report with statistical tests | ✅ DO: Create heatmap showing missingness pattern, compute rates per column, categorize: severe (>70%), moderate (20-70%), low (<20%), perform MNAR chi-square test for high-missing features<br>❌ DON'T: Only show missing counts, ignore patterns, skip statistical tests | 🔴 |
| 1.3.1 | Compute missing rates per column | Quantify data quality issues | Table/DataFrame showing feature, missing_count, missing_pct | ✅ DO: Use df.isnull().sum() and divide by len(df), sort by missing_pct descending, highlight DomainAgeMonths 68%, Robots 12%, IsResponsive 8%<br>❌ DON'T: Show only features with missing values (lose context of complete features) | 🟡 |
| 1.3.2 | Create missing value heatmap | Visual pattern recognition | Heatmap showing missing data pattern by row | ✅ DO: Use seaborn.heatmap on df.isnull(), cmap='viridis', add interpretation: "Missingness not randomly distributed—clusters in phishing class suggest MNAR"<br>❌ DON'T: Use unclear colors, skip axis labels, no interpretation | 🟢 |
| 1.3.3 | Categorize features by missing severity | Prioritize which features need special handling | Three lists: severe[], moderate[], low[] | ✅ DO: Severe: DomainAgeMonths (68%), Moderate: Robots (12%), IsResponsive (8%), Low: all others. Document decision: severe features get MNAR test + missing flags<br>❌ DON'T: Treat all missing equally, no categorization | 🟡 |
| 1.3.4 | Perform MNAR test for DomainAgeMonths | Statistical validation of missingness pattern | Chi-square test result proving MNAR | ✅ DO: Create contingency table: rows=is_missing (True/False), columns=target (0/1). Compute missingness rate by class: legit 45%, phishing 68%. Run chi-square independence test: χ²=450, p<0.001. Interpret: "p<0.001 means <0.1% chance this pattern is random. Reject H₀ (independence) → MNAR confirmed. Phishing sites intentionally hide domain age."<br>❌ DON'T: Skip statistical test, just eyeball pattern, no interpretation | 🔴 |
| 1.3.5 | Document imputation strategy per feature | Plan preprocessing, justify choices | Table: feature, missing_%, strategy, reason | ✅ DO: DomainAgeMonths: Create missing flag (MNAR signal) + median impute (24 months), Robots: Create missing flag + mode impute, Numeric features: median (robust to outliers), Categorical: mode with fallback to 'unknown'<br>❌ DON'T: Use mean imputation (sensitive to outliers), drop rows with missing (lose 68% of data), no justification | 🟡 |
| **1.4.0** | **Section 3: Univariate Analysis** | Per-feature distribution understanding, preprocessing needs | Complete statistical profile of each feature | ✅ DO: For each numeric: histogram, skewness, outlier count (IQR method), transformation needs. For each categorical: bar chart, value counts, cardinality. Document preprocessing decisions per feature<br>❌ DON'T: Only visualize, no statistics, skip transformation planning | 🟡 |
| 1.4.1 | Analyze numeric features: compute skewness | Distribution shape assessment, normality check | Table with feature, skewness, severity, requires_transform | ✅ DO: Compute df[col].skew() for all numeric, categorize: severe (abs>2), moderate (abs>1), low (abs<1). Find 10 features with abs skew >2. Document: "LineOfCode skew=3.2 (heavy right tail) → requires log-transform + clipping"<br>❌ DON'T: Ignore skewness, assume normality, no categorization | 🟡 |
| 1.4.2 | Detect outliers via IQR method | Extreme value identification, clipping strategy | Outlier counts and bounds per feature | ✅ DO: For each numeric: Q1 = 25th percentile, Q3 = 75th, IQR = Q3-Q1, lower_bound = Q1-1.5×IQR, upper_bound = Q3+1.5×IQR. Count outliers outside bounds. Example: LineOfCode Q1=500, Q3=1500, IQR=1000 → bounds=[-1000, 3000], 42 outliers (3.8%). Decision: Clip at 99th percentile (2500) then log-transform<br>❌ DON'T: Use Z-score method (assumes normality), arbitrary cutoffs, no justification | 🟢 |
| 1.4.3 | Create histograms for numeric features | Distribution visualization | Grid of histograms showing skewness and outliers | ✅ DO: Use plt.subplots for grid layout, add vertical lines for Q1/median/Q3, annotate skewness value, overlay normal distribution for comparison, explain: "LineOfCode heavily right-skewed (most sites 500-2000 lines, outliers to 50K)"<br>❌ DON'T: Default matplotlib with no annotations, separate plots (loses comparison), no interpretation | 🟢 |
| 1.4.4 | Analyze categorical features | Category distribution, cardinality assessment | Bar charts with value counts for Industry, HostingProvider | ✅ DO: For Industry: 8 unique values, relatively balanced. For HostingProvider: 15 unique values, some rare (<1%). Decision: One-hot encode both, handle rare values via frequency threshold or grouping<br>❌ DON'T: Ignore cardinality (high cardinality = dimensionality explosion), skip rare value handling | 🟢 |
| 1.4.5 | Document preprocessing needs per feature | Explicit transformation plan | Table: feature, issue, transformation, reason | ✅ DO: LineOfCode: skew=3.2, outliers → clip at 99th percentile then log1p → reduces skew to 0.4. NoOfImage: skew=2.8 → same. DomainAgeMonths: 68% missing, MNAR → create missing flag + median impute<br>❌ DON'T: Generic "normalize all features", no feature-specific rationale | 🟡 |
| **1.5.0** | **Section 4: Bivariate Analysis** | Feature-target relationships, feature importance, correlation | Statistical evidence for feature selection | ✅ DO: Compute correlation with target, perform t-tests for numeric features, chi-square for categorical, identify top predictors, check multicollinearity, validate feature interactions<br>❌ DON'T: Skip statistical tests, rely only on correlation, ignore interactions | 🟡 |
| 1.5.1 | Compute correlation matrix | Linear relationships, multicollinearity detection | Heatmap showing pairwise correlations | ✅ DO: Use df.corr(), create seaborn heatmap with annotations, highlight correlations with target, identify high correlations (abs r >0.95) between features for multicollinearity check. Find max inter-feature correlation = 0.94 (NoOfImage × NoOfiFrame) → keep both as <0.95 threshold<br>❌ DON'T: Show full matrix without focusing on target column, no multicollinearity assessment | 🟡 |
| 1.5.2 | Rank features by correlation with target | Feature importance indication | Sorted list of features by abs correlation | ✅ DO: Extract df.corr()['label'].sort_values(), identify top 5: ExternalSelfRatio (0.42), NoOfPopup (0.38), DomainAgeMonths (-0.31), NoOfExternalRef (0.29), LineOfCode (0.24). Note limitation: "Pearson correlation only captures linear relationships—tree models may find non-linear patterns"<br>❌ DON'T: Only show correlation values without ranking, no interpretation of signs (negative = lower in phishing) | 🟡 |
| 1.5.3 | Perform t-tests for top numeric features | Statistical significance validation | T-test results with p-values and effect sizes | ✅ DO: For ExternalSelfRatio: phishing mean=8.3, legit mean=2.1, independent samples t-test: t=12.4, p<0.001, Cohen's d=0.8 (large effect). Interpret: "Phishing sites have significantly more external links relative to self-links. Effect size large → strong predictor."<br>❌ DON'T: Only report p-values without effect size (significance ≠ importance), skip interpretation | 🟡 |
| 1.5.4 | Create scatter plots: top features vs target | Visual relationship confirmation | Scatter plots with trend lines or box plots by class | ✅ DO: For continuous features: scatter with target jitter + transparency, add trend line. For discrete: box plots by class. Example: ExternalSelfRatio box plot shows phishing median=8.3, legit=2.1, clear separation, some overlap in middle range<br>❌ DON'T: Scatter plot raw binary target (unreadable), no class separation visualization | 🟢 |
| 1.5.5 | Test categorical features with chi-square | Independence testing for categoricals | Chi-square test results for Industry, HostingProvider | ✅ DO: Create contingency tables: Industry × target, HostingProvider × target. Chi-square tests: Industry χ²=87, p<0.001, Cramér's V=0.28 (moderate association). HostingProvider χ²=124, p<0.001, V=0.33. Interpret: "Both categorical features significantly associated with target, worth keeping"<br>❌ DON'T: Skip categorical testing (assume only numeric matter), no effect size measure | 🟢 |
| **1.6.0** | **Section 5: Multivariate Patterns** | Feature interactions, dimensionality insights, model selection hints | Understanding of feature space structure | ✅ DO: PCA visualization (2D projection), identify feature groups, check for non-linear patterns, interpret variance explained, connect findings to model choice<br>❌ DON'T: Skip entirely (miss interaction opportunities), no interpretation of projections | 🟢 |
| 1.6.1 | Perform PCA dimensionality reduction | High-dimensional visualization, variance analysis | 2D scatter plot of first 2 principal components | ✅ DO: Standardize features first (critical for PCA), fit PCA with 2 components, scatter plot colored by target class. Compute variance explained: PC1=23%, PC2=12%, total=35%. Interpret: "Partial separation visible between classes—phishing cluster in high external links + low domain age region. Full separation requires more dimensions → suggests complex decision boundary → tree models may outperform linear"<br>❌ DON'T: Apply PCA without scaling (dominated by high-variance features), no variance explained reporting | 🟢 |
| 1.6.2 | Identify potential feature interactions | Non-linear pattern detection | List of feature pairs with suspected interactions | ✅ DO: Look for patterns where combination matters more than individual features. Example: "High NoOfExternalRef AND low DomainAgeMonths strongly indicates phishing (t-test p<0.001), but either alone is weaker. This suggests XGBoost (captures interactions) will outperform Logistic (additive only)."<br>❌ DON'T: Assume features are independent, no interaction hypothesis | 🟢 |
| **1.7.0** | **Section 6: Key Findings Summary** | Synthesize insights, create EDA→MLP mapping, justify pipeline decisions | Complete table connecting every EDA finding to pipeline action | ✅ DO: Create comprehensive table with columns: EDA Finding, Statistical Evidence, Pipeline Decision, Expected Impact, FAQ Link. Cover all major decisions: MNAR flags, log-transforms, stratified splits, model choice, threshold tuning<br>❌ DON'T: Vague summaries with no evidence, disconnect EDA from pipeline, no statistical backing | 🔴 |
| 1.7.1 | Create EDA→MLP mapping table | Explicit decision justification | Table showing finding → evidence → decision chain | ✅ DO: Row 1: "DomainAge 68% missing concentrated in phishing | χ²=450, p<0.001 (MNAR) | Create DomainAge_missing binary flag | Ablation study: +7% recall". Row 2: "10 features with abs skew >2 | Median skew=1.8 | Clip at 99th percentile + log1p transform | Reduces median skew to 0.4". Continue for 8-10 major findings<br>❌ DON'T: Generic statements like "cleaned data", no evidence column, no impact quantification | 🔴 |
| 1.7.2 | State hypothesis for model selection | Predict which models will work best | Written hypothesis based on EDA observations | ✅ DO: "Hypothesis: XGBoost will outperform Logistic Regression because: (1) PCA shows non-linear separation suggesting complex decision boundary, (2) Feature interactions detected (external links × domain age), (3) Tree models naturally handle skewed distributions without transforms. Predict XGBoost achieves 72-75% recall vs Logistic 68-71%."<br>❌ DON'T: Skip hypothesis, no prediction, no reasoning | 🟢 |
| 1.7.3 | Document statistical validation plan | Preview Phase 2 work | List of hypothesis tests to perform | ✅ DO: Plan to run: (1) Class balance significance (chi-square), (2) MNAR tests for high-missing features, (3) Stratification validation post-split, (4) Feature importance validation. Note: "All tests use α=0.05 significance level"<br>❌ DON'T: No testing plan, proceed without validation strategy | 🟡 |
| **1.8.0** | **Polish and finalize eda.ipynb** | Professional presentation, clear narrative, easy to follow | Publication-ready notebook | ✅ DO: Run "Restart Kernel and Run All Cells" to verify reproducibility, add markdown cell transitions between sections explaining flow, proofread all text for typos/grammar, ensure every visualization has interpretation paragraph, add final conclusion section summarizing key takeaways<br>❌ DON'T: Submit with cells out of order, missing explanations, broken outputs, no narrative flow | 🟢 |

---

## Phase 2: Statistical Hypothesis Testing (1-2 hours, integrate into Task 1 & 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **2.1.0** | **Create hypothesis_tester.py module** | Statistical rigor, automated validation, audit trail | HypothesisTester class with test methods | ✅ DO: Class-based design for state management, each test returns structured dict with chi2, p_value, reject_h0, interpretation. Store alpha=0.05 as instance variable. Implement save_results method for JSON export<br>❌ DON'T: Module-level functions (harder to maintain state), print results instead of returning, no persistence | 🟡 |
| **2.2.0** | **Test 1: Class Balance Significance** | Validate imbalance is real, not sampling noise | Chi-square test confirming 55:45 imbalance is significant | ✅ DO: H₀: P(phishing)=0.5 (50-50 balance). Observed=[6050, 4950], expected=[5500, 5500]. scipy.stats.chisquare computes χ²=110, p<0.001. Interpret: "p<0.001 → <0.1% chance this is random → reject H₀ → imbalance is statistically significant. Pipeline impact: (1) Use stratified splits to preserve ratio, (2) Set XGBoost scale_pos_weight=1.22 (6050/4950), (3) Prioritize recall over accuracy."<br>❌ DON'T: Skip test and assume imbalance matters, no interpretation of p-value, ignore pipeline implications | 🟡 |
| 2.2.1 | Implement test_class_balance_significance method | Automate chi-square test for imbalance | Method returning TestResult dict | ✅ DO: Accept y array and null_prob parameter, compute observed counts via np.bincount, compute expected as null_prob × len(y), run chi-square, return {test: 'class_balance', h0, observed_counts, observed_proportions, chi2, p_value, reject_h0, conclusion}<br>❌ DON'T: Hardcode null_prob (should be parameter), return only p-value (lose context) | 🟡 |
| 2.2.2 | Add to eda.ipynb Section 1 | Show test results in presentation | Markdown + printed test result | ✅ DO: Import HypothesisTester, run test, display results in formatted table, add interpretation: "This proves imbalance requires special handling—not optional"<br>❌ DON'T: Only mention test in passing, no visual result | 🟢 |
| **2.3.0** | **Test 2: MNAR Hypothesis for DomainAge** | Validate missingness depends on target | Chi-square independence test proving MNAR | ✅ DO: H₀: Missingness independent of target. Create contingency: rows=is_missing (True/False), cols=target (0/1). Observed: [[2850, 3200], [3550, 1400]] showing 45% missing in legit, 68% in phishing. Chi-square independence test via scipy.stats.chi2_contingency → χ²=450, p<0.001 → reject H₀ → MNAR. Interpret: "Missingness pattern is NOT random—phishing sites systematically hide domain age. This justifies creating DomainAge_missing binary flag to capture this intentional hiding signal."<br>❌ DON'T: Only compute missing rates without testing, assume MNAR without evidence, skip interpretation | 🔴 |
| 2.3.1 | Implement test_mnar_hypothesis method | Automate MNAR testing | Method accepting df, col, target_col, returning MNARResult | ✅ DO: Create is_missing column via df[col].isna(), build contingency table with pd.crosstab(is_missing, target), run chi2_contingency, compute missingness rate by class via groupby, return {test: 'mnar_independence', feature, h0, contingency_table, missingness_rate_by_class, chi2, p_value, reject_h0, conclusion: 'MNAR' if p<0.05 else 'MAR/MCAR'}<br>❌ DON'T: Only test one feature (should be reusable), no contingency table in output, unclear conclusion | 🔴 |
| 2.3.2 | Test DomainAge, Robots, IsResponsive | Apply to all high-missing features | MNAR status for each feature | ✅ DO: Run test_mnar_hypothesis for each, collect results. DomainAge: MNAR (p<0.001), Robots: borderline (p=0.04), IsResponsive: MAR (p=0.12). Decision: Create flags for DomainAge and Robots<br>❌ DON'T: Only test DomainAge, skip borderline cases | 🟡 |
| 2.3.3 | Add to eda.ipynb Section 2 | Document MNAR findings | Table showing feature, χ², p-value, conclusion | ✅ DO: Present results in formatted table, show contingency tables for MNAR features, explain: "This statistical evidence justifies missing flags—not arbitrary feature engineering"<br>❌ DON'T: Relegate to appendix, skip visual presentation | 🔴 |
| **2.4.0** | **Test 3: Stratification Validation (in pipeline)** | Verify splits preserve class distribution | Chi-square tests confirming valid stratification | ✅ DO: After stratified_split in pipeline, test each split vs full distribution. H₀: Split distribution matches full. For train: observed=[4235, 3115], expected from full distribution scaled by split size. Chi-square test: χ²=2.94, p=0.086 >0.05 → cannot reject H₀ → stratification valid. Repeat for val (p=0.76) and test (p=0.82). All p>0.05 confirms success.<br>❌ DON'T: Visually check proportions without statistical test, assume stratify parameter worked | 🟡 |
| 2.4.1 | Implement validate_stratified_splits method | Automate split validation | Method testing all splits, returning StratificationReport | ✅ DO: Accept y_full and splits_dict mapping split_name to y_split, compute full_dist as proportions, for each split: compute expected counts as full_dist × len(split), run chi-square, collect results: {split_name: {chi2, p_value, is_stratified: p>alpha, observed_pct, expected_pct}}<br>❌ DON'T: Only test train split, no expected counts shown, binary pass/fail without p-values | 🟡 |
| 2.4.2 | Integrate into pipeline validation | Call after splitting | Validation report in results/hypothesis_tests.json | ✅ DO: In main pipeline, after split, call validate_stratified_splits, log results, raise warning if any p<0.05<br>❌ DON'T: Skip in automated runs, only manual checking | 🟢 |
| **2.5.0** | **Save all test results** | Create audit trail, enable CI/CD gates | results/hypothesis_tests.json with all tests | ✅ DO: HypothesisTester.save_results writes comprehensive JSON: {test_name: {h0, chi2, p_value, reject_h0, timestamp, interpretation}}. Include metadata: alpha level, date run, data hash for reproducibility. This enables: (1) Reproducibility (same data → same p-values), (2) CI/CD gates (pipeline fails if p-values unexpected), (3) Regulatory audit trail<br>❌ DON'T: Only print to console (ephemeral), save as text file (harder to parse), no metadata | 🟡 |
| **2.6.0** | **Document in README** | Explain statistical rigor to interviewers | Section "Statistical Validation" in README | ✅ DO: Create table: Test Name, H₀, Test Statistic, p-value, Conclusion, Pipeline Impact. Example row: "Class Balance Significance | P(phishing)=0.5 | χ²=110 | p<0.001 | Reject H₀: Imbalance significant | Use stratified splits + scale_pos_weight". Explain: "All decisions backed by hypothesis tests at α=0.05 significance level"<br>❌ DON'T: Bury in appendix, no table format, skip impact column | 🟡 |

---

## Phase 3: Feature Engineering & Preprocessing (2-3 hours for Task 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **3.1.0** | **CRITICAL: Understand SPLIT FIRST paradigm** | Prevent data leakage, maintain train/test independence | Mental model: never let test influence preprocessing | ✅ DO: Memorize flow: Load → Split → FeatureEngineer.fit(train) → transform(all) → Preprocessor.fit(train) → transform(all). Key insight: fit methods ONLY see training data. Transform methods apply LEARNED parameters to any data without recomputing<br>❌ DON'T: Preprocess full dataset then split (DATA LEAKAGE), call fit on validation/test sets, think "normalize all data" | 🔴 |
| **3.2.0** | **Create preprocessing.py with FeatureEngineer class** | Domain-driven feature creation, parameter learning separation | FeatureEngineer class with fit/transform methods | ✅ DO: Class stores learned parameters (quantile_bins, freq_maps) in __init__ without data. fit method learns from train only, returns self for chaining. transform method applies stored parameters to any DataFrame. No computation in transform—only lookup and apply<br>❌ DON'T: Compute statistics in transform (recomputes on test), store training data (memory waste), no fit method | 🔴 |
| 3.2.1 | Implement __init__ method | Initialize parameter storage | Empty containers for learned parameters | ✅ DO: Set enable_flags, enable_bins, enable_ratios as boolean config options. Initialize self.quantile_bins=None, self.freq_maps=None. Will be populated in fit<br>❌ DON'T: Initialize with default values (should learn from data), accept DataFrame in init | 🟢 |
| 3.2.2 | Implement fit method for parameter learning | Learn engineering rules from training data | Method that learns and stores quantile bins, frequency maps | ✅ DO: Accept df_train only. If enable_bins: compute self.quantile_bins = {col: df_train[col].quantile([0.25,0.5,0.75])} for numeric cols. If enable_frequency_encoding: compute self.freq_maps = {col: value_counts/len(df_train)} for categoricals. Return self for method chaining. Store NO actual data, only statistics<br>❌ DON'T: Accept df_all parameter (enables leakage), store df_train (memory waste), compute stats but don't store | 🔴 |
| 3.2.3 | Implement transform method for feature creation | Apply learned rules to any data | Method that transforms DataFrame using stored parameters | ✅ DO: Accept df (can be train/val/test/prod). If enable_flags: create missing flags via create_missing_flags helper. If enable_bins: apply stored quantile_bins via pd.cut. If enable_ratios: create ExternalSelfRatio. Return df_out with new columns. Never recompute statistics—only use self.quantile_bins etc<br>❌ DON'T: Recompute quantiles on df input (DATA LEAKAGE), modify df in place (side effects), return different schema than learned | 🔴 |
| **3.3.0** | **Implement MNAR flag creation** | Capture predictive missingness signal | Helper method creating binary indicators | ✅ DO: create_missing_flags(df) creates columns: DomainAge_missing = df['DomainAgeMonths'].isna().astype(int), Robots_missing same, IsResponsive_missing same. Returns df with new columns. Rationale: "MNAR test showed χ²=450, p<0.001 → missingness itself is predictive signal. Ablation validation: removing flag drops recall 7%"<br>❌ DON'T: Skip flags because "it's just missing data", create for all features (only MNAR ones), forget to convert bool to int | 🔴 |
| **3.4.0** | **Implement domain-specific ratio feature** | Encode phishing behavior pattern | ExternalSelfRatio feature creation | ✅ DO: create_external_self_ratio(df) creates df['ExternalSelfRatio'] = df['NoOfExternalRef'] / (df['NoOfSelfRef'] + 1). +1 prevents division by zero, preserves extreme cases (e.g., 50/2=25 shows strong phishing pattern). Justification from EDA: "Phishing median=8.3 vs legit=2.1, t-test p<0.001, Cohen's d=0.8 (large effect). Feature importance: rank #3 in XGBoost"<br>❌ DON'T: Use Ext/(Ext+Self) which saturates at 1.0 and loses dynamic range, skip +1 in denominator (crashes on zero), no justification | 🟡 |
| **3.5.0** | **Create Preprocessor class** | Scaling, imputation, encoding with leakage prevention | Preprocessor with fit/transform methods | ✅ DO: Separate from FeatureEngineer for modularity. Preprocessor handles: log-clipping, imputation, one-hot encoding, column alignment, scaling. All via fit/transform pattern. Stores clip_values_, imputers_, scaler_params_, columns_ as learned parameters<br>❌ DON'T: Combine with FeatureEngineer (violates separation of concerns), use sklearn Pipeline (less control for this assessment) | 🔴 |
| 3.5.1 | Implement __init__ with configuration | Set preprocessing options | Instance with clip_quantile, impute_strategy, scale_method | ✅ DO: Accept clip_quantile=0.99, impute_strategy='median', scale_method='standard' as parameters. Initialize learned parameter containers as None. Document in docstring what each parameter controls<br>❌ DON'T: Hardcode configuration (reduces flexibility), use class variables (shared across instances) | 🟢 |
| 3.5.2 | Implement fit_transform for training data | Learn all preprocessing parameters and apply | Method that fits and transforms training data | ✅ DO: Accept df_train, extract y_train = df_train['label'], work on features. Sequence: (1) Learn clip values: self.clip_values = df_train.quantile(0.99) per numeric col, (2) Apply log-clip: df = _log_clip(df, self.clip_values), (3) Learn imputers: self.imputers = {numeric: median, categorical: mode}, (4) Apply imputation, (5) One-hot encode categoricals, (6) Store self.columns = df.columns, (7) Learn scaler: self.scaler_params = {mean, std}, (8) Apply scaling. Return X_train_scaled, y_train<br>❌ DON'T: Skip storing parameters (breaks transform), apply transforms in wrong order (clip after log crashes), no column storage (fails on test) | 🔴 |
| 3.5.3 | Implement transform for validation/test data | Apply learned parameters without refitting | Method that transforms new data consistently | ✅ DO: Accept df_new, extract y_new, apply SAME sequence as fit_transform but use STORED parameters: (1) Clip using self.clip_values, (2) Log-transform, (3) Impute using self.imputers, (4) One-hot encode, (5) Align columns: df.reindex(columns=self.columns_, fill_value=0), (6) Scale using self.scaler_params. Return X_new_scaled, y_new. NEVER recompute statistics<br>❌ DON'T: Call fit again (DATA LEAKAGE), compute new statistics, skip column alignment (shape mismatch errors) | 🔴 |
| **3.6.0** | **Implement log-clipping helper** | Handle skewness and outliers | _log_clip private method | ✅ DO: _log_clip(df, clip_values) iterates numeric columns, clips: df[col] = np.clip(df[col], 0, clip_values[col]), then log-transforms: df[col] = np.log1p(df[col]). Returns transformed df. Rationale: "Clipping at 99th percentile (train-learned) removes extreme outliers that dominate variance. log1p reduces skewness (median |skew| 1.8→0.4) and stabilizes variance for linear models"<br>❌ DON'T: Clip at fixed value (should be train-learned), use log instead of log1p (crashes on zero), clip after log (wrong order) | 🟡 |
| **3.7.0** | **Implement imputation helper** | Fill missing values robustly | _impute private method | ✅ DO: _impute(df, imputers) fills df.fillna(imputers['numeric']) for numeric columns (median), df.fillna(imputers['categorical']) for categorical (mode with fallback to 'unknown' if all missing). Rationale: "Median robust to outliers (vs mean), mode most common category, fallback prevents errors on all-missing"<br>❌ DON'T: Use mean (outlier-sensitive), drop rows (lose data), forward-fill (inappropriate for tabular), no fallback | 🟢 |
| **3.8.0** | **Implement encoding with column alignment** | Handle categorical variables, ensure schema consistency | One-hot encoding with reindex for unseen categories | ✅ DO: Use pd.get_dummies(df, columns=categorical_cols). In fit_transform: store self.columns_ = df.columns.tolist(). In transform: after get_dummies, call df.reindex(columns=self.columns_, fill_value=0). This handles: val/test has new category → creates column with zeros, drops after reindex. Val/test missing a category from train → reindex adds column with zeros. Ensures consistent shape<br>❌ DON'T: No column alignment (shape mismatch on unseen categories), use LabelEncoder for non-ordinal categoricals, drop_first for tree models (XGBoost handles collinearity) | 🔴 |
| **3.9.0** | **Implement scaling helper** | Standardize features for distance-based models | _scale private method | ✅ DO: _scale(df, scaler_params, method='standard') applies (df - scaler_params['mean']) / scaler_params['std'] if standard. Returns ndarray ready for model. Rationale: "Standardization gives equal weighting in distance metrics (critical for KNN). Logistic: improves gradient stability. XGBoost: doesn't need scaling but doesn't hurt"<br>❌ DON'T: Recompute mean/std in transform (LEAKAGE), use MinMaxScaler without justification, skip for all models (KNN needs it) | 🟡 |
| **3.10.0** | **Implement main.py orchestration** | Control preprocessing flow correctly | Script that runs split → fit → transform sequence | ✅ DO: Load data, SPLIT FIRST via stratified_split, create FeatureEngineer and fit on df_train, transform train/val/test, create Preprocessor and fit_transform on train, transform val/test. Save preprocessor.pkl for inference. Log each step. This is THE critical flow—test thoroughly<br>❌ DON'T: Preprocess before split (LEAKAGE), fit on val/test, skip saving preprocessor (can't reproduce) | 🔴 |
| **3.11.0** | **Add extensive docstrings** | Document Responsibility S-V-O pattern | Every method has Subject-Verb-Object docstring | ✅ DO: "FeatureEngineer learns quantile bins and frequency maps from training data", "Preprocessor transforms features via learned scaling parameters", "transform applies learned parameters to new data without refitting". Include Parameters, Returns, Raises, Example sections<br>❌ DON'T: Generic docstrings like "processes data", no examples, skip Raises section | 🟢 |
| **3.12.0** | **Validate preprocessing output** | Ensure no data quality issues remain | Assertions checking preprocessed data | ✅ DO: After preprocessing, assert: (1) No missing values: not X_train.isna().any().any(), (2) No infinities: not np.isinf(X_train).any(), (3) Shape preserved: X_train.shape[0] == len(df_train), (4) Consistent columns: X_val.shape[1] == X_train.shape[1]. Log validation to results/preprocessing_validation.json<br>❌ DON'T: Skip validation (silent errors), only visual inspection, no automated checks | 🟡 |

---

## Phase 4: Data Splitting & Validation (30 minutes for Task 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **4.1.0** | **Create data_splitter.py module** | Stratified splitting, reproducibility, statistical validation | stratified_split function with chi-square validation | ✅ DO: Module-level function acceptable here (no state to manage). Accept df, test_size, val_size, random_state as parameters. Return tuple of DataFrames. Use numpy.random with seed for reproducibility<br>❌ DON'T: Use sklearn without understanding internals, random split without stratification, no random seed | 🟡 |
| **4.2.0** | **Implement stratified_split function** | Preserve class distribution across splits | Function that splits data class-proportionally | ✅ DO: Algorithm: (1) Extract y = df['label'].values, get unique_classes, (2) For each class: get indices where y==class, shuffle with rng, (3) Compute split sizes: n_test = int(n_class × test_size), n_val similar, n_train = remainder, (4) Partition indices: test_indices = shuffled[:n_test], val_indices = shuffled[n_test:n_test+n_val], train_indices = shuffled[n_test+n_val:], (5) Combine across classes, return df.iloc[indices]. Rationale: "Per-class splitting preserves 55:45 ratio in all splits—prevents train 80% legit, test 40% legit (unrepresentative)"<br>❌ DON'T: Use sklearn.train_test_split with stratify (acceptable but shows less understanding), random split (breaks class balance), no shuffling (temporal patterns) | 🟡 |
| 4.2.1 | Set random seed for reproducibility | Enable exact replication | Same splits every run | ✅ DO: Accept random_state=42 parameter, use np.random.default_rng(random_state) for modern numpy, seed at start of function. Document: "random_state=42 ensures reproducibility—same data always splits same way. Critical for debugging, comparing models fairly, audit trail"<br>❌ DON'T: No seed (different results each run), hardcode seed (inflexible), use legacy np.random.seed | 🟡 |
| 4.2.2 | Verify split sizes are reasonable | Ensure adequate samples per split | Print split sizes and percentages | ✅ DO: Log: "Train: 7350 samples (66.8%), Val: 1650 (15.0%), Test: 1650 (15.0%)". Check test set has ≥150 samples per class for adequate CI precision<br>❌ DON'T: Silent splitting, ignore small splits, no size logging | 🟢 |
| **4.3.0** | **Create pipeline_validator.py module** | Post-split quality assurance, automated gates | validate_processed and validate_stratification functions | ✅ DO: Two functions: (1) validate_processed checks data quality (no missing, correct shapes), (2) validate_stratification performs chi-square tests. Both return structured ValidationReport dicts<br>❌ DON'T: Skip validation entirely, only visual checks, no structured output | 🟡 |
| **4.4.0** | **Implement validate_stratification function** | Statistical proof splits are stratified | Chi-square tests confirming valid stratification | ✅ DO: Accept y_full and dict mapping split_name to y_split. Compute full_dist = np.bincount(y_full) / len(y_full) as proportions. For each split: (1) observed = np.bincount(y_split), (2) expected = full_dist × len(y_split), (3) chi2, p_value = scipy.stats.chisquare(observed, expected), (4) is_stratified = p_value > 0.05. Return {split_name: {chi2, p_value, is_stratified, observed_pct, expected_pct}}. Interpretation: "Train p=0.08 >0.05 → cannot reject H₀ that split matches full distribution → stratification valid"<br>❌ DON'T: Only check proportions visually, no statistical test, binary pass/fail without p-values | 🟡 |
| 4.4.1 | Test all three splits | Comprehensive validation | Chi-square results for train, val, test | ✅ DO: Call with splits_dict = {'train': y_train, 'val': y_val, 'test': y_test}. Expect all p>0.05. If any p<0.05, log warning but don't necessarily fail (might be small sample variation)<br>❌ DON'T: Only test train, skip val/test, fail pipeline on borderline p-values like 0.04 | 🟡 |
| 4.4.2 | Save validation results | Audit trail for statistical validation | results/stratification_validation.json | ✅ DO: Write comprehensive JSON with all chi-square results, p-values, interpretation. Include metadata: date run, random_state used, full distribution. Enables reproducibility and audit<br>❌ DON'T: Only print to console, no persistence, missing metadata | 🟢 |
| **4.5.0** | **Implement validate_processed function** | Final quality check before training | Validation of preprocessed data quality | ✅ DO: Accept X_train, X_val, X_test, y_train, y_val, y_test. Check: (1) No missing: assert not X_train.isna().any().any() for all splits, (2) No infinities: assert not np.isinf(X_train).any(), (3) Label proportions: compute per split, (4) Call validate_stratification on labels, (5) Sample size adequacy: test set ≥150 samples per class. Return ValidationReport {no_missing, no_infinities, label_proportions, stratification, sample_sizes}<br>❌ DON'T: Skip checks, assume preprocessing worked, no structured output | 🟡 |
| **4.6.0** | **Compute confidence interval for test set** | Assess metric precision, validate sample size | CI calculation showing ±3.6% for 742 phishing samples | ✅ DO: Compute: n_test_phishing = test_size × phishing_rate = 1650 × 0.45 = 742. For recall estimate p=0.70, CI = ±1.96 × sqrt(p(1-p)/n) = ±1.96 × sqrt(0.7×0.3/742) = ±0.036 = ±3.6%. Interpret: "70% recall has 95% CI [66.4%, 73.6%]. This precision is acceptable for business decisions. If test set were only 150 samples (67 phishing) → CI ±12% (too wide)"<br>❌ DON'T: Skip CI calculation, no interpretation, don't validate sample size adequacy | 🟢 |
| **4.7.0** | **Integrate validation into main pipeline** | Automated quality gates | Validation runs after preprocessing | ✅ DO: In main.py, after preprocessing, call validate_processed and log results. If any check fails, raise ValidationError with clear message. Save to results/preprocessing_validation.json<br>❌ DON'T: Manual validation only, skip in automated runs, silent failures | 🟡 |

---

## Phase 5: Model Training & Selection (2-3 hours for Task 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **5.1.0** | **Create models.py module** | Model implementations, consistent interfaces | Three model classes with fit/predict_proba methods | ✅ DO: Class per model: LogisticRegressionModel, KNNModel, XGBoostModel. Each has: (1) __init__ with hyperparameters, (2) fit(X_train, y_train) returning self, (3) predict_proba(X) returning (n, 2) array. Document Responsibility S-V-O for each: "LogisticRegressionModel trains via gradient descent with L2 regularization"<br>❌ DON'T: Use sklearn directly without wrapper (less control), inconsistent interfaces, missing predict_proba | 🟡 |
| **5.2.0** | **Implement LogisticRegressionModel (Model 1)** | Baseline, interpretable, gradient descent training | Custom logistic regression implementation | ✅ DO: Hyperparameters: learning_rate=0.01, n_epochs=1000, L2_lambda=0.1. fit method: (1) Initialize weights with small random values, (2) For each epoch: forward pass z = X @ w + b, y_pred = sigmoid(z), compute log-loss + L2 penalty, backward pass for gradients dw and db, update w -= lr × dw. Store self.weights and self.bias. predict_proba: compute sigmoid(X @ w + b), return np.column_stack([1-prob, prob]). Justification: "Interpretable coefficients show feature importance. Fast training (2s). Assumes linear separability. Result: 71.2% recall @ 4.8% FPR"<br>❌ DON'T: Use sklearn.LogisticRegression directly (shows less understanding), no L2 regularization, return 1D probabilities | 🟡 |
| 5.2.1 | Implement __init__ with hyperparameters | Configuration storage | Instance with lr, epochs, L2_lambda | ✅ DO: Store hyperparameters as instance variables, initialize weights/bias as None (set in fit), document default values in docstring<br>❌ DON'T: Hardcode hyperparameters, initialize weights before fit (premature) | 🟢 |
| 5.2.2 | Implement fit method with gradient descent | Model training | Trained weights and bias | ✅ DO: Extract n_samples, n_features from X_train.shape. Initialize weights small random, bias zero. For epoch loop: compute predictions, loss, gradients, update. Optionally: track loss per epoch for convergence check, add early stopping if loss plateaus<br>❌ DON'T: No regularization (overfitting), fixed epochs without convergence check, no loss tracking | 🟡 |
| 5.2.3 | Implement predict_proba method | Probability prediction interface | (n, 2) probability array | ✅ DO: Compute z = X @ self.weights + self.bias, prob_class1 = 1 / (1 + np.exp(-z)), return np.column_stack([1-prob_class1, prob_class1]). Shape must be (n, 2) for threshold tuning compatibility<br>❌ DON'T: Return 1D array (breaks threshold tuning), use predict returning 0/1 (need probabilities) | 🟡 |
| **5.3.0** | **Implement KNNModel (Model 2)** | Non-parametric, local patterns, lazy learning | K-nearest neighbors classifier | ✅ DO: Hyperparameters: k=15, metric='euclidean'. fit method: store self.X_train and self.y_train (lazy learning—no training phase). predict_proba: (1) For each test point, compute distances to all training points, (2) Find k nearest indices, (3) Count labels of neighbors, (4) Return proportion as probabilities. Justification: "Captures local clustering patterns. Non-parametric—no distribution assumptions. Tests if phishing sites cluster in feature space. Downside: O(n) inference slow (50ms). Result: 68.5% recall @ 4.9% FPR (3rd place)"<br>❌ DON'T: Use sklearn.KNeighborsClassifier directly (acceptable but less impressive), no k tuning, ignore inference speed issue | 🟢 |
| 5.3.1 | Implement fit method (lazy storage) | Store training data | Stored X_train, y_train | ✅ DO: Simply save: self.X_train = X_train, self.y_train = y_train. Return self. Note: no actual "training"—this is lazy learning<br>❌ DON'T: Copy data unnecessarily, try to "train" KNN | 🟢 |
| 5.3.2 | Implement predict_proba with distance calculation | Inference via nearest neighbors | Probability predictions | ✅ DO: For each test point x: (1) distances = np.linalg.norm(self.X_train - x, axis=1), (2) k_indices = np.argsort(distances)[:self.k], (3) k_labels = self.y_train[k_indices], (4) prob_class1 = np.mean(k_labels), (5) prob_class0 = 1 - prob_class1. Vectorize over all test points. Return (n, 2) array<br>❌ DON'T: Inefficient loop without vectorization, wrong distance metric for scaled data, return hard predictions | 🟢 |
| **5.4.0** | **Implement XGBoostModel (Model 3)** | Production model, handles interactions, gradient boosting | Wrapper around xgboost.XGBClassifier | ✅ DO: Hyperparameters: max_depth=6, n_estimators=100, learning_rate=0.1, scale_pos_weight=1.22 (class balance correction). fit method: initialize self.model = XGBClassifier(params), call self.model.fit(X_train, y_train), optionally enable eval_set for validation monitoring. predict_proba: return self.model.predict_proba(X). Justification: "Handles feature interactions (high external links × low domain age = phishing). Gradient boosting ensemble robust to outliers and skew. scale_pos_weight=1.22 corrects 55:45 imbalance. Fast inference (18ms). Result: 74.1% recall @ 4.9% FPR (WINNER). +3% over Logistic = 13,500 more attacks caught = $6.75M monthly value"<br>❌ DON'T: No imbalance correction, ignore hyperparameter tuning, no justification for param choices | 🔴 |
| 5.4.1 | Configure hyperparameters thoughtfully | Prevent overfitting, optimize performance | Well-tuned XGBoost instance | ✅ DO: max_depth=6 prevents overfitting (deeper trees memorize noise), n_estimators=100 from cross-validation (more doesn't help), learning_rate=0.1 balances speed and accuracy, scale_pos_weight=n_legit/n_phishing=6050/4950=1.22 corrects imbalance. Document: "These params found via 5-fold CV with custom scoring=recall @ FPR≤0.05"<br>❌ DON'T: Use defaults blindly, extreme values (depth=20 overfits), no scale_pos_weight (ignores imbalance) | 🔴 |
| 5.4.2 | Optionally add hyperparameter tuning | Optimize model performance | Grid search or random search results | ✅ DO: Use sklearn.GridSearchCV or RandomizedSearchCV with: param_grid = {max_depth: [3,6,9], n_estimators: [50,100,200], learning_rate: [0.01,0.1]}, cv=5 stratified folds, scoring=custom metric (recall @ FPR≤0.05). Fit on train, report best params. Note: Time-intensive (2 hours on laptop)—maybe skip for interview, but document you know how<br>❌ DON'T: Manual trial-and-error, no cross-validation, optimize wrong metric (accuracy) | 🟢 |
| **5.5.0** | **Create model_selector.py module** | Metric hierarchy ranking, business-driven selection | ModelSelector class with compare_models method | ✅ DO: Class with compare_models accepting list of metrics dicts. Ranking logic: sort by (-tuned_recall, fpr, -roc_auc). Return {best_model: name, ranking: sorted list, selection_criteria: explanation}. select_best extracts top-ranked model. Justification documented: "Metric hierarchy: (1) Tuned recall @ FPR≤5% (PRIMARY KPI), (2) FPR minimization, (3) ROC AUC (tiebreaker), (4) PR AUC (sanity check)"<br>❌ DON'T: Select on accuracy (wrong metric), manual selection without criteria, no ranking documentation | 🔴 |
| 5.5.1 | Implement compare_models method | Rank all models by business criteria | Sorted comparison table | ✅ DO: Extract key metrics from each model: tuned_recall (from threshold tuning), fpr (at tuned threshold), roc_auc. Sort: primary by recall descending, secondary by fpr ascending, tertiary by auc descending. Create ranking list with all models. Example output: [{model: 'XGBoost', tuned_recall: 0.741, fpr: 0.049, roc_auc: 0.888}, {model: 'Logistic', tuned_recall: 0.712, ...}]<br>❌ DON'T: Only compare on single metric, no secondary criteria for ties, unclear sorting logic | 🔴 |
| 5.5.2 | Implement select_best method | Extract winner for deployment | Best model metrics dict | ✅ DO: Call compare_models, get best_model_name from ranking[0], find full metrics dict for that model, return it. Used by deployment pipeline to know which model.pkl to load<br>❌ DON'T: Hardcode model choice, return only name without metrics | 🟡 |
| **5.6.0** | **Train all three models** | Execute training pipeline | Three trained models with predictions | ✅ DO: In main.py: (1) Initialize all three models with documented hyperparameters, (2) For each: fit on X_train/y_train, (3) Generate predictions on val set first for threshold tuning, (4) Save models to models/ folder as model_name.pkl using pickle, (5) Log training time per model for comparison. Track memory usage if possible<br>❌ DON'T: Only train one model, skip validation predictions, no timing, don't save models | 🟡 |
| **5.7.0** | **Document model choices in README** | Justify selection to interviewers | Section "Model Selection Rationale" with 3+ models | ✅ DO: Create subsection per model with: (1) Name and type, (2) Why chosen (hypothesis from EDA), (3) Hyperparameters and justification, (4) Results (recall, FPR, ROC AUC), (5) Pros and cons, (6) Training/inference time. Final paragraph: Selection criteria explanation with metric hierarchy. Conclusion: "XGBoost selected for deployment due to +3% recall advantage = 13,500 additional attacks caught = $6.75M monthly value"<br>❌ DON'T: Vague descriptions like "tried 3 models", no justification, missing performance comparison, skip business value | 🔴 |

---

## Phase 6: Threshold Tuning & Optimization (1-2 hours for Task 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **6.1.0** | **THIS IS YOUR REDEMPTION MOMENT** | Fix the critical error that caused 12% recall | Understanding that max_fpr=0.03 was WRONG | ✅ DO: Acknowledge in presentation: "In my original submission, I set max_fpr=0.03 which resulted in only 12% recall. The business requirement is FPR≤5%, not 3%. This single parameter error caused me to miss 87% of attacks, resulting in $198M monthly fraud exposure vs $58.5M with correct threshold. Fixing this saves $139.5M monthly—the most impactful change in the entire pipeline."<br>❌ DON'T: Gloss over this mistake, not explain business impact, fail to fix it | 🔴 |
| **6.2.0** | **Create config.yaml with CORRECT KPI** | Centralize configuration, prevent errors | config.yaml with max_fpr: 0.05 | ✅ DO: Create config.yaml with: max_fpr: 0.05, models_to_train: [Logistic, KNN, XGBoost], random_state: 42, threshold_resolution: 1001. Comment: "max_fpr: 0.05  # Business constraint: FPR ≤ 5% maximum false alarm rate". Load in main.py via yaml.safe_load. Document in README: "To change FPR constraint, edit config.yaml max_fpr parameter"<br>❌ DON'T: Hardcode max_fpr=0.03 in code, no configuration file, no comments explaining parameter | 🔴 |
| **6.3.0** | **Implement evaluate_tuned function** | Find optimal threshold under constraint | Function performing threshold sweep | ✅ DO: In evaluation.py, create evaluate_tuned(y_true, y_proba, max_fpr=0.05, thresholds_len=1001). Algorithm: (1) thresholds = np.linspace(1.0, 0.0, thresholds_len) for fine granularity, (2) For each t: y_pred = (y_proba >= t).astype(int), compute tn/fp/fn/tp from confusion_matrix, compute fpr = fp/(fp+tn), recall = tp/(tp+fn), precision = tp/(tp+fp), f1 = 2×precision×recall/(precision+recall), (3) Track best_recall: if fpr <= max_fpr AND recall > best_recall['recall']: update best_recall, (4) Track best_f1 similarly, (5) Return {best_recall: {threshold, recall, fpr, f1}, best_f1: {...}, constraint: f'FPR≤{max_fpr}'}. Save all (t, recall, fpr, f1) to threshold_sweep.csv<br>❌ DON'T: Coarse threshold grid (only 10 points), no CSV output, optimize wrong metric (F1 without constraint), skip FPR constraint | 🔴 |
| 6.3.1 | Generate fine-grained threshold grid | Ensure optimal threshold found | 1001 thresholds from 1.0 to 0.0 | ✅ DO: Use np.linspace(1.0, 0.0, 1001) for 0.001 precision. Rationale: "Fine granularity ensures we don't miss optimal threshold. Example: coarse grid [0.9, 0.8, 0.7] might miss optimal at 0.78. Cost: minimal (1001 iterations on 1650 samples = <1 second)"<br>❌ DON'T: Only 10-20 thresholds (miss optimal), logarithmic spacing (uneven precision), start at 0.5 (miss high thresholds) | 🔴 |
| 6.3.2 | Compute metrics at each threshold | Build complete threshold landscape | DataFrame with threshold, recall, fpr, f1, precision | ✅ DO: For each threshold, compute full confusion matrix, derive all metrics, store in list. Convert to DataFrame for easy analysis. Save as threshold_sweep.csv with columns: threshold, tn, fp, fn, tp, fpr, recall, precision, f1. Enables: (1) Threshold analysis, (2) Pareto frontier extraction, (3) Audit trail, (4) Visualization<br>❌ DON'T: Only track best threshold (lose landscape), no intermediate storage, skip saving CSV | 🟡 |
| 6.3.3 | Filter by FPR constraint | Apply business requirement | Subset of thresholds meeting FPR≤max_fpr | ✅ DO: acceptable_thresholds = sweep_df[sweep_df['fpr'] <= max_fpr]. This is the feasible set. If empty: raise ValueError("No threshold achieves FPR≤{max_fpr}"). From acceptable set, select threshold with max recall. Document: "This enforces business constraint—we CANNOT accept solutions with FPR>5% regardless of recall"<br>❌ DON'T: Ignore constraint entirely, select best recall without FPR check, allow violations "just this once" | 🔴 |
| 6.3.4 | Select best recall under constraint | Optimize primary KPI | Optimal threshold and associated metrics | ✅ DO: best_recall_row = acceptable_thresholds.loc[acceptable_thresholds['recall'].idxmax()]. Extract: optimal_threshold = best_recall_row['threshold'], achieved_recall = best_recall_row['recall'], achieved_fpr = best_recall_row['fpr']. Return structured dict. Interpretation: "At threshold=0.78, achieve 74.1% recall with 4.9% FPR—maximizes attack detection within business constraint"<br>❌ DON'T: Return only threshold (lose metrics), no interpretation, unclear if constraint satisfied | 🔴 |
| **6.4.0** | **Optional: Implement Pareto analysis** | Visualize recall-FPR trade-off for stakeholders | Pareto frontier plot and analysis | ✅ DO: In threshold_analyzer.py, create compute_pareto_frontier(sweep_df). Algorithm: (1) Sort by fpr ascending, recall descending, (2) Iterate: keep point if recall > max_recall_seen, update max_recall_seen, (3) Return pareto_df. Create plot_pareto_curve: scatter all thresholds (gray), plot Pareto frontier (red line), mark chosen threshold (green star), draw FPR≤5% constraint (blue vertical line). Annotate axes: "False Positive Rate (%)" x "Recall (%)". Save as pareto_curve.png<br>❌ DON'T: Skip visualization (purely numerical), unclear axes, no chosen threshold marked, missing constraint line | 🟢 |
| 6.4.1 | Compute Pareto-optimal points | Extract non-dominated thresholds | DataFrame of Pareto-optimal (threshold, recall, fpr) | ✅ DO: Point A dominates B if recall_A ≥ recall_B AND fpr_A ≤ fpr_B (or one strict inequality). Pareto frontier = set of non-dominated points. Efficient algorithm: sort by fpr, scan once keeping points with higher recall than previous. These are thresholds where you can't improve recall without increasing FPR. Used for stakeholder presentation: "Here are all reasonable options"<br>❌ DON'T: Brute force O(n²) comparison (slow), unclear dominance criteria, no interpretation | 🟢 |
| 6.4.2 | Create Pareto visualization | Communicate trade-offs clearly | Professional plot showing trade-off curve | ✅ DO: Use matplotlib with: figsize=(10,6), scatter all points with alpha=0.3 (background), plot Pareto frontier as connected line (linewidth=2, color='red'), scatter chosen threshold as star (s=200, marker='*', color='green'), axvline for constraint (x=5.0, linestyle='--', color='blue'), labels and legend, title "Pareto Frontier: Recall-FPR Trade-off". Add text annotation for chosen point: f"Chosen: {recall:.1%} recall at {fpr:.1%} FPR"<br>❌ DON'T: Ugly default matplotlib, no annotations, missing constraint line, unclear which point is chosen | 🟢 |
| **6.5.0** | **Calculate business impact of threshold change** | Quantify value of fixing the error | ROI calculation showing $139.5M monthly savings | ✅ DO: Compare OLD (max_fpr=0.03, recall=12%) vs NEW (max_fpr=0.05, recall=74%). Scale to monthly volume: 1M visits × 45% phishing = 450K monthly attacks. OLD: 12% recall = 54K caught, 396K missed × $500 = $198M fraud + FP cost. NEW: 74% recall = 333K caught, 117K missed × $500 = $58.5M fraud + FP cost. Savings: $198M - $58.6M = $139.5M monthly. Document: "This is why threshold alignment is CRITICAL—single parameter drives 9-figure business impact"<br>❌ DON'T: Skip calculation, not quantify savings, fail to emphasize magnitude, no comparison table | 🔴 |
| **6.6.0** | **Integrate threshold tuning into pipeline** | Apply to all models | Tuned metrics for Logistic, KNN, XGBoost | ✅ DO: In main.py, after training each model: (1) Get validation predictions y_proba_val, (2) Call evaluate_tuned(y_val, y_proba_val, max_fpr=config['max_fpr']), (3) Store tuned_metrics per model, (4) Use tuned_recall as primary metric in model selection. Log: "XGBoost tuned: threshold=0.78, recall=74.1%, FPR=4.9%"<br>❌ DON'T: Only tune on test set (information leakage), use default threshold 0.5, no per-model tuning | 🔴 |
| **6.7.0** | **Document threshold tuning in README** | Explain methodology and impact | Section "Threshold Tuning & Optimization" | ✅ DO: Subsection with: (1) Algorithm explanation (1001 threshold sweep, FPR constraint, maximize recall), (2) Results table per model showing default vs tuned performance, (3) OLD vs NEW comparison with business impact, (4) Pareto curve image if created, (5) Interpretation: "Threshold tuning is where business requirements meet technical implementation. This phase translates 'FPR≤5%' constraint into actual decision boundary"<br>❌ DON'T: Bury in methods section, no results shown, skip business impact, missing OLD/NEW comparison | 🔴 |

---

## Phase 7: Evaluation & Metrics (1 hour for Task 2)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **7.1.0** | **Implement evaluate function** | Comprehensive metric computation | Function returning full metrics dict | ✅ DO: In evaluation.py, create evaluate(model, X_test, y_test). Compute: (1) y_pred = model.predict(X_test), y_proba = model.predict_proba(X_test)[:, 1], (2) Confusion matrix via sklearn.metrics.confusion_matrix, extract tn/fp/fn/tp via ravel(), (3) Rates: fpr = fp/(fp+tn), recall (TPR) = tp/(tp+fn), precision = tp/(tp+fp), specificity = tn/(tn+fp), (4) Composite: f1 = 2×precision×recall/(precision+recall), (5) Threshold-independent: roc_auc via roc_auc_score, pr_auc via average_precision_score, brier_score via brier_score_loss. Return comprehensive dict<br>❌ DON'T: Only compute accuracy (misleading), skip threshold-independent metrics, no confusion matrix breakdown | 🟡 |
| 7.1.1 | Compute confusion matrix | Foundation for all other metrics | [[TN, FP], [FN, TP]] matrix | ✅ DO: Use sklearn.metrics.confusion_matrix(y_test, y_pred), call ravel() to unpack as tn, fp, fn, tp. Display as 2×2 matrix with clear labels: "Predicted Legit | Predicted Phishing" as columns, "Actual Legit | Actual Phishing" as rows. Annotate with values and percentages<br>❌ DON'T: Wrong order (sklearn returns [[tn,fp],[fn,tp]] not [[tp,fp],[fn,tn]]), no labels, just print numbers | 🟡 |
| 7.1.2 | Derive classification rates | Interpret confusion matrix | FPR, recall, precision, specificity computed | ✅ DO: Compute from confusion matrix components: FPR = fp/(fp+tn) "false alarm rate on legit sites", Recall = tp/(tp+fn) "fraction of attacks caught", Precision = tp/(tp+fp) "fraction of warnings that are correct", Specificity = tn/(tn+fp) "fraction of legit sites correctly allowed". Handle edge cases: if denominator zero, return 0.0<br>❌ DON'T: Confuse recall with precision, no edge case handling, no interpretation | 🟡 |
| 7.1.3 | Compute threshold-independent metrics | Assess overall discrimination | ROC AUC, PR AUC, Brier score | ✅ DO: ROC AUC = roc_auc_score(y_test, y_proba) "88.8% probability model ranks random phishing > random legit". PR AUC = average_precision_score(y_test, y_proba) "focuses on positive class, better for imbalance". Brier = brier_score_loss(y_test, y_proba) "mean squared error of probabilities, lower is better, measures calibration". Note limitation: "High AUC doesn't guarantee good performance at business-constrained threshold"<br>❌ DON'T: Skip these (lose holistic view), no interpretation, claim AUC alone determines model quality | 🟡 |
| **7.2.0** | **Implement BusinessImpactCalculator** | Translate metrics to business costs | Class computing fraud exposure and support costs | ✅ DO: In business_impact.py, create class with constructor accepting fraud_loss_per_fn=500, support_cost_per_fp=5, monthly_volume=1_000_000. Method calculate(confusion_matrix, phishing_rate=0.45): (1) Extract tn/fp/fn/tp, (2) Compute scale_factor_phishing = (monthly_volume × phishing_rate) / (tp+fn), (3) Scale: monthly_fn = fn × scale_factor_phishing, monthly_fp similarly for legit, (4) Costs: fraud_exposure = monthly_fn × fraud_loss, support_cost = monthly_fp × support_cost, total_cost = sum, (5) Value: fraud_prevented = monthly_tp × fraud_loss. Return ImpactReport dict<br>❌ DON'T: Skip business translation, only technical metrics, no scaling to real volume, hardcoded costs | 🔴 |
| 7.2.1 | Implement calculate method | Scale test metrics to production volume | Monthly cost breakdown | ✅ DO: Key insight: test confusion matrix is from 1650 samples, but production is 1M monthly. Scaling: monthly_phishing = 1M × 0.45 = 450K, test_phishing = tp+fn, scale_factor = 450K / test_phishing. Example: test FN=258, scale_factor=453.3, monthly_FN=117K, fraud_exposure=117K × $500 = $58.5M. Include all components: attacks_caught, attacks_missed, false_alarms, fraud_exposure_usd, support_cost_usd, total_monthly_cost_usd, fraud_prevented_usd, catch_rate_pct<br>❌ DON'T: Use test numbers directly (undersells impact), no scale_factor explanation, miss any cost component | 🔴 |
| 7.2.2 | Implement compare_thresholds method | Quantify OLD vs NEW impact | Delta showing savings from fix | ✅ DO: Accept cm_strict (max_fpr=0.03) and cm_benchmark (max_fpr=0.05). Call calculate on both. Compute delta: additional_attacks_caught = benchmark_caught - strict_caught, additional_false_alarms = benchmark_fp - strict_fp, cost_savings_usd = strict_total_cost - benchmark_total_cost. Return {strict_3pct_fpr: {...}, benchmark_5pct_fpr: {...}, delta: {...}}. Interpretation: "$139.5M monthly savings for accepting 15 more false positives per day = 116:1 ROI"<br>❌ DON'T: Only show final numbers, no delta calculation, miss ROI interpretation, skip comparison | 🔴 |
| **7.3.0** | **Create comprehensive model comparison** | Present all metrics in organized format | Table comparing Logistic, KNN, XGBoost | ✅ DO: Create table with columns: Model, ROC AUC, PR AUC, Default Threshold, Default Recall, Tuned Threshold, Tuned Recall, Tuned FPR, Business Value. Example row: "XGBoost | 0.888 | 0.847 | 0.5 | 68% | 0.78 | 74.1% | 4.9% | $166.3M". Sort by Tuned Recall descending (primary metric). Add interpretation row summarizing winner and why<br>❌ DON'T: Only compare on one metric, no tuned vs default comparison, missing business value column, unclear sorting | 🔴 |
| **7.4.0** | **Interpret confusion matrix for each model** | Explain what numbers mean in context | Written interpretation per model | ✅ DO: For XGBoost @ threshold=0.78: "Confusion Matrix: TN=616 legit sites correctly allowed (93.8% of legit), FP=41 false alarms (6.2% false positive rate), FN=258 attacks missed (26% miss rate), TP=735 attacks caught (74% recall). This means: out of 993 phishing sites in test, we catch 735 (74%) with 41 false warnings on 657 legit sites. Trade-off: accepting 41/657=6.2% false alarm rate enables catching 735/993=74% of attacks."<br>❌ DON'T: Just show numbers without interpretation, skip rates, no trade-off explanation, miss business context | 🔴 |
| **7.5.0** | **Document metric justifications** | Explain why each metric matters | Section "Evaluation Metrics Explained" in README | ✅ DO: For each metric, provide: (1) Definition/formula, (2) Why it matters for this problem, (3) Business interpretation, (4) Limitations. Example: "Recall (TPR): Definition: TP/(TP+FN). Why: Security priority—must catch majority of attacks. Business: Each missed attack costs $500 fraud vs $5 per false alarm = 100:1 cost ratio favors recall. Limitation: Can achieve 100% recall by flagging everything, but FPR would be 100% too—hence the FPR≤5% constraint"<br>❌ DON'T: Just list metric names, no justification, skip business connection, ignore limitations | 🟡 |
| **7.6.0** | **Run evaluation on test set** | Final performance assessment | Test metrics for selected model | ✅ DO: ONLY evaluate on test set ONCE with final selected model. Call evaluate(best_model, X_test, y_test). Call evaluate_tuned with config max_fpr. Compute business impact via BusinessImpactCalculator. Save all to results/test_evaluation.json. Log: "Final Test Results: XGBoost @ threshold=0.78: Recall=74.1%, FPR=4.9%, ROC AUC=0.888, Monthly value=$166.3M". No further tuning after seeing test results—report honestly<br>❌ DON'T: Evaluate test set multiple times (information leakage), tune based on test results, cherry-pick best test run, hide worse results | 🔴 |
| **7.7.0** | **Create results summary for README** | Present findings professionally | Section "Model Evaluation Results" | ✅ DO: Include: (1) Confusion matrix visualization, (2) Metrics comparison table, (3) Business impact calculation with clear methodology, (4) Interpretation paragraph synthesizing findings, (5) Comparison to original submission showing improvements. Use markdown tables, bold best values. Add: "All metrics computed on held-out test set (n=1650, 742 phishing, 908 legit) using XGBoost with threshold=0.78 tuned on validation set"<br>❌ DON'T: Wall of numbers with no structure, missing comparison, no interpretation, unclear which metrics are test vs validation | 🔴 |

---

## Phase 8: Deployment & Monitoring (1 hour for README)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do/Don't) | Priority |
|---|---------------|-------------------------|---------|------------------------------|----------|
| **8.1.0** | **Document deployment architecture options** | Show production awareness | Section "Deployment Considerations" in README | ✅ DO: Present two architectures: (1) Client-side (browser extension): Load WASM model, extract features from URL/DOM, predict locally <10ms. Pros: fast, private, offline. Cons: model updates require extension update, limited to lightweight models. (2) Server-side (REST API): FastAPI on Kubernetes, client sends URL/HTML, server extracts features and predicts. Pros: easy updates, scalable, A/B testing. Cons: network latency, server cost. Recommendation: Server-side initially for rapid iteration, consider client-side later for latency optimization<br>❌ DON'T: Single architecture with no alternatives, no pros/cons, ignore deployment challenges, "just put model.pkl in production" | 🟡 |
| 8.1.1 | Describe client-side deployment | Browser extension option | Detailed client architecture | ✅ DO: Architecture: (1) Browser extension manifest.json, (2) Background script loads WASM-compiled model (5MB), (3) Content script extracts features from page: URL structure (NoOfURLRedirect), DOM analysis (NoOfiFrame, NoOfImage), (4) Send to background, predict locally, (5) Show warning modal if phishing. Advantages: p50 latency <10ms, no data leaves device (privacy), works offline. Implementation: Convert XGBoost to ONNX, compile to WASM via emscripten. Deployment: Chrome/Firefox web store, auto-updates. Limitation: Model size (5MB) affects extension install time<br>❌ DON'T: Vague "put in browser", no technical details, ignore privacy implications, unrealistic performance claims | 🟢 |
| 8.1.2 | Describe server-side deployment | REST API service | Detailed server architecture | ✅ DO: Architecture: (1) FastAPI app.py with POST /v1/predict endpoint, (2) Request schema: {url: str, html_content: str}, (3) Feature extraction: call extract_features(url, html), (4) Preprocessing: load preprocessor.pkl, call transform, (5) Prediction: load model.pkl, call predict_proba, (6) Response: {is_phishing: bool, confidence: float, threshold: float}. Infrastructure: Docker container with Python 3.10 + dependencies, deploy on Kubernetes cluster with 3 replicas, horizontal autoscaling based on CPU >70%, load balancer for traffic distribution. SLA: p99 latency <100ms, 99.9% uptime. Cost: ~$500/month for baseline (AWS EKS)<br>❌ DON'T: No API specification, ignore infrastructure needs, unrealistic SLA without justification, no cost estimate | 🟡 |
| **8.2.0** | **Document monitoring strategy** | Show production ops understanding | Section "Production Monitoring" in README | ✅ DO: Four-layer monitoring: Layer 1 System Health - metrics: p50/p95/p99 latency, error rate, throughput (requests/sec), alerts: latency p99>500ms for 5min → PagerDuty, error rate >1% → instant rollback. Layer 2 Feature Drift - weekly KL divergence per feature vs training baseline, alert threshold: KL>0.5 → investigate + consider retraining, example: median(LineOfCode) 850→1500 → KL=0.8 → alert. Layer 3 Model Performance - weekly sample predictions vs ground truth, recall degrades >5% → trigger automated retraining, FPR increases >2% → investigate false alarm surge. Layer 4 Business Metrics - attacks blocked per day, fraud prevented USD per month, dashboard with trend lines + confidence bands, escalate if attacks_blocked drops >20% week-over-week<br>❌ DON'T: Single-layer monitoring, no specific thresholds, no automated actions, ignore business metrics, "we'll monitor it somehow" | 🟡 |
| 8.2.1 | Specify system health monitoring | Infrastructure observability | Prometheus/Grafana setup | ✅ DO: Tools: Prometheus for metrics collection (pull model, 15s scrape interval), Grafana for dashboards (real-time + historical). Metrics instrumented: request_duration_seconds (histogram), predictions_total (counter by label), model_score_current (gauge). Dashboards: (1) Service health: latency percentiles, error rate, request volume, (2) Model performance: prediction distribution (phishing%), confidence histogram, (3) Alerts: triggered alerts timeline. Alerting: AlertManager routes to PagerDuty for critical (latency SLA breach), email for warnings (feature drift)<br>❌ DON'T: No specific tools, vague "we'll log things", no alert routing, unrealistic metrics without instrumentation plan | 🟢 |
| 8.2.2 | Specify feature drift detection | Distribution shift monitoring | Weekly drift reports | ✅ DO: Process: (1) Store training distribution per feature as reference histograms, (2) Weekly: sample 1000 production predictions, extract feature values, (3) Compute KL divergence: KL(prod || train) per feature, (4) Generate drift report: feature, KL_score, severity, delta_from_baseline. Example: Week 1: LineOfCode KL=0.2 (OK), Week 4: KL=0.8 (DRIFT detected). Root cause investigation: phishing sites evolving to mimic legit complexity. Action: Collect labels for recent samples, retrain model with expanded training set, deploy via blue-green<br>❌ DON'T: No baseline storage, no quantitative threshold, manual checks only, "we'll notice if it breaks" | 🟡 |
| 8.2.3 | Specify performance monitoring | Model accuracy tracking | Weekly performance reports | ✅ DO: Data collection: Sample 200 predictions weekly, send to manual labeling service (e.g., Mechanical Turk with 3-way consensus), collect ground truth labels. Metrics: Compute recall, FPR on weekly sample, compare to baseline (recall_baseline=70%, fpr_baseline=5%). Degradation thresholds: Recall drops from 70% to 64% (6% degradation >5% threshold) → trigger automated retraining pipeline. FPR increases from 5% to 7% (2% increase >2% threshold) → escalate to investigate (possible legitimate site pattern shift, not necessarily model issue)<br>❌ DON'T: No ground truth collection, assume model stays accurate forever, only monitor after complaints, no degradation thresholds | 🟡 |
| **8.3.0** | **Document model update strategy** | Show safe deployment process understanding | Section "Model Update Strategy" in README | ✅ DO: Blue-green deployment with four phases: Phase 1 Shadow Mode (0% traffic) - new model v1.1 logs predictions alongside production v1.0, compare agreement rate (target >95%), monitor for errors, duration: 3 days. Phase 2 Canary (5% traffic) - route 5% traffic to v1.1, monitor: recall ≥ v1.0_recall, FPR ≤ v1.0_FPR, error_rate <1%, p99 latency <120% of v1.0, duration: 3 days. Phase 3 Gradual Rollout - if canary passes, increase: 25% for 2 days, 50% for 2 days, 100%. Phase 4 Circuit Breaker - automated rollback if: error_rate >1% OR FPR > v1.0_FPR × 1.2 OR recall < v1.0_recall × 0.95, instant switch to v1.0 with zero user impact<br>❌ DON'T: Direct production deployment, no staged rollout, manual rollback only, ignore error monitoring, "push and hope" | 🟡 |
| 8.3.1 | Describe shadow mode | Safe validation before traffic | Phase 1 details | ✅ DO: Setup: Both v1.0 and v1.1 receive same requests, v1.0 serves responses (production), v1.1 logs predictions only (shadow). Comparison metrics: agreement_rate = fraction where v1.0_prediction == v1.1_prediction, target >95%. Disagreement analysis: inspect 100 random disagreement cases, understand if v1.1 improvements or regressions. Performance: v1.1 p99 latency vs v1.0, memory usage, error logs. Success criteria: agreement ≥95%, zero errors, latency <120% of v1.0. If fail: debug v1.1, never expose to users<br>❌ DON'T: Skip shadow mode (too risky), short duration (<1 day), ignore disagreements, no error monitoring | 🟢 |
| 8.3.2 | Describe canary deployment | Controlled user exposure | Phase 2 details | ✅ DO: Traffic split: 95% → v1.0 (blue), 5% → v1.1 (green). Per-version metrics: track recall, FPR, latency, error rate separately for each version. Example: v1.0 (95% traffic): recall=70%, FPR=5%, p99=180ms vs v1.1 (5% traffic): recall=72%, FPR=4.8%, p99=190ms. Success criteria: v1.1 metrics ≥ v1.0 (allow slight latency increase if performance improves), zero increase in user complaints. Monitoring: Real-time dashboard comparing versions side-by-side. Duration: 3 days minimum to capture daily patterns<br>❌ DON'T: 50% canary (too risky), insufficient monitoring, ignore user feedback, rush to 100% | 🟡 |
| 8.3.3 | Describe circuit breaker | Automated rollback protection | Phase 4 safety net | ✅ DO: Triggers: (1) Error rate: if v1.1 error_rate >1% for 5 consecutive minutes → rollback, (2) Performance degradation: if recall < baseline × 0.95 OR FPR > baseline × 1.2 → rollback, (3) Latency SLA: if p99 > 500ms for 10 minutes → rollback. Action: Instant traffic switch: 100% → v1.0, preserve v1.1 logs for debugging, alert team via PagerDuty, create incident ticket. Recovery: Debug v1.1 offline, fix issues, restart from shadow mode. Rationale: "Automated rollback ensures user experience never degrades—human reaction time (minutes) too slow for production incidents"<br>❌ DON'T: Manual rollback only (too slow), unclear trigger thresholds, no alerting, lose debugging data | 🟡 |
| **8.4.0** | **Document limitations honestly** | Show self-awareness and critical thinking | Section "Limitations & Future Work" in README | ✅ DO: Current Limitations: (1) Temporal drift - phishing tactics evolve, model trained on 2025 data may degrade by 2026, mitigation: quarterly retraining schedule, (2) Adversarial attacks - attackers can engineer features to evade detection (e.g., manipulate LineOfCode to match legit distribution), mitigation: ensemble models + anomaly detection layer, (3) Missing data - DomainAge lookup may fail for brand-new domains or privacy-protected registrations, mitigation: graceful degradation with missing flags, (4) Class imbalance - while 55:45 is mild, more severe imbalance could hurt minority class, mitigation: scale_pos_weight adjustment, consider SMOTE if imbalance worsens, (5) Feature correlation changes - if legitimate sites adopt phishing patterns (e.g., more pop-ups for engagement), false positives increase, mitigation: continuous monitoring + retraining<br>❌ DON'T: Claim no limitations, defensive about weaknesses, ignore adversarial scenarios, "model is perfect" | 🟡 |
| 8.4.1 | Acknowledge temporal drift | Models decay over time | Limitation with mitigation | ✅ DO: Explanation: "Phishing tactics evolve—2025 attackers use different techniques than 2024. Features like NoOfPopup distribution shift as legitimate sites adopt pop-ups for engagement. Model trained on current data will degrade as attacker behavior changes." Evidence: "Literature shows phishing detection models degrade 5-10% annually without retraining." Mitigation: "Quarterly retraining with recent labeled data (rolling 12-month window). Weekly drift monitoring flags when retraining urgent. Consider online learning for continuous adaptation."<br>❌ DON'T: Ignore concept drift, assume static attacker behavior, no retraining plan | 🟡 |
| 8.4.2 | Acknowledge adversarial attacks | Attackers can game the system | Limitation with mitigation | ✅ DO: Explanation: "Once attackers learn our model uses LineOfCode as feature, they can engineer their phishing sites to have 'normal' LineOfCode distribution (e.g., 800-2000 lines matching legit sites)." Attack vectors: Feature manipulation (pad code, fake images), mimicry attacks (copy legit site structure), adversarial examples (gradient-based perturbations if model exposed). Mitigation: "Don't expose model publicly, keep ensemble approach (harder to reverse engineer all models), add anomaly detection layer (detect sites that 'try too hard' to look legit), periodic red-team exercises"<br>❌ DON'T: Assume attackers are passive, ignore gaming incentives, no defensive strategy | 🟡 |
| 8.4.3 | Acknowledge missing data handling | Incomplete features affect predictions | Limitation with mitigation | ✅ DO: Explanation: "DomainAge lookup via WHOIS may fail for: newly registered domains (no age yet), privacy-protected registrations (WHOIS blocked), domains with malformed registration data." Impact: "68% missing DomainAge in training—MNAR flag captures some signal, but imputed median (24 months) may be wrong for new domains (age=0)." Mitigation: "Graceful degradation: DomainAge_missing=1 flag activates, impute with median, model still predicts (doesn't crash). Monitor missing rates in production—if >80%, investigate data pipeline. Consider alternative age source: domain registrar API"<br>❌ DON'T: Assume perfect data, ignore edge cases, claim imputation solves everything | 🟢 |
| **8.5.0** | **Propose future improvements** | Show forward thinking and research awareness | Subsection "Future Work" | ✅ DO: (1) Online learning - continuous model updates with incremental training on new labeled data, avoids periodic full retraining, adapts faster to drift, (2) Ensemble approach - combine XGBoost with other models (Random Forest, Neural Network), voting or stacking for robustness, harder for adversaries to game, (3) Deep learning on screenshots - CNN trained on website screenshots captures visual features (layout, colors, logo quality) that HTML features miss, complementary to structural features, (4) Graph analysis - analyze link structure (internal vs external), domain reputation networks, detect phishing clusters, (5) Explainability layer - SHAP values or LIME for per-prediction explanations, helps users understand why site flagged, builds trust, aids debugging<br>❌ DON'T: Generic "try deep learning", no specifics on how, unrealistic proposals (quantum ML), ignore practical constraints | 🟡 |
| **8.6.0** | **Finalize README.md** | Professional documentation | Complete, well-structured README | ✅ DO: Final review checklist: (1) All 9 required sections present (identity, structure, quickstart, flow, EDA summary, feature table, models, evaluation, deployment), (2) Proofread for typos and grammar, (3) Verify all links work (images, references), (4) Test instructions: can another person run bash run.sh successfully following only README, (5) Format consistency: consistent header levels, table formatting, code blocks, (6) Visual aids: add flowcharts if helpful, include confusion matrix image, Pareto curve if created, (7) Length: comprehensive but not overwhelming (aim for 8-12 pages), (8) Tone: professional but accessible, confident but humble about limitations<br>❌ DON'T: Submit with placeholder TODOs, broken links, inconsistent formatting, missing required sections, too short (<4 pages) or too long (>20 pages) | 🔴 |

---

## Final Pre-Interview Checklist (24 Hours Before)

| # | Category | Check | How to Verify | Priority |
|---|----------|-------|---------------|----------|
| **9.1** | **Code Functionality** | Pipeline runs end-to-end without errors | Run: bash run.sh from clean state, verify all results files generated | 🔴 |
| 9.1.1 | Data loading | phishing.db loads successfully | Check: data_loader.py runs, prints row count | 🔴 |
| 9.1.2 | Preprocessing | No data leakage, split before preprocess | Verify: main.py has split → fit → transform sequence | 🔴 |
| 9.1.3 | Training | All 3 models train successfully | Check: models/ folder has 3 .pkl files | 🔴 |
| 9.1.4 | Evaluation | Test metrics computed and saved | Check: results/test_evaluation.json exists, XGBoost recall ≥70% | 🔴 |
| **9.2** | **Documentation** | README complete and accurate | Open README.md, verify all sections present | 🔴 |
| 9.2.1 | Identity | Name and email stated | Check: README header has full name from NRIC | 🔴 |
| 9.2.2 | EDA→MLP table | Connection explicit | Check: table with Finding | Evidence | Decision columns | 🔴 |
| 9.2.3 | Feature table | Processing documented | Check: table with 15+ features showing preprocessing steps | 🟡 |
| 9.2.4 | Model comparison | 3+ models compared | Check: table comparing Logistic, KNN, XGBoost with metrics | 🔴 |
| 9.2.5 | Business impact | ROI calculated | Check: $139.5M savings documented with calculation | 🔴 |
| **9.3** | **Statistical Validation** | Hypothesis tests implemented | Check results/hypothesis_tests.json | 🟡 |
| 9.3.1 | Class balance | Chi-square test for imbalance | Verify: χ²=110, p<0.001 in results | 🟡 |
| 9.3.2 | MNAR tests | DomainAge tested | Verify: χ²=450, p<0.001 for DomainAge | 🟡 |
| 9.3.3 | Stratification | All splits validated | Verify: train/val/test all have p>0.05 | 🟡 |
| **9.4** | **Threshold Tuning** | max_fpr=0.05 (NOT 0.03) | Check config.yaml or main.py | 🔴 |
| 9.4.1 | Configuration | max_fpr value correct | Verify: config.yaml has max_fpr: 0.05 | 🔴 |
| 9.4.2 | Results | Recall ≥70% achieved | Check: XGBoost tuned_recall in results ≥0.70 | 🔴 |
| 9.4.3 | Documentation | OLD vs NEW comparison | Verify: README shows 12% vs 74% comparison | 🔴 |
| **9.5** | **EDA Notebook** | eda.ipynb complete | Open notebook, run all cells | 🟡 |
| 9.5.1 | Reproducibility | All cells run without errors | Kernel → Restart & Run All, verify success | 🟡 |
| 9.5.2 | Explanations | Every visualization explained | Scan: each plot has markdown interpretation after | 🟡 |
| 9.5.3 | Statistical tests | MNAR test visible | Check: Section 2 has chi-square test for DomainAge | 🔴 |
| **9.6** | **Presentation Prep** | 10-minute presentation ready | Rehearse with timer | 🔴 |
| 9.6.1 | Opening | Mistake acknowledgment scripted | Practice: "I made 3 critical mistakes..." | 🔴 |
| 9.6.2 | Comparison | OLD vs NEW slides/section ready | Prepare: side-by-side showing fixes | 🔴 |
| 9.6.3 | Closing | Business impact stated | Practice: "$139.5M monthly savings" | 🔴 |
| 9.6.4 | Timing | Fits in 10 minutes | Run through with timer, aim for 9:30 | 🔴 |
| **9.7** | **Q&A Prep** | Can explain key concepts without notes | Self-test on critical questions | 🔴 |
| 9.7.1 | Data leakage | Explain fit vs transform | Practice: explain 2-minute answer no notes | 🔴 |
| 9.7.2 | MNAR | Explain chi-square test | Practice: "H₀, contingency table, χ²=450..." | 🔴 |
| 9.7.3 | Threshold | Explain why 0.05 not 0.03 | Practice: cost-benefit with $139.5M | 🔴 |
| 9.7.4 | Business | Calculate fraud exposure | Practice: scale_factor calculation | 🔴 |
| **9.8** | **Group Exercise Prep** | Ready for unknown dataset | Mental preparation | 🟡 |
| 9.8.1 | Mindset | Collaborate, not compete | Remember: help teammates, share findings | 🟢 |
| 9.8.2 | Priority | No data leakage | Memorize: split → fit(train) → transform(all) | 🔴 |
| 9.8.3 | Template | Quick EDA checklist | Review: shape, missing, target, correlations | 🟡 |
| 9.8.4 | Speed | Simple working > complex broken | Remember: baseline model first, iterate if time | 🟡 |

---

## Common Pitfalls & How to Avoid

| Pitfall | Why It Happens | How to Avoid | Red Flag Check |
|---------|----------------|--------------|----------------|
| **Data Leakage** | Intuitive to "prepare all data first" | Memorize: SPLIT FIRST always, fit only on train | Code review: any .fit() call on full dataset? |
| **Wrong KPI** | Misread requirement or no validation | Re-read problem: "FPR≤5%" explicitly stated | Config check: max_fpr value is 0.05 not 0.03? |
| **No Statistical Tests** | Don't know they're expected | Review rubric: hypothesis testing = 10 points | Code check: hypothesis_tester.py exists? |
| **Poor README** | Write code first, document last | Start README early, update as you build | README check: all 9 sections complete? |
| **Weak EDA→MLP Connection** | EDA and pipeline developed separately | Create mapping table in Phase 1, reference throughout | README check: explicit table linking EDA to decisions? |
| **Missing Business Impact** | Focus only on technical metrics | Always ask: "So what? What does this cost/save?" | README check: $139.5M calculation present? |
| **Inconsistent Column Names** | One-hot encoding creates new columns | Use reindex after get_dummies in transform | Test check: val/test predictions work? |
| **Overfitting to Test** | Check test set multiple times | Lock test set, only evaluate ONCE with final model | Process check: test set touched only once? |
| **Unclear S-V-O Docstrings** | Generic documentation habits | Use template: "[Class] [verbs] [object] via [method]" | Code review: docstrings specific and clear? |
| **No Confidence Intervals** | Don't know they're needed | Compute: CI = ±1.96 × sqrt(p(1-p)/n) for test set | Analysis check: CI mentioned in README? |

---

## Success Indicators (You're Ready When...)

✅ **Technical Competence**:
- You can draw the correct preprocessing flow: split → fit → transform
- You can explain why max_fpr=0.03 was wrong and what it cost
- You can walk through chi-square test: H₀, contingency table, interpretation
- You can compute business impact: scale_factor, fraud_exposure calculation

✅ **Professional Communication**:
- You can explain every decision with statistical evidence
- You use Responsibility (S-V-O) pattern naturally in speech
- You acknowledge limitations honestly without being defensive
- You connect technical choices to business outcomes automatically

✅ **Production Thinking**:
- You consider inference latency, not just training accuracy
- You think about monitoring, drift, and degradation
- You design for updates: blue-green, shadow mode, circuit breakers
- You document for others: clear README, runnable code, audit trails

✅ **Learning Demonstration**:
- You own your mistakes openly: "I made data leakage error because..."
- You show deep understanding: not just "I fixed it" but "Here's why it was wrong"
- You validate fixes: "I confirmed with chi-square test that stratification worked"
- You quantify impact: "Fixing threshold alignment saves $139.5M monthly"

✅ **Group Exercise Readiness**:
- You think: "First question: is there data leakage risk?"
- You collaborate: "Let me handle EDA while you code the model"
- You test incrementally: Print metrics after each step, not at the end
- You present clearly: Simple working solution with clear business value

---

## Final Words: Your Interview Strategy

**Your Story**: "I failed because I didn't understand fundamentals. I spent [X time] learning deeply. Here's what I fixed and why it matters."

**Your Advantage**: Most candidates haven't failed and retried. You have battle scars. Use them.

**Your Goal**: By end of interview, they should think: "Strong learning ability. Made mistakes but learned deeply. Can grow into excellent ML engineer."

**Your Mindset**: Confident humility. You know you improved, but you know there's more to learn.

**You're ready. Go show them what you've learned.** 🚀

---

**Version History**:
- v1.0: Complete phase-by-phase implementation guide with m.n.o hierarchy, 9-phase coverage, checklist, and pitfalls

---

# Prompt_202601121300

```
**forbid code blocks, interactive demo**
generate phase-by-phase, step-by-step, lod-by-lod `interview-session-implementation-guide.md`

## Phase-by-Phase Implementation Guide  

### Phase 0: Setup & Data Acquisition (30 minutes)

| # | Step/Sub-step | Reasoning (Key Concepts) | Outcome | Notes (Do (Excellent Application)/Don't) | Priority | 
| 0.1.0 | Download phishing.db to data/ folder | ...
| 0.2.0 | Create project structure | ...
| 0.3.0 | In data_loader.py, implement: |
| 0.3.1 | load_from_sqlite function |
| 0.3.2 | validate_schema function | 
...
| 8.4.0 | In README, acknowledge limitations: |

where `m.n.o`, 
m: Phase,
n: Step,
o: Sub-step
```

---

## Note

## Structure Highlights:

### **9 Complete Phases** (Phase 0-8)
Each with hierarchical m.n.o numbering:
- **m**: Phase (0-8)
- **n**: Step within phase
- **o**: Sub-step within step

### **Every Row Contains**:
1. **Step Number** (e.g., 3.2.1)
2. **Reasoning**: Why this step matters (Key Concepts)
3. **Outcome**: What you'll produce
4. **Notes**: 
   - ✅ DO: Shows what impresses interviewers
   - ❌ DON'T: Common mistakes to avoid
5. **Priority**: 🔴 CRITICAL → 🟡 HIGH → 🟢 MEDIUM → ⚪ LOW

## Critical Focus Areas:

### **Phase 3** (Preprocessing) - 🔴 MOST CRITICAL
- **3.1.0**: Understanding SPLIT FIRST paradigm (prevents data leakage)
- **3.2.0-3.12.0**: Complete fit/transform implementation
- This phase alone determines if you pass or fail

### **Phase 6** (Threshold Tuning) - 🔴 YOUR REDEMPTION
- **6.1.0**: "THIS IS YOUR REDEMPTION MOMENT" - acknowledges max_fpr=0.03 error
- **6.5.0**: $139.5M savings calculation
- Shows you learned from the mistake that killed your original submission

### **Phase 1** (EDA) - Most Comprehensive
- **1.3.4**: MNAR chi-square test (χ²=450, p<0.001)
- **1.7.1**: EDA→MLP mapping table (critical connection)
- Demonstrates statistical rigor beyond basic visualization

## Special Sections:

### **Final Pre-Interview Checklist** (Section 9)
24-hour before checklist with:
- Code functionality verification
- Documentation completeness
- Statistical validation checks
- Presentation rehearsal
- Q&A prep on critical concepts

### **Common Pitfalls Table**
Shows:
- Why each pitfall happens
- How to avoid it
- Red flag checks

### **Success Indicators**
You're ready when you can:
- ✅ Draw preprocessing flow from memory
- ✅ Explain why max_fpr=0.03 was wrong ($139.5M impact)
- ✅ Compute business impact with scale_factor
- ✅ Own mistakes openly and show learning

## Time Budget:
- **Phase 0**: 30 minutes
- **Phase 1**: 3-4 hours (EDA)
- **Phase 2**: 1-2 hours (Statistical tests)
- **Phase 3**: 2-3 hours (Preprocessing - CRITICAL)
- **Phase 4**: 30 minutes (Splitting)
- **Phase 5**: 2-3 hours (Training)
- **Phase 6**: 1-2 hours (Tuning - REDEMPTION)
- **Phase 7**: 1 hour (Evaluation)
- **Phase 8**: 1 hour (Deployment docs)

**Total**: ~12-15 hours for complete implementation

This guide transforms you from "failed candidate" to "shows exceptional learning ability and technical fundamentals" by following every step systematically. Good luck! 🚀

---

I've created a comprehensive Mermaid flowchart that visualizes your entire implementation journey! Here's what makes this diagram powerful:

## Structure:

### **9 Phases + Final Checklist**
- **Phase 0**: Setup (30 min)
- **Phase 1**: EDA (3-4 hours) - Most comprehensive
- **Phase 2**: Statistical Tests (1-2 hours)
- **Phase 3**: Preprocessing (2-3 hours) - 🔴 CRITICAL (Red)
- **Phase 4**: Splitting (30 min)
- **Phase 5**: Model Training (2-3 hours)
- **Phase 6**: Threshold Tuning (1-2 hours) - 🔴 REDEMPTION (Red)
- **Phase 7**: Evaluation (1 hour)
- **Phase 8**: Deployment Docs (1 hour)
- **Phase 9**: Final Checklist (24 hours before)

### **Visual Highlights**:

1. **🔴 RED** = CRITICAL phases where you failed before:
   - Phase 3: "SPLIT FIRST" - prevents data leakage
   - Phase 6: "max_fpr=0.05 NOT 0.03" - fixes wrong KPI

2. **🟡 YELLOW** = Key decision points:
   - "SPLIT DATA FIRST 70/15/15" node
   - "max_fpr: 0.05 ✓ NOT 0.03 ✗" configuration

3. **🟢 GREEN** = Success outcomes:
   - "$139.5M monthly savings" - your redemption calculation
   - Final "SUCCESS: Ready for Interview" node

### **Subgraphs Group Key Concepts**:
- **Missing Value Analysis**: MNAR testing (χ²=450)
- **Feature Engineering**: fit/transform pattern
- **Leakage Prevention**: Train-only parameter learning
- **Threshold Sweep**: 1001 thresholds → max recall under constraint
- **Business Impact**: OLD vs NEW comparison
- **Four-Layer Monitoring**: System, drift, performance, business
- **Blue-Green Deployment**: Shadow → Canary → Gradual → Circuit breaker

### **Critical Path** (Follow the RED nodes):
1. Start: "Failed Assessment, Last Chance"
2. Phase 3: SPLIT FIRST paradigm (prevents leakage)
3. Phase 6: Fix max_fpr=0.05 (unlocks 74% recall)
4. Calculate: $139.5M monthly savings
5. End: "Ready for Interview"

### **How to Use**:
1. **Copy to Mermaid Live Editor**: https://mermaid.live
2. **View in GitHub**: Save as `.mmd` file, GitHub renders automatically
3. **VSCode**: Install Mermaid extension, preview live
4. **Export**: Generate PNG/SVG for presentation slides

### **Interview Strategy**:
Show this diagram in your presentation to demonstrate:
- ✅ Complete understanding of pipeline flow
- ✅ Awareness of critical failure points (RED nodes)
- ✅ Systematic approach to fixing mistakes
- ✅ Business impact thinking ($139.5M savings highlighted)

The flowchart tells your redemption story visually: Failed → Learned → Fixed → Validated → Succeeded 🚀
