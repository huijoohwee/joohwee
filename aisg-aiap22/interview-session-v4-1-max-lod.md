# Interview Session: Maximum LOD Table (Complete Drill-Down)

**Version**: 2.0 (Complete Responsibility Table Integration)  
**Purpose**: Exhaustive LOD pattern reference with all Class.Method signatures, dependencies, and artifacts  
**Format**: One row per function/method from clean-slate responsibility tables  
**Organization**: Phase-by-phase (0-8) with complete implementation details

---

## Table Format

Each row contains:
- **Class/Object.Method**: Full signature from responsibility tables
- **LOD Pattern**: Implementation pattern name
- **Dependencies**: Input requirements and libraries
- **Artifacts/Outputs**: What the function produces
- **Excellent Application**: Interview-ready explanation
- **Key Concepts**: Related technical concepts
- **Priority**: 🔴🟡🟢⚪🔵
- **FAQ**: Cross-reference to FAQ questions

---

## Priority Legend

- 🔴 **CRITICAL** - Asked in 80-100% of interviews
- 🟡 **HIGH** - Asked in 40-80% of interviews
- 🟢 **MEDIUM** - Asked in 10-40% of interviews
- ⚪ **LOW** - Rarely asked
- 🔵 **LOD** - Core implementation pattern (must know)

---

## Phase 0: Data Acquisition

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `DataLoader.load_from_sqlite` | Schema-Validated Loading | `sqlite3`, `pandas`, `expected_schema` | `DataFrame[n×k]`, `ValidationReport` | "DataLoader loads data and enforces schema contract. Validates 46+1 columns with dtype assertions before returning DataFrame. Prevents silent failures if upstream changes schema (e.g., DomainAge becomes string). Example: `assert df.columns == SCHEMA.keys()`. Returns ValidationReport for audit trail." | Data contracts, defensive programming, fail-fast, type safety | 🟢 | 0.1 |
| `DataLoader.validate_schema` | Schema Contract Enforcement | `DataFrame`, `SchemaDefinition` | `ValidationReport{is_valid, errors[]}` | "validate_schema checks columns and types against contract. Returns structured report: `{is_valid: bool, errors: List[str], columns_found, row_count}`. Example: If DomainAge expected float64 but got object → error appended. Used by load_from_sqlite to fail fast on schema violations." | Schema validation, data quality, contract testing | 🟢 | 0.1 |
| `DataLoader.check_row_count` | Minimum Sample Enforcement | `DataFrame`, `MIN_ROWS=1000` | `bool` or raises exception | "check_row_count enforces minimum viable dataset size. Below 1000 rows → 15% test = 150 samples → 67 phishing @ 45% rate → recall 95% CI ±12% (too wide for business decisions). Raises `DataQualityError` with alert to data engineering team. Prevents training on insufficient data." | Sample size, statistical power, quality gates, CI bounds | 🟢 | 0.2 |
| `DataLoader.parse_target_variable` | Target Encoding Validation | `DataFrame['label']`, `expected_values={0,1}` | `validated_labels` | "parse_target_variable validates label encoding. Asserts `unique_labels == {0, 1}`. Prevents silent failures if encoding changes upstream: {-1,1} → model trains on wrong labels, {'phish','legit'} → string labels cause errors. Logs class counts [6050, 4950] for imbalance detection." | Label encoding, defensive validation, data quality | 🟢 | 0.3 |

---

## Phase 1: Exploratory Data Analysis

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `UnivariateAnalyzer.analyze_missingness` | Missingness Profiling | `pandas.DataFrame` | `MissingnessReport{severe[], moderate[], low[]}` | "UnivariateAnalyzer computes missing rates and categorizes severity: severe (>70%), moderate (20-70%), low (<20%). Example: DomainAge 68% → severe[], Robots 12% → moderate[]. Returns structured report driving MNAR testing decisions. Reusable across datasets via modular design." | Per-feature analysis, distribution profiling, structured outputs | 🟡 | 1.1, 1.2 |
| `UnivariateAnalyzer.compute_skewness` | Skewness Detection | `DataFrame[numeric_cols]` | `SkewnessReport{col: {skew, requires_transform}}` | "compute_skewness identifies heavy-tailed distributions requiring transform. Calculates `skew = df[col].skew()`, categorizes: severe (\|skew\|>2), moderate (\|skew\|>1), low. Returns `{col: {skewness: 3.2, severity: 'severe', requires_transform: True}}`. Example: 10 features with \|skew\|>2 → log-transform candidates." | Distribution analysis, transformation planning, normality | 🟡 | 3.2 |
| `UnivariateAnalyzer.detect_outliers` | IQR Outlier Detection | `DataFrame[numeric_cols]`, `method='IQR'` | `OutlierReport{col: {count, bounds}}` | "detect_outliers identifies extreme values via IQR method. Computes Q1-1.5×IQR, Q3+1.5×IQR bounds. Example: LineOfCode Q1=500, Q3=1500, IQR=1000 → bounds=[−1000, 3000]. Count=42 outliers (3.8%) → clip at 99th percentile (2500). Returns `{col: {count, pct, lower_bound, upper_bound}}`." | Extreme value handling, robust statistics, clipping | 🟢 | 3.2 |
| `BivariateAnalyzer.compute_correlation_matrix` | Correlation Analysis | `DataFrame[numeric_cols]` | `CorrMatrix[n×n]`, `HighCorrPairs[]` | "BivariateAnalyzer calculates pairwise correlations and flags multicollinearity. Computes Pearson r for all pairs, extracts \|r\|>0.95. Example: NoOfImage × NoOfiFrame r=0.94 → high_corr_pairs. Used for: (1) Feature selection by \|r\| with target, (2) Multicollinearity check, (3) Leakage detection (r≈1.0)." | Feature interactions, multicollinearity, redundancy | 🟡 | 1.3 |
| `BivariateAnalyzer.test_missingness_independence` | MNAR Chi-Square Test | `DataFrame`, `col`, `target_col`, `scipy.stats` | `Chi2Result{statistic, p_value, is_mnar}` | "test_missingness_independence performs chi-square MNAR test. Creates contingency: [missing=True/False × target=0/1]. Example: DomainAge missing 45% in legit, 68% in phishing → χ²=450, p<0.001 → reject H₀ (independence) → MNAR confirmed. Returns `{chi2, p_value, is_mnar, interpretation}`." | Statistical validation, MNAR detection, contingency analysis | 🔴 | 1.2 |

---

## Phase 2: Statistical Hypothesis Testing

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `HypothesisTester.test_class_balance_significance` | Class Balance Chi-Square | `scipy.stats.chisquare`, `y`, `null_prob` | `TestResult{chi2, p_value, reject_h0}` | "HypothesisTester validates imbalance is not sampling noise via chi-square. H₀: P(phishing)=0.5. Observed [6050, 4950] vs expected [5500, 5500] → χ²=110, p<0.001 → reject H₀. Imbalance is statistically significant. Pipeline impact: (1) Stratified splits required, (2) Class weights needed, (3) Focus on recall over accuracy." | Hypothesis testing, imbalance validation, statistical evidence | 🟡 | 2.1 |
| `HypothesisTester.test_mnar_hypothesis` | MNAR Independence Test | `scipy.stats.chi2_contingency`, `DataFrame` | `MNARResult{chi2, p_value, is_mnar}` | "test_mnar_hypothesis determines if missingness depends on target class. Creates 2×2 contingency table: [is_missing × target]. Performs chi-square independence test. Example: DomainAge missingness rate by class: legit 45%, phishing 68% → χ²=450, p<0.001 → MNAR. Drives feature engineering: create DomainAge_missing binary flag." | MNAR detection, contingency analysis, feature engineering driver | 🔴 | 1.2, 2.1 |
| `HypothesisTester.validate_stratified_splits` | Stratification Chi-Square | `scipy.stats.chisquare`, `y_full`, `splits_dict` | `StratificationReport{per_split: {chi2, p_value}}` | "validate_stratified_splits confirms splits preserve class distribution. For each split, tests observed vs expected (from full distribution). Example: Train observed [4235, 3115], expected [4043, 3307] → χ²=2.94, p=0.086 >0.05 → cannot reject H₀ → stratification valid. Returns `{train: {chi2, p_value, is_stratified}, val: {...}, test: {...}}`." | Split quality, statistical validation, representative sampling | 🟡 | 4.1 |
| `HypothesisTester.save_results` | Audit Trail Persistence | `json`, `filepath` | `hypothesis_tests.json` | "save_results persists all test results for audit trail. Writes `{test_name: {h0, chi2, p_value, reject_h0, timestamp}}` to JSON. Enables: (1) Reproducibility (rerun with same random seed → same p-values), (2) CI/CD gates (pipeline fails if p<0.05 for stratification), (3) Regulatory compliance, (4) Debugging (compare test results across runs)." | Traceability, compliance, reproducibility, quality gates | 🟢 | 2.2 |

---

## Phase 3: Feature Engineering & Preprocessing

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `FeatureEngineer.fit` | Learn Feature Engineering Parameters | `DataFrame[train]` | `self.quantile_bins`, `self.freq_maps` | "FeatureEngineer learns quantile bins and frequency maps from training data. Stores `self.quantile_bins = {col: [Q1, Q2, Q3]}` for numeric features, `self.freq_maps = {col: {value: freq}}` for categoricals. CRITICAL: Only sees training data to prevent leakage. Returns `self` for method chaining. Example: `engineer.fit(df_train).transform(df_val)`." | Parameter learning, training-only, leakage prevention | 🔴🔵 | 3.1 |
| `FeatureEngineer.transform` | Apply Feature Engineering | `DataFrame`, learned parameters | `DataFrame[engineered]` | "transform applies learned feature engineering to data. Uses stored `self.quantile_bins` for binning, `self.freq_maps` for encoding. Stateless application—can be called on train/val/test/prod. Example: Apply Q1/Q2/Q3 bins learned from train to transform val/test. Consistent transformation ensures no leakage." | Inference operation, parameter application, production path | 🔴🔵 | 3.3 |
| `FeatureEngineer.create_missing_flags` | MNAR Indicator Creation | `DataFrame` | `DataFrame[with *_missing columns]` | "create_missing_flags generates MNAR indicators for predictive missingness. For MNAR features (DomainAge, Robots, IsResponsive), creates binary flag: `df['DomainAge_missing'] = df['DomainAge'].isna().astype(int)`. Captures intentional data hiding signal. Ablation study: removing flag drops recall 7% (74%→67%), confirming MNAR signal is predictive." | Feature engineering, MNAR signal, domain knowledge | 🔴 | 1.2, 3.1 |
| `FeatureEngineer.create_external_self_ratio` | Domain-Specific Ratio | `DataFrame[NoOfExternalRef, NoOfSelfRef]` | `DataFrame[with ExternalSelfRatio]` | "create_external_self_ratio computes domain-specific ratio feature. Formula: `Ext/(Self+1)` prevents division by zero. Hypothesis: phishing sites have high external links. Validation: phishing median=8.3 vs legit=2.1 (t-test p<0.001). Unbounded ratio preserves extreme cases (e.g., 50 ext, 2 self → ratio=25). Feature importance: rank #3 in XGBoost (gain=0.08)." | Feature engineering, domain knowledge, hypothesis-driven | 🟡 | 3.3 |
| `Preprocessor.fit_transform` | Learn and Apply Preprocessing | `DataFrame[train]` | `X_train[scaled]`, `y_train`, learned parameters | "Preprocessor learns preprocessing parameters from train and applies them. Sequence: (1) Learn clip values (99th percentile), (2) Learn imputers (median/mode), (3) Learn scaler params (mean/std), (4) Apply all to train. Stores `self.clip_values_`, `self.imputers_`, `self.scaler_params_`, `self.columns_`. Returns transformed train data. ONLY use on training split." | Combined operation, training pipeline, leakage prevention | 🔴🔵 | 3.1, 3.2 |
| `Preprocessor.transform` | Apply Learned Preprocessing | `DataFrame[val/test]`, learned parameters | `X_new[scaled]`, `y_new` | "transform applies learned parameters to new data without refitting. Uses TRAIN-LEARNED: clip_values (99th percentile), imputers (median/mode), scaler_params (mean/std). Column alignment via `reindex(columns=self.columns_, fill_value=0)` handles new categorical values. Example: Val has 'Industry_healthcare' not in train → filled with 0. Prevents shape mismatch at inference." | Inference operation, learned parameters, production path | 🔴🔵 | 3.1 |
| `Preprocessor._log_clip` | Log-Clipping Transform | `DataFrame[numeric]`, `clip_values` | `DataFrame[transformed]` | "_log_clip applies log1p transform after clipping outliers. Steps: (1) Clip at TRAIN-LEARNED 99th percentile (prevents test outliers from affecting transform), (2) Apply `np.log1p(clipped)`. Example: LineOfCode with max=50000 outlier → 99th percentile=2500 → clip to [0, 2500] → log1p. Reduces median \|skew\| from 1.8→0.4. Stabilizes variance for linear models." | Skewness reduction, outlier handling, distribution normalization | 🟡 | 3.2 |
| `Preprocessor._impute` | Missing Value Imputation | `DataFrame`, `imputers` | `DataFrame[no_missing]` | "_impute fills missing values with train-learned statistics. Numeric: median (robust to outliers). Categorical: mode with fallback to 'unknown' if all missing. Example: `df['DomainAge'].fillna(self.imputers_['numeric']['DomainAge'])` where median=24 months learned from train. CRITICAL: Uses stored imputers to prevent leakage (test median ≠ train median)." | Missing value handling, leakage prevention, robust statistics | 🟢 | 3.2 |
| `Preprocessor._scale` | Feature Standardization | `DataFrame`, `scaler_params` | `ndarray[scaled]` | "_scale standardizes features using train-learned mean/std. Formula: `(x - mean_train) / std_train`. All features → mean≈0, std≈1. Critical for: (1) KNN (equal weighting in distance metric), (2) Logistic (gradient stability in optimization). NOT needed for XGBoost (scale-invariant). Returns numpy array ready for model training." | Feature normalization, equal weighting, gradient stability | 🟡 | 3.2 |

---

## Phase 4: Data Splitting & Validation

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `(module).stratified_split` | Class-Preserving Split | `numpy.random`, `DataFrame` | `df_train`, `df_val`, `df_test` | "stratified_split partitions data preserving class distribution. Algorithm: (1) Get indices per class, (2) Shuffle within each class (random_state=42), (3) Partition proportionally (70/15/15). Example: 55% legit → each split has ~55% legit. Prevents: train 80% legit, test 40% legit (unrepresentative). Returns three DataFrames with preserved 55:45 ratio." | Class-preserving splits, representative sampling, reproducibility | 🟡 | 4.1, 4.2 |
| `(module).validate_processed` | Post-Processing Quality Check | `DataFrame`, `scipy.stats` | `ValidationReport{no_missing, stratification}` | "validate_processed performs quality checks and stratification tests. Checks: (1) No missing values (assert `not X.isna().any().any()`), (2) Label proportions computed per split, (3) Chi-square stratification tests. Example: Train no_missing=True ✓, label_props=[0.576, 0.424] ✓, chi2 p=0.08 >0.05 ✓. Returns structured ValidationReport for audit." | Quality gates, defensive programming, audit trail | 🟡 | 4.1 |
| `(module).validate_stratification` | Chi-Square Stratification Test | `scipy.stats.chisquare`, `y_arrays` | `Chi2Results{per_split: {chi2, p_value, is_stratified}}` | "validate_stratification performs chi-square tests per split. For each split: (1) Observed counts from split, (2) Expected counts from full distribution scaled by split size, (3) Chi-square test. Example: Train χ²=2.94, p=0.086 >0.05 → cannot reject H₀ → stratification valid. Returns `{train: {chi2, p_value, is_stratified: True, observed_pct, expected_pct}}`." | Statistical validation, split quality, hypothesis testing | 🟡 | 4.1 |

---

## Phase 5: Model Training & Selection

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `LogisticRegressionModel.fit` | Gradient Descent Training | `numpy`, `X_train`, `y_train` | `self.weights`, `self.bias` | "LogisticRegressionModel trains model via gradient descent with L2 regularization. Algorithm: (1) Forward pass: `z = X @ w + b; y_pred = sigmoid(z)`, (2) Loss: log-loss + L2 penalty, (3) Backward pass: gradients `dw`, `db`, (4) Update: `w -= lr × dw`. Params: lr=0.01, epochs=1000, L2_lambda=0.1. Returns trained model. Result: 71.2% recall @ 5% FPR (2nd place)." | Custom implementation, interpretable, L2 regularization | 🟡 | 5.1 |
| `LogisticRegressionModel.predict_proba` | Probability Prediction | `numpy`, `X`, `self.weights` | `probabilities[n×2]` | "predict_proba returns class probabilities via sigmoid. Computes `z = X @ self.weights + self.bias; prob_class1 = sigmoid(z)`. Returns `np.column_stack([1-prob_class1, prob_class1])` with shape (n, 2). Required interface for threshold tuning. All models must return 2D array: [prob_class0, prob_class1]." | Probability scores, threshold tuning, interface consistency | 🟡 | 6.2 |
| `KNNModel.fit` | Lazy Learning Storage | `X_train`, `y_train` | `self.X_train`, `self.y_train` | "KNNModel stores training data for lazy learning. No training phase—just saves `self.X_train = X_train; self.y_train = y_train`. Prediction: find k=15 nearest neighbors via Euclidean distance, majority vote. Trade-offs: Captures local patterns (phishing clusters), O(n) inference (50ms, slowest), curse of dimensionality with 50+ features. Requires standardization for equal feature weighting." | Non-parametric, distance-based, lazy learning | 🟡 | 5.2 |
| `XGBoostModel.fit` | Gradient Boosting Training | `xgboost`, `X_train`, `y_train`, `params` | `self.model` | "XGBoostModel wraps xgboost.XGBClassifier for training. Params: max_depth=6 (prevents overfitting), n_estimators=100 (ensemble size), learning_rate=0.1, scale_pos_weight=1.22 (imbalance correction). Handles feature interactions (e.g., high external links + low domain age = phishing). Fast inference (18ms). Result: 74.1% recall @ 5% FPR (WINNER). Beats Logistic by +3% recall = 13,500 attacks caught = $6.75M fraud prevented monthly." | Gradient boosting, feature interactions, production-grade | 🔴 | 5.1, 5.3 |
| `ModelSelector.compare_models` | Metric Hierarchy Ranking | `metrics_list` | `ComparisonReport{ranking, criteria}` | "ModelSelector ranks models by business-driven metric hierarchy. Priority: (1) tuned_recall (primary KPI—maximize attack detection under constraint), (2) FPR (secondary—minimize false alarms within 5% limit), (3) ROC AUC (tertiary—tiebreaker), (4) PR AUC (quaternary—sanity). Sorting: `(-tuned_recall, fpr, -roc_auc)`. Returns `{best_model, ranking, selection_criteria}`. Example: XGBoost 74.1% > Logistic 71.2% > KNN 68.5%." | Business alignment, model selection, prioritization | 🔴 | 5.3 |
| `ModelSelector.select_best` | Best Model Extraction | `metrics_list` | `best_model_metrics` | "select_best returns top-ranked model for deployment. Calls `compare_models()`, extracts best_model_name, returns full metrics dict for that model. Example: Returns `{model: 'XGBoost', tuned: {best_recall: {threshold: 0.78, recall: 0.741, fpr: 0.049}}, roc_auc: 0.888}`. Used by deployment pipeline to determine which model.pkl to serve." | Model selection, deployment preparation, metrics extraction | 🔴 | 5.3 |

---

## Phase 6: Threshold Tuning & Optimization

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `(module).evaluate_tuned` | FPR-Constrained Optimization | `numpy`, `sklearn.metrics`, `y_true`, `y_proba` | `TunedMetrics{best_recall, best_f1}` | "evaluate_tuned finds optimal threshold maximizing recall under FPR constraint. Algorithm: (1) Generate 1001 thresholds [1.0→0.0], (2) For each: compute FPR, recall, (3) Filter to FPR≤max_fpr, (4) Select threshold with max recall. Example: max_fpr=0.05 → threshold=0.78 → recall=74.1%, FPR=4.9%. Returns `{best_recall: {threshold, recall, fpr, f1}, best_f1: {...}, constraint: 'FPR≤0.05'}`." | Threshold optimization, business constraint, recall maximization | 🔴 | 6.1, 6.2 |
| `ThresholdAnalyzer.compute_pareto_frontier` | Pareto Extraction | `DataFrame[threshold, recall, fpr]` | `DataFrame[pareto_points]` | "ThresholdAnalyzer extracts non-dominated thresholds from sweep. Algorithm: (1) Sort by FPR ascending, recall descending, (2) Iterate: keep point if recall > max_recall_seen. Non-dominated: can't improve recall without increasing FPR. Example: threshold=0.90 (recall=30%, FPR=2.5%) dominates threshold=0.92 (recall=20%, FPR=2.5%). Returns DataFrame of Pareto-optimal thresholds for visualization." | Multi-objective optimization, non-dominated solutions, trade-off | 🟡 | 6.3 |
| `ThresholdAnalyzer.plot_pareto_curve` | Trade-off Visualization | `matplotlib`, `sweep_df`, `chosen_threshold` | `pareto_curve.png` | "plot_pareto_curve visualizes recall-FPR trade-off with annotations. Plots: (1) All thresholds (gray scatter), (2) Pareto frontier (red line), (3) Chosen threshold (green star), (4) FPR≤5% constraint (blue vertical line). Axes: FPR (%), Recall (%). Saves to `pareto_curve.png`. Used in stakeholder presentations to explain threshold choice and trade-offs." | Visualization, stakeholder communication, decision support | 🟡 | 6.3 |
| `ThresholdAnalyzer.analyze_business_constraints` | Constraint-Aware Selection | `pareto_df`, `max_fpr` | `ConstraintAnalysis{optimal_threshold, achieved_recall}` | "analyze_business_constraints finds optimal threshold under FPR limit. Filters Pareto points to FPR≤max_fpr, selects max recall. Example: max_fpr=0.05 → acceptable points with FPR≤5% → optimal: threshold=0.78, recall=74.1%, FPR=4.9%. Returns `{max_fpr_constraint, optimal_threshold, achieved_recall, achieved_fpr, interpretation: '74.1% recall at 4.9% FPR'}`. Handles edge case: no threshold meets constraint → error message." | Constraint satisfaction, optimal solution, business alignment | 🔴 | 6.1, 6.3 |

---

## Phase 7: Evaluation & Metrics

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `(module).evaluate` | Comprehensive Metrics | `sklearn.metrics`, `model`, `X_test`, `y_test` | `Metrics{cm, FPR, recall, ROC_AUC, PR_AUC}` | "evaluate computes comprehensive classification metrics from predictions. Outputs: (1) Confusion matrix [[TN, FP], [FN, TP]], (2) Rates: FPR, recall, precision, specificity, (3) Composite: F1, (4) Threshold-independent: ROC AUC, PR AUC, Brier. Example: XGBoost @ default threshold=0.5 → [[631, 26], [874, 119]], recall=12%, ROC AUC=0.888. Returns structured Metrics dict for logging and comparison." | Performance quantification, multi-faceted evaluation, metric selection | 🟡 | 7.1, 7.2 |
| `BusinessImpactCalculator.calculate` | Business Cost Translation | `confusion_matrix`, `phishing_rate`, `cost_params` | `ImpactReport{fraud_exposure, support_cost, catch_rate}` | "BusinessImpactCalculator translates confusion matrix to monthly business costs. Algorithm: (1) Scale test to monthly: `monthly_phishing = 1M × 0.45 = 450K`, (2) Compute scale_factor: `450K / (tp+fn) = 453.3`, (3) Scale TP/FN/FP, (4) Calculate costs: `FN × $500 + FP × $5`. Example: FN=874 → monthly_fn=396K → fraud_exposure=$198M. Returns `{monthly_phishing, attacks_caught, attacks_missed, false_alarms, fraud_exposure_usd, support_cost_usd, total_monthly_cost_usd, fraud_prevented_usd, catch_rate_pct}`." | Business translation, cost-benefit, ROI, scale factor | 🔴 | 7.3 |
| `BusinessImpactCalculator.compare_thresholds` | Threshold ROI Analysis | `cm_strict`, `cm_benchmark` | `ComparisonReport{delta: {cost_savings, attacks_caught}}` | "compare_thresholds quantifies business impact of threshold change. Calls `calculate()` for both confusion matrices, computes delta. Example: Strict (3% FPR): $198M cost. Benchmark (5% FPR): $58.6M cost. Delta: $139.5M monthly savings, 261 additional attacks caught, 15 additional false alarms. Returns `{strict_3pct_fpr: {...}, benchmark_5pct_fpr: {...}, delta: {additional_attacks_caught, additional_false_alarms, cost_savings_usd}}`. ROI: 139.5/0.058 = 2,405:1." | Cost-benefit, trade-off quantification, decision support | 🔴 | 7.3 |

---

## Phase 8: Deployment & Monitoring

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| `ModelPackager.create_model_card` | Model Documentation | `model`, `metrics`, `config` | `model_card.json` | "ModelPackager generates human-readable model documentation. Includes: (1) Model name/version with timestamp, (2) Performance: ROC AUC, tuned recall, threshold, (3) Training data: n_samples, features, class_balance, (4) Intended use, (5) Limitations (temporal drift, adversarial attacks, missing data). Example: `{model_name: 'XGBoost', version: '20260112-093045', performance: {roc_auc: 0.888, recall_at_5pct_fpr: 0.741, threshold: 0.78}}`. Saved as model_card.json for transparency." | Documentation, transparency, reproducibility, audit trail | 🟡 | 8.1 |
| `FeatureDriftDetector.detect_drift` | KL Divergence Monitoring | `reference_distribution`, `production_features`, `scipy.stats` | `DriftReport{kl_scores, alerts}` | "FeatureDriftDetector monitors production feature distributions via KL divergence. Computes `KL(p_prod || p_train)` per feature using histogrammed distributions. Example: Week 1 median(LineOfCode) 850→920 → KL=0.2 (OK). Week 4: 850→1500 → KL=0.8 (DRIFT!). Alert threshold: KL>0.5 → trigger retraining. Returns `{drift_scores: {col: kl_div}, alerts: [{feature, kl_divergence, severity}], requires_retraining: bool}`." | Distribution shift, model degradation, monitoring | 🟡 | 8.2 |
| `PerformanceMonitor.monitor_weekly` | Performance Degradation Tracking | `y_true_sample`, `y_pred_sample`, `baseline_metrics` | `MonitoringReport{alerts, requires_intervention}` | "PerformanceMonitor tracks weekly model performance vs baseline. Computes current_recall, current_fpr from weekly sample. Compares to baseline: (1) Recall degradation >5% → alert + trigger retraining, (2) FPR increase >2% → investigate false alarm surge. Example: Baseline recall=70%, current=64% → degradation=6% >5% → alert. Returns `{current_metrics, baseline_metrics, alerts: [{metric, baseline, current, degradation, action}], requires_intervention: bool}`." | Model degradation, production monitoring, alerting | 🟡 | 8.2 |

---

## Cross-Phase Patterns (Core LOD Patterns)

| Class/Object.Method | LOD Pattern | Dependencies | Artifacts/Outputs | Excellent Application | Key Concepts | Priority | FAQ |
|---------------------|-------------|--------------|-------------------|----------------------|--------------|----------|-----|
| **fit() Paradigm** | Learn Parameters from Training | Training data only | Learned parameters (NOT data) | "CRITICAL LEAKAGE PREVENTION: `fit(df_train)` learns parameters from training ONLY. Stores state: clip_values (99th percentiles), imputers (medians/modes), scaler_params (mean/std), quantile_bins, freq_maps. Returns `self` for chaining. Example: `preprocessor.fit(df_train)` stores `self.scaler_params_['mean'] = df_train.mean()`. NEVER call fit() on val/test/prod—this causes leakage." | Parameter learning, training-only, leakage prevention, state storage | 🔴🔵 | 3.1 |
| **transform() Paradigm** | Apply Learned Parameters | DataFrame + learned parameters | Transformed DataFrame | "Apply LEARNED parameters to any data (val/test/prod). Uses stored state—does NOT recompute. Example: `preprocessor.transform(df_test)` uses `self.scaler_params_['mean']` learned from train. Stateless application—can be called repeatedly. Column alignment via `reindex()` handles schema changes. This is the production inference path." | Inference operation, stateless, production path, reproducibility | 🔴🔵 | 3.1 |
| **fit_transform() Paradigm** | Combined Fit and Transform | Training data | Transformed training data + learned parameters | "Convenience method = `fit()` then `transform()` on training data. Sequence: (1) Learn parameters from df_train, (2) Apply them to df_train. ONLY use on training split. Example: `X_train = preprocessor.fit_transform(df_train)` learns scaler params AND returns scaled train. Enables method chaining: `preprocessor.fit_transform(train).transform(test)`." | Training pipeline, convenience, combined operation | 🔴🔵 | 3.1 |
| **Learned Parameters Storage** | State Management | Training statistics | Serialized parameters (.pkl) | "Store statistics, NOT data: `clip_values_` (dict of 99th percentiles), `imputers_` (dict of medians/modes), `scaler_params_` (dict of means/stds), `columns_` (list of column names). Serialized to `preprocessor.pkl` via pickle. At inference: `preprocessor = pickle.load('preprocessor.pkl'); X_new = preprocessor.transform(df_new)`. Enables reproducible predictions—same input → same output." | State management, serialization, reproducibility, production artifacts | 🔵 | 3.1 |
| **Responsibility (S-V-O)** | Documentation Pattern | Function signature | Precise responsibility statement | "Template: '[Subject] [Verb] [Object] [via/using Method]'. Examples: 'DataLoader loads data and enforces schema contract', 'Preprocessor transforms features via learned scaling parameters', 'ThresholdAnalyzer extracts non-dominated thresholds from sweep'. Benefits: (1) Precise (testable), (2) Single Responsibility Principle, (3) Contract clarity. Used in all responsibility tables." | Documentation, clear contracts, SRP, maintainability | 🔵 | All |
| **Defensive Validation** | Input/Output Checking | DataFrame, assertions | ValidationReport or exception | "Every critical function validates: (1) Input types/shapes (`assert isinstance(df, pd.DataFrame)`), (2) Preconditions (schema, row count, label encoding), (3) Postconditions (no NaNs, row count preserved). Example: `assert not X_train.isna().any().any()` after preprocessing. Benefits: Fail-fast, clear error messages, prevent silent failures. Used in DataLoader, Preprocessor, all validation functions." | Fail-fast, error prevention, quality gates, defensive programming | 🔵 | 0.1, 4.1 |
| **Column Alignment** | Schema Consistency | One-hot encoded DataFrame + stored columns | Aligned DataFrame | "Handle schema changes between train/val/test via `reindex()`. Problem: Test may have 'Industry_healthcare' not in train. Solution: `df_test = df_test.reindex(columns=self.columns_, fill_value=0)`. Ensures test features align exactly with trained model expectations. Prevents: `ValueError: X has 48 features but model expects 50`. Used in `Preprocessor.transform()` after one-hot encoding." | One-hot consistency, inference robustness, production safety | 🔵 | 3.1 |
| **Graceful Degradation** | Fallback Handling | Imputation with edge cases | Robust imputation | "Handle edge cases gracefully. Example: `mode = df[col].mode(); fill_value = mode[0] if len(mode) > 0 else 'unknown'`. If all values missing → mode is empty array → fallback to 'unknown'. At inference: if DomainAge lookup fails → missing flag=1, imputed value=median, model still works (doesn't crash). Prevents production outages on degraded input." | Error handling, robustness, production resilience, fallbacks | 🔵 | 3.1 |
| **ValidationReport Pattern** | Structured Output | Validation logic | Structured dict/JSON | "All validation functions return structured reports, not just bool. Template: `{status: 'pass'/'fail', timestamp, errors: [], warnings: [], metadata: {}}`. Example: `validate_schema()` returns `{is_valid: bool, errors: List[str], columns_found, row_count}`. Benefits: (1) Machine-readable (CI/CD gates), (2) Human-readable (debugging), (3) Audit trail (compliance), (4) Actionable (errors specify what failed)." | Structured output, quality reporting, audit trail, actionability | 🔵 | 0.1, 4.1 |
| **Artifact Persistence** | Output Tracking | Function outputs | Files (.json, .csv, .png, .pkl) | "Every function produces traceable artifacts. Examples: `hypothesis_tests.json` (statistical validation), `threshold_sweep.csv` (tuning analysis), `pareto_curve.png` (visualization), `preprocessor.pkl` (fitted parameters), `model_card.json` (documentation). Benefits: (1) Reproducibility (rerun → same artifacts), (2) Debugging (inspect intermediate results), (3) Audit compliance (trail of decisions), (4) Version control (git track artifacts)." | Traceability, reproducibility, debugging, compliance | 🔵 | All |

---

## Study Priority Guide

### Must Memorize (Top 10 LOD Patterns)

1. 🔴🔵 **fit() vs transform() Paradigm** - Prevents data leakage (FAQ 3.1)
2. 🔴 **FPR-Constrained Tuning** - Explains poor results (FAQ 6.1)
3. 🔴 **Business Cost Calculation** - ROI justification (FAQ 7.3)
4. 🔴 **MNAR Independence Test** - Statistical rigor (FAQ 1.2)
5. 🔴 **Metric Hierarchy Selection** - Model selection (FAQ 5.3)
6. 🔴 **Confusion Matrix Interpretation** - Business translation (FAQ 7.2)
7. 🔴 **XGBoost Training** - Algorithm choice (FAQ 5.1)
8. 🔵 **Learned Parameters Storage** - Production implementation
9. 🔵 **Column Alignment** - Inference robustness
10. 🔵 **Responsibility (S-V-O)** - Documentation quality

### Quick Lookup Index

**By FAQ Number**:
- FAQ 0.1-0.3: Phase 0 (Data Acquisition)
- FAQ 1.1-1.3: Phase 1 (EDA)
- FAQ 2.1-2.2: Phase 2 (Hypothesis Testing)
- FAQ 3.1-3.3: Phase 3 (Feature Engineering & Preprocessing)
- FAQ 4.1-4.2: Phase 4 (Data Splitting)
- FAQ 5.1-5.3: Phase 5 (Model Training & Selection)
- FAQ 6.1-6.3: Phase 6 (Threshold Tuning)
- FAQ 7.1-7.3: Phase 7 (Evaluation & Metrics)
- FAQ 8.1-8.3: Phase 8 (Deployment & Monitoring)

**By Priority**:
- 🔴 CRITICAL: 15 patterns (memorize first)
- 🔵 LOD Core: 10 patterns (implementation-focused)
- 🟡 HIGH: 18 patterns (understand well)
- 🟢 MEDIUM: 8 patterns (know basics)
- ⚪ LOW: 0 patterns (all patterns are relevant)

---

## Usage Notes

**For Interviews**:
1. Start with Class/Object.Method when asked "How did you implement X?"
2. Reference Dependencies to show technical depth
3. Cite Artifacts/Outputs to demonstrate production thinking
4. Use Excellent Application for complete, quotable answers

**For Implementation**:
1. Use LOD Pattern names for code organization
2. Copy Dependencies list for import statements
3. Ensure Artifacts/Outputs match function returns
4. Validate Responsibility (S-V-O) in docstrings

**For Review**:
1. Filter by Priority (🔴🔵 first)
2. Group by FAQ number for topic-based study
3. Cross-reference with original clean-slate document
4. Practice explaining Excellent Application without notes

---

**Version History**:
- v1.0: Initial consolidation with core patterns
- v2.0: Complete drill-down with all Class.Method signatures, dependencies, and artifacts from responsibility tables