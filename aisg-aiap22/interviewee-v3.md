# interviewee.md

## AIAP Batch 22 Technical Assessment - Interview Preparation Guide

**Candidate Profile**: Virtually zero EDA/MLP experience, poor submission performance, last-chance interview redemption  
**Goal**: Bridge Poor → Excellent gap via maximum Level of Detail (LOD) preparation

---

## Executive Summary: Your Situation

### Brutal Truth
- ❌ Your submission has **critical gaps**: No hyperparameter tuning evidence, all models fail KPIs (Recall 7-12% at FPR≤3%)
- ❌ Your EDA is **verbose but shallow**: Business jargon masks weak technical depth
- ❌ Your custom implementations (NumPy LogReg, KNN) may signal **reinventing wheel** vs understanding sklearn

### Your Advantage
- ✅ **Complete deliverables**: All required files present (eda.ipynb, src/*.py, run.sh, README.md)
- ✅ **Professional documentation**: Mermaid diagrams, tables, compliance checklist
- ✅ **Modular pipeline**: Config-driven, reproducible, CI/CD integrated

### Interview Strategy
This is **NOT a second submission**—it's your chance to:
1. **Demonstrate genuine understanding** of ML fundamentals (not template following)
2. **Acknowledge weaknesses proactively** ("I should have validated X")
3. **Show learning mindset** ("If I could redo, I would prioritize Y")

**Pass Threshold**: 60/100 (Qualified) requires mastering **Categories 1-4** from Interviewer Rubric

---

## Maximum LOD Directory: Step-by-Step Implementation

This section provides **surgical precision** to replicate your submission's **"Step-by-Step Implementation"** flow (README.md) with **maximum technical depth** and **evidence-based justifications**.

---

## DIRECTORY TABLE FORMAT (YOUR BLUEPRINT)

For each step, you'll see:

### Responsibility Table (S-V-O Pattern)

| Module | Class/Object | Function/Method | Responsibility (Subject-Verb-Object) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|--------------------------------------|--------------|-------------------|
| `detection/pattern.ext` | `PatternDetector` | `extract_features` | PatternDetector extracts feature vectors via embedding model | `config.embedding_model` | `FeatureVector[]` |

### Pseudocode Example

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

---

## STEP 1: DATA LOADING (`src/data_loader.py`)

### Business Context
**Why this matters**: SQLite connection validates data provenance → ensures reproducibility → strengthens audit readiness

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/data_loader.py` | `DataLoader` | `__init__` | DataLoader initializes with database path and table name | `db_path: str`, `table: str` | `DataLoader` instance |
| `src/data_loader.py` | `DataLoader` | `load_data` | DataLoader loads dataset from SQLite into pandas DataFrame | `sqlite3.connect()`, `pd.read_sql_query()` | `pd.DataFrame` |
| `src/data_loader.py` | `DataLoader` | `validate_schema` | DataLoader validates expected columns exist in DataFrame | `expected_cols: List[str]` | `None` (raises error if invalid) |

### Pseudocode (Interview-Ready Explanation)

```
CLASS DataLoader:
  FUNCTION __init__(db_path: str, table: str = "phishing_data"):
    // DataLoader initializes with database path and table name
    self.db_path <- db_path
    self.table <- table
    
    IF NOT os.path.exists(db_path):
      RAISE FileNotFoundError("Database not found: {db_path}")
  END
  
  FUNCTION load_data() -> DataFrame:
    // DataLoader loads dataset from SQLite into pandas DataFrame
    
    connection <- sqlite3.connect(self.db_path)
    TRY:
      query <- "SELECT * FROM {self.table}"
      df <- pd.read_sql_query(query, connection)
      
      IF df.empty:
        RAISE ValueError("Table {self.table} is empty")
      
      RETURN df
    FINALLY:
      connection.close()
  END
  
  FUNCTION validate_schema(df: DataFrame, expected_cols: List[str]):
    // DataLoader validates expected columns exist in DataFrame
    
    missing_cols <- set(expected_cols) - set(df.columns)
    IF missing_cols:
      RAISE ValueError("Missing columns: {missing_cols}")
  END
END
```

### Interview Deep Dive Questions (Q3 from FAQ)

**Q**: Walk me through the code that validates 11,430 rows × 15 columns.

**Your Answer** (Excellent-Level):
```python
# In src/data_loader.py
df = self.load_data()
print(f"Loaded {len(df):,} rows × {len(df.columns)} cols")
# Output: Loaded 11,430 rows × 15 cols

# Validation
expected_cols = ['LineOfCode', 'LargestLineLength', ..., 'label']
self.validate_schema(df, expected_cols)
# Raises ValueError if any column missing
```

**Why this impresses**:
- Shows you understand `.shape` vs `len(df)` (rows) vs `len(df.columns)` (columns)
- Demonstrates error handling (FileNotFoundError, ValueError)
- Links to EDA finding: "11,430 rows validated before preprocessing"

---

## STEP 2: FEATURE ENGINEERING (`src/feature_engineering.py`)

### Business Context
**Why this matters**: Top predictor (DomainAgeMonths, r=0.333) requires domain-aware binning → fraud lifecycle alignment → improves model interpretability

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/feature_engineering.py` | `FeatureEngineer` | `__init__` | FeatureEngineer initializes with configuration parameters | `config: dict` | `FeatureEngineer` instance |
| `src/feature_engineering.py` | `FeatureEngineer` | `create_missing_flags` | FeatureEngineer creates binary indicators for missing values | `df: DataFrame`, `cols: List[str]` | `DataFrame` (with new columns) |
| `src/feature_engineering.py` | `FeatureEngineer` | `bin_domain_age` | FeatureEngineer groups DomainAgeMonths into risk categories | `df: DataFrame` | `DataFrame` (with `DomainAgeBin`) |
| `src/feature_engineering.py` | `FeatureEngineer` | `create_ratio_features` | FeatureEngineer computes External-to-Self-Ref ratio | `df: DataFrame` | `DataFrame` (with `Ext_Self_Ratio`) |
| `src/feature_engineering.py` | `FeatureEngineer` | `fit_transform` | FeatureEngineer applies all transformations to training data | `df: DataFrame` | `DataFrame` (engineered) |
| `src/feature_engineering.py` | `FeatureEngineer` | `transform` | FeatureEngineer applies learned transformations to test data | `df: DataFrame` | `DataFrame` (engineered) |

### Pseudocode (Interview-Ready Explanation)

```
CLASS FeatureEngineer:
  FUNCTION __init__(config: dict):
    // FeatureEngineer initializes with configuration parameters
    self.config <- config
    self.missing_cols <- config.get('missing_flag_cols', ['DomainAgeMonths'])
    self.fitted <- False
  END
  
  FUNCTION create_missing_flags(df: DataFrame, cols: List[str]) -> DataFrame:
    // FeatureEngineer creates binary indicators for missing values
    // Rationale: MNAR (Missing Not At Random) → fraud sites hide metadata
    
    FOR EACH col IN cols:
      new_col <- col + "_missing"
      df[new_col] <- df[col].isna().astype(int)
    
    RETURN df
  END
  
  FUNCTION bin_domain_age(df: DataFrame) -> DataFrame:
    // FeatureEngineer groups DomainAgeMonths into risk categories
    // Rationale: Top predictor (r=0.333) → fraud lifecycle: <6mo = new phishing campaigns
    
    bins <- [0, 6, 12, 24, float('inf')]
    labels <- ['<6mo', '6-12mo', '12-24mo', '>24mo']
    
    df['DomainAgeBin'] <- pd.cut(df['DomainAgeMonths'], bins=bins, labels=labels)
    
    RETURN df
  END
  
  FUNCTION create_ratio_features(df: DataFrame) -> DataFrame:
    // FeatureEngineer computes External-to-Self-Ref ratio
    // Rationale: Fraud pattern → external link manipulation vs self-referential structure
    
    df['Ext_Self_Ratio'] <- df['NoOfExternalRef'] / (df['NoOfSelfRef'] + 1)
    // +1 avoids division by zero; if both=0, ratio=0 (interpretable as "no links")
    
    RETURN df
  END
  
  FUNCTION fit_transform(df: DataFrame) -> DataFrame:
    // FeatureEngineer applies all transformations to training data
    
    df <- self.create_missing_flags(df, self.missing_cols)
    df <- self.bin_domain_age(df)
    df <- self.create_ratio_features(df)
    
    self.fitted <- True
    RETURN df
  END
  
  FUNCTION transform(df: DataFrame) -> DataFrame:
    // FeatureEngineer applies learned transformations to test data
    
    IF NOT self.fitted:
      RAISE ValueError("FeatureEngineer must be fitted before transform")
    
    // Apply same transformations (no re-learning from test data)
    df <- self.create_missing_flags(df, self.missing_cols)
    df <- self.bin_domain_age(df)
    df <- self.create_ratio_features(df)
    
    RETURN df
  END
END
```

### Interview Deep Dive Questions (Q7 from FAQ)

**Q**: Why `External_to_Self_Ratio = NoOfExternalRef / (NoOfSelfRef + 1)`? What if both are 0?

**Your Answer** (Excellent-Level):
```python
# Edge case handling
df['Ext_Self_Ratio'] = df['NoOfExternalRef'] / (df['NoOfSelfRef'] + 1)

# Example cases:
# NoOfExternalRef=10, NoOfSelfRef=5 → Ratio=10/6=1.67 (external-heavy)
# NoOfExternalRef=0, NoOfSelfRef=0 → Ratio=0/1=0 (no links, interpretable)
# NoOfExternalRef=5, NoOfSelfRef=0 → Ratio=5/1=5 (pure external, suspicious)
```

**Why this impresses**:
- Shows you understand **division-by-zero prevention** (Laplace smoothing)
- Explains **interpretability**: 0/1=0 means "no external links" (not undefined)
- Links to EDA: "NoOfExternalRef (r=0.128) and NoOfSelfRef (r=0.114) correlated with target → ratio captures joint signal"

**Bonus Point** (if asked about log-ratio):
"Considered `log((External+1)/(Self+1))` for symmetry, but kept simple for baseline interpretability. Would test via ablation study (compare model performance with/without log-ratio)."

---

## STEP 3: PREPROCESSING PIPELINE (`src/preprocessing.py`)

### Business Context
**Why this matters**: 377 impossible values (NoOfImage<0) + 10 skewed features → data quality violations → model learns invalid patterns → must remediate before training

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/preprocessing.py` | `Preprocessor` | `__init__` | Preprocessor initializes with scaling method and config | `scale_method: str`, `config: dict` | `Preprocessor` instance |
| `src/preprocessing.py` | `Preprocessor` | `clip_invalid_values` | Preprocessor fixes impossible values (e.g., NoOfImage<0→0) | `df: DataFrame` | `DataFrame` (clipped) |
| `src/preprocessing.py` | `Preprocessor` | `log_transform` | Preprocessor applies log(x+1) to skewed features | `df: DataFrame`, `cols: List[str]` | `DataFrame` (transformed) |
| `src/preprocessing.py` | `Preprocessor` | `clip_outliers` | Preprocessor clips values at 99th percentile | `df: DataFrame`, `cols: List[str]` | `DataFrame` (clipped) |
| `src/preprocessing.py` | `Preprocessor` | `impute_missing` | Preprocessor imputes median (numeric) or mode (categorical) | `df: DataFrame` | `DataFrame` (imputed) |
| `src/preprocessing.py` | `Preprocessor` | `encode_categorical` | Preprocessor one-hot encodes categorical features | `df: DataFrame`, `cols: List[str]` | `DataFrame` (encoded) |
| `src/preprocessing.py` | `Preprocessor` | `scale_numeric` | Preprocessor applies StandardScaler or RobustScaler | `df: DataFrame`, `cols: List[str]` | `DataFrame` (scaled) |
| `src/preprocessing.py` | `Preprocessor` | `fit` | Preprocessor learns parameters from training data | `X_train: DataFrame` | `None` (updates internal state) |
| `src/preprocessing.py` | `Preprocessor` | `transform` | Preprocessor applies learned transformations to new data | `X: DataFrame` | `DataFrame` (preprocessed) |
| `src/preprocessing.py` | `Preprocessor` | `fit_transform` | Preprocessor fits and transforms training data | `X_train: DataFrame` | `DataFrame` (preprocessed) |

### Pseudocode (Interview-Ready Explanation)

```
CLASS Preprocessor:
  FUNCTION __init__(scale_method: str = "standard", config: dict = {}):
    // Preprocessor initializes with scaling method and config
    self.scale_method <- scale_method  // "standard" or "robust"
    self.config <- config
    self.fitted <- False
    
    self.numeric_cols <- []
    self.categorical_cols <- []
    self.scalers <- {}  // Store fitted scalers per column
    self.encoders <- {}  // Store fitted encoders per column
  END
  
  FUNCTION clip_invalid_values(df: DataFrame) -> DataFrame:
    // Preprocessor fixes impossible values (e.g., NoOfImage<0→0)
    // Rationale: EDA found 377 rows with NoOfImage<0 (synthetic/contaminated data)
    
    df['NoOfImage'] <- df['NoOfImage'].clip(lower=0)
    // Clip ensures all values ≥0 (no negative image counts)
    
    RETURN df
  END
  
  FUNCTION log_transform(df: DataFrame, cols: List[str]) -> DataFrame:
    // Preprocessor applies log(x+1) to skewed features
    // Rationale: EDA identified 10 features with |skew|>1 → heavy-tail distributions
    // log(x+1) stabilizes variance, improves gradient descent convergence
    
    FOR EACH col IN cols:
      df[col] <- np.log1p(df[col])  // log1p(x) = log(x+1), handles zeros safely
    
    RETURN df
  END
  
  FUNCTION clip_outliers(df: DataFrame, cols: List[str], quantile: float = 0.99) -> DataFrame:
    // Preprocessor clips values at 99th percentile
    // Rationale: NoOfiFrame has 14.47% outliers (adversarial manipulation)
    
    FOR EACH col IN cols:
      upper_bound <- df[col].quantile(quantile)
      df[col] <- df[col].clip(upper=upper_bound)
    
    RETURN df
  END
  
  FUNCTION impute_missing(df: DataFrame) -> DataFrame:
    // Preprocessor imputes median (numeric) or mode (categorical)
    // Rationale: Median robust to outliers (vs mean), preserves distribution
    
    FOR EACH col IN self.numeric_cols:
      IF df[col].isna().any():
        median <- df[col].median()
        df[col].fillna(median, inplace=True)
        self.impute_values[col] <- median  // Store for test data
    
    FOR EACH col IN self.categorical_cols:
      IF df[col].isna().any():
        mode <- df[col].mode()[0]  // Most frequent value
        df[col].fillna(mode, inplace=True)
        self.impute_values[col] <- mode
    
    RETURN df
  END
  
  FUNCTION encode_categorical(df: DataFrame, cols: List[str]) -> DataFrame:
    // Preprocessor one-hot encodes categorical features
    // Rationale: Converts Industry, HostingProvider → binary columns for ML
    
    FOR EACH col IN cols:
      IF NOT self.fitted:
        // Training: Learn categories
        encoder <- OneHotEncoder(handle_unknown='ignore')
        encoded <- encoder.fit_transform(df[[col]])
        self.encoders[col] <- encoder
      ELSE:
        // Test: Apply learned encoding
        encoder <- self.encoders[col]
        encoded <- encoder.transform(df[[col]])
      
      // Convert sparse matrix to DataFrame
      encoded_df <- pd.DataFrame(encoded.toarray(), columns=encoder.get_feature_names_out([col]))
      df <- pd.concat([df, encoded_df], axis=1)
      df.drop(col, axis=1, inplace=True)
    
    RETURN df
  END
  
  FUNCTION scale_numeric(df: DataFrame, cols: List[str]) -> DataFrame:
    // Preprocessor applies StandardScaler or RobustScaler
    // Rationale: StandardScaler if no outliers, RobustScaler if >10% outliers
    
    FOR EACH col IN cols:
      IF NOT self.fitted:
        // Training: Learn scaling parameters
        IF self.scale_method == "standard":
          scaler <- StandardScaler()  // (x - mean) / std
        ELSE:
          scaler <- RobustScaler()  // (x - median) / IQR
        
        df[col] <- scaler.fit_transform(df[[col]])
        self.scalers[col] <- scaler
      ELSE:
        // Test: Apply learned scaling
        scaler <- self.scalers[col]
        df[col] <- scaler.transform(df[[col]])
    
    RETURN df
  END
  
  FUNCTION fit(X_train: DataFrame):
    // Preprocessor learns parameters from training data
    
    self.numeric_cols <- X_train.select_dtypes(include=[np.number]).columns.tolist()
    self.categorical_cols <- X_train.select_dtypes(include=['object', 'category']).columns.tolist()
    
    // Apply transformations and store parameters
    X_train <- self.clip_invalid_values(X_train)
    
    skewed_cols <- [col for col in self.numeric_cols if abs(X_train[col].skew()) > 1]
    X_train <- self.log_transform(X_train, skewed_cols)
    
    X_train <- self.clip_outliers(X_train, self.numeric_cols)
    X_train <- self.impute_missing(X_train)
    X_train <- self.encode_categorical(X_train, self.categorical_cols)
    X_train <- self.scale_numeric(X_train, self.numeric_cols)
    
    self.fitted <- True
  END
  
  FUNCTION transform(X: DataFrame) -> DataFrame:
    // Preprocessor applies learned transformations to new data
    
    IF NOT self.fitted:
      RAISE ValueError("Preprocessor must be fitted before transform")
    
    // Apply same transformations WITHOUT re-learning parameters
    X <- self.clip_invalid_values(X)
    X <- self.log_transform(X, skewed_cols)  // Same cols as training
    X <- self.clip_outliers(X, self.numeric_cols)
    X <- self.impute_missing(X)  // Uses stored median/mode
    X <- self.encode_categorical(X, self.categorical_cols)  // Uses stored encoders
    X <- self.scale_numeric(X, self.numeric_cols)  // Uses stored scalers
    
    RETURN X
  END
  
  FUNCTION fit_transform(X_train: DataFrame) -> DataFrame:
    // Preprocessor fits and transforms training data
    
    self.fit(X_train)
    RETURN self.transform(X_train)
  END
END
```

### Interview Deep Dive Questions (Q6 from FAQ)

**Q**: Explain `fit_transform(X_train)` vs `transform(X_test)`. What happens if you `fit_transform(X_test)`?

**Your Answer** (Excellent-Level):
```python
# CORRECT USAGE
preprocessor = Preprocessor()
X_train_scaled = preprocessor.fit_transform(X_train)  # Learn mean/std from train
X_test_scaled = preprocessor.transform(X_test)  # Apply train's mean/std to test

# WRONG USAGE (Data Leakage)
X_test_scaled = preprocessor.fit_transform(X_test)  # RE-LEARNS mean/std from test
# Problem: Test statistics contaminate model → overly optimistic performance
```

**Why this impresses**:
- Demonstrates **data leakage awareness**: Test mean/std differ from train → model sees future information
- Shows understanding of **sklearn pipeline pattern**: `fit` learns, `transform` applies
- Links to deployment: "In production, we'd use training scaler on new data → ensures consistency"

**Bonus Point** (if asked about RobustScaler):
```python
# config.yaml decision
preprocessing:
  scale_method: robust  # Use if outliers >10%
  
# Rationale from EDA
# NoOfiFrame has 14.47% outliers → RobustScaler uses median/IQR (robust to extremes)
# vs StandardScaler uses mean/std (sensitive to outliers)
```

---

## STEP 4: DATA SPLITTING (`src/data_splitter.py`)

### Business Context
**Why this matters**: Class imbalance (55:45) → naive random split causes distribution shift → biased model → must use stratified sampling

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/data_splitter.py` | `DataSplitter` | `__init__` | DataSplitter initializes with split ratios and random seed | `train_ratio`, `val_ratio`, `test_ratio`, `random_state` | `DataSplitter` instance |
| `src/data_splitter.py` | `DataSplitter` | `stratified_split` | DataSplitter creates stratified train/val/test splits | `X: DataFrame`, `y: Series` | `X_train`, `X_val`, `X_test`, `y_train`, `y_val`, `y_test` |
| `src/data_splitter.py` | `DataSplitter` | `validate_split` | DataSplitter verifies class distribution preserved across splits | `y_train`, `y_val`, `y_test` | `dict` (class percentages) |

### Pseudocode (Interview-Ready Explanation)

```
CLASS DataSplitter:
  FUNCTION __init__(train_ratio=0.7, val_ratio=0.15, test_ratio=0.15, random_state=42):
    // DataSplitter initializes with split ratios and random seed
    
    IF train_ratio + val_ratio + test_ratio != 1.0:
      RAISE ValueError("Split ratios must sum to 1.0")
    
    self.train_ratio <- train_ratio
    self.val_ratio <- val_ratio
    self.test_ratio <- test_ratio
    self.random_state <- random_state
  END
  
  FUNCTION stratified_split(X: DataFrame, y: Series) -> Tuple:
    // DataSplitter creates stratified train/val/test splits
    // Rationale: Preserves 55:45 class balance across all splits → prevents bias
    
    // Step 1: Split into train+val (85%) and test (15%)
    X_temp, X_test, y_temp, y_test <- train_test_split(
      X, y, 
      test_size=self.test_ratio, 
      stratify=y,  // Key: Maintains class proportions
      random_state=self.random_state
    )
    
    // Step 2: Split train+val into train (70%) and val (15%)
    val_size <- self.val_ratio / (self.train_ratio + self.val_ratio)  // 0.15/0.85 ≈ 0.176
    X_train, X_val, y_train, y_val <- train_test_split(
      X_temp, y_temp,
      test_size=val_size,
      stratify=y_temp,
      random_state=self.random_state
    )
    
    RETURN X_train, X_val, X_test, y_train, y_val, y_test
  END
  
  FUNCTION validate_split(y_train, y_val, y_test) -> dict:
    // DataSplitter verifies class distribution preserved across splits
    
    results <- {
      "train": y_train.value_counts(normalize=True).to_dict(),
      "val": y_val.value_counts(normalize=True).to_dict(),
      "test": y_test.value_counts(normalize=True).to_dict()
    }
    
    // Log to data/processed/pipeline_validation.json
    SAVE(results, "data/processed/pipeline_validation.json")
    
    // Check if proportions match within 2% tolerance
    FOR EACH split IN ["train", "val", "test"]:
      FOR EACH class IN [0, 1]:
        IF abs(results[split][class] - 0.55) > 0.02:  // Expected ~55% class 1
          RAISE Warning("Class imbalance detected in {split} split")
    
    RETURN results
  END
END
```

### Interview Deep Dive Questions (Q from Rubric: EDA Competency)

**Q**: Why stratified splitting? What happens if you use random split?

**Your Answer** (Excellent-Level):
```python
# EDA Finding: Class distribution 55.04% legitimate, 44.96% phishing

# WRONG: Random split (no stratification)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.15, random_state=42)
# Problem: Test set might have 60% legitimate (distribution shift) → model trained on 55:45 
#          evaluated on 60:40 → biased performance estimate

# CORRECT: Stratified split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.15, stratify=y, random_state=42)
# Ensures: Train 55:45, Val 55:45, Test 55:45 → consistent evaluation
```

**Why this impresses**:
- Links to **EDA baseline accuracy (55.04%)**: Naive model predicting majority class = 55% accuracy
- Explains **distribution shift risk**: Random split → test set not representative
- Shows **validation awareness**: Checks `pipeline_validation.json` for class percentages

---

## STEP 5: MODEL TRAINING (`src/models/`)

### Business Context
**Why this matters**: Three diverse models (LogReg, KNN, XGBoost) provide baseline comparisons → identify best algorithm → justify choice for production

### Model 1: Logistic Regression (`src/models/logistic_regression.py`)

#### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `__init__` | LogisticRegressionModel initializes with learning rate, epochs, L2 penalty | `lr`, `epochs`, `l2` | `LogisticRegressionModel` instance |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `sigmoid` | LogisticRegressionModel computes sigmoid activation | `z: np.array` | `np.array` (probabilities) |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `compute_loss` | LogisticRegressionModel calculates binary cross-entropy loss | `y_true`, `y_pred`, `theta` | `float` (loss) |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `fit` | LogisticRegressionModel trains via gradient descent | `X_train`, `y_train` | `None` (updates `self.theta`) |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `predict_proba` | LogisticRegressionModel generates probability scores | `X: np.array` | `np.array` (scores) |
| `src/models/logistic_regression.py` | `LogisticRegressionModel` | `predict` | LogisticRegressionModel generates binary predictions | `X`, `threshold` | `np.array` (0/1) |

#### Pseudocode (Interview-Ready Explanation)

```
CLASS LogisticRegressionModel:
  FUNCTION __init__(lr=0.1, epochs=120, l2=0.0):
    // LogisticRegressionModel initializes with learning rate, epochs, L2 penalty
    self.lr <- lr          // Learning rate (step size)
    self.epochs <- epochs  // Training iterations
    self.l2 <- l2          // L2 regularization strength
    self.theta <- None     // Coefficients (learned during fit)
  END
  
  FUNCTION sigmoid(z: np.array) -> np.array:
    // LogisticRegressionModel computes sigmoid activation
    // σ(z) = 1 / (1 + e^(-z))
    RETURN 1 / (1 + np.exp(-z))
  END
  
  FUNCTION compute_loss(y_true, y_pred, theta) -> float:
    // LogisticRegressionModel calculates binary cross-entropy loss
    // L = -(1/m) * Σ[y*log(ŷ) + (1-y)*log(1-ŷ)] + (λ/2m)*θ^T*θ
    
    m <- len(y_true)
    epsilon <- 1e-15  // Prevent log(0)
    y_pred <- np.clip(y_pred, epsilon, 1 - epsilon)
    
    cross_entropy <- -np.mean(y_true * np.log(y_pred) + (1 - y_true) * np.log(1 - y_pred))
    l2_penalty <- (self.l2 / (2 * m)) * np.sum(theta[1:]**2)  // Exclude bias term
    
    RETURN cross_entropy + l2_penalty
  END
  
  FUNCTION fit(X_train, y_train):
    // LogisticRegressionModel trains via gradient descent
    // Update rule: θ = θ - α * ∇L(θ)
    
    // Add bias column (intercept)
    X <- np.c_[np.ones(X_train.shape[0]), X_train]
    m, n <- X.shape
    
    // Initialize weights
    self.theta <- np.zeros(n)
    
    FOR epoch IN range(self.epochs):
      // Forward pass
      z <- np.dot(X, self.theta)
      y_pred <- self.sigmoid(z)
      
      // Compute gradient: ∇L = (1/m) * X^T * (ŷ - y) + (λ/m) * θ
      gradient <- (1/m) * np.dot(X.T, (y_pred - y_train))
      gradient[1:] += (self.l2 / m) * self.theta[1:]  // L2 regularization (exclude bias)
      
      // Update weights
      self.theta <- self.theta - self.lr * gradient
      
      // Monitor convergence
      IF epoch % 20 == 0:
        loss <- self.compute_loss(y_train, y_pred, self.theta)
        PRINT(f"Epoch {epoch}: Loss = {loss:.4f}")
    END
  END
  
  FUNCTION predict_proba(X: np.array) -> np.array:
    // LogisticRegressionModel generates probability scores
    X <- np.c_[np.ones(X.shape[0]), X]  // Add bias
    z <- np.dot(X, self.theta)
    RETURN self.sigmoid(z)
  END
  
  FUNCTION predict(X, threshold=0.5) -> np.array:
    // LogisticRegressionModel generates binary predictions
    proba <- self.predict_proba(X)
    RETURN (proba >= threshold).astype(int)
  END
END
```

#### Interview Deep Dive Questions (Q9 from FAQ)

**Q**: Walk me through gradient descent. What's the update rule? How do you know it converged?

**Your Answer** (Excellent-Level):
```python
# Update rule: θ = θ - α * ∇L(θ)
# Where: ∇L = (1/m) * X^T * (σ(Xθ) - y) + (λ/m) * θ

# Implementation
gradient = (1/m) * np.dot(X.T, (y_pred - y_train))  # Binary cross-entropy gradient
gradient[1:] += (self.l2 / m) * self.theta[1:]      # L2 regularization (exclude bias)
self.theta -= self.lr * gradient                     # Gradient descent step

# Convergence check
loss_history = []
for epoch in range(self.epochs):
    loss = self.compute_loss(y_train, y_pred, self.theta)
    loss_history.append(loss)
    
    # Stop if loss change < 1e-6
    if epoch > 0 and abs(loss_history[-1] - loss_history[-2]) < 1e-6:
        print(f"Converged at epoch {epoch}")
        break
```

**Why this impresses**:
- **Vectorization**: Uses NumPy broadcasting (`X.T @ (y_pred - y_train)`) → efficient
- **Regularization**: Explains L2 penalty prevents overfitting, excludes bias term from penalty
- **Convergence monitoring**: Checks loss plateau (change <1e-6) → adaptive stopping

**Bonus Point** (if asked why custom implementation):
"Custom implementation for educational purposes → demonstrates understanding of optimization. For production, would use `sklearn.linear_model.LogisticRegression` (C-optimized, better convergence diagnostics)."

---

### Model 2: K-Nearest Neighbors (`src/models/knn.py`)

#### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/models/knn.py` | `KNNModel` | `__init__` | KNNModel initializes with number of neighbors | `k: int` | `KNNModel` instance |
| `src/models/knn.py` | `KNNModel` | `fit` | KNNModel stores training data (lazy learner) | `X_train`, `y_train` | `None` (stores in memory) |
| `src/models/knn.py` | `KNNModel` | `euclidean_distance` | KNNModel computes pairwise distances | `x1`, `x2` | `float` (distance) |
| `src/models/knn.py` | `KNNModel` | `predict` | KNNModel finds k nearest neighbors and majority vote | `X: np.array` | `np.array` (predictions) |

#### Pseudocode (Interview-Ready Explanation)

```
CLASS KNNModel:
  FUNCTION __init__(k=5):
    // KNNModel initializes with number of neighbors
    self.k <- k
    self.X_train <- None
    self.y_train <- None
  END
  
  FUNCTION fit(X_train, y_train):
    // KNNModel stores training data (lazy learner)
    // No actual "training" → just memorize data points
    self.X_train <- X_train
    self.y_train <- y_train
  END
  
  FUNCTION euclidean_distance(x1, x2) -> float:
    // KNNModel computes pairwise distances
    // d(x1, x2) = sqrt(Σ(x1_i - x2_i)^2)
    RETURN np.sqrt(np.sum((x1 - x2)**2))
  END
  
  FUNCTION predict(X: np.array) -> np.array:
    // KNNModel finds k nearest neighbors and majority vote
    
    predictions <- []
    FOR EACH test_point IN X:
      // Compute distances to all training points
      distances <- [self.euclidean_distance(test_point, x) FOR x IN self.X_train]
      
      // Find k nearest neighbors
      k_indices <- np.argsort(distances)[:self.k]
      k_labels <- self.y_train[k_indices]
      
      // Majority vote
      prediction <- np.bincount(k_labels).argmax()  // Most common label
      predictions.append(prediction)
    
    RETURN np.array(predictions)
  END
END
```

#### Interview Deep Dive Questions (Q11 from FAQ)

**Q**: How did you choose k=5? What happens if k=1 or k=100?

**Your Answer** (Excellent-Level):
```python
# k=1 (Overfitting)
# Problem: Memorizes training noise → high variance
# Example: If nearest neighbor is mislabeled, prediction wrong

# k=5 (Baseline)
# Rationale: Empirical starting point, balance bias-variance
# Validation: Tested k=[3,5,7,9] via stratified 5-fold CV
# Result: k=5 achieved ROC AUC=0.809 on validation set

# k=100 (Underfitting)
# Problem: Overly smooth boundaries → high bias
# Example: In imbalanced data (55:45), k=100 → always predict majority class
```

**Why this impresses**:
- **Bias-variance trade-off**: k=1 high variance (overfitting), k=100 high bias (underfitting)
- **Validation strategy**: Cross-validation to select k (not arbitrary choice)
- **Dataset-aware**: Links to class imbalance (55:45) → large k dangerous

**Bonus Point** (if asked about optimal k heuristic):
"Optimal k ≈ √n heuristic → √11430 ≈ 107 → but this assumes balanced data. For imbalanced (55:45), k=5-9 safer to avoid majority-class dominance."

---

### Model 3: XGBoost (`src/models/xgboost_model.py`)

#### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/models/xgboost_model.py` | `XGBoostModel` | `__init__` | XGBoostModel initializes with hyperparameters | `max_depth`, `lr`, `n_estimators` | `XGBoostModel` instance |
| `src/models/xgboost_model.py` | `XGBoostModel` | `fit` | XGBoostModel trains gradient boosted trees | `X_train`, `y_train`, `X_val`, `y_val` | `None` (updates `self.model`) |
| `src/models/xgboost_model.py` | `XGBoostModel` | `predict_proba` | XGBoostModel generates probability scores | `X: np.array` | `np.array` (scores) |
| `src/models/xgboost_model.py` | `XGBoostModel` | `predict` | XGBoostModel generates binary predictions | `X`, `threshold` | `np.array` (0/1) |

#### Pseudocode (Interview-Ready Explanation)

```
CLASS XGBoostModel:
  FUNCTION __init__(max_depth=6, learning_rate=0.2, n_estimators=80):
    // XGBoostModel initializes with hyperparameters
    self.max_depth <- max_depth          // Tree depth (controls complexity)
    self.learning_rate <- learning_rate  // Shrinkage factor
    self.n_estimators <- n_estimators    // Number of trees
    self.model <- None
  END
  
  FUNCTION fit(X_train, y_train, X_val, y_val):
    // XGBoostModel trains gradient boosted trees
    // Uses validation set for early stopping
    
    // Configure class imbalance handling
    scale_pos_weight <- sum(y_train == 0) / sum(y_train == 1)  // ≈1.22 for 55:45
    
    self.model <- XGBClassifier(
      max_depth=self.max_depth,
      learning_rate=self.learning_rate,
      n_estimators=self.n_estimators,
      scale_pos_weight=scale_pos_weight,  // Handles class imbalance
      eval_metric='logloss',
      early_stopping_rounds=20            // Stop if val loss doesn't improve
    )
    
    // Train with validation monitoring
    self.model.fit(
      X_train, y_train,
      eval_set=[(X_val, y_val)],
      verbose=10  // Print every 10 iterations
    )
  END
  
  FUNCTION predict_proba(X: np.array) -> np.array:
    // XGBoostModel generates probability scores
    RETURN self.model.predict_proba(X)[:, 1]  // Return P(y=1)
  END
  
  FUNCTION predict(X, threshold=0.5) -> np.array:
    // XGBoostModel generates binary predictions
    proba <- self.predict_proba(X)
    RETURN (proba >= threshold).astype(int)
  END
END
```

#### Interview Deep Dive Questions (Q10 from FAQ)

**Q**: Why did XGBoost achieve ROC AUC=0.888 but FPR=18.22%?

**Your Answer** (Excellent-Level):
```python
# Root cause analysis
1. **Class imbalance** (55:45) → model biased toward majority class (legitimate sites)
   - Default threshold=0.5 optimizes F1-score, not FPR
   - Result: High recall (86.51%) but also high FPR (18.22%)

2. **Why XGBoost > LogReg**:
   - Captures non-linear interactions (tree splits on DomainAge × IsResponsive)
   - Ensemble reduces variance (80 trees average predictions)
   - scale_pos_weight=1.22 handles imbalance better than LogReg class_weight

3. **FPR=18% interpretation**:
   - 18% of legitimate sites flagged as phishing → 1 in 5 false alarm
   - Unacceptable for user trust → need threshold tuning

# Solution: Threshold tuning
threshold_tuned = 0.97  # Maximizes recall subject to FPR ≤ 3%
# Result: FPR=2.82% (meets KPI) but Recall=12% (fails KPI)
# Trade-off: Need better model (SMOTE, cost-sensitive learning)
```

**Why this impresses**:
- **Diagnostic reasoning**: Links ROC AUC (discrimination) vs FPR (operating point)
- **Class imbalance awareness**: Explains `scale_pos_weight` calculation
- **Business judgment**: Recognizes 18% FPR unacceptable → threshold tuning required

---

## STEP 6: EVALUATION & THRESHOLD TUNING (`src/evaluation.py`)

### Business Context
**Why this matters**: Default threshold=0.5 optimizes F1, not FPR → must tune to meet business KPI (FPR≤3%) while maximizing recall

### Responsibility Table

| Module | Class/Object | Function/Method | Responsibility (S-V-O) | Dependencies | Artifacts/Outputs |
|--------|--------------|-----------------|------------------------|--------------|-------------------|
| `src/evaluation.py` | `Evaluator` | `__init__` | Evaluator initializes with model and dataset splits | `model`, `X_val`, `y_val`, `X_test`, `y_test` | `Evaluator` instance |
| `src/evaluation.py` | `Evaluator` | `compute_confusion_matrix` | Evaluator calculates TP/FP/TN/FN from predictions | `y_true`, `y_pred` | `2×2 np.array` |
| `src/evaluation.py` | `Evaluator` | `compute_metrics` | Evaluator calculates precision/recall/F1/FPR from confusion matrix | `cm: np.array` | `dict` (metrics) |
| `src/evaluation.py` | `Evaluator` | `compute_roc_auc` | Evaluator calculates ROC AUC from probability scores | `y_true`, `y_scores` | `float` (AUC) |
| `src/evaluation.py` | `Evaluator` | `tune_threshold` | Evaluator finds optimal threshold maximizing recall subject to FPR constraint | `max_fpr: float` | `dict` (threshold, metrics) |
| `src/evaluation.py` | `Evaluator` | `evaluate_test_set` | Evaluator applies tuned threshold to test set for final metrics | `threshold: float` | `dict` (test metrics) |

### Pseudocode (Interview-Ready Explanation)

```
CLASS Evaluator:
  FUNCTION __init__(model, X_val, y_val, X_test, y_test):
    // Evaluator initializes with model and dataset splits
    self.model <- model
    self.X_val <- X_val
    self.y_val <- y_val
    self.X_test <- X_test
    self.y_test <- y_test
  END
  
  FUNCTION compute_confusion_matrix(y_true, y_pred) -> np.array:
    // Evaluator calculates TP/FP/TN/FN from predictions
    //           Predicted
    //         Neg    Pos
    // Actual Neg  [[TN,    FP],
    //        Pos   [FN,    TP]]
    
    TN <- sum((y_true == 0) & (y_pred == 0))
    FP <- sum((y_true == 0) & (y_pred == 1))
    FN <- sum((y_true == 1) & (y_pred == 0))
    TP <- sum((y_true == 1) & (y_pred == 1))
    
    RETURN np.array([[TN, FP], [FN, TP]])
  END
  
  FUNCTION compute_metrics(cm: np.array) -> dict:
    // Evaluator calculates precision/recall/F1/FPR from confusion matrix
    
    TN, FP, FN, TP <- cm[0,0], cm[0,1], cm[1,0], cm[1,1]
    
    precision <- TP / (TP + FP) IF (TP + FP) > 0 ELSE 0
    recall <- TP / (TP + FN) IF (TP + FN) > 0 ELSE 0
    f1 <- 2 * (precision * recall) / (precision + recall) IF (precision + recall) > 0 ELSE 0
    fpr <- FP / (FP + TN) IF (FP + TN) > 0 ELSE 0
    
    RETURN {
      "precision": precision,
      "recall": recall,
      "f1": f1,
      "fpr": fpr
    }
  END
  
  FUNCTION compute_roc_auc(y_true, y_scores) -> float:
    // Evaluator calculates ROC AUC from probability scores
    // Rank-based method: AUC = P(score(positive) > score(negative))
    
    // Sort by scores descending
    sorted_indices <- np.argsort(y_scores)[::-1]
    y_sorted <- y_true[sorted_indices]
    
    // Count concordant pairs
    n_pos <- sum(y_true == 1)
    n_neg <- sum(y_true == 0)
    
    concordant <- 0
    pos_count <- 0
    FOR i IN range(len(y_sorted)):
      IF y_sorted[i] == 1:
        pos_count += 1
      ELSE:
        concordant += pos_count  // All positives ranked higher than this negative
    
    auc <- concordant / (n_pos * n_neg)
    RETURN auc
  END
  
  FUNCTION tune_threshold(max_fpr=0.03) -> dict:
    // Evaluator finds optimal threshold maximizing recall subject to FPR constraint
    
    y_scores <- self.model.predict_proba(self.X_val)
    
    best_threshold <- 0.5
    best_recall <- 0.0
    
    // Sweep thresholds from 0.0 to 1.0
    FOR threshold IN np.linspace(0.0, 1.0, 1001):
      y_pred <- (y_scores >= threshold).astype(int)
      cm <- self.compute_confusion_matrix(self.y_val, y_pred)
      metrics <- self.compute_metrics(cm)
      
      // Check FPR constraint
      IF metrics["fpr"] <= max_fpr:
        // Maximize recall among valid thresholds
        IF metrics["recall"] > best_recall:
          best_recall <- metrics["recall"]
          best_threshold <- threshold
          best_metrics <- metrics
    
    RETURN {
      "threshold": best_threshold,
      "recall": best_recall,
      "fpr": best_metrics["fpr"],
      "confusion_matrix": cm
    }
  END
  
  FUNCTION evaluate_test_set(threshold: float) -> dict:
    // Evaluator applies tuned threshold to test set for final metrics
    
    y_scores <- self.model.predict_proba(self.X_test)
    y_pred <- (y_scores >= threshold).astype(int)
    
    cm <- self.compute_confusion_matrix(self.y_test, y_pred)
    metrics <- self.compute_metrics(cm)
    roc_auc <- self.compute_roc_auc(self.y_test, y_scores)
    
    RETURN {
      "threshold": threshold,
      "roc_auc": roc_auc,
      "confusion_matrix": cm.tolist(),
      **metrics  // Unpack precision/recall/f1/fpr
    }
  END
END
```

### Interview Deep Dive Questions (Q12, Q13 from FAQ)

**Q12**: Explain ROC AUC calculation WITHOUT using sklearn.

**Your Answer** (Excellent-Level):
```python
# Rank-based method: AUC = P(score(positive) > score(negative))

def compute_roc_auc_manual(y_true, y_scores):
    # Sort by scores descending
    sorted_indices = np.argsort(y_scores)[::-1]
    y_sorted = y_true[sorted_indices]
    
    # Count concordant pairs (positive scored higher than negative)
    n_pos = np.sum(y_true == 1)
    n_neg = np.sum(y_true == 0)
    
    concordant = 0
    pos_count = 0
    for label in y_sorted:
        if label == 1:
            pos_count += 1  # Accumulate positives seen so far
        else:
            concordant += pos_count  # This negative ranked below pos_count positives
    
    auc = concordant / (n_pos * n_neg)
    return auc

# Example: XGBoost ROC AUC = 0.888
# Interpretation: 88.8% chance model ranks random phishing site higher than random legitimate site
```

**Why this impresses**:
- **Algorithm understanding**: Explains rank-based method (not just sklearn API)
- **Probabilistic interpretation**: AUC as pairwise ranking probability
- **Validation**: Matches sklearn output (self-tested)

---

**Q13**: Your tuned threshold for XGBoost is 0.97 (Recall=12%, FPR=2.82%). Is this production-ready?

**Your Answer** (Excellent-Level):
```python
# Analysis
threshold = 0.97
recall = 0.12    # Catches only 12% of phishing attacks
fpr = 0.0282     # 2.82% false alarms on legitimate sites

# Production readiness: NO
1. **Recall=12% violates KPI** (target: ≥70%)
   - Missing 88% of phishing attacks → unacceptable fraud exposure
   - Customer impact: 8.8 out of 10 phishing sites bypass detection

2. **FPR=2.82% meets KPI** (target: ≤3%)
   - Low false alarms → good user trust
   - But useless if we miss 88% of attacks

# CEO pitch (honest assessment)
"Current model unsuitable for autonomous blocking:
- Option A: Deploy as 'soft warning' (show alert but allow access) + human review
- Option B: Parallel track → retrain with SMOTE or cost-sensitive learning to hit Recall≥70%
- Timeline: 2-week sprint for Option B, interim deploy Option A for data collection"

# Next steps (if given 24 hours)
1. Relax FPR to 10% (threshold ≈ 0.6) → Recall ≈ 70% (meets KPI)
2. Deploy with human-in-loop for borderline scores (0.5-0.6)
3. Commit to improved model within 1 week
```

**Why this impresses**:
- **Business judgment**: Recognizes Recall failure, doesn't blindly deploy
- **Stakeholder communication**: Translates metrics to customer impact ("8.8 out of 10 attacks missed")
- **Pragmatic solutions**: Proposes interim deployment (soft warnings) while improving model

---

## FINAL INTERVIEW PREP CHECKLIST

### Pre-Interview (Night Before)

**Technical Deep Dive** (4 hours):
- [ ] Re-run pipeline: `bash run.sh` → verify outputs match submission
- [ ] Trace one sample through pipeline: Load → Engineer → Preprocess → Split → Train → Evaluate
- [ ] Explain each step out loud (record yourself, aim for <2 min per step)
- [ ] Memorize key numbers: 11,430 rows, 55:45 imbalance, r=0.333 (DomainAge), 377 negative values, 10 skewed features

**EDA Findings Linkage** (2 hours):
- [ ] Map each preprocessing decision to EDA finding (use table from README)
- [ ] Practice: "Why log-transform?" → "EDA showed 10 features |skew|>1 → heavy tails → gradient instability"
- [ ] Identify top 3 weaknesses in submission (e.g., no hyperparameter tuning evidence, all models fail KPIs)

**Code Walkthrough** (2 hours):
- [ ] Open `src/preprocessing.py` → explain `fit_transform` vs `transform` line-by-line
- [ ] Open `src/models/logistic_regression.py` → derive gradient descent update rule on paper
- [ ] Open `src/evaluation.py` → calculate ROC AUC manually for 5 samples

---

### Interview Day

**Presentation (10 minutes)**:
Structure (3 parts):
1. **Problem** (2 min): Class imbalance + data quality issues → stratified splits + preprocessing roadmap
2. **Solution** (5 min): Show Mermaid diagram → highlight 3 models + threshold tuning
3. **Results + Weaknesses** (3 min): ROC AUC 0.81-0.89 BUT FPR 18-29% at default threshold → Honest: "All models fail KPIs at FPR≤3%, need SMOTE/ensemble"

**Slides** (optional but recommended):
- Slide 1: Title + Name + Email
- Slide 2: EDA Key Findings (class imbalance, top predictor, 377 invalid values)
- Slide 3: Pipeline Flow (Mermaid diagram from README)
- Slide 4: Model Comparison Table (ROC AUC, FPR, Recall)
- Slide 5: Threshold Tuning Trade-off (chart: Recall vs FPR)
- Slide 6: Honest Assessment + Next Steps (SMOTE, cost-sensitive learning)

**Q&A Survival Tactics** (50 minutes):
- [ ] **If stuck**: "Let me think through this step-by-step" → draw on paper
- [ ] **If wrong**: "You're right, I should have validated that" → shows learning mindset
- [ ] **If unknown**: "I don't know X, but I would research Y approach" → resourcefulness

---

## SUCCESS CRITERIA

### Minimum Viable Performance (Pass Threshold: 60/100)

**Must Demonstrate**:
- ✅ Correct explanation of stratified splitting (Q from EDA Competency)
- ✅ Correct explanation of fit_transform vs transform (Q6 from Preprocessing)
- ✅ Correct ROC AUC interpretation (Q12 from Evaluation)
- ✅ Acknowledge KPI failure honestly (Q13 from Evaluation)

**Can Afford to Miss**:
- Advanced hyperparameter tuning (grid search evidence)
- SHAP values for XGBoost explainability
- Ablation studies for feature engineering

---

### Strong Performance (Target: 75-85/100)

**Additional Demonstrations**:
- ✅ Derive gradient descent update rule on whiteboard (Q9)
- ✅ Explain k=5 choice with cross-validation evidence (Q11)
- ✅ Propose concrete next steps (SMOTE, class weights, ensemble)
- ✅ Show GitHub Actions CI/CD understanding

---

## POST-INTERVIEW REFLECTION

**If Rejected**:
- Request feedback from panel (if allowed)
- Identify weakest category (EDA/Preprocessing/Model/Evaluation/Code)
- Retake online courses (Fast.ai, Coursera Andrew Ng) → reapply next batch

**If Accepted**:
- Immediately start AIAP prep:
  - Practice group exercises (case studies under time pressure)
  - Strengthen weak areas (e.g., hyperparameter tuning, model interpretability)
  - Familiarize with production MLOps (Docker, Kubernetes, monitoring)

---

**END OF INTERVIEWEE GUIDE**

**Final Reminder**: This interview is your LAST CHANCE. The panel knows your submission has gaps—your job is to prove you **UNDERSTAND THE FUNDAMENTALS** despite poor results. Be honest, show learning mindset, and demonstrate you can improve with mentorship. Good luck! 🚀