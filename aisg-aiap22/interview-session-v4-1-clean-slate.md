
# Interview Session: Maximum LOD Guide (FAQ-Driven Implementation)

**Version**: 1.0  
**Purpose**: Consolidate FAQ-driven learning framework with phase-by-phase implementation patterns  
**Format**: Pseudocode patterns + Responsibility tables + FAQ integration

---

## Table of Contents

1. [Phase 0: Data Acquisition](#phase-0)
2. [Phase 1: Exploratory Data Analysis](#phase-1)
3. [Phase 2: Statistical Hypothesis Testing](#phase-2)
4. [Phase 3: Feature Engineering & Preprocessing](#phase-3)
5. [Phase 4: Data Splitting & Validation](#phase-4)
6. [Phase 5: Model Training & Selection](#phase-5)
7. [Phase 6: Threshold Tuning & Optimization](#phase-6)
8. [Phase 7: Evaluation & Metrics](#phase-7)
9. [Phase 8: Deployment & Monitoring](#phase-8)
10. [FAQ Study Priority Matrix](#faq-priority)

---

## Phase 0: Data Acquisition {#phase-0}

### Pattern: Schema-Validated Data Loading

```
FUNCTION DataLoader.load_from_sqlite({ db_path, expected_schema }) -> { df, validation_report }
  // DataLoader loads data and enforces schema contract
  
  IF NOT file_exists(db_path):
    RAISE FileNotFoundError("Database not found")
  
  conn <- sqlite3.connect(db_path)
  table_name <- detect_table(conn)
  df <- pd.read_sql(f"SELECT * FROM {table_name}", conn)
  
  // Schema validation
  validation <- validate_schema(df, expected_schema)
  IF NOT validation.is_valid:
    RAISE DataQualityError(validation.errors)
  
  // Row count gate
  IF len(df) < MIN_ROWS:
    RAISE DataQualityError(f"Insufficient data: {len(df)} < {MIN_ROWS}")
  
  // Target validation
  unique_labels <- df['label'].unique()
  IF NOT set(unique_labels) == {0, 1}:
    RAISE ValueError(f"Invalid labels: {unique_labels}")
  
  RETURN {
    df: df,
    validation_report: build_report(df, validation)
  }
END

FUNCTION validate_schema({ df, schema }) -> { validation_report }
  // validate_schema checks columns and types against contract
  
  errors <- []
  
  // Check column presence
  missing_cols <- set(schema.keys()) - set(df.columns)
  IF missing_cols:
    errors.append(f"Missing columns: {missing_cols}")
  
  // Check types
  FOR col, expected_type IN schema.items():
    IF col IN df.columns AND df[col].dtype != expected_type:
      errors.append(f"{col}: expected {expected_type}, got {df[col].dtype}")
  
  RETURN {
    is_valid: len(errors) == 0,
    errors: errors,
    columns_found: df.columns.tolist(),
    row_count: len(df)
  }
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/data_loader.py` | `DataLoader` | `load_from_sqlite` | DataLoader loads data and enforces schema contract | `sqlite3`, `pandas`, `expected_schema` | `DataFrame[nxk]`, `ValidationReport` | **FAQ 0.1** |
| `src/data_loader.py` | `DataLoader` | `validate_schema` | validate_schema checks columns and types against contract | `DataFrame`, `SchemaDefinition` | `ValidationReport{is_valid, errors[]}` | **FAQ 0.1** |
| `src/data_loader.py` | `DataLoader` | `check_row_count` | check_row_count enforces minimum viable dataset size | `DataFrame`, `MIN_ROWS=1000` | `bool` or raises exception | **FAQ 0.2** |
| `src/data_loader.py` | `DataLoader` | `parse_target_variable` | parse_target_variable validates label encoding | `DataFrame['label']`, `expected_values={0,1}` | `validated_labels` | **FAQ 0.3** |

### FAQ Integration (Phase 0)

**Study Priority**: ⭐⭐ (Medium - foundational but less frequently asked)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **0.1** | "Why no schema validation?" | "In production I'd implement `validate_schema` with assertions for 46+1 columns and dtype checks. Prevents silent failures if upstream changes schema." | `validate_schema()` above |
| **0.2** | "What if only 500 rows?" | "Below 1000 rows, test set has ~67 phishing cases → ±12% CI too wide. I'd abort with `DataQualityError` and log to alert data engineering team." | `check_row_count()` |
| **0.3** | "How verify target encoding?" | "Assert `unique_labels == {0,1}` and check class counts. Prevents silent failures if encoding changes to {-1,1} or string labels." | `parse_target_variable()` |

---

## Phase 1: Exploratory Data Analysis {#phase-1}

### Pattern: Modular EDA Components

```
CLASS UnivariateAnalyzer:
  // UnivariateAnalyzer computes per-feature statistics and distributions
  
  FUNCTION analyze_missingness({ df }) -> { missingness_report }
    // analyze_missingness computes missing rates and patterns
    
    rates <- df.isna().sum() / len(df)
    
    // Categorize by severity
    severe <- rates[rates > 0.7]
    moderate <- rates[(rates > 0.2) & (rates <= 0.7)]
    low <- rates[(rates > 0) & (rates <= 0.2)]
    
    RETURN {
      rates: rates.to_dict(),
      severe_features: severe.index.tolist(),
      moderate_features: moderate.index.tolist(),
      low_features: low.index.tolist(),
      total_missing_pct: rates.mean()
    }
  END
  
  FUNCTION compute_skewness({ df, numeric_cols }) -> { skewness_report }
    // compute_skewness identifies heavy-tailed distributions
    
    skew_values <- {}
    for col in numeric_cols:
      skew <- df[col].skew()
      skew_values[col] <- {
        skewness: skew,
        severity: "severe" IF abs(skew) > 2 ELSE "moderate" IF abs(skew) > 1 ELSE "low",
        requires_transform: abs(skew) > 1
      }
    
    RETURN skew_values
  END
  
  FUNCTION detect_outliers({ df, numeric_cols, method='IQR' }) -> { outlier_report }
    // detect_outliers identifies extreme values per feature
    
    outliers <- {}
    for col in numeric_cols:
      Q1 <- df[col].quantile(0.25)
      Q3 <- df[col].quantile(0.75)
      IQR <- Q3 - Q1
      lower_bound <- Q1 - 1.5 * IQR
      upper_bound <- Q3 + 1.5 * IQR
      
      outlier_mask <- (df[col] < lower_bound) | (df[col] > upper_bound)
      outliers[col] <- {
        count: outlier_mask.sum(),
        pct: outlier_mask.mean(),
        lower_bound: lower_bound,
        upper_bound: upper_bound
      }
    
    RETURN outliers
  END
END

CLASS BivariateAnalyzer:
  // BivariateAnalyzer computes feature interactions and correlations
  
  FUNCTION compute_correlation_matrix({ df, numeric_cols }) -> { corr_matrix, high_corr_pairs }
    // compute_correlation_matrix calculates pairwise correlations
    
    corr_matrix <- df[numeric_cols].corr()
    
    // Extract high correlation pairs
    high_corr_pairs <- []
    for i, col1 in enumerate(numeric_cols):
      for j, col2 in enumerate(numeric_cols):
        if i < j AND abs(corr_matrix[col1][col2]) > 0.95:
          high_corr_pairs.append({
            feature1: col1,
            feature2: col2,
            correlation: corr_matrix[col1][col2]
          })
    
    RETURN {
      matrix: corr_matrix,
      high_correlations: high_corr_pairs
    }
  END
  
  FUNCTION test_missingness_independence({ df, col, target_col }) -> { chi2_result }
    // test_missingness_independence performs MNAR hypothesis test
    
    df_copy <- df.copy()
    df_copy['is_missing'] <- df_copy[col].isna()
    
    contingency <- pd.crosstab(df_copy['is_missing'], df_copy[target_col])
    chi2, p_value, dof, expected <- scipy.stats.chi2_contingency(contingency)
    
    RETURN {
      chi2_statistic: chi2,
      p_value: p_value,
      is_mnar: p_value < 0.05,
      interpretation: "MNAR" IF p_value < 0.05 ELSE "MAR/MCAR"
    }
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/eda/univariate.py` | `UnivariateAnalyzer` | `analyze_missingness` | UnivariateAnalyzer computes missing rates and categorizes severity | `pandas.DataFrame` | `MissingnessReport{severe[], moderate[], low[]}` | **FAQ 1.1, 1.2** |
| `src/eda/univariate.py` | `UnivariateAnalyzer` | `compute_skewness` | compute_skewness identifies heavy-tailed distributions requiring transform | `DataFrame[numeric_cols]` | `SkewnessReport{col: {skew, requires_transform}}` | **FAQ 3.2** |
| `src/eda/univariate.py` | `UnivariateAnalyzer` | `detect_outliers` | detect_outliers identifies extreme values via IQR method | `DataFrame[numeric_cols]`, `method` | `OutlierReport{col: {count, bounds}}` | **FAQ 3.2** |
| `src/eda/bivariate.py` | `BivariateAnalyzer` | `compute_correlation_matrix` | BivariateAnalyzer calculates pairwise correlations and flags multicollinearity | `DataFrame[numeric_cols]` | `CorrMatrix[nxn]`, `HighCorrPairs[]` | **FAQ 1.3** |
| `src/eda/bivariate.py` | `BivariateAnalyzer` | `test_missingness_independence` | test_missingness_independence performs chi-square MNAR test | `DataFrame`, `col`, `target_col`, `scipy.stats` | `Chi2Result{statistic, p_value, is_mnar}` | **FAQ 1.2** |

### FAQ Integration (Phase 1)

**Study Priority**: ⭐⭐⭐ (High - connects EDA to pipeline)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **1.1** | "Why notebook not `src/eda/`?" | "Notebook appropriate for Task 1. For production, I'd modularize into `UnivariateAnalyzer` and `BivariateAnalyzer` classes for reusability across datasets." | Class structure above |
| **1.2** | "68% missing DomainAge—how handle?" | "Three steps: (1) MNAR test: χ²=450, p<0.001 proves missingness correlates with target. (2) Created `DomainAge_missing` flag. (3) Median imputation for compatibility. Flag carries predictive power." | `test_missingness_independence()` |
| **1.3** | "How use correlations?" | "Three uses: (1) Feature selection by |r| with target. (2) Multicollinearity check: drop if r>0.98. (3) Leakage detection: check for r≈1.0. Limitation: Pearson only captures linear." | `compute_correlation_matrix()` |

---

## Phase 2: Statistical Hypothesis Testing {#phase-2}

### Pattern: Automated Hypothesis Testing Suite

```
CLASS HypothesisTester:
  // HypothesisTester performs statistical validation of data assumptions
  
  CONSTRUCTOR({ alpha=0.05 }):
    self.alpha <- alpha
    self.results <- {}
  END
  
  FUNCTION test_class_balance_significance({ y, null_prob=0.5 }) -> { test_result }
    // test_class_balance_significance validates imbalance is not sampling noise
    
    observed <- np.bincount(y)
    expected <- np.array([null_prob, 1-null_prob]) * len(y)
    
    chi2, p_value <- scipy.stats.chisquare(observed, expected)
    
    result <- {
      test: "class_balance",
      h0: f"P(phishing) = {null_prob}",
      observed_counts: observed.tolist(),
      observed_proportions: (observed / len(y)).tolist(),
      chi2_statistic: chi2,
      p_value: p_value,
      reject_h0: p_value < self.alpha,
      conclusion: "Significant imbalance" IF p_value < self.alpha ELSE "Balanced"
    }
    
    self.results["class_balance"] <- result
    RETURN result
  END
  
  FUNCTION test_mnar_hypothesis({ df, col, target_col }) -> { test_result }
    // test_mnar_hypothesis determines if missingness depends on target class
    
    df_copy <- df.copy()
    df_copy['is_missing'] <- df_copy[col].isna().astype(int)
    
    contingency <- pd.crosstab(df_copy['is_missing'], df_copy[target_col])
    chi2, p_value, dof, expected <- scipy.stats.chi2_contingency(contingency)
    
    miss_rate_by_class <- df_copy.groupby(target_col)['is_missing'].mean()
    
    result <- {
      test: "mnar_independence",
      feature: col,
      h0: f"Missingness in {col} independent of target",
      contingency_table: contingency.to_dict(),
      missingness_rate_by_class: miss_rate_by_class.to_dict(),
      chi2_statistic: chi2,
      p_value: p_value,
      reject_h0: p_value < self.alpha,
      conclusion: "MNAR" IF p_value < self.alpha ELSE "MAR/MCAR"
    }
    
    self.results[f"mnar_{col}"] <- result
    RETURN result
  END
  
  FUNCTION validate_stratified_splits({ y_full, splits_dict }) -> { validation_result }
    // validate_stratified_splits confirms splits preserve class distribution
    
    full_dist <- np.bincount(y_full) / len(y_full)
    results <- {}
    
    for split_name, y_split in splits_dict.items():
      observed <- np.bincount(y_split)
      expected <- full_dist * len(y_split)
      chi2, p_value <- scipy.stats.chisquare(observed, expected)
      
      results[split_name] <- {
        chi2: chi2,
        p_value: p_value,
        is_stratified: p_value > self.alpha,
        observed_pct: (observed / observed.sum()).tolist(),
        expected_pct: full_dist.tolist()
      }
    
    self.results["stratification"] <- results
    RETURN results
  END
  
  FUNCTION save_results({ filepath="results/hypothesis_tests.json" }) -> void:
    // save_results persists all test results for audit trail
    
    write_json(self.results, filepath)
    log.info(f"Hypothesis tests saved to {filepath}")
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/hypothesis_tester.py` | `HypothesisTester` | `test_class_balance_significance` | HypothesisTester validates imbalance is not sampling noise via chi-square | `scipy.stats.chisquare`, `y`, `null_prob` | `TestResult{chi2, p_value, reject_h0}` | **FAQ 2.1** |
| `src/hypothesis_tester.py` | `HypothesisTester` | `test_mnar_hypothesis` | test_mnar_hypothesis determines if missingness depends on target class | `scipy.stats.chi2_contingency`, `DataFrame` | `MNARResult{chi2, p_value, is_mnar}` | **FAQ 1.2, 2.1** |
| `src/hypothesis_tester.py` | `HypothesisTester` | `validate_stratified_splits` | validate_stratified_splits confirms splits preserve class distribution | `scipy.stats.chisquare`, `y_full`, `splits_dict` | `StratificationReport{per_split: {chi2, p_value}}` | **FAQ 4.1** |
| `src/hypothesis_tester.py` | `HypothesisTester` | `save_results` | save_results persists all test results for audit trail | `json`, `filepath` | `hypothesis_tests.json` | **FAQ 2.2** |

### FAQ Integration (Phase 2)

**Study Priority**: ⭐⭐⭐ (High - demonstrates statistical rigor)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **2.1** | "Test class imbalance significance?" | "Chi-square test: H₀: P(phishing)=0.5. Observed: [6050, 4950]. χ²=110, p<0.001 → reject H₀. Imbalance is real, not sampling noise. Pipeline impact: stratified splits, focus on recall." | `test_class_balance_significance()` |
| **2.2** | "Why no HypothesisTester module?" | "Gap acknowledged. Would implement for CI/CD gates: automated validation on new data, audit trail via hypothesis_tests.json, fail pipeline if assumptions violated. ~2 hours to implement." | Full `HypothesisTester` class |

---

## Phase 3: Feature Engineering & Preprocessing {#phase-3}

### Pattern: Leakage-Free Preprocessing Pipeline

```
CLASS FeatureEngineer:
  // FeatureEngineer creates domain-specific features from raw data
  
  CONSTRUCTOR({ enable_flags=True, enable_bins=True, enable_ratios=True }):
    self.enable_flags <- enable_flags
    self.enable_bins <- enable_bins
    self.enable_ratios <- enable_ratios
    self.quantile_bins <- None  // Learned from train
    self.freq_maps <- None      // Learned from train
  END
  
  FUNCTION fit({ df_train }) -> self:
    // fit learns feature engineering parameters from training data only
    
    IF self.enable_bins:
      // Learn quantile bin edges from train
      numeric_cols <- df_train.select_dtypes('number').columns
      self.quantile_bins <- {}
      for col in numeric_cols:
        self.quantile_bins[col] <- df_train[col].quantile([0.25, 0.5, 0.75])
    
    IF self.enable_frequency_encoding:
      // Learn frequency maps from train
      cat_cols <- df_train.select_dtypes('object').columns
      self.freq_maps <- {}
      for col in cat_cols:
        value_counts <- df_train[col].value_counts()
        self.freq_maps[col] <- value_counts / len(df_train)
    
    RETURN self
  END
  
  FUNCTION transform({ df }) -> { df_engineered }:
    // transform applies learned feature engineering to data
    
    df_out <- df.copy()
    
    IF self.enable_flags:
      df_out <- create_missing_flags(df_out)
    
    IF self.enable_bins:
      df_out <- create_domain_age_bins(df_out)
      df_out <- apply_quantile_bins(df_out, self.quantile_bins)
    
    IF self.enable_ratios:
      df_out <- create_external_self_ratio(df_out)
    
    RETURN df_out
  END
  
  FUNCTION create_missing_flags({ df }) -> { df_with_flags }:
    // create_missing_flags generates MNAR indicators
    
    mnar_cols <- ['DomainAgeMonths', 'Robots', 'IsResponsive']
    for col in mnar_cols:
      IF col IN df.columns:
        df[f"{col}_missing"] <- df[col].isna().astype(int)
    
    RETURN df
  END
  
  FUNCTION create_external_self_ratio({ df }) -> { df_with_ratio }:
    // create_external_self_ratio computes predictive ratio feature
    
    IF 'NoOfExternalRef' IN df.columns AND 'NoOfSelfRef' IN df.columns:
      df['ExternalSelfRatio'] <- df['NoOfExternalRef'] / (df['NoOfSelfRef'] + 1)
    
    RETURN df
  END
END

CLASS Preprocessor:
  // Preprocessor handles missing values, encoding, and scaling
  
  CONSTRUCTOR({ clip_quantile=0.99, impute_strategy='median', scale_method='standard' }):
    self.clip_quantile <- clip_quantile
    self.impute_strategy <- impute_strategy
    self.scale_method <- scale_method
    self.clip_values <- None
    self.imputers <- None
    self.scaler_params <- None
    self.columns <- None
  END
  
  FUNCTION fit_transform({ df_train }) -> { X_train, y_train }:
    // fit_transform learns preprocessing parameters from train and applies them
    
    y_train <- df_train['label']
    df_features <- df_train.drop('label', axis=1)
    
    numeric_cols <- df_features.select_dtypes('number').columns
    cat_cols <- df_features.select_dtypes('object').columns
    
    // Learn and apply log-clipping
    self.clip_values <- {}
    for col in numeric_cols:
      self.clip_values[col] <- df_features[col].quantile(self.clip_quantile)
    df_features[numeric_cols] <- _log_clip(df_features[numeric_cols], self.clip_values)
    
    // Learn and apply imputation
    self.imputers <- {
      'numeric': df_features[numeric_cols].median(),
      'categorical': df_features[cat_cols].mode().iloc[0]
    }
    df_features <- _impute(df_features, self.imputers)
    
    // Apply one-hot encoding
    df_features <- pd.get_dummies(df_features, columns=cat_cols)
    self.columns <- df_features.columns.tolist()
    
    // Learn and apply scaling
    self.scaler_params <- {
      'mean': df_features.mean(),
      'std': df_features.std()
    }
    X_train <- _scale(df_features, self.scaler_params, self.scale_method)
    
    RETURN X_train, y_train
  END
  
  FUNCTION transform({ df_new }) -> { X_new, y_new }:
    // transform applies learned parameters to new data (val/test)
    
    y_new <- df_new['label']
    df_features <- df_new.drop('label', axis=1)
    
    // Apply log-clipping with TRAIN-LEARNED clip values
    numeric_cols <- df_features.select_dtypes('number').columns
    df_features[numeric_cols] <- _log_clip(df_features[numeric_cols], self.clip_values)
    
    // Apply imputation with TRAIN-LEARNED imputers
    df_features <- _impute(df_features, self.imputers)
    
    // Apply one-hot encoding
    cat_cols <- df_features.select_dtypes('object').columns
    df_features <- pd.get_dummies(df_features, columns=cat_cols)
    
    // Align columns with train
    df_features <- df_features.reindex(columns=self.columns, fill_value=0)
    
    // Apply scaling with TRAIN-LEARNED params
    X_new <- _scale(df_features, self.scaler_params, self.scale_method)
    
    RETURN X_new, y_new
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/feature_engineering.py` | `FeatureEngineer` | `fit` | FeatureEngineer learns quantile bins and frequency maps from training data | `DataFrame[train]` | `self.quantile_bins`, `self.freq_maps` | **FAQ 3.1** |
| `src/feature_engineering.py` | `FeatureEngineer` | `transform` | transform applies learned feature engineering to data | `DataFrame`, learned parameters | `DataFrame[engineered]` | **FAQ 3.3** |
| `src/feature_engineering.py` | `FeatureEngineer` | `create_missing_flags` | create_missing_flags generates MNAR indicators for predictive missingness | `DataFrame` | `DataFrame[with *_missing columns]` | **FAQ 1.2, 3.1** |
| `src/feature_engineering.py` | `FeatureEngineer` | `create_external_self_ratio` | create_external_self_ratio computes domain-specific ratio feature | `DataFrame[NoOfExternalRef, NoOfSelfRef]` | `DataFrame[with ExternalSelfRatio]` | **FAQ 3.3** |
| `src/preprocessing.py` | `Preprocessor` | `fit_transform` | Preprocessor learns preprocessing parameters from train and applies them | `DataFrame[train]` | `X_train[scaled]`, `y_train`, learned parameters | **FAQ 3.1, 3.2** |
| `src/preprocessing.py` | `Preprocessor` | `transform` | transform applies learned parameters to new data without refitting | `DataFrame[val/test]`, learned parameters | `X_new[scaled]`, `y_new` | **FAQ 3.1** |
| `src/preprocessing.py` | `Preprocessor` | `_log_clip` | _log_clip applies log1p transform after clipping outliers | `DataFrame[numeric]`, `clip_values` | `DataFrame[transformed]` | **FAQ 3.2** |
| `src/preprocessing.py` | `Preprocessor` | `_impute` | _impute fills missing values with train-learned statistics | `DataFrame`, `imputers` | `DataFrame[no_missing]` | **FAQ 3.2** |
| `src/preprocessing.py` | `Preprocessor` | `_scale` | _scale standardizes features using train-learned mean/std | `DataFrame`, `scaler_params` | `ndarray[scaled]` | **FAQ 3.2** |

### FAQ Integration (Phase 3)

**Study Priority**: ⭐⭐⭐⭐⭐ (CRITICAL - #1 most asked question)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **3.1** | "Why preprocessing on full dataset?" | "**DATA LEAKAGE**: Scaler learned mean from test set → optimistic bias. Fix: `df → split → fit(train) → transform(val/test)`. Impact: test recall drops 3-7% to reflect true performance." | `fit_transform()` vs `transform()` pattern |
| **3.2** | "Why log-transform and clip?" | "EDA: 10 features |skew|>2 → heavy tails. Strategy: clip at 99th percentile (train-learned) → log1p. Validation: median skew drops 1.8→0.4. Stabilizes variance for linear models." | `_log_clip()` |
| **3.3** | "How design ExternalSelfRatio?" | "Hypothesis: phishing sites have high external links. EDA: phishing median=8.3 vs legit=2.1, t-test p<0.001. Formula: `Ext/(Self+1)` preserves dynamic range. Feature importance: #3 in XGBoost." | `create_external_self_ratio()` |

---

## Phase 4: Data Splitting & Validation {#phase-4}

### Pattern: Stratified Splitting with Statistical Validation

```
FUNCTION stratified_split({ df, test_size=0.15, val_size=0.15, random_state=42 }) -> { df_train, df_val, df_test }:
  // stratified_split partitions data preserving class distribution
  
  y <- df['label'].values
  unique_classes <- np.unique(y)
  
  train_indices <- []
  val_indices <- []
  test_indices <- []
  
  rng <- np.random.default_rng(random_state)
  
  FOR class_label IN unique_classes:
    // Get indices for this class
    class_indices <- np.where(y == class_label)[0]
    n_class <- len(class_indices)
    
    // Shuffle within class
    rng.shuffle(class_indices)
    
    // Compute split sizes
    n_test <- int(n_class * test_size)
    n_val <- int(n_class * val_size)
    n_train <- n_class - n_test - n_val
    
    // Partition indices
    test_indices.extend(class_indices[:n_test])
    val_indices.extend(class_indices[n_test:n_test+n_val])
    train_indices.extend(class_indices[n_test+n_val:])
  END
  
  RETURN {
    df_train: df.iloc[train_indices],
    df_val: df.iloc[val_indices],
    df_test: df.iloc[test_indices]
  }
END

FUNCTION validate_processed({ X_train, X_val, X_test, y_train, y_val, y_test }) -> { validation_report }:
  // validate_processed performs quality checks and stratification tests
  
  // Check for missing values
  no_missing <- {
    'train': NOT X_train.isna().any().any(),
    'val': NOT X_val.isna().any().any(),
    'test': NOT X_test.isna().any().any()
  }
  
  // Compute label proportions
  label_props <- {
    'train': compute_class_proportions(y_train),
    'val': compute_class_proportions(y_val),
    'test': compute_class_proportions(y_test)
  }
  
  // Statistical stratification test
  y_full <- np.concatenate([y_train, y_val, y_test])
  strat_results <- validate_stratification(y_full, y_train, y_val, y_test)
  
  RETURN {
    no_missing: no_missing,
    label_proportions: label_props,
    stratification: strat_results
  }
END

FUNCTION validate_stratification({ y_full, y_train, y_val, y_test, alpha=0.05 }) -> { chi2_results }:
  // validate_stratification performs chi-square tests per split
  
  full_dist <- np.bincount(y_full) / len(y_full)
  results <- {}
  
  FOR name, y_split IN [("train", y_train), ("val", y_val), ("test", y_test)]:
    observed <- np.bincount(y_split)
    expected <- full_dist * len(y_split)
    chi2, p_value <- scipy.stats.chisquare(observed, expected)
    
    results[name] <- {
      chi2: chi2,
      p_value: p_value,
      is_stratified: p_value > alpha,
      observed_pct: (observed / observed.sum()).tolist(),
      expected_pct: full_dist.tolist()
    }
  END
  
  RETURN results
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/data_splitter.py` | (module) | `stratified_split` | stratified_split partitions data preserving class distribution | `numpy.random`, `DataFrame` | `df_train`, `df_val`, `df_test` | **FAQ 4.1, 4.2** |
| `src/pipeline_validator.py` | (module) | `validate_processed` | validate_processed performs quality checks and stratification tests | `DataFrame`, `scipy.stats` | `ValidationReport{no_missing, stratification}` | **FAQ 4.1** |
| `src/pipeline_validator.py` | (module) | `validate_stratification` | validate_stratification performs chi-square tests per split | `scipy.stats.chisquare`, `y_arrays` | `Chi2Results{per_split: {chi2, p_value, is_stratified}}` | **FAQ 4.1** |

### FAQ Integration (Phase 4)

**Study Priority**: ⭐⭐⭐ (High - demonstrates statistical validation)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **4.1** | "Verify stratification worked?" | "Chi-square test per split vs full distribution. Train p=0.08, val p=0.76, test p=0.82; all >0.05 → cannot reject H₀ (stratification successful). Confirms splits are representative." | `validate_stratification()` |
| **4.2** | "Risk of 70/15/15?" | "15% test = 1650 rows → 742 phishing → recall 95% CI ±3.6% (acceptable precision). Risk: if dataset shrinks to 1000 rows → 67 phishing → CI ±12% (too wide). Alternative: 60/20/20 for more stable test metrics." | `stratified_split()` proportions |

---

## Phase 5: Model Training & Selection {#phase-5}

### Pattern: Model Comparison Framework

```
CLASS LogisticRegressionModel:
  // LogisticRegressionModel implements custom gradient descent classifier
  
  CONSTRUCTOR({ learning_rate=0.01, n_epochs=1000, l2_lambda=1.0, random_state=42 }):
    self.lr <- learning_rate
    self.epochs <- n_epochs
    self.l2_lambda <- l2_lambda
    self.weights <- None
    self.bias <- None
  END
  
  FUNCTION fit({ X_train, y_train }) -> self:
    // fit trains model via gradient descent with L2 regularization
    
    n_samples, n_features <- X_train.shape
    self.weights <- np.random.randn(n_features) * 0.01
    self.bias <- 0.0
    
    FOR epoch IN range(self.epochs):
      // Forward pass
      z <- X_train @ self.weights + self.bias
      y_pred <- sigmoid(z)
      
      // Compute loss (log-loss + L2 penalty)
      loss <- -np.mean(y_train * np.log(y_pred + 1e-10) + 
                       (1 - y_train) * np.log(1 - y_pred + 1e-10)) + 
              self.l2_lambda * np.sum(self.weights ** 2)
      
      // Backward pass (gradients)
      dw <- (X_train.T @ (y_pred - y_train)) / n_samples + 2 * self.l2_lambda * self.weights
      db <- np.mean(y_pred - y_train)
      
      // Update weights
      self.weights <- self.weights - self.lr * dw
      self.bias <- self.bias - self.lr * db
    END
    
    RETURN self
  END
  
  FUNCTION predict_proba({ X }) -> { probabilities }:
    // predict_proba returns class probabilities
    
    z <- X @ self.weights + self.bias
    prob_class1 <- sigmoid(z)
    prob_class0 <- 1 - prob_class1
    
    RETURN np.column_stack([prob_class0, prob_class1])
  END
END

CLASS ModelSelector:
  // ModelSelector compares models and selects best for deployment
  
  FUNCTION compare_models({ metrics_list }) -> { comparison_report }:
    // compare_models ranks models by business-driven metric hierarchy
    
    // Priority: tuned_recall > FPR > ROC_AUC > PR_AUC
    ranked <- []
    FOR metrics IN metrics_list:
      score <- {
        model_name: metrics['model'],
        tuned_recall: metrics['tuned']['best_recall']['recall'],
        tuned_fpr: metrics['tuned']['best_recall']['fpr'],
        roc_auc: metrics['roc_auc'],
        pr_auc: metrics['pr_auc']
      }
      ranked.append(score)
    END
    
    // Sort by recall DESC, then FPR ASC, then ROC AUC DESC
    ranked.sort(key=lambda x: (-x['tuned_recall'], x['tuned_fpr'], -x['roc_auc']))
    
    RETURN {
      best_model: ranked[0]['model_name'],
      ranking: ranked,
      selection_criteria: "Maximize recall under FPR constraint, then minimize FPR, then maximize AUC"
    }
  END
  
  FUNCTION select_best({ metrics_list }) -> { best_model_metrics }:
    // select_best returns top-ranked model for deployment
    
    comparison <- compare_models(metrics_list)
    best_name <- comparison['best_model']
    best_metrics <- [m FOR m IN metrics_list IF m['model'] == best_name][0]
    
    RETURN best_metrics
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `fit` | LogisticRegressionModel trains model via gradient descent with L2 regularization | `numpy`, `X_train`, `y_train` | `self.weights`, `self.bias` | **FAQ 5.1** |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `predict_proba` | predict_proba returns class probabilities via sigmoid | `numpy`, `X`, `self.weights` | `probabilities[n×2]` | **FAQ 5.1** |
| `src/models/knn.py` | `KNNModel` | `fit` | KNNModel stores training data for lazy learning | `X_train`, `y_train` | `self.X_train`, `self.y_train` | **FAQ 5.2** |
| `src/models/xgboost_model.py` | `XGBoostModel` | `fit` | XGBoostModel wraps xgboost.XGBClassifier for training | `xgboost`, `X_train`, `y_train`, `params` | `self.model` | **FAQ 5.1, 5.3** |
| `src/model_selector.py` | `ModelSelector` | `compare_models` | ModelSelector ranks models by business-driven metric hierarchy | `metrics_list` | `ComparisonReport{ranking, criteria}` | **FAQ 5.3** |
| `src/model_selector.py` | `ModelSelector` | `select_best` | select_best returns top-ranked model for deployment | `metrics_list` | `best_model_metrics` | **FAQ 5.3** |

### FAQ Integration (Phase 5)

**Study Priority**: ⭐⭐⭐⭐ (Very High - core ML understanding)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **5.1** | "Why these 3 models?" | "**Logistic**: 82.5% AUC, interpretable, 2s train. **KNN**: 80.9% AUC, non-parametric, 50ms inference (slow). **XGBoost**: 88.8% AUC, handles interactions, 18s train. Choice: XGBoost for +6% AUC = 13.5K more attacks caught monthly." | Model comparison in `compare_models()` |
| **5.2** | "KNN has null tuned metrics?" | "Two hypotheses: (1) optimization disabled in config, (2) predict_proba shape error. Debug: check `proba.shape == (n_test, 2)`. Fix predict_proba or enable optimization. Given lower AUC, wouldn't be selected anyway." | `KNNModel` structure |
| **5.3** | "Best model selection?" | "Metric hierarchy: (1) tuned recall @ FPR≤5% (business constraint), (2) FPR (minimize false alarms), (3) ROC AUC (discrimination power). XGBoost: 74.1% recall > Logistic 71.2% > KNN 68.5%." | `select_best()` sorting logic |

---

## Phase 6: Threshold Tuning & Optimization {#phase-6}

### Pattern: FPR-Constrained Threshold Optimization

```
FUNCTION evaluate_tuned({ y_true, y_proba, max_fpr=0.05, thresholds_len=1001 }) -> { tuned_metrics }:
  // evaluate_tuned finds optimal threshold maximizing recall under FPR constraint
  
  thresholds <- np.linspace(1.0, 0.0, thresholds_len)
  best_recall <- {threshold: None, recall: 0, fpr: 1, f1: 0}
  best_f1 <- {threshold: None, recall: 0, fpr: 1, f1: 0}
  
  FOR t IN thresholds:
    y_pred <- (y_proba >= t).astype(int)
    tn, fp, fn, tp <- confusion_matrix(y_true, y_pred).ravel()
    
    fpr <- fp / (fp + tn) IF (fp + tn) > 0 ELSE 0
    recall <- tp / (tp + fn) IF (tp + fn) > 0 ELSE 0
    precision <- tp / (tp + fp) IF (tp + fp) > 0 ELSE 0
    f1 <- 2 * precision * recall / (precision + recall) IF (precision + recall) > 0 ELSE 0
    
    // Track best recall under FPR constraint
    IF fpr <= max_fpr AND recall > best_recall['recall']:
      best_recall <- {threshold: t, recall: recall, fpr: fpr, f1: f1}
    
    // Track best F1 under FPR constraint
    IF fpr <= max_fpr AND f1 > best_f1['f1']:
      best_f1 <- {threshold: t, recall: recall, fpr: fpr, f1: f1}
  END
  
  RETURN {
    best_recall: best_recall,
    best_f1: best_f1,
    constraint: f"FPR ≤ {max_fpr}"
  }
END

CLASS ThresholdAnalyzer:
  // ThresholdAnalyzer performs Pareto analysis on threshold sweep
  
  FUNCTION compute_pareto_frontier({ threshold_sweep_df }) -> { pareto_df }:
    // compute_pareto_frontier extracts non-dominated thresholds
    
    df <- threshold_sweep_df.sort_values(['fpr', 'recall'], ascending=[True, False])
    
    pareto_points <- []
    max_recall_seen <- -1
    
    FOR _, row IN df.iterrows():
      IF row['recall'] > max_recall_seen:
        pareto_points.append(row)
        max_recall_seen <- row['recall']
    END
    
    RETURN pd.DataFrame(pareto_points)
  END
  
  FUNCTION plot_pareto_curve({ sweep_df, chosen_threshold, save_path }) -> { pareto_df }:
    // plot_pareto_curve visualizes recall-FPR trade-off
    
    pareto_df <- compute_pareto_frontier(sweep_df)
    
    fig, ax <- plt.subplots(figsize=(10, 6))
    
    // All thresholds (gray)
    ax.scatter(sweep_df['fpr'] * 100, sweep_df['recall'] * 100, c='lightgray', alpha=0.5)
    
    // Pareto frontier (red line)
    ax.plot(pareto_df['fpr'] * 100, pareto_df['recall'] * 100, 'r-o', linewidth=2)
    
    // Chosen threshold (green star)
    IF chosen_threshold:
      chosen <- sweep_df[sweep_df['threshold'] == chosen_threshold].iloc[0]
      ax.scatter(chosen['fpr'] * 100, chosen['recall'] * 100, c='green', s=200, marker='*')
    
    // Business constraint (blue line)
    ax.axvline(x=5.0, color='blue', linestyle='--', label='FPR≤5% constraint')
    
    ax.set_xlabel('False Positive Rate (%)')
    ax.set_ylabel('Recall (%)')
    ax.set_title('Pareto Frontier: Recall-FPR Trade-off')
    ax.legend()
    plt.savefig(save_path)
    
    RETURN pareto_df
  END
  
  FUNCTION analyze_business_constraints({ pareto_df, max_fpr=0.05 }) -> { analysis }:
    // analyze_business_constraints finds optimal threshold under constraint
    
    acceptable <- pareto_df[pareto_df['fpr'] <= max_fpr]
    
    IF len(acceptable) == 0:
      RETURN {error: f"No threshold achieves FPR ≤ {max_fpr}"}
    
    optimal <- acceptable.loc[acceptable['recall'].idxmax()]
    
    RETURN {
      max_fpr_constraint: max_fpr,
      optimal_threshold: optimal['threshold'],
      achieved_recall: optimal['recall'],
      achieved_fpr: optimal['fpr'],
      interpretation: f"{optimal['recall']:.1%} recall at {optimal['fpr']:.1%} FPR"
    }
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/evaluation.py` | (module) | `evaluate_tuned` | evaluate_tuned finds optimal threshold maximizing recall under FPR constraint | `numpy`, `sklearn.metrics`, `y_true`, `y_proba` | `TunedMetrics{best_recall, best_f1}` | **FAQ 6.1, 6.2** |
| `src/threshold_analyzer.py` | `ThresholdAnalyzer` | `compute_pareto_frontier` | ThresholdAnalyzer extracts non-dominated thresholds from sweep | `DataFrame[threshold, recall, fpr]` | `DataFrame[pareto_points]` | **FAQ 6.3** |
| `src/threshold_analyzer.py` | `ThresholdAnalyzer` | `plot_pareto_curve` | plot_pareto_curve visualizes recall-FPR trade-off with annotations | `matplotlib`, `sweep_df`, `chosen_threshold` | `pareto_curve.png` | **FAQ 6.3** |
| `src/threshold_analyzer.py` | `ThresholdAnalyzer` | `analyze_business_constraints` | analyze_business_constraints finds optimal threshold under FPR limit | `pareto_df`, `max_fpr` | `ConstraintAnalysis{optimal_threshold, achieved_recall}` | **FAQ 6.1, 6.3** |

### FAQ Integration (Phase 6)

**Study Priority**: ⭐⭐⭐⭐⭐ (CRITICAL - explains poor results)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **6.1** | "Why max_fpr=0.03 not 0.05?" | "**WRONG KPI**: 0.03→12% recall catches 54/450 attacks. 0.05→74% recall catches 333/450 attacks (261 more!). Business impact: $139.5M monthly savings. Fix: change config.yaml to max_fpr: 0.05." | `evaluate_tuned()` constraint parameter |
| **6.2** | "How threshold tuning works?" | "Algorithm: (1) Generate 1001 thresholds [1.0→0.0]. (2) For each, compute FPR and recall. (3) Filter to FPR≤max_fpr. (4) Select threshold with max recall. Output: threshold_sweep.csv with all (t, recall, FPR) triplets." | Full `evaluate_tuned()` function |
| **6.3** | "What is Pareto analysis?" | "Pareto frontier = thresholds where can't improve recall without increasing FPR. Computed by sorting by FPR, keeping points with higher recall than previous. Used to visualize trade-offs for stakeholders." | `compute_pareto_frontier()` + `plot_pareto_curve()` |

---

## Phase 7: Evaluation & Metrics {#phase-7}

### Pattern: Business-Aware Evaluation

```
FUNCTION evaluate({ model, X_test, y_test }) -> { metrics }:
  // evaluate computes comprehensive classification metrics
  
  y_pred <- model.predict(X_test)
  y_proba <- model.predict_proba(X_test)[:, 1]
  
  tn, fp, fn, tp <- confusion_matrix(y_test, y_pred).ravel()
  
  metrics <- {
    // Confusion matrix
    confusion_matrix: [[tn, fp], [fn, tp]],
    
    // Rates
    fpr: fp / (fp + tn),
    recall: tp / (tp + fn),
    precision: tp / (tp + fp) IF (tp + fp) > 0 ELSE 0,
    specificity: tn / (tn + fp),
    
    // Composite metrics
    f1: 2 * precision * recall / (precision + recall) IF (precision + recall) > 0 ELSE 0,
    
    // Threshold-independent metrics
    roc_auc: roc_auc_score(y_test, y_proba),
    pr_auc: average_precision_score(y_test, y_proba),
    brier: brier_score_loss(y_test, y_proba),
    
    // Per-class report
    classification_report: classification_report(y_test, y_pred, output_dict=True)
  }
  
  RETURN metrics
END

CLASS BusinessImpactCalculator:
  // BusinessImpactCalculator translates confusion matrix to business costs
  
  CONSTRUCTOR({ fraud_loss_per_fn=500, support_cost_per_fp=5, monthly_volume=1_000_000 }):
    self.fraud_loss <- fraud_loss_per_fn
    self.support_cost <- support_cost_per_fp
    self.volume <- monthly_volume
  END
  
  FUNCTION calculate({ confusion_matrix, phishing_rate=0.45 }) -> { impact }:
    // calculate translates confusion matrix to monthly business costs
    
    tn, fp, fn, tp <- confusion_matrix.ravel()
    
    // Scale to monthly volume
    monthly_phishing <- self.volume * phishing_rate
    monthly_legit <- self.volume * (1 - phishing_rate)
    
    scale_phishing <- monthly_phishing / (tp + fn)
    scale_legit <- monthly_legit / (tn + fp)
    
    monthly_fn <- fn * scale_phishing
    monthly_fp <- fp * scale_legit
    monthly_tp <- tp * scale_phishing
    
    // Calculate costs
    fraud_exposure <- monthly_fn * self.fraud_loss
    support_costs <- monthly_fp * self.support_cost
    total_cost <- fraud_exposure + support_costs
    
    // Calculate value
    fraud_prevented <- monthly_tp * self.fraud_loss
    
    RETURN {
      monthly_phishing_attacks: monthly_phishing,
      attacks_caught: monthly_tp,
      attacks_missed: monthly_fn,
      false_alarms: monthly_fp,
      fraud_exposure_usd: fraud_exposure,
      support_cost_usd: support_costs,
      total_monthly_cost_usd: total_cost,
      fraud_prevented_usd: fraud_prevented,
      catch_rate_pct: (monthly_tp / monthly_phishing) * 100
    }
  END
  
  FUNCTION compare_thresholds({ cm_strict, cm_benchmark }) -> { comparison }:
    // compare_thresholds quantifies business impact of threshold change
    
    strict <- calculate(cm_strict)
    benchmark <- calculate(cm_benchmark)
    
    RETURN {
      strict_3pct_fpr: strict,
      benchmark_5pct_fpr: benchmark,
      delta: {
        additional_attacks_caught: benchmark['attacks_caught'] - strict['attacks_caught'],
        additional_false_alarms: benchmark['false_alarms'] - strict['false_alarms'],
        cost_savings_usd: strict['total_monthly_cost_usd'] - benchmark['total_monthly_cost_usd']
      }
    }
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `src/evaluation.py` | (module) | `evaluate` | evaluate computes comprehensive classification metrics from predictions | `sklearn.metrics`, `model`, `X_test`, `y_test` | `Metrics{cm, FPR, recall, ROC_AUC, PR_AUC}` | **FAQ 7.1, 7.2** |
| `src/business_impact.py` | `BusinessImpactCalculator` | `calculate` | BusinessImpactCalculator translates confusion matrix to monthly business costs | `confusion_matrix`, `phishing_rate`, `cost_params` | `ImpactReport{fraud_exposure, support_cost, catch_rate}` | **FAQ 7.3** |
| `src/business_impact.py` | `BusinessImpactCalculator` | `compare_thresholds` | compare_thresholds quantifies business impact of threshold change | `cm_strict`, `cm_benchmark` | `ComparisonReport{delta: {cost_savings, attacks_caught}}` | **FAQ 7.3** |

### FAQ Integration (Phase 7)

**Study Priority**: ⭐⭐⭐⭐ (Very High - demonstrates business thinking)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **7.1** | "Why ROC AUC?" | "Threshold-independent summary of discrimination power. AUC=0.888 means 88.8% chance model ranks random phishing > random legit. Also report PR AUC (0.847) for imbalanced classes. Together give complete picture." | `evaluate()` metrics |
| **7.2** | "What does confusion matrix tell you?" | "TP=119, FN=874 → catching only 12% of attacks (87.7% miss rate). Business: 874 missed attacks = $437K fraud exposure. Problem: threshold=0.97 too conservative. Fix: lower to 0.78 → TP=695, FN=298 → 70% recall." | Confusion matrix interpretation |
| **7.3** | "Calculate business impact?" | "FN × $500 fraud_loss + FP × $5 support_cost. Current (thresh=0.97): $198M fraud + $77K support = $198.1M monthly. Benchmark (thresh=0.78): $58.5M fraud + $135K support = $58.6M. Savings: $139.5M monthly." | `BusinessImpactCalculator.calculate()` |

---

## Phase 8: Deployment & Monitoring {#phase-8}

### Pattern: Production-Ready Deployment (Conceptual)

```
CLASS ModelPackager:
  // ModelPackager serializes model and dependencies for deployment
  
  FUNCTION create_model_card({ model, metrics, config }) -> { model_card }:
    // create_model_card generates human-readable model documentation
    
    RETURN {
      model_name: model.__class__.__name__,
      version: datetime.now().strftime("%Y%m%d-%H%M%S"),
      performance: {
        roc_auc: metrics['roc_auc'],
        recall_at_5pct_fpr: metrics['tuned']['best_recall']['recall'],
        threshold: metrics['tuned']['best_recall']['threshold']
      },
      training_data: {
        n_samples: config['n_train'],
        features: config['feature_names'],
        class_balance: config['class_distribution']
      },
      intended_use: "Phishing website detection for browser extension",
      limitations: [
        "Temporal drift: phishing tactics evolve",
        "Adversarial attacks: features can be engineered",
        "Missing data: DomainAge lookup may fail"
      ]
    }
  END
END

CLASS FeatureDriftDetector:
  // FeatureDriftDetector monitors production feature distributions
  
  CONSTRUCTOR({ reference_distribution, kl_threshold=0.5 }):
    self.reference <- reference_distribution  // From training data
    self.kl_threshold <- kl_threshold
  END
  
  FUNCTION detect_drift({ production_features }) -> { drift_report }:
    // detect_drift computes KL divergence vs reference distribution
    
    drift_scores <- {}
    alerts <- []
    
    FOR feature IN production_features.columns:
      // Compute KL divergence
      ref_hist <- histogram(self.reference[feature])
      prod_hist <- histogram(production_features[feature])
      kl_div <- compute_kl_divergence(ref_hist, prod_hist)
      
      drift_scores[feature] <- kl_div
      
      IF kl_div > self.kl_threshold:
        alerts.append({
          feature: feature,
          kl_divergence: kl_div,
          severity: "high" IF kl_div > 1.0 ELSE "medium"
        })
    END
    
    RETURN {
      drift_scores: drift_scores,
      alerts: alerts,
      requires_retraining: len(alerts) > 0
    }
  END
END

CLASS PerformanceMonitor:
  // PerformanceMonitor tracks weekly model performance metrics
  
  FUNCTION monitor_weekly({ y_true_sample, y_pred_sample, baseline_metrics }) -> { monitoring_report }:
    // monitor_weekly compares current performance to baseline
    
    current_recall <- recall_score(y_true_sample, y_pred_sample)
    current_fpr <- false_positive_rate(y_true_sample, y_pred_sample)
    
    baseline_recall <- baseline_metrics['recall']
    baseline_fpr <- baseline_metrics['fpr']
    
    recall_degradation <- baseline_recall - current_recall
    fpr_increase <- current_fpr - baseline_fpr
    
    alerts <- []
    IF recall_degradation > 0.05:  // >5% drop
      alerts.append({
        metric: "recall",
        baseline: baseline_recall,
        current: current_recall,
        degradation: recall_degradation,
        action: "Trigger model retraining"
      })
    
    IF fpr_increase > 0.02:  // >2% increase
      alerts.append({
        metric: "fpr",
        baseline: baseline_fpr,
        current: current_fpr,
        increase: fpr_increase,
        action: "Investigate false alarm surge"
      })
    
    RETURN {
      current_metrics: {recall: current_recall, fpr: current_fpr},
      baseline_metrics: {recall: baseline_recall, fpr: baseline_fpr},
      alerts: alerts,
      requires_intervention: len(alerts) > 0
    }
  END
END
```

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs | FAQ Link |
|--------|--------------|-----------------|------------------------|--------------|-------------------|----------|
| `deployment/packager.py` | `ModelPackager` | `create_model_card` | ModelPackager generates human-readable model documentation | `model`, `metrics`, `config` | `model_card.json` | **FAQ 8.1** |
| `monitoring/drift_detector.py` | `FeatureDriftDetector` | `detect_drift` | FeatureDriftDetector monitors production feature distributions via KL divergence | `reference_distribution`, `production_features`, `scipy.stats` | `DriftReport{kl_scores, alerts}` | **FAQ 8.2** |
| `monitoring/performance.py` | `PerformanceMonitor` | `monitor_weekly` | PerformanceMonitor tracks weekly model performance vs baseline | `y_true_sample`, `y_pred_sample`, `baseline_metrics` | `MonitoringReport{alerts, requires_intervention}` | **FAQ 8.2** |

### FAQ Integration (Phase 8)

**Study Priority**: ⭐⭐⭐ (High - shows production awareness)

| FAQ ID | Question Trigger | Must-Know Answer Pattern | Code Reference |
|--------|-----------------|-------------------------|----------------|
| **8.1** | "How deploy to production?" | "Browser extension architecture: (1) Client-side: extract features from URL/HTML. (2) Server-side API: FastAPI service with model inference. (3) Containerize with Docker. (4) Deploy on Kubernetes with autoscaling. Latency: <100ms p95." | `ModelPackager` conceptual |
| **8.2** | "What monitoring?" | "Four-layer: (1) System health (latency p99<500ms), (2) Feature drift (KL divergence>0.5 alert), (3) Performance (weekly recall vs baseline), (4) Business metrics (attacks blocked, support cost). Automated retraining trigger." | `FeatureDriftDetector` + `PerformanceMonitor` |
| **8.3** | "Handle model updates?" | "Blue-green deployment: (1) Shadow mode (0% traffic, compare predictions), (2) Canary (5% traffic, monitor metrics), (3) Gradual rollout (25→50→100%), (4) Auto-rollback if error_rate>1% or FPR>baseline×1.2." | Deployment pattern conceptual |

---

## FAQ Study Priority Matrix {#faq-priority}

### Week 1 Must-Know (High Interview Probability)

| Priority | FAQ ID | Question | Probability | Impact | Study Time |
|----------|--------|----------|-------------|--------|------------|
| ⭐⭐⭐⭐⭐ | **3.1** | "Why preprocessing on full dataset?" | 90% | CRITICAL - explains leakage | 2 hours |
| ⭐⭐⭐⭐⭐ | **6.1** | "Why max_fpr=0.03 not 0.05?" | 85% | CRITICAL - explains poor results | 1.5 hours |
| ⭐⭐⭐⭐ | **7.2** | "What does confusion matrix tell you?" | 75% | HIGH - business thinking | 1 hour |
| ⭐⭐⭐⭐ | **5.3** | "How select best model?" | 70% | HIGH - ML judgment | 1 hour |
| ⭐⭐⭐⭐ | **8.1** | "How deploy to production?" | 65% | HIGH - production readiness | 1 hour |

**Total Week 1**: 6.5 hours

### Week 2 Should-Know (Medium Probability)

| Priority | FAQ ID | Question | Probability | Impact | Study Time |
|----------|--------|----------|-------------|--------|------------|
| ⭐⭐⭐ | **1.2** | "68% missing DomainAge—how handle?" | 60% | MED - EDA connection | 45 min |
| ⭐⭐⭐ | **3.2** | "Why log-transform and clip?" | 55% | MED - preprocessing rationale | 45 min |
| ⭐⭐⭐ | **4.1** | "Verify stratification worked?" | 50% | MED - statistical validation | 30 min |
| ⭐⭐⭐ | **5.1** | "Why these 3 models?" | 50% | MED - model comparison | 30 min |
| ⭐⭐⭐ | **6.2** | "How threshold tuning works?" | 45% | MED - threshold mechanics | 30 min |
| ⭐⭐⭐ | **7.3** | "Calculate business impact?" | 45% | MED - cost calculation | 30 min |

**Total Week 2**: 3.5 hours

### Week 3 Nice-to-Know (Lower Probability)

| Priority | FAQ ID | Question | Probability | Impact | Study Time |
|----------|--------|----------|-------------|--------|------------|
| ⭐⭐ | **0.1-0.3** | Phase 0 questions | 30% | LOW - foundational | 1 hour |
| ⭐⭐ | **2.1-2.2** | Hypothesis testing | 35% | LOW - statistical depth | 1 hour |
| ⭐⭐ | **8.2-8.3** | Advanced deployment | 25% | LOW - beyond scope | 1 hour |

**Total Week 3**: 3 hours

### Study Technique: Spaced Repetition

```
Day 1: Read FAQ + write answer in own words
Day 2: Recite answer without notes (check accuracy)
Day 3: Practice with code examples
Day 7: Review (should be automatic by now)
Day 14: Final review before interview
```

---

## Implementation Checklist

### Tier 1 Fixes (Must-Do, 8 hours)

- [ ] **Fix 3.1**: Refactor leakage (split FIRST, then fit preprocessing)
  - [ ] Modify `main.py` orchestration
  - [ ] Update `FeatureEngineer` to have `fit()` method
  - [ ] Update README with "Data Leakage Prevention" section
  - **Expected impact**: Test recall drops 3-7% (this is good—reflects true performance)

- [ ] **Fix 6.1**: Update KPI alignment
  - [ ] Change `config.yaml`: `max_fpr: 0.05`
  - [ ] Re-run pipeline
  - [ ] Document threshold comparison in README
  - **Expected impact**: Recall improves to ~70%

- [ ] **Fix 4.1**: Add statistical validation
  - [ ] Implement `validate_stratification()` with chi-square tests
  - [ ] Update `pipeline_validation.json` output
  - [ ] Add README section showing p-values
  - **Expected impact**: Demonstrates statistical rigor

### Tier 2 Enhancements (Should-Do, 8 hours)

- [ ] **Fix 1.2**: Create EDA→MLP mapping table in README
  - [ ] 5-row table linking EDA findings to pipeline decisions
  - **Expected impact**: Interview answer key

- [ ] **Fix 7.3**: Implement BusinessImpactCalculator
  - [ ] Create `src/business_impact.py`
  - [ ] Integrate into `main.py`
  - [ ] Add README section with cost calculations
  - **Expected impact**: Quantifies business value ($139M savings)

- [ ] **Fix 2.2**: Create HypothesisTester module
  - [ ] Implement `test_class_balance_significance()`
  - [ ] Implement `test_mnar_hypothesis()`
  - [ ] Generate `results/hypothesis_tests.json`
  - **Expected impact**: Automated statistical validation

- [ ] **Fix 6.3**: Add Pareto analysis
  - [ ] Create `src/threshold_analyzer.py`
  - [ ] Generate `pareto_curve.png`
  - [ ] Add `results/pareto_analysis.json`
  - **Expected impact**: Visual threshold trade-off analysis

### Documentation Polish (4 hours)

- [ ] Comprehensive README review
- [ ] Clean up `eda.ipynb` with markdown explanations
- [ ] Verify all code runs end-to-end
- [ ] GitHub Actions passes

---

**Next Action**: Start with **FAQ 3.1** and **FAQ 6.1** (highest impact). Master these two, and you'll pass the interview.

---

## Prompt_202601120915

consolidate "EDA → MLP Interview Prep Guide: Clean Slate to Excellence Version: 3.0 (FAQ-Driven Framework)" "3. The FAQ-Driven Learning Framework", "4. Phase-by-Phase Implementation Roadmap" into `interview-session-max-LOD.md`
```
**Pattern Example**:
```
FUNCTION PatternDetector.extract_features({ entities, config }) -> { feature_vectors }
  // PatternDetector extracts feature vectors via embedding model
  
  vectors <- []
  FOR EACH entity IN entities:
    vector <- compute_embedding(entity, config.embedding_model)
    vectors.append({
      entity_id: entity.id,
      vector: vector,
      provenance: build_provenance(entity, "extract_features")
    })
  
  RETURN vectors
END
```
**Developers document function in responsibility table**:
| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `detection/pattern.ext` | `PatternDetector` | `extract_features` | PatternDetector extracts feature vectors via embedding model | `config.embedding_model` | `FeatureVector[]` |
```