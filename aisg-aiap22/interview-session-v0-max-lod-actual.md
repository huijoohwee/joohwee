---
title: "eda-mlp-interview-session – Actual vs Benchmark (aiap22-hui-joo-hwee-045B)"
author: "joohwee"
tags: [EDA, MLP, ActualCoverage]
date: 2026-01-10
mermaidAnchorsOnly: true
mermaid: |
  graph TB
    START([🎯 Business Problem:<br/>Phishing Detection])
    
    %% ===== PHASE 0: DATA ACQUISITION (ACTUAL) =====
    subgraph P0["📥 PHASE 0: Data Acquisition (src/data_loader.py)"]
      P0_LOAD["load_data<br/>→ DataFrame[n×k] with 'label'"]
    end
    
    %% ===== PHASE 1: OFFLINE EDA (NOTEBOOK) =====
    subgraph P1["📊 PHASE 1: Exploratory Data Analysis (EDA, notebook)"]
      P1_EDA["aisg-aiap22-task-1-eda-ipynb_20251201<br/>→ metrics.json, reports/*.csv, *.png"]
    end
    
    %% ===== PHASE 3: FEATURE ENGINEERING & PREPROCESSING (ACTUAL) =====
    subgraph P3["⚙️ PHASE 3: Feature Engineering & Preprocessing (src/feature_engineering.py, src/preprocessing.py)"]
      P3_FE["FeatureEngineer.transform<br/>→ engineered features"]
      P3_PRE["Preprocessor.fit_transform<br/>→ X_all, y_all, preprocessor.pkl"]
    end
    
    %% ===== PHASE 4: DATA SPLITTING & VALIDATION (ACTUAL) =====
    subgraph P4["🎲 PHASE 4: Data Splitting & Validation (src/data_splitter.py, src/pipeline_validator.py)"]
      P4_SPLIT["stratified_split<br/>→ 70/15/15 stratified splits"]
      P4_VAL["validate_processed<br/>→ pipeline_validation.json"]
    end
    
    %% ===== PHASE 5: MODEL TRAINING & SELECTION (ACTUAL) =====
    subgraph P5["🤖 PHASE 5: Model Training & Selection (models, optimization, model_selector)"]
      P5_TRAIN["LogisticRegressionModel / KNNModel / XGBoostModel.train"]
      P5_OPT["Optimizer.search (optional)<br/>→ tuned hyperparameters"]
      P5_SEL["select_best<br/>→ best_model.json"]
    end
    
    %% ===== PHASE 6: THRESHOLD TUNING (ACTUAL) =====
    subgraph P6["🎚️ PHASE 6: Threshold Tuning & Optimization (evaluation.py)"]
      P6_TUNED["evaluate_tuned on test<br/>(max_fpr from config.yaml, default 0.03)"]
      P6_SWEEP["sweep_thresholds on val<br/>→ threshold_sweep.csv"]
    end
    
    %% ===== PHASE 7: EVALUATION & METRICS (ACTUAL) =====
    subgraph P7["📈 PHASE 7: Evaluation & Metrics (evaluation.py, main.py)"]
      P7_EVAL["evaluate on test<br/>→ baseline_metrics.json (per-model metrics)"]
    end
    
    START --> P0_LOAD
    P0_LOAD --> P3_FE
    P3_FE --> P3_PRE
    P3_PRE --> P4_SPLIT
    P4_SPLIT --> P4_VAL
    P4_VAL --> P5_TRAIN
    P5_TRAIN --> P5_OPT
    P5_OPT --> P5_SEL
    P5_SEL --> P6_TUNED
    P6_TUNED --> P6_SWEEP
    P6_SWEEP --> P7_EVAL
    
    %% Offline EDA notebook is used to design features/preprocessing but is not called by src.main
    P1_EDA -. informs .-> P3_FE
---

# EDA → MLP Interview Session: Actual Maximum LOD Directory Table

**Version**: 1.0  
**Purpose**: Describe actual coverage vs benchmark for the EDA→MLP flow in aiap22-hui-joo-hwee-045B  
**Organization**: Module → Class/Object → Function/Method → Responsibility (S-V-O) → Dependencies → Artifacts

**Source of truth for “actual”**:
- EDA notebook summary: aisg-aiap22-task-1-eda-ipynb_20251201.md
- Code and config in: /Users/huijoohwee/Documents/GitHub/aiap22-hui-joo-hwee-045B
- Stored metrics: results/baseline_metrics.json

**Scope**:
- Read-only inspection only (no changes in aiap22-hui-joo-hwee-045B)
- No invented modules or metrics; everything below is directly grounded in the inspected files

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

**Business Context**: Load raw phishing dataset from SQLite for model training and evaluation.

### 0.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/data_loader.py` | (module-level) | `detect_table` | detect_table selects phishing table name from SQLite connection | `sqlite3`, SQLite connection | `table_name: str` | Prefers `"phishing_data"` if available; otherwise uses first table | Dedicated DataLoader method selecting configured phishing table with explicit schema awareness |
| `src/data_loader.py` | (module-level) | `load_data` | load_data loads full table into DataFrame and enforces presence of `label` | `pandas`, `sqlite3`, `"data/phishing.db"` | `DataFrame[n×k]` | Ensures target column exists; no explicit 46+1 schema or row-count gate | `DataLoader.load_from_sqlite` + `validate_schema` + `check_row_count` + `parse_target_variable` + `DataLogger.log_load_summary` |

### 0.2 Gap Analysis (vs benchmark)

**Benchmark expectation (from benchmark LOD table and mermaid):**
- DataLoader.load_from_sqlite → DataFrame[11000×47]
- DataLoader.validate_schema → explicit 46 features + 1 target check
- DataLoader.check_row_count → gate on ≥1000 rows, else abort
- DataLoader.parse_target_variable → y ∈ {0,1}
- DataLogger.log_load_summary → pipeline.log

**Observed implementation (aiap22-hui-joo-hwee-045B):**
- Module: data_loader.py  
  - Functions:
    - detect_table(conn): chooses "phishing_data" if present, else first table  
      (lines 5–7 in data_loader.py)
    - load_data(db_path="data/phishing.db", table=None):  
      - Checks that db_path exists  
      - Connects via sqlite3 and reads entire table into a pandas DataFrame  
      - Ensures target column "label" exists, else raises RuntimeError  
      (lines 9–21 in data_loader.py)
- No dedicated DataLoader class; data access is function-based.
- No DataLogger usage in this module; no logging of load summary is performed here.

**Gaps vs benchmark (fact-based):**
- Schema validation:
  - Benchmark calls out validate_schema with explicit expected columns and a ValidationReport.
  - In the actual code, load_data only enforces the presence of "label"; it does not compare the DataFrame schema against a fixed set of 46 features + 1 target.
- Row-count gate:
  - No check_row_count equivalent or abort condition on “<1000 rows”.
- Target parsing:
  - load_data requires a "label" column but does not map or coerce it to a documented {0,1} encoding beyond whatever is in the SQLite table.
- Load logging:
  - No DataLogger.log_load_summary call from data_loader.py. Pipeline logging is handled elsewhere (e.g. pipeline.log mentioned in README), but there is no per-load summary recorded by this module.

---

## Phase 1: Exploratory Data Analysis (EDA) {#phase-1-eda}

### 1.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | load_and_profile | loads data, profiles shape and memory, saves raw snapshot | `pandas`, `sqlite3` | `reports/metrics.json`, raw CSV snapshot | EDA performed in notebook, not src/ module | `UnivariateAnalyzer.compute_class_balance` + dataset load integrated into EDA package |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | analyze_missingness | analyzes missingness rates and patterns per feature | `DataFrame.isna` | `missingness_report.csv`, `missingness_top15.csv`, plots | Identifies MNAR-like patterns, but no reusable class | `UnivariateAnalyzer.analyze_missingness` + `BivariateAnalyzer.test_missingness_independence` |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | distribution_and_skew | computes skewness and plots histograms | `pandas`, plotting libs | `distribution_report.csv`, `distribution_histograms.png` | Drives later log/clip choices, but only in notebook | `UnivariateAnalyzer.compute_skewness` + `generate_qq_plots` |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | detect_outliers | detects outliers via IQR, plots boxplots | `numpy`, `pandas` | `outlier_report.csv`, `outlier_boxplots.png` | Outlier analysis not encapsulated in src/ | `UnivariateAnalyzer.detect_outliers` used downstream by preprocessing |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | correlation_analysis | computes correlation matrices and target correlations | `pandas` | `correlation_matrix.csv`, `target_correlation.csv`, `correlation_heatmap.png` | Used to reason about multicollinearity conceptually | `BivariateAnalyzer.compute_correlation_matrix` + `compute_vif` |

### 1.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- Dedicated EDA modules and classes, e.g.:
  - eda/univariate.py → UnivariateAnalyzer (class balance, missingness, skewness, QQ plots, outliers)
  - eda/bivariate.py → BivariateAnalyzer (correlation matrix, VIF, MNAR tests)
- Outputs:
  - ClassBalance with chi-square test
  - MissingnessReport
  - SkewnessReport
  - QQPlot artifacts
  - OutlierReport
  - CorrMatrix[46×46], VIF metrics

**Observed implementation (Task 1 notebook description):**
- File aisg-aiap22-task-1-eda-ipynb_20251201.md describes a single EDA notebook that:
  - Loads data from data/phishing.db and writes metrics to reports/metrics.json.
  - Profiles shape, memory usage, and saves a raw CSV snapshot.
  - Computes class distribution and baseline accuracy.
  - Generates summary statistics for numeric and categorical features.
  - Produces missingness reports and visualizations (missingness_report.csv, missingness_top15.csv, missingness_bar.png, missingness_heatmap.png).
  - Performs skewness analysis and histograms, generating distribution_report.csv and distribution_histograms.png.
  - Runs outlier detection via IQR, producing outlier_report.csv and outlier_boxplots.png.
  - Computes correlation_matrix.csv, target_correlation.csv, and correlation_heatmap.png, plus a ranked list of top predictive features.
  - Checks duplicates, zero-variance, and near-zero-variance features and writes a consolidated data_quality_report.md.
- All of the above is implemented as notebook code (Python cells) rather than as reusable modules under src/.

**Gaps vs benchmark:**
- EDA code structure:
  - Benchmark expects reusable module structure (UnivariateAnalyzer, BivariateAnalyzer classes).
  - Actual EDA is notebook-based; there is no eda/ package or these Analyzer classes in the aiap22-hui-joo-hwee-045B/src directory.
- Statistical tests in code:
  - The notebook narrative references chi-square, missingness thresholds, and correlation, but there is no dedicated HypothesisTester or separate EDA module in src/ implementing those tests as functions/classes.
- Artifact naming alignment:
  - The notebook produces reports and figures (metrics.json, data_quality_report.md, various CSV and PNG files) but not the specific artifacts named in the benchmark (e.g., eda_report.pdf).

---

## Phase 2: Statistical Hypothesis Testing {#phase-2-statistical-testing}

### 2.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | analyze_class_imbalance | computes class proportions and baseline accuracy | `pandas` | metrics in `reports/metrics.json` | Discusses imbalance qualitatively; no dedicated HypothesisTester in src/ | `HypothesisTester.test_class_balance_significance` with χ² and p-values |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | missingness_strata_analysis | segments features by missingness bands and class | `pandas` | narrative, plots, tables in notebook | Describes MNAR-like behaviour but not persisted as structured test results | `HypothesisTester.test_mnar_hypothesis` with explicit χ² results and decisions |
| `aisg-aiap22-task-1-eda-ipynb_20251201` | (notebook) | correlation_and_leakage_checks | examines correlations and potential leakage | `pandas` | `correlation_matrix.csv`, `target_correlation.csv` | Used to motivate later preprocessing choices | `HypothesisTester.validate_stratified_splits` and normality tests feeding later phases |

### 2.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- HypothesisTester.* functions for:
  - test_class_balance_significance (e.g., χ² test vs 50:50 null)
  - test_mnar_hypothesis for missingness patterns (MNAR vs MCAR/MAR)
  - validate_stratified_splits and test_normality_post_transform as explicit hypothesis tests
- Dedicated artifacts:
  - HypothesisTestReport.pdf
  - hypothesis_results.json

**Observed implementation:**
- From aisg-aiap22-task-1-eda-ipynb_20251201.md:
  - There is conceptual discussion of:
    - Class imbalance and its implications (baseline accuracy ~55.04%).
    - Threshold-based missingness categorisation (>70%, 20–70%, <20%).
    - MNAR-like patterns (e.g., missingness concentrated in phishing class).
  - The code shown focuses on:
    - Percentage calculations and threshold-based categorisation.
    - Visualization of missingness patterns.
    - Correlation and outlier detection.
- In the src/ folder of aiap22-hui-joo-hwee-045B:
  - There is no HypothesisTester module or equivalent functions.
  - There is no dedicated hypothesis testing artifact generator (no HypothesisTestReport.pdf or hypothesis_results.json file referenced in the pipeline code.

**Gaps vs benchmark:**
- Encapsulated hypothesis testing:
  - Benchmark specifies a named HypothesisTester component; the actual repository does not implement this as a module under src/.
- Formal tests and artifacts:
  - While the EDA notebook performs analyses sufficient to support decisions, there is no standalone hypothesis_results.json or HypothesisTestReport.pdf produced by the code in src/.

---

## Phase 3: Feature Engineering & Preprocessing {#phase-3-feature-engineering}

### 3.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/feature_engineering.py` | `FeatureEngineer` | `create_missing_flags` | FeatureEngineer creates binary *_missing flags for selected columns | `pandas` | additional *_missing columns | Implements MNAR flags for DomainAgeMonths, Robots, IsResponsive | `MissingValueHandler.create_mnar_flags` for all MNAR candidates with tests |
| `src/feature_engineering.py` | `FeatureEngineer` | `create_domain_age_bins` | bins DomainAgeMonths into age bands with labels | `pandas` | `DomainAgeMonths_bin` | Domain-aware age bins used as categorical features | `DomainFeatureEngineer.create_age_bins` aligned to EDA-derived cut points |
| `src/feature_engineering.py` | `FeatureEngineer` | `external_self_ratio` | creates ExternalSelfRatio = NoOfExternalRef/(NoOfSelfRef+1) | `pandas`, `numpy` | `ExternalSelfRatio` | Ratio feature encoding external vs self references | `DomainFeatureEngineer.create_ratio_features` tuned via EDA hypotheses |
| `src/feature_engineering.py` | `FeatureEngineer` | `quantile_bins` | applies quantile binning to numeric features (excluding DomainAgeMonths) | `pandas` | *_qbin columns | Generic quantile bins; parameters via config | `FeatureScaler.apply_log_transform` + binning only where EDA flags skew |
| `src/feature_engineering.py` | `FeatureEngineer` | `frequency_encode` | frequency-encodes categorical/boolean columns with rare bucket | `pandas` | *_freq columns | Handles high-cardinality categorical features | `DomainFeatureEngineer.encode_categorical` with scheme traced to schema |
| `src/preprocessing.py` | `Preprocessor` | `_log_clip` | clips numeric features and applies log1p | `numpy`, `pandas` | transformed numeric matrix | Applies to all numeric columns with configurable quantile | `FeatureScaler.apply_log_transform` on EDA-identified skewed features, with validation |
| `src/preprocessing.py` | `Preprocessor` | `_impute` | imputes numeric (median) and categorical (mode/unknown) values | `pandas`, `numpy` | fully imputed feature matrix | No explicit post-check for remaining NaNs | `MissingValueHandler.impute_numerical` / `impute_categorical` + `validate_no_missing` gate |
| `src/preprocessing.py` | `Preprocessor` | `_encode` | one-hot encodes categorical features | `pandas` | expanded one-hot matrix | Uses get_dummies without drop_first | `DomainFeatureEngineer.encode_categorical` with controlled cardinality and schema alignment |
| `src/preprocessing.py` | `Preprocessor` | `_scale` | standard or robust scales numeric features | `numpy` | scaled numeric matrix | Scaling choice driven by config | `FeatureScaler.standardize_features` tied to hypothesis tests on normality |
| `src/preprocessing.py` | `Preprocessor` | `fit_transform` / `transform` / `save` | fits preprocessing pipeline, transforms data, and persists state | `joblib`/`pickle`, `numpy` | `models/preprocessor.pkl`, transformed X, y | Fits on full dataset before split; single artifact for all phases | Preprocessor fitted on TRAIN only, artifact versioned and schema-validated |

### 3.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- MissingValueHandler:
  - create_mnar_flags → DomainAge_missing ∈ {0,1}
  - impute_numerical (e.g., median=24.0 months)
  - impute_categorical (mode-based)
  - validate_no_missing → abort if NaNs remain
- FeatureScaler:
  - apply_log_transform on 10 features with |skew|>1
  - validate_transform_effectiveness with updated skew
  - standardize_features → mean≈0, std≈1
- DomainFeatureEngineer:
  - age bins (new, medium, old)
  - ratio features, one-hot encoding
- Artifact: preprocessor.pkl with 51 final features.

**Observed implementation (aiap22-hui-joo-hwee-045B):**

Feature engineering:
- Module: feature_engineering.py → FeatureEngineer class:
  - create_missing_flags:
    - Creates binary flags for ["DomainAgeMonths", "Robots", "IsResponsive"] when present.  
      (lines 14–16)
  - create_domain_age_bins:
    - Bins DomainAgeMonths into [0,6), [6,12), [12,24), ≥24 months, with labels "<6mo", "6-12mo", "12-24mo", ">24mo".  
      (lines 18–23)
  - external_self_ratio:
    - Computes NoOfExternalRef / (NoOfSelfRef + 1) where both columns exist; returns "ExternalSelfRatio".  
      (lines 25–29)
  - quantile_bins:
    - Applies qcut (bin_quantiles, default 4) to other numeric columns and returns *_qbin columns, skipping DomainAgeMonths.  
      (lines 31–41)
  - frequency_encode:
    - Frequency encoding for categorical/boolean columns with rare values bucketed into "__RARE__"; produces *_freq columns.  
      (lines 43–51)
  - transform:
    - Applies the above steps conditionally (enable_flags, enable_bins, enable_ratios, enable_frequency_encoding) and appends engineered features to the original inputs.  
      (lines 53–76)

Preprocessing:
- Module: preprocessing.py → Preprocessor class:
  - _log_clip:
    - For each numeric column:
      - Clips values at lower=0 then at upper quantile (clip_quantile, default 0.99).
      - Applies np.log1p to the clipped values.  
      (lines 22–26)
  - _impute:
    - Numeric: median imputation.
    - Categorical: mode imputation, falling back to "unknown" if mode is empty.  
      (lines 28–33)
  - _encode:
    - One-hot encodes categorical features using pandas.get_dummies (no drop_first).  
      (lines 35–38)
  - _scale:
    - Standard scaling by default (mean/std), or robust scaling (median/IQR) depending on config.  
      (lines 40–48)
  - _remove_low_variance:
    - Optionally drops low-variance numeric features based on variance_threshold (default 0.0).  
      (lines 51–58)
  - _remove_high_correlation:
    - Optionally drops highly correlated numeric features based on correlation_threshold (default 0.98).  
      (lines 60–68)
  - fit_transform:
    - Splits label, identifies numeric/categorical columns.
    - Applies log-clipping → imputation → encoding → variance and correlation filtering → scaling.
    - Records resulting column list and scaling statistics.
    - Returns X (numpy array) and y.  
      (lines 70–83)
  - transform:
    - Applies log-clipping, fills missing values, aligns one-hot columns with fitted columns_, and applies stored scaling parameters.  
      (lines 85–102)
  - save:
    - Persists preprocessing state to models/preprocessor.pkl.  
      (lines 104–118)

**Gaps vs benchmark:**
- Separation of concerns:
  - Benchmark splits responsibilities across MissingValueHandler, FeatureScaler, and DomainFeatureEngineer; actual implementation combines them into FeatureEngineer and Preprocessor classes. The functionality is present but not structured into the same fine-grained modules.
- Validation of “no missing” post-imputation:
  - Preprocessor._impute and fit_transform handle missingness, but there is no explicit validate_no_missing check that aborts if NaNs remain after preprocessing.
- Transform-effectiveness validation:
  - _log_clip applies log+clip to numeric features, but there is no code that recomputes skewness inside src/ to validate that transformations achieved “no severe skew” as described in the benchmark.

**Alignment with benchmark:**
- MNAR flags:
  - DomainAgeMonths, Robots, and IsResponsive all get *_missing flags via FeatureEngineer, matching the MNAR-flag behaviour described in the benchmark.
- Imputation:
  - Numeric median and categorical mode/“unknown” imputation are implemented in Preprocessor._impute, in line with the benchmark’s imputation rules.
- Log-transform and clipping:
  - All numeric columns are clipped at 0 and at a 99th percentile by default, then transformed via log1p; this aligns with the benchmark’s heavy-tail handling, though the implementation is generic across numeric features instead of explicitly targeting a curated list of 10 skewed features.
- Standardization:
  - Preprocessor._scale implements both standard and robust scaling, fulfilling the “mean≈0, std≈1 / robust” requirement.
- Artifact:
  - Preprocessor.save writes models/preprocessor.pkl, satisfying the benchmark’s preprocessor artifact expectation.

---

## Phase 4: Data Splitting & Validation

### 4.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/data_splitter.py` | (module-level) | `stratified_split` | stratified_split partitions X, y into train/val/test with per-class stratification | `numpy` | X_train, X_val, X_test, y_train, y_val, y_test | Uses random_state=42; operates on already preprocessed features | `DataSplitter.stratified_train_test_split` with integrated statistical validation hooks |
| `src/pipeline_validator.py` | (module-level) | `validate_processed` | validates that splits contain no NaNs and reports label proportions | `numpy` | `data/processed/pipeline_validation.json` | Checks basic quality and class ratios; no χ² test | `DataSplitter.validate_split_stratification` returning p-values and detailed diagnostics |
| `src/main.py` | (module-level orchestration) | split_and_validate_pipeline | orchestrates preprocessing, splitting, and validation | `Preprocessor`, `stratified_split`, `validate_processed` | persisted processed data and validation report | Preprocessor fitted on full dataset before split (potential leakage) | Preprocessing fitted on TRAIN only, followed by stratified validation and leakage guardrails |

### 4.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- Stratified 70/15/15 splits (train/val/test) with class-balance validation (e.g., chi-square or similar).
- Validation that stratification preserves class ratios.
- Prevention of data leakage: preprocessing fitted on train only.

**Observed implementation:**
- Module: data_splitter.py:
  - stratified_split(X, y, test_size=0.15, val_size=0.15, random_state=42):
    - Implements custom stratified splitting by class.
    - Computes per-class indices, shuffles them, and slices them into test, val, and train sets with the requested proportions.  
      (lines 1–21)
- Module: pipeline_validator.py:
  - validate_processed(X_train, X_val, X_test, y_train, y_val, y_test):
    - Confirms that none of X_train, X_val, X_test contain NaNs.
    - Computes per-split label proportions via numpy.bincount and returns train_label_pct, val_label_pct, test_label_pct as lists.  
      (lines 1–15)
- Module: main.py:
  - Uses stratified_split to create train/val/test sets.
  - Calls validate_processed and writes the output to data/processed/pipeline_validation.json.
  - Preprocessor.fit_transform is called once before splitting; the transformed X, y are then split. This means preprocessing is applied on the full dataset prior to splitting.

**Gaps vs benchmark:**
- Statistical validation of stratification:
  - pipeline_validator reports per-split label percentages but does not perform a chi-square or similar statistical test to quantify whether the splits are statistically consistent with the full distribution.
- Data leakage perspective:
  - Benchmark explicitly mentions fitting scaler/imputer on TRAIN only.
  - Actual implementation fits Preprocessor on the full dataset before splitting, then splits the processed features. This differs from the strict “fit-on-train-only” pattern described in the benchmark and in the Task 1 EDA quality gates.

**Alignment with benchmark:**
- Split proportions and stratification:
  - stratified_split implements a 70/15/15 partition with class-wise stratification, matching the proportions and intent in the benchmark and the EDA document.
- Split validation output:
  - pipeline_validation.json provides machine-readable label proportions for train/val/test, enabling manual or downstream checks of class balance.

---

## Phase 5: Model Training & Selection

### 5.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `fit` / `predict_proba` | trains custom logistic regression via gradient descent and outputs probabilities | `numpy` | `models/logistic_regression.pkl` | Uses learning rate, epochs, L2 regularisation from config | `LogisticRegressionModel.train` with cross-validated hyperparameters and sklearn parity checks |
| `src/models/knn.py` | `KNNModel` | `fit` / `predict_proba` | stores training data and computes k-NN probabilities | `numpy` | `models/knn.pkl` (optional) | Lazy learner; tuned via Optimizer when enabled | `KNNModel.train` as part of model comparison grid with robust validation |
| `src/models/xgboost_model.py` | `XGBoostModel` | `fit` / `predict_proba` | wraps xgboost.XGBClassifier for training and inference | `xgboost`, `numpy` | `models/xgboost.pkl` | Parameters supplied from config/Optimizer | `XGBoostModel.grid_search_cv` + early stopping on validation |
| `src/optimization.py` | `Optimizer` | `search` | runs cross-validated search over model hyperparameters | `sklearn.model_selection`, `evaluation` | best_params per model (in-memory, persisted via metrics) | Driven by config.optimization; can be disabled | XGBoost grid search with fixed-size grid (e.g. “54 configs × 5-fold”) |
| `src/model_selector.py` | (module-level) | `select_best` | selects best model based on tuned recall, FPR, AUC metrics | `json`-serialised metrics dicts | `results/best_model.json` | Ranks by tuned recall, then FPR, then ROC/PR AUC | `ModelSelector.compare_validation_performance` with richer comparison report artifact |
| `src/main.py` | (module-level) | `run` (training loop) | orchestrates training, evaluation, tuning, and persistence for enabled models | all models, `Optimizer`, `evaluation` | `results/baseline_metrics.json`, models/*.pkl | Respects config to enable/disable models and optimisation | Central training orchestration plus explicit ModelComparisonReport.pdf |

### 5.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- Three models:
  - LogisticRegressionModel (custom gradient descent)
  - KNNModel
  - XGBoostModel
- Hyperparameter tuning:
  - XGBoost grid search (multiple configs × CV)
  - Early stopping with a validation set
- ModelSelector:
  - Compares models using recall, FPR, ROC AUC.
  - Selects best production model.
- Artifacts: model pickles and ModelComparisonReport.

**Observed implementation:**
- Models:
  - src/models/logistic_regression.py → LogisticRegressionModel:
    - Implements custom gradient descent with learning rate, epochs, and L2 regularisation.  
      (full file)
  - src/models/knn.py → KNNModel:
    - Distance-based k-NN classifier with configurable k, lazy training, and probability outputs.  
      (full file)
  - src/models/xgboost_model.py → XGBoostModel:
    - Present in src/models (confirmed via README and SearchCodebase), used from main.py.
- Orchestration (main.run):
  - Ensure directories (models, results, data/processed, experiments).
  - Load config from config.yaml.
  - Load data via load_data.
  - Apply FeatureEngineer and Preprocessor.
  - Split via stratified_split.
  - Validate processed splits (no NaNs, label proportions) and write data/processed/pipeline_validation.json.
  - For each enabled model:
    - Optionally run cross-validated hyperparameter optimisation via Optimizer (if optimization.enabled is true in config.yaml).
    - Train model on X_train, y_train.
    - Evaluate on X_test, y_test with evaluate.
    - Compute tuned metrics via evaluate_tuned.
    - Persist metrics into results/baseline_metrics.json.
    - Dump model weights/artifacts into models/*.pkl where applicable.
- Model selection:
  - src/model_selector.py → select_best(metrics_list):
    - Ranks models by:
      - Highest tuned recall (via tuned["best_recall"]["recall"]).
      - Then lower tuned FPR.
      - Then higher ROC AUC and PR AUC.
    - Returns the best metrics dict, which is saved to results/best_model.json.

**Gaps vs benchmark:**
- Model comparison report artifacts:
  - The code writes baseline_metrics.json and best_model.json but does not generate a separate ModelComparisonReport.pdf as described in the benchmark mermaid.
- Exact hyperparameter grid shape:
  - The benchmark mermaid mentions “54 configs × 5-fold = 270 fits” for XGBoost; the actual grid is defined in config.yaml and can be changed. The provided config includes a grid but the exact number of combinations is driven by that config, not hard-coded to 54.

**Alignment with benchmark:**
- Model set:
  - Logistic, KNN, and XGBoost models are all present and used, matching the benchmark.
- Hyperparameter optimisation:
  - src/optimization.py implements cross-validated search for logistic, KNN, and XGBoost, with scoring based on tuned recall under max_fpr.
- Model selection logic:
  - select_best ranks models using tuned recall and FPR plus ROC AUC/PR AUC, consistent with the benchmark’s intent to prioritise recall under an FPR constraint.
- Artifacts:
  - models/logistic_regression.pkl, models/xgboost.pkl, and baseline_metrics.json are produced; these correspond to the model artifacts and metrics described in the benchmark.

---

## Phase 6: Threshold Tuning & Optimization

### 6.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/evaluation.py` | (module-level) | `evaluate_tuned` | sweeps thresholds, enforcing max_fpr and tracking best recall/F1 | `numpy`, `sklearn.metrics` | tuned metrics embedded in baseline_metrics.json | max_fpr and grid size driven by config.yaml | `ThresholdTuner.select_optimal_threshold` under fixed FPR KPI (≤0.05) |
| `src/evaluation.py` | (module-level) | `sweep_thresholds` | computes recall and FPR across a grid of thresholds | `numpy` | raw sweep data (per-call) | Used by main to build threshold_sweep.csv | `ThresholdTuner.sweep_thresholds` feeding Pareto analysis |
| `src/main.py` | (module-level) | threshold_tuning_pipeline | runs evaluate_tuned on test and sweep_thresholds on val | `evaluation`, models | `results/threshold_sweep.csv` | Uses evaluation.max_fpr (0.03) and evaluation.threshold_grid (1001) | Pipeline enforcing business FPR target (≤0.05) with visual Pareto artifacts |

### 6.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- ThresholdTuner:
  - Generates probability scores on validation set.
  - Sweeps thresholds (e.g., 1000 values from 0 to 1).
  - Applies business constraint FPR ≤ 0.05.
  - Selects threshold that maximises recall under that constraint.
  - Validates generalisation on test set (recall and FPR deviations).
- Artifacts:
  - threshold value, threshold_sweep data, pareto_curve.png, pareto_analysis.json.

**Observed implementation:**
- Module: evaluation.py:
  - evaluate_tuned(y_true, y_proba, max_fpr=0.05, thresholds_len=101):
    - Creates thresholds with numpy.linspace(1.0, 0.0, thresholds_len).
    - For each threshold:
      - Computes confusion matrix, FPR, recall for class "1", and F1.
    - Tracks:
      - best_recall: best recall subject to fpr ≤ max_fpr.
      - best_f1: best F1 subject to fpr ≤ max_fpr.
    - Returns a dict containing best_recall and best_f1.  
      (lines 29–53)
  - sweep_thresholds(y_true, y_proba, thresholds):
    - Produces triplets of (threshold, recall, fpr) for each threshold.  
      (lines 55–84)
- Module: main.py:
  - For each model, evaluates base metrics on X_test, y_test via evaluate.
  - Computes tuned metrics on X_test probabilities (y_test, model.predict_proba(X_test)[:, 1]) using evaluate_tuned, with max_fpr and thresholds_len controlled by config.yaml.
  - After test evaluation, performs threshold sweep on the validation set (y_val and val probabilities) via sweep_thresholds and writes results/threshold_sweep.csv with model, threshold, recall, fpr columns.
- Config:
  - config.yaml sets:
    - evaluation.max_fpr: 0.03
    - evaluation.threshold_grid: 1001
  - This means:
    - Threshold grid length is 1001 (fine-grained sweep).
    - FPR constraint is stricter (≤3%) than the 5% mentioned in the benchmark mermaid.
- Stored metrics (results/baseline_metrics.json snapshot):
  - Logistic (example from file):
    - roc_auc ≈ 0.825
    - base confusion_matrix and fpr correspond to default threshold (likely 0.5).
    - tuned:
      - threshold: 0.88
      - fpr ≈ 0.0226
      - recall ≈ 0.0761
  - XGBoost:
    - roc_auc ≈ 0.888
    - tuned:
      - threshold: 0.97
      - fpr ≈ 0.0282
      - recall ≈ 0.1200
  - KNN:
    - roc_auc ≈ 0.809
    - tuned is null in this stored file.

**Gaps vs benchmark:**
- FPR constraint and KPI alignment:
  - Benchmark narrative and mermaid reference FPR ≤ 0.05 with recall ≈ 73.8% on test; in contrast, the current config uses max_fpr = 0.03 and the stored tuned thresholds in baseline_metrics.json yield very low recall (≈7.6–12%) at ≈2–3% FPR.
  - This means the stored tuned thresholds do not achieve the “Recall ≥70% under FPR ≤5%” KPI described in the benchmark; they prioritise a much stricter FPR with substantial recall loss.
- Pareto analysis artifacts:
  - The threshold_sweep.csv file is produced and contains the raw sweep data, but there is no pareto_curve.png or pareto_analysis.json produced by the code in src/.

**Alignment with benchmark:**
- Threshold sweep implementation:
  - sweep_thresholds and evaluate_tuned implement the same core idea as the benchmark’s ThresholdTuner: scanning thresholds, enforcing an FPR constraint, and extracting best recall/F1.
- Granularity:
  - threshold_grid: 1001 matches the “1000 thresholds from 0 to 1” spirit.
- Artifacts:
  - results/threshold_sweep.csv provides a threshold vs recall vs FPR table, which can be used to perform Pareto analysis, even though the pipeline does not currently emit a dedicated pareto visualization artifact.

---

## Phase 7: Evaluation & Metrics

### 7.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| `src/evaluation.py` | (module-level) | `evaluate` | computes core classification metrics and confusion matrix on test data | `sklearn.metrics`, `numpy` | metrics dict per model | Returns roc_auc, pr_auc, precision, recall, f1, specificity, brier, classification_report, confusion_matrix, fpr | `MetricsCalculator.compute_*` with parallel custom AUC check |
| `src/evaluation.py` | (module-level) | `confusion`, `specificity`, `auc_rank`, `cls_report` | helper functions to compute confusion matrix and derived metrics | `numpy`, `sklearn.metrics` | used inside evaluate/evaluate_tuned | Compose metric calculations rather than a single class | `MetricsCalculator` methods reused across phases with consistent API |
| `src/main.py` | (module-level) | evaluation_stage | runs evaluate and evaluate_tuned for each model | `evaluation`, models | `results/baseline_metrics.json` | Stores both base and tuned metrics; per-model entries | Distinct `test_results.json` dedicated to final chosen threshold and model |
| `src/main.py` | (module-level) | plot_roc_pr_integration | optionally generates ROC/PR plots | `matplotlib`/`seaborn` (via helper) | ROC/PR PNGs when enabled | Controlled by config.evaluation.enable_plots | Explicit confusion_matrix.png and ExecutiveSummary.pdf for business stakeholders |

### 7.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- MetricsCalculator:
  - Confusion matrix (TP, FN, FP, TN) for final threshold.
  - Recall, FPR, ROC AUC, custom AUC check.
  - BusinessImpactCalculator for fraud exposure and support cost.
- Artifacts:
  - test_results.json
  - confusion_matrix.png
  - ExecutiveSummary.pdf

**Observed implementation:**
- Module: evaluation.py:
  - confusion(y_true, y_pred): returns [[tn, fp], [fn, tp]].
  - specificity(y_true, y_pred): TN/(TN+FP).
  - auc_rank(y_true, y_score): uses sklearn.metrics.roc_auc_score.
  - cls_report: per-class precision and recall.
  - evaluate(model, X_test, y_test): returns:
    - roc_auc, pr_auc, precision, recall, f1, specificity, brier, classification_report, confusion_matrix, fpr.  
      (lines 17–35)
  - evaluate_tuned: as described in Phase 6.
- Artifacts:
  - results/baseline_metrics.json stores evaluation metrics for each model, including confusion matrices and FPR, plus tuned metrics.
  - ROC/PR plots can be generated as PNGs when config.evaluation.enable_plots is true (plot_roc_pr is imported and used in main.py under this condition).
- Business impact:
  - There is no BusinessImpactCalculator implemented under src/, and no code in this repository that computes monetary fraud exposure or support costs from confusion matrix entries.

**Gaps vs benchmark:**
- Business impact metrics:
  - No implementation of fraud exposure or support cost calculations.
  - No ExecutiveSummary.pdf or equivalent business-facing report generated by the code in src/.
- Result file naming:
  - The repository uses baseline_metrics.json and best_model.json rather than a distinct test_results.json as named in the benchmark.

**Alignment with benchmark:**
- Core classification metrics:
  - The evaluation module computes the same core metrics (confusion matrix, recall, FPR, ROC AUC), plus additional ones (PR AUC, Brier score).
- Visualization:
  - ROC/PR curve generation is supported when enabled in config.yaml, aligning with the benchmark’s emphasis on ROC/PR analysis.

---

## Phase 8: Deployment & Monitoring

### 8.1 Actual LOD Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | LOD Notes | Benchmark |
|--------|--------------|-----------------|------------------------|--------------|-------------------|-----------|-----------|
| (not present in src/) | (N/A) | (N/A) | repository focuses on training/evaluation only (no deployment pipeline) | CI (GitHub Actions) as described in README | model .pkl files, metrics JSON/CSV/PNG artifacts | No ModelPackager, blue/green deployer, or monitoring stack implemented | `ModelPackager.serialize_model` / `create_model_card` / `containerize_model` |
| (not present in src/) | (N/A) | (N/A) | no production deployment or traffic shifting logic | N/A | N/A | No blue/green or shadow deployments in this repo | `BlueGreenDeployer.*` for shadow mode and gradual traffic shift |
| (not present in src/) | (N/A) | (N/A) | no runtime monitoring or alerting code | N/A | N/A | No drift, latency, or KPI monitors in code | `SystemHealthMonitor`, `FeatureDriftDetector`, `PerformanceMonitor`, `AlertManager` stack |

### 8.2 Gap Analysis (vs benchmark)

**Benchmark expectation:**
- ModelPackager:
  - serialize_model, create_model_card, containerize_model.
- Deployment pattern:
  - Blue/green, shadow mode, gradual traffic shifting.
- Monitoring components:
  - SystemHealthMonitor (latency percentiles).
  - FeatureDriftDetector (KL divergence).
  - PerformanceMonitor (weekly recall/FPR).
  - BusinessMetricsTracker and AlertManager.
- Artifacts:
  - Docker image, Grafana dashboard, audit logs.

**Observed implementation:**
- aiap22-hui-joo-hwee-045B is scoped to training and evaluation:
  - README focuses on the ML pipeline and CI that runs the pipeline on push.
  - There is no deployment-specific code in src/ (no packager, blue/green deployment, drift detection, or monitoring modules).
  - No Dockerfile or monitoring configuration is present in this repository.

**Gaps vs benchmark:**
- Deployment and monitoring stack:
  - None of the deployment/monitoring components described in the benchmark mermaid (ModelPackager, BlueGreenDeployer, monitoring and alerting modules) are implemented in this repository.
- Production artifacts:
  - The pipeline produces model .pkl files and metrics JSON/CSV/PNG artifacts, but not a container image, monitoring dashboards, or long-term audit logs as described in the benchmark.

---

## Cross-Cutting Concerns

**Benchmark expectation:**
- CROSS_LOG: centralised pipeline logging for each phase.
- CROSS_VALIDATE: validation hooks at multiple gates.
- CROSS_ERROR: retry and error handling for IO/DB.
- CROSS_REPRO: reproducibility manager controlling random seeds.

**Observed implementation:**
- Logging:
  - README references pipeline.log as a full execution trace, but there is no dedicated PipelineLogger class in src/.
  - Logging details are not centrally abstracted into a cross-cutting logger module in the code inspected here.
- Validation:
  - pipeline_validator.validate_processed ensures no NaNs and reports class proportions for splits.
  - src/compliance_check.py checks:
    - Required files and directories exist.
    - run.sh does not install dependencies and correctly invokes python -m src.main.
    - requirements.txt uses pinned versions with a consistent format.
    - data_loader.py uses sqlite3 and the expected db path string.
    - evaluation.py contains required metric tokens such as roc_auc, classification_report, confusion_matrix, fpr.
- Error handling:
  - data_loader.load_data raises explicit exceptions on missing db or missing target column.
  - There is no central ErrorHandler with retry/backoff logic.
- Reproducibility:
  - stratified_split uses numpy.random.default_rng(random_state=42).
  - This ensures reproducible splits but there is no globally centralised ReproducibilityManager beyond this usage and config.yaml parameters.

**Gaps vs benchmark:**
- Centralised cross-cutting modules:
  - No PipelineLogger, ErrorHandler, or ReproducibilityManager modules as named components.
  - Validation logic is present but split across pipeline_validator and compliance_check, rather than a single CROSS_VALIDATE abstraction.

**Alignment with benchmark:**
- Validation:
  - The combination of pipeline_validator and compliance_check covers structural and basic data-quality gates consistent with the assessment’s automated checks.
- Reproducibility:
  - Hard-coded random_state=42 in stratified_split and configuration-driven parameters follow the spirit of reproducibility, even though there is no dedicated ReproducibilityManager class.

---

## Summary: High-Level Gap View

Grounded in the inspected files, the relationship between the benchmark EDA→MLP specification and aiap22-hui-joo-hwee-045B can be summarised as follows:

- Strong alignment in:
  - Core data loading from SQLite, basic target validation, and use of a consistent DB path.
  - EDA-driven feature engineering (MNAR flags, domain age bins, ratios, frequency encoding).
  - Preprocessing steps (log-transform, clipping, imputation, scaling, low-variance and high-correlation filtering).
  - Stratified 70/15/15 splits and post-split label distribution checks.
  - Training of three models (logistic, KNN, XGBoost) with cross-validated optimisation and model selection based on recall under an FPR constraint plus ROC/PR AUC.
  - Threshold sweeping with recorded sweeps and tuned metrics constrained by max_fpr.

- Partial alignment / structural differences:
  - EDA and hypothesis testing are implemented in a notebook and not refactored into reusable Analyzer/HypothesisTester modules under src/.
  - Preprocessing and feature engineering combine several responsibilities into two classes (FeatureEngineer and Preprocessor) rather than the more granular handlers described in the benchmark.
  - Stratification validation reports proportions but not explicit chi-square tests.

- Clear gaps relative to the benchmark scope:
  - No dedicated hypothesis-testing module or associated artifacts (HypothesisTestReport.pdf, hypothesis_results.json) in src/.
  - Current threshold configuration (max_fpr=0.03) and stored tuned thresholds in baseline_metrics.json do not achieve the benchmark KPI of recall ≥70% under FPR ≤5%; they enforce a stricter FPR threshold at the cost of recall.
  - No implementation of BusinessImpactCalculator or generation of business-facing reports (fraud exposure, support cost, executive summaries) in src/.
  - No deployment, monitoring, or alerting components (ModelPackager, BlueGreenDeployer, FeatureDriftDetector, SystemHealthMonitor, etc.) in this repository; its scope is training/evaluation only.

All statements above are grounded directly in the referenced markdown files, config.yaml, and the Python source code under /Users/huijoohwee/Documents/GitHub/aiap22-hui-joo-hwee-045B/src.

---

**1. Compact BENCHMARK vs ACTUAL diff table (material divergences only)**

| Phase | BENCHMARK (what’s expected) | ACTUAL (what’s implemented) | Material Divergence |
|-------|-----------------------------|-----------------------------|---------------------|
| 0 – Data Acquisition | DataLoader class with `load_from_sqlite`, `validate_schema` (46+1), `check_row_count` (≥1000), `parse_target_variable`, `DataLogger.log_load_summary` → `pipeline.log`. | Module-level `load_data(db_path, table)` enforces DB file exists, chooses table, loads DataFrame, asserts `label` column present. No logging. | No explicit schema check, no row-count gate, no target coercion, no load-summary logging module. |
| 1 – EDA | Reusable `eda/univariate.py` / `eda/bivariate.py` with analyzers (class balance, missingness, skew, QQ, outliers, corr, VIF). Artifacts like `eda_report.pdf`. | Single notebook `aisg-aiap22-task-1-eda-ipynb_20251201` with all EDA logic in cells and CSV/PNG outputs. No EDA package in `src/`. | EDA is not modularized into `src/`; lives in notebook only, artifacts not in benchmarked form. |
| 2 – Hypothesis Testing | `HypothesisTester.*` functions for class-balance, MNAR, split validation, post-transform normality. Artifacts: `HypothesisTestReport.pdf`, `hypothesis_results.json`. | Hypothesis reasoning (imbalance, missingness patterns, leakage) appears in notebook narrative only. No `HypothesisTester` module or dedicated hypothesis artifacts in `src/`. | No encapsulated hypothesis-testing code or artifacts; only informal notebook-level discussion. |
| 3 – FE & Preprocessing | Separate `MissingValueHandler`, `FeatureScaler`, `DomainFeatureEngineer`. Preprocessing fitted on TRAIN only. Explicit `validate_no_missing`, log-transform only EDA-flagged features, transform-effectiveness checks. | `FeatureEngineer` (flags, age bins, ratios, quantile bins, frequency encoding) + `Preprocessor` (log-clip all numerics, impute, one-hot, variance/corr filter, scale). `fit_transform` is called on the full dataset before split. | Responsibilities collapsed into two classes; no train-only fit; no explicit “no missing” validation step or skew re-checks. |
| 4 – Splitting & Validation | `DataSplitter.stratified_train_test_split` 70/15/15 with class-balance stats (e.g. chi-square). Guardrails against leakage (fit-on-train preprocessor). | `stratified_split` does 70/15/15 stratified by class. `validate_processed` checks for NaNs and returns label proportions; `pipeline_validation.json` stores these. Preprocessing was done on full dataset beforehand. | No chi-square or p-value strat validation; leakage risk due to global fit of preprocessing. |
| 5 – Model Training & Selection | Logistic, KNN, XGBoost with CV tuning; `ModelSelector.compare_validation_performance`; human-facing `ModelComparisonReport.pdf`. | `LogisticRegressionModel`, `KNNModel`, `XGBoostModel` implemented; `Optimizer` runs CV; `select_best` ranks models by tuned recall, FPR, ROC/PR AUC; artifacts: `baseline_metrics.json`, `best_model.json`, model `.pkl`s. | Functional parity for models and selection, but no separate comparison report artifact; grid size not fixed to the “54 configs” narrative. |
| 6 – Threshold Tuning | ThresholdTuner on val → sweep ~1000 thresholds, enforce FPR ≤ 0.05, pick threshold maximising recall; validate on test; emit `pareto_curve.png`, `pareto_analysis.json`. | `evaluate_tuned` + `sweep_thresholds` implement FPR-constrained threshold sweep. Config: `max_fpr=0.03`, `threshold_grid=1001`. `threshold_sweep.csv` written; tuned thresholds in `baseline_metrics.json` yield very low recall (~7–12%) at strict FPR (~2–3%). | Mechanism matches; KPI does not. FPR tighter than 0.05 and recall far below ~70%; Pareto artifacts (curve + JSON) not produced. |
| 7 – Evaluation & Metrics | `MetricsCalculator` + `BusinessImpactCalculator` for recall/FPR, ROC AUC, custom AUC, fraud exposure, support cost. Artifacts: `test_results.json`, `confusion_matrix.png`, `ExecutiveSummary.pdf`. | `evaluate` returns confusion matrix + rich metrics (ROC AUC, PR AUC, FPR, etc.). Metrics stored in `baseline_metrics.json`. Optional ROC/PR plots. No business-impact computation or executive report. | Core classification metrics covered; business impact metrics and business-facing artifacts not implemented. |
| 8 – Deployment & Monitoring | `ModelPackager`, `BlueGreenDeployer`, `SystemHealthMonitor`, `FeatureDriftDetector`, `PerformanceMonitor`, `AlertManager` etc. Production artifacts (image, dashboards, audit logs). | No deployment or monitoring code; repository ends at training/tuning/evaluation. CI exists but no runtime components. | Entire deployment/monitoring stack is out of scope for this repo. |
| Cross-cutting | Central `PipelineLogger`, `ErrorHandler` (retries/backoff), `ReproducibilityManager` controlling seeds. | `pipeline_validator` + `compliance_check` cover some checks; `data_loader` raises exceptions; `stratified_split` uses `random_state=42`. No centralized logger, error handler, or reproducibility manager. | Validation is present but distributed; logging/error-handling/reproducibility not factored as dedicated cross-cutting modules. |

---

**2. Lowest-effort BENCHMARK upgrades on top of the current aiap22 codebase**

Below are the upgrades that give the biggest benchmark alignment per unit of effort, grouped by priority.

**Tier 1 – Very low effort, high impact**

- **A. Train-only preprocessing (leakage fix)**
  - **What to change (high-level):**
    - In `src/main.py`:
      - Instead of `df -> FeatureEngineer.transform -> Preprocessor.fit_transform -> stratified_split(X, y)`, do:
        - `df -> stratified_split(df_features, y)` first on pandas data (or on `(df, y)`),
        - Fit `FeatureEngineer` + `Preprocessor` on TRAIN only,
        - Transform VAL/TEST via `Preprocessor.transform`.
  - **Effect:**
    - Removes leakage from val/test into preprocessing.
    - Aligns with BENCHMARK Phase 3/4 requirement “fit scaler/imputer on TRAIN only”.
  - **Effort:**
    - Local orchestration refactor in `main.run`; no algorithm changes.

- **B. Chi-square stratification validation**
  - **What to add:**
    - Extend `validate_processed` in [pipeline_validator.py](file:///Users/huijoohwee/Documents/GitHub/aiap22-hui-joo-hwee-045B/src/pipeline_validator.py#L1-L15) to:
      - Compute overall label distribution,
      - For each split (train/val/test), compare with overall using a chi-square test,
      - Include `chi2` and `p_value` per split in `pipeline_validation.json`.
  - **Effect:**
    - Bridges Phase 4 toward benchmark’s “validate stratified splits” with explicit statistical evidence.
  - **Effort:**
    - A few lines of extra calculations. Can be done with:
      - SciPy (`scipy.stats.chisquare`), or
      - A simple hand-rolled chi-square using NumPy only.

- **C. KPI-aligned threshold experiment (FPR ≤ 0.05)**  
  *(Even if you keep the current stricter 0.03 for production)*

  - **What to do:**
    - Add a small “benchmark mode” in `config.yaml`, e.g.:
      - `evaluation.benchmark_max_fpr: 0.05`.
    - In `main.run`, after current tuning at `max_fpr=0.03`, run a second `evaluate_tuned` pass for the chosen model with `max_fpr=0.05` to see:
      - Whether recall ≳70% is achievable,
      - What threshold and FPR that implies.
  - **Effect:**
    - Quantifies how far current pipeline is from BENCHMARK KPI, using existing functions.
  - **Effort:**
    - Extra call to `evaluate_tuned` and a small snippet to store those results (e.g., in `baseline_metrics.json` under `"benchmark_tuned"`).

---

**Tier 2 – Moderate but contained**

- **D. Simple BusinessImpactCalculator**
  - **What to add:**
    - A new small module, e.g. `src/business_impact.py` with functions:
      - `compute_fraud_exposure(fn, value_per_fn)` → monthly/annual fraud loss,
      - `compute_support_cost(fp, cost_per_fp)` → support cost due to false positives,
      - Optionally `summarize_business_impact(confusion_matrix, config)` to return a structured dict.
    - Hook it in `main.run` after picking the best model and a chosen threshold (e.g., the tuned one).
  - **Effect:**
    - Implements the essence of BENCHMARK Phase 7’s `BusinessImpactCalculator` without heavy reporting machinery.
    - Makes baseline_metrics more interpretable for stakeholders.
  - **Effort:**
    - Pure Python arithmetic and config constants; no new dependencies needed.

- **E. Pareto analysis over `threshold_sweep.csv`**
  - **What to add:**
    - Small script or module (e.g. `src/threshold_analysis.py`) to:
      - Read `results/threshold_sweep.csv`,
      - For each model, compute Pareto frontier on (FPR, recall),
      - Save a `results/pareto_analysis.json` summarizing non-dominated thresholds.
    - Optionally, produce `results/pareto_curve.png` with a simple matplotlib plot.
  - **Effect:**
    - Upgrades Phase 6 from raw grid to BENCHMARK-style Pareto analysis.
  - **Effort:**
    - Data-frame-level processing plus one simple plot; limited surface area.

---

**Tier 3 – Higher effort structural improvements**

- **F. Refactor notebook EDA into `src/eda/` modules**
  - Lift EDA logic from `aisg-aiap22-task-1-eda-ipynb_20251201` into:
    - `src/eda/univariate.py` (class balance, missingness, skew, outliers),
    - `src/eda/bivariate.py` (correlation, VIF).
  - Implement a `HypothesisTester` facade that calls into these and writes JSON results.
  - This gets Phases 1–2 structurally very close to BENCHMARK, but is more refactor-heavy.

- **G. Deployment & monitoring**
  - Introduce packaging, containerization, drift/metric monitoring, etc.
  - This goes well beyond the current repo’s training/evaluation scope.

---

If you tell me which subset of upgrades you’d like to prioritize (A–E), I can sketch the exact code diffs (e.g., for train-only preprocessing and chi-square validation) so you can see how they drop into the existing `src/main.py` and `src/pipeline_validator.py`.