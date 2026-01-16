# EDA-MLP Detailed Implementation LOD Steps - Interview Preparation Guide

**Version**: Interview Prep 1.0  
**Purpose**: Step-by-step roadmap from clean slate to qualified-to-excellent submission with FAQs and scoring rubrics  
**Target Audience**: Candidates with zero EDA/MLP experience preparing for AIAP22 Interview Session

---

## 🎯 Executive Summary: Your Success Blueprint

### Current Situation Analysis
- **Your Starting Point**: Virtually zero EDA/MLP experience
- **Your Submission**: Performed poorly against assessment criteria
- **Your Opportunity**: Last chance to redo from scratch before interview
- **Time Constraint**: Limited window to demonstrate competence

### What Interviewers Are Looking For
1. **Technical Competence**: Can you build a working ML pipeline?
2. **Communication Skills**: Can you explain your choices clearly?
3. **Problem-Solving**: Do you understand why you made each decision?
4. **Team Readiness**: Can you contribute to the Group Exercise?

### Your 10-Minute Presentation Strategy
**DO**:
- Start with business impact ("I built a phishing detector that catches 86% of attacks")
- Show 1-2 compelling visualizations from EDA
- Explain your top 3 design decisions with business rationale
- End with deployment considerations

**DON'T**:
- Read code line-by-line from your notebook
- Show every chart you made
- Apologize for what you didn't do
- Rush through technical jargon without explaining

---

## 📊 Scoring Rubric: Poor → Qualified → Excellent

### Task 1: EDA Jupyter Notebook

| Criterion | Poor (0-3) | Qualified (4-6) | Excellent (7-10) | Your Action Plan |
|-----------|-----------|-----------------|------------------|------------------|
| **Organization** | Random cells, no markdown | Sections with headers | Clear story arc with business context | Use this template: Problem → Data → Analysis → Insights → Recommendations |
| **Visualizations** | Excel-quality charts, no titles | Proper labels, 3-5 relevant plots | Publication-ready, annotated, tells a story | Every chart needs: title, axis labels, interpretation paragraph |
| **Statistical Rigor** | Just `.describe()` | Correlation matrix, outlier detection | Hypothesis tests, confidence intervals, effect sizes | Calculate: correlation with target, IQR outliers, skewness for transforms |
| **Business Translation** | "DomainAgeMonths has mean 15.3" | "Younger domains correlate with phishing" | "55% baseline → 86% model = $2M fraud prevented" | Link every finding to: fraud risk, customer trust, or deployment feasibility |
| **Code Quality** | Copy-paste from internet | Works but messy | Reusable functions, clear variable names | Create helper functions for: plot_distribution(), detect_outliers(), calculate_correlation() |

**Your Improvement Path**:
1. **Poor → Qualified**: Add section headers, fix chart labels, calculate correlation matrix
2. **Qualified → Excellent**: Write business interpretations, create summary tables, add statistical tests

---

### Task 2: ML Pipeline (Python Scripts)

| Criterion | Poor (0-3) | Qualified (4-6) | Excellent (7-10) | Your Action Plan |
|-----------|-----------|-----------------|------------------|------------------|
| **run.sh Execution** | Crashes with errors | Runs but hardcoded paths | Configurable, validates environment | Add checks: venv active? phishing.db exists? Creates required directories |
| **Code Structure** | One giant script | Functions but no classes | Clean OOP, separation of concerns | Structure: data_loader.py, preprocessing.py, models/, evaluation.py |
| **Preprocessing** | No handling of negatives/NaNs | Median imputation, standard scaling | Log-transforms for skew, missing-value flags, domain bins | Implement: clip NoOfImage<0, log-transform 10 features, create DomainAgeMonths_missing flag |
| **Model Selection** | Single model (e.g., only LogReg) | 3 diverse models trained | Justified choices with trade-offs | Train: LogReg (fast, interpretable), KNN (non-parametric), XGBoost (ensemble); explain why each |
| **Evaluation** | Just accuracy | Precision, recall, F1 | ROC/PR curves, threshold tuning, confusion matrix analysis | Calculate: ROC AUC, tune threshold for FPR≤5%, analyze high-confidence errors |
| **README.md** | Installation steps only | Covers requirements | Business problem → solution → deployment | Structure: Problem, Solution, Quick Start, EDA→Pipeline Decisions, Model Comparison, Deployment |

**Your Improvement Path**:
1. **Poor → Qualified**: Fix run.sh errors, add preprocessing steps, train 3 models
2. **Qualified → Excellent**: Add threshold tuning, write business-focused README, create deployment section

---

## 🚀 Clean Slate Implementation Roadmap

### Phase 0: Pre-Work (2 hours)
**Goal**: Set up environment and validate dataset

#### Step 0.1: Environment Setup
```bash
# Create project structure
mkdir -p aiap22-yourname-XXXX/{src,data,models,results,notebooks}
cd aiap22-yourname-XXXX
python3 -m venv .venv
source .venv/bin/activate

# Install dependencies
cat > requirements.txt << 'EOF'
pandas==2.0.3
numpy==1.24.3
matplotlib==3.7.1
seaborn==0.12.2
scikit-learn==1.3.0
xgboost==2.0.3
pyyaml==6.0
EOF

pip install -r requirements.txt
```

**FAQ**: *Q: Do I need these exact versions?* A: Pin major versions (2.0.x is fine) to prevent breaking changes; minor versions flexible.

#### Step 0.2: Download and Validate Dataset
```python
# In notebooks/00_data_validation.ipynb
import sqlite3
import pandas as pd

# Download phishing.db from assessment URL
# Place in data/phishing.db

conn = sqlite3.connect('data/phishing.db')
df = pd.read_sql_query("SELECT * FROM phishing_data", conn)
conn.close()

print(f"✓ Loaded {len(df):,} rows × {len(df.columns)} columns")
print(f"✓ Target: {df['label'].value_counts().to_dict()}")
assert len(df) == 11430, "Row count mismatch!"
assert 'label' in df.columns, "Missing target!"
```

**Scoring Impact**: Validates dataset before EDA (prevents errors during interview demo)

---

### Phase 1: EDA (Jupyter Notebook) - 6 hours
**Goal**: Create compelling eda.ipynb that tells a fraud detection story

#### Step 1.1: Dataset Profiling (1 hour)
**Action Items**:
1. Shape, memory, dtypes → basic stats table
2. Class distribution → bar chart with percentages
3. Missing value heatmap → identify MNAR patterns

**Code Template**:
```python
# Cell 1: Setup
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

# Cell 2: Load Data
df = pd.read_sql_query("SELECT * FROM phishing_data", conn)

# Cell 3: Profile Shape
print(f"Dataset: {df.shape[0]:,} rows × {df.shape[1]} columns")
print(f"Memory: {df.memory_usage(deep=True).sum()/1024/1024:.2f} MB")

# Cell 4: Class Distribution (BUSINESS-FOCUSED)
counts = df['label'].value_counts()
plt.figure(figsize=(8, 5))
bars = plt.bar(['Phishing (0)', 'Legitimate (1)'], counts.values, color=['#e03131', '#2b8a3e'])
plt.title('Fraud Exposure: 55% Baseline Accuracy = 45% Missed Attacks', fontsize=14, fontweight='bold')
for bar, count in zip(bars, counts.values):
    plt.text(bar.get_x() + bar.get_width()/2., count, f'{count}\n({count/len(df)*100:.1f}%)', 
             ha='center', va='bottom')
plt.ylabel('Count')
plt.tight_layout()
plt.savefig('../results/class_distribution.png', dpi=100)
plt.show()

# Cell 5: Interpretation
print("🎯 BUSINESS IMPACT:")
print("- Baseline: 55.04% (naive 'always predict legitimate')")
print("- Risk: Untrained model would miss 44.96% of phishing attacks")
print("- Action: Stratified splits required to prevent bias toward majority class")
```

**FAQ**: *Q: Why emphasize business impact?* A: Interviewers want to see you understand real-world consequences, not just technical mechanics.

**Scoring Rubric**:
- **Poor**: Just shows `df.head()` and `df.describe()`
- **Qualified**: Class distribution chart + baseline accuracy calculation
- **Excellent**: Above + business interpretation (fraud exposure) + stratification justification

---

#### Step 1.2: Univariate Analysis (2 hours)
**Action Items**:
1. Histogram grid for numeric features → identify skewness
2. Box plots for top 5 features → outlier detection
3. Categorical frequency tables → rare category analysis

**Key Insight to Highlight**:
```python
# Cell 6: Skewness Analysis
skew_df = pd.DataFrame({
    'feature': df.select_dtypes(include=[np.number]).columns,
    'skewness': df.select_dtypes(include=[np.number]).skew().values
}).sort_values('skewness', key=abs, ascending=False)

print("🔍 PREPROCESSING DECISION:")
print(f"- {(abs(skew_df['skewness']) > 1).sum()} features need log-transform (|skew| > 1)")
print("- Rationale: Heavy-tailed distributions reduce model convergence")
print("\nTop 5 Skewed Features:")
print(skew_df.head().to_string(index=False))
```

**Scoring Rubric**:
- **Poor**: No skewness analysis
- **Qualified**: Identifies skewed features
- **Excellent**: Links skewness → log-transform → preprocessing decision

---

#### Step 1.3: Correlation Analysis (1.5 hours)
**Action Items**:
1. Correlation matrix heatmap → multicollinearity check
2. Target correlation bar chart → feature importance ranking
3. Document top 10 predictors for README

**Critical Code**:
```python
# Cell 7: Target Correlation
target_corr = df.select_dtypes(include=[np.number]).corrwith(df['label']).abs().sort_values(ascending=False)
target_corr = target_corr.drop('label')  # Remove self-correlation

plt.figure(figsize=(10, 6))
plt.barh(range(10), target_corr.head(10).values, color='#1c7ed6')
plt.yticks(range(10), target_corr.head(10).index)
plt.xlabel('Absolute Correlation with Phishing Risk')
plt.title('Top 10 Predictive Features: Fraud Detection Priority', fontsize=14, fontweight='bold')
plt.gca().invert_yaxis()
plt.tight_layout()
plt.savefig('../results/target_correlation.png', dpi=100)
plt.show()

print("📊 FEATURE ENGINEERING INSIGHT:")
print(f"- Top Predictor: {target_corr.index[0]} (r={target_corr.iloc[0]:.3f})")
print("- Missing values in top predictor → create missing-value flag")
print("- Rationale: MNAR pattern (phishing sites hide metadata)")
```

**Interview Preparation**: Memorize your top 3 predictors and why they matter for phishing detection.

**Scoring Rubric**:
- **Poor**: No correlation analysis
- **Qualified**: Correlation heatmap + identifies top predictor
- **Excellent**: Above + explains MNAR → missing-value flags + business justification

---

#### Step 1.4: Data Quality Report (1.5 hours)
**Action Items**:
1. Identify impossible values (`NoOfImage < 0`)
2. Calculate outlier percentages (IQR method)
3. Create actionable recommendations table

**Template**:
```python
# Cell 8: Data Quality Issues
issues = {
    'Impossible Values': f"{(df['NoOfImage'] < 0).sum()} rows with NoOfImage < 0",
    'High Missingness': f"{(df.isna().mean() > 0.7).sum()} features > 70% missing",
    'Outliers': f"{outlier_counts.max():.1f}% in {outlier_counts.idxmax()}",
    'Class Imbalance': f"55:45 ratio → stratified splits required"
}

print("🚨 CRITICAL QUALITY ISSUES:")
for issue, detail in issues.items():
    print(f"- {issue}: {detail}")
```

**Scoring Rubric**:
- **Poor**: No data quality section
- **Qualified**: Lists issues without recommendations
- **Excellent**: Issues + actionable preprocessing plan + business impact

---

### Phase 2: ML Pipeline (Python Scripts) - 8 hours
**Goal**: Create production-ready pipeline that passes run.sh execution

#### Step 2.1: Data Loader (1 hour)
**File**: `src/data_loader.py`

**Template**:
```python
import sqlite3
import pandas as pd

class DataLoader:
    def __init__(self, db_path='data/phishing.db'):
        self.db_path = db_path
    
    def load(self):
        """Load data from SQLite and validate schema."""
        try:
            conn = sqlite3.connect(self.db_path)
            df = pd.read_sql_query("SELECT * FROM phishing_data", conn)
            conn.close()
        except sqlite3.Error as e:
            raise RuntimeError(f"Database error: {e}")
        
        # Validate schema
        assert len(df) >= 1000, f"Insufficient rows: {len(df)}"
        assert 'label' in df.columns, "Missing target column"
        assert set(df['label'].unique()) == {0, 1}, "Invalid label encoding"
        
        print(f"✓ Loaded {len(df):,} rows × {len(df.columns)} columns")
        return df

# Usage in main.py:
# df = DataLoader().load()
```

**FAQ**: *Q: Why assert statements?* A: Fail-fast principle; better to crash early with clear error than corrupt results later.

**Scoring Rubric**:
- **Poor**: Hardcoded paths, no error handling
- **Qualified**: Error handling + schema validation
- **Excellent**: Configurable paths + assertion messages + logging

---

#### Step 2.2: Preprocessing Pipeline (2.5 hours)
**File**: `src/preprocessing.py`

**EDA-Driven Implementation**:
```python
import numpy as np
import pandas as pd
from sklearn.preprocessing import StandardScaler

class Preprocessor:
    def __init__(self):
        self.scalers = {}
        self.fill_values = {}
    
    def fit(self, df, target_col='label'):
        """Learn preprocessing parameters from training data."""
        X = df.drop(columns=[target_col])
        
        # Step 1: Fix impossible values (EDA finding: 377 rows NoOfImage < 0)
        X['NoOfImage'] = X['NoOfImage'].clip(lower=0)
        
        # Step 2: Learn imputation values
        numeric_cols = X.select_dtypes(include=[np.number]).columns
        for col in numeric_cols:
            self.fill_values[col] = X[col].median()  # Median robust to outliers
        
        # Step 3: Create missing-value flags (EDA: MNAR pattern in top predictors)
        for col in ['DomainAgeMonths', 'Robots', 'IsResponsive']:
            X[f'{col}_missing'] = X[col].isna().astype(int)
        
        # Step 4: Learn scaling parameters
        for col in numeric_cols:
            self.scalers[col] = StandardScaler()
            self.scalers[col].fit(X[[col]].fillna(self.fill_values[col]))
        
        return self
    
    def transform(self, df, target_col='label'):
        """Apply learned transformations."""
        X = df.drop(columns=[target_col]) if target_col in df else df.copy()
        
        # Apply all fit steps in same order
        X['NoOfImage'] = X['NoOfImage'].clip(lower=0)
        
        for col in ['DomainAgeMonths', 'Robots', 'IsResponsive']:
            X[f'{col}_missing'] = X[col].isna().astype(int)
        
        numeric_cols = X.select_dtypes(include=[np.number]).columns
        for col in numeric_cols:
            if col in self.fill_values:
                X[col] = X[col].fillna(self.fill_values[col])
            if col in self.scalers:
                X[col] = self.scalers[col].transform(X[[col]])
        
        return X
```

**Scoring Rubric**:
- **Poor**: No preprocessing or copy-paste sklearn Pipeline
- **Qualified**: Handles missing values + scaling
- **Excellent**: EDA-driven (fixes negatives, missing flags) + fit/transform pattern + comments linking to EDA

---

#### Step 2.3: Model Training (2 hours)
**File**: `src/models/logistic_regression.py`, `knn.py`, `xgboost_model.py`

**Logistic Regression (Gradient Descent)**:
```python
import numpy as np

class LogisticRegression:
    def __init__(self, lr=0.1, epochs=120):
        self.lr = lr
        self.epochs = epochs
        self.weights = None
    
    def _sigmoid(self, z):
        return 1 / (1 + np.exp(-np.clip(z, -500, 500)))  # Prevent overflow
    
    def fit(self, X, y):
        X = np.c_[np.ones(len(X)), X]  # Add intercept
        self.weights = np.zeros(X.shape[1])
        
        for epoch in range(self.epochs):
            predictions = self._sigmoid(X @ self.weights)
            gradient = X.T @ (predictions - y) / len(y)
            self.weights -= self.lr * gradient
        
        return self
    
    def predict_proba(self, X):
        X = np.c_[np.ones(len(X)), X]
        return self._sigmoid(X @ self.weights)
    
    def predict(self, X, threshold=0.5):
        return (self.predict_proba(X) >= threshold).astype(int)
```

**Interview Prep**: Be ready to explain why you used gradient descent (interpretable coefficients) vs sklearn's LogisticRegression (solver='lbfgs').

**Scoring Rubric**:
- **Poor**: Only uses sklearn models (no custom implementation)
- **Qualified**: 1 custom model (LogReg) + 2 sklearn models
- **Excellent**: All 3 models justified + gradient descent implemented correctly + overflow handling

---

#### Step 2.4: Evaluation & Threshold Tuning (1.5 hours)
**File**: `src/evaluation.py`

**Critical Implementation**:
```python
def calculate_roc_auc(y_true, y_scores):
    """Calculate ROC AUC without sklearn (rank-based method)."""
    positive_scores = y_scores[y_true == 1]
    negative_scores = y_scores[y_true == 0]
    
    # Count pairs where positive scored higher than negative
    pairs_correct = sum(pos > neg for pos in positive_scores for neg in negative_scores)
    total_pairs = len(positive_scores) * len(negative_scores)
    
    return pairs_correct / total_pairs if total_pairs > 0 else 0.5

def tune_threshold(y_true, y_scores, max_fpr=0.05):
    """Find threshold maximizing recall subject to FPR constraint."""
    thresholds = np.linspace(0, 1, 1001)
    best_threshold, best_recall = 0.5, 0.0
    
    for threshold in thresholds:
        y_pred = (y_scores >= threshold).astype(int)
        
        # Calculate FPR and recall
        tn = ((y_true == 0) & (y_pred == 0)).sum()
        fp = ((y_true == 0) & (y_pred == 1)).sum()
        fn = ((y_true == 1) & (y_pred == 0)).sum()
        tp = ((y_true == 1) & (y_pred == 1)).sum()
        
        fpr = fp / (fp + tn) if (fp + tn) > 0 else 0
        recall = tp / (tp + fn) if (tp + fn) > 0 else 0
        
        if fpr <= max_fpr and recall > best_recall:
            best_recall = recall
            best_threshold = threshold
    
    return best_threshold, best_recall
```

**Interview Question**: *"Why tune threshold on validation set?"*  
**Your Answer**: "To prevent overfitting to test set. Validation set gives unbiased estimate of threshold performance."

**Scoring Rubric**:
- **Poor**: No threshold tuning (uses default 0.5)
- **Qualified**: Tunes threshold on test set (data leakage!)
- **Excellent**: Validation-based tuning + FPR constraint + documents trade-off (recall vs FPR)

---

#### Step 2.5: run.sh & Main Orchestrator (1 hour)
**File**: `run.sh`

```bash
#!/bin/bash
set -e  # Exit on error

# Validate environment
if [ -z "$VIRTUAL_ENV" ]; then
    echo "❌ Error: Virtual environment not activated"
    echo "Run: source .venv/bin/activate"
    exit 1
fi

if [ ! -f "data/phishing.db" ]; then
    echo "❌ Error: data/phishing.db not found"
    echo "Download from: https://techassessment.blob.core.windows.net/aiap22-assessment-data/phishing.db"
    exit 1
fi

# Create directories
mkdir -p models results data/processed

# Run pipeline
echo "🚀 Starting ML Pipeline..."
python -m src.main

echo "✅ Pipeline complete! Results in results/baseline_metrics.json"
```

**File**: `src/main.py`

```python
import json
from data_loader import DataLoader
from preprocessing import Preprocessor
from data_splitter import DataSplitter
from models.logistic_regression import LogisticRegression
from models.knn import KNN
from models.xgboost_model import XGBoostModel
from evaluation import calculate_metrics, tune_threshold

def main():
    # Load data
    df = DataLoader().load()
    
    # Split data (70/15/15 stratified)
    splitter = DataSplitter(random_state=42)
    train, val, test = splitter.split(df, test_size=0.15, val_size=0.15)
    
    # Preprocess
    preprocessor = Preprocessor()
    X_train = preprocessor.fit(train).transform(train)
    X_val = preprocessor.transform(val)
    X_test = preprocessor.transform(test)
    
    y_train, y_val, y_test = train['label'], val['label'], test['label']
    
    # Train models
    models = {
        'logistic': LogisticRegression(lr=0.1, epochs=120),
        'knn': KNN(k=5),
        'xgboost': XGBoostModel(max_depth=6, learning_rate=0.2, n_estimators=80)
    }
    
    results = []
    for name, model in models.items():
        print(f"\n🔧 Training {name}...")
        model.fit(X_train, y_train)
        
        # Evaluate on validation set
        y_scores = model.predict_proba(X_val)
        tuned_threshold, tuned_recall = tune_threshold(y_val, y_scores, max_fpr=0.05)
        
        # Apply tuned threshold to test set
        y_pred_test = (model.predict_proba(X_test) >= tuned_threshold).astype(int)
        metrics = calculate_metrics(y_test, y_pred_test)
        
        results.append({
            'model': name,
            'tuned_threshold': tuned_threshold,
            'test_metrics': metrics
        })
    
    # Save results
    with open('results/baseline_metrics.json', 'w') as f:
        json.dump(results, f, indent=2)
    
    print("\n✅ Results saved to results/baseline_metrics.json")

if __name__ == '__main__':
    main()
```

**Scoring Rubric**:
- **Poor**: run.sh crashes or requires manual edits
- **Qualified**: Runs end-to-end but no validation checks
- **Excellent**: Pre-flight checks + creates dirs + clear error messages + saves all artifacts

---

### Phase 3: Documentation (README.md) - 2 hours
**Goal**: Create interview-ready README that showcases business understanding

#### Template Structure

```markdown
# Phishing Detection ML Pipeline - AIAP Batch 22

**Full Name:** [Your Name]  
**Email:** [Your Email]

## Executive Summary

### Business Problem
CyberProtect users face credential theft from phishing attacks. Need **real-time detection** for browser extension.

### Solution Delivered
End-to-end ML pipeline with **3 production-ready models**:
- **XGBoost**: 86.51% recall, 18.22% FPR (best overall)
- **Logistic Regression**: 81.20% recall, interpretable coefficients
- **KNN**: 82.35% recall, non-parametric baseline

### Key Results
- ✅ **Fraud Reduction**: 55% baseline → 86% model = 31% improvement
- ✅ **ROC AUC**: 0.888 (XGBoost) meets 0.80 requirement
- ⚠️ **FPR Trade-off**: Tuned threshold (FPR≤3%) reduces recall to 12% → recommend deployment threshold balancing trust vs security

---

## Quick Start

```bash
# Setup
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# Download data (place in data/phishing.db)
# URL: https://techassessment.blob.core.windows.net/aiap22-assessment-data/phishing.db

# Run pipeline
bash run.sh

# View results
cat results/baseline_metrics.json
```

---

## EDA Findings → Pipeline Decisions

| EDA Finding | Business Impact | Pipeline Solution |
|-------------|----------------|-------------------|
| **DomainAgeMonths** strongest predictor (r=0.333) | Missing values lose top signal | Median imputation + risk binning |
| **377 negative NoOfImage** | Impossible data → invalid patterns | Clip to 0 |
| **10 features |skew| > 1** | Poor convergence | Log-transform |
| **55:45 class imbalance** | Naive split → distribution shift | Stratified sampling |

---

## Model Selection Rationale

| Model | Why Selected | Trade-offs |
|-------|-------------|------------|
| **Logistic Regression** | ✅ Interpretable coefficients (regulatory)<br>✅ Fast inference (~1ms) | ❌ Linear boundary misses complex patterns |
| **KNN** | ✅ Non-parametric (captures local patterns) | ❌ Slow inference (distance calculations) |
| **XGBoost** | ✅ Industry standard for fraud detection<br>✅ Handles imbalance natively | ❌ Black-box (requires SHAP for explainability) |

---

## Evaluation Metrics Explained

- **ROC AUC**: 0.888 → 88.8% chance model ranks random phishing higher than legitimate
- **Recall**: 86.51% → catches 86.51% of phishing attacks (misses 13.49%)
- **FPR**: 18.22% → 18.22% of legitimate sites flagged as phishing (false alarms)

**Business Decision**: Recommend threshold=0.65 (balances recall 86% + FPR 18%) over strict FPR≤3% (recall drops to 12%).

---

## Deployment Considerations

**Technical Requirements**:
- Latency: <100ms inference (XGBoost ~15MB model achieves this)
- Memory: <100MB total (current: 23MB)
- Throughput: 100K+ predictions/day (horizontal scaling via Kubernetes)

**Monitoring**:
- Track feature drift in top 3 predictors (DomainAgeMonths, IsResponsive, Robots)
- Alert if recall drops below 70% on weekly phishing samples
- Retrain quarterly (phishing tactics evolve ~3-6 month cycles)
```

**Scoring Rubric**:
- **Poor**: Installation steps only, no business context
- **Qualified**: Covers technical requirements, missing business impact
- **Excellent**: Business problem → solution → results → deployment with quantified impact

---

## 🎤 Interview Presentation Strategy (10 Minutes)

### Slide 1: Problem & Impact (1 min)
**Script**: "CyberProtect users face phishing attacks leading to credential theft. My task was to build an automated detection system for a browser extension. The business impact: reducing fraud exposure from 45% missed attacks to 13%."

### Slide 2: EDA Highlights (2 min)
**Show**: Class distribution chart + top 10 predictors bar chart  
**Script**: "I started with EDA. Key findings: 55:45 class imbalance requires stratified splits. DomainAgeMonths is the strongest predictor—younger domains correlate with phishing. I also found 377 impossible values (negative image counts) and 10 heavily skewed features requiring log-transforms."

### Slide 3: Pipeline Architecture (2 min)
**Show**: Mermaid flowchart from README  
**Script**: "My pipeline follows this flow: SQLite load → preprocessing (clip negatives, log-transforms, missing-value flags) → stratified 70/15/15 split → train 3 models → threshold tuning on validation set → test evaluation. Each step addresses an EDA finding."

### Slide 4: Model Comparison (2 min)
**Show**: Table with recall, FPR, ROC AUC for 3 models  
**Script**: "I trained 3 diverse models: Logistic Regression for interpretability, KNN for non-parametric flexibility, XGBoost for performance. XGBoost achieves 86% recall but 18% FPR. I tuned thresholds on validation set to balance fraud detection vs false alarms."

### Slide 5: Deployment & Next Steps (2 min)
**Show**: Deployment considerations table  
**Script**: "For production, I recommend XGBoost with threshold=0.65. This meets latency (<100ms) and memory (<100MB) requirements. Key monitoring: track feature drift in DomainAgeMonths, retrain quarterly. Trade-off: achieving FPR≤3% reduces recall to 12%—I recommend balancing customer trust vs security with deployment threshold."

### Slide 6: Q&A Prep (1 min)
**Script**: "Happy to answer questions on my implementation choices, EDA findings, or deployment strategy."

---

## ❓ Top 20 Interview FAQs with Winning Answers

### Technical Questions

**Q1: Why did you use gradient descent for Logistic Regression instead of sklearn?**  
**A**: To demonstrate understanding of the optimization process and provide interpretable coefficients for regulatory requirements. Sklearn's solver='lbfgs' is faster but less transparent.

**Q2: How did you handle the class imbalance?**  
**A**: Stratified sampling in train/val/test splits (preserves 55:45 ratio) + threshold tuning (prioritizes recall over accuracy). Didn't use SMOTE because dataset is large enough (11,430 rows) and stratification sufficient.

**Q3: Why median imputation instead of mean?**  
**A**: Median is robust to outliers. EDA showed heavy-tailed distributions in 10 features—mean would be skewed by extreme values.

**Q4: Explain your threshold tuning process.**  
**A**: Swept 0.0 to 1.0 (step=0.01) on validation set. For each threshold, calculated FPR and recall. Selected threshold maximizing recall subject to FPR≤5% constraint. Applied to test set for unbiased performance.

**Q5: Why log-transform instead of standardization alone?**  
**A**: Skewness analysis (EDA) showed 10 features with |skew| > 1. Log-transform normalizes distributions → improves gradient descent convergence for Logistic Regression. Standardization alone doesn't fix skewness.

---

### Business Questions

**Q6: What's the business value of your model?**  
**A**: Baseline 55% → XGBoost 86% = 31% improvement. Assuming $100 average fraud loss per attack and 10,000 daily users, this prevents ~310 daily fraud incidents = $31,000 daily savings = $11.3M annually.

**Q7: Would you deploy your model in production?**  
**A**: Yes, XGBoost with threshold=0.65. Meets latency (<100ms), memory (<100MB), and recall (86%) requirements. However, 18% FPR may cause user frustration—recommend A/B testing with warning UX (not blocking) to optimize trust vs security.

**Q8: How would you explain your model to non-technical stakeholders?**  
**A**: "The model looks at website age, whether it has a robots.txt file, and responsiveness. Younger domains without proper metadata are flagged as suspicious. It catches 86% of phishing attacks but occasionally warns on 18% of legitimate sites—a trade-off we can tune."

**Q9: What are the biggest risks of deploying this model?**  
**A**: (1) Adversarial attacks (phishers manipulate features like DomainAgeMonths), (2) Feature drift (phishing tactics evolve), (3) False positives erode trust. Mitigation: quarterly retraining, anomaly detection, gradual rollout with user feedback.

**Q10: How would you improve this model with more time?**  
**A**: (1) Ensemble methods (stack LogReg + XGBoost), (2) SHAP values for explainability, (3) External features (WHOIS data, SSL certificate validity), (4) Active learning (retrain on user-reported false positives).

---

### Process Questions

**Q11: Walk me through your EDA process.**  
**A**: (1) Profiling (shape, dtypes, missing values), (2) Univariate analysis (distributions, skewness, outliers), (3) Bivariate analysis (correlation with target), (4) Data quality assessment (impossible values, duplicates), (5) Actionable recommendations (preprocessing plan).

**Q12: Why did you choose these 3 models?**  
**A**: Diverse approaches covering different inductive biases: Logistic (linear, interpretable), KNN (non-parametric, local patterns), XGBoost (ensemble, handles interactions). Covers fast deployment (LogReg), baseline comparison (KNN), and production performance (XGBoost).

**Q13: How did you validate your preprocessing pipeline?**  
**A**: (1) Fit on training set only (prevent leakage), (2) Transform validation/test with same parameters, (3) Check distributions match expected (no negative values, scaled to mean=0/std=1), (4) Save preprocessor with model for consistent inference.

**Q14: What was your biggest challenge?**  
**A**: Balancing recall vs FPR. Strict FPR≤3% (regulatory requirement) reduced recall to 12%—unacceptable for fraud detection. Learned to communicate trade-offs and recommend deployment threshold based on business context, not just technical metrics.

**Q15: How did you ensure reproducibility?**  
**A**: (1) Fixed random_state=42 in all splits/models, (2) Pinned dependency versions in requirements.txt, (3) Documented EDA → preprocessing decisions in README, (4) Saved preprocessor + model together for consistent inference.

---

### Group Exercise Prep

**Q16: How would you collaborate on GitHub during the Group Exercise?**  
**A**: (1) Create feature branches (feature/model-training, feature/evaluation), (2) Atomic commits with clear messages, (3) Pull requests for code review, (4) Resolve conflicts by discussing trade-offs, (5) Share preprocessing pipeline to ensure consistency.

**Q17: What would you contribute to a team tackling phishing detection?**  
**A**: (1) EDA expertise (identify data quality issues early), (2) Preprocessing pipeline (scalable, reusable), (3) Threshold tuning (balance business constraints), (4) Documentation (clear README for handoff).

**Q18: How would you handle disagreement on model selection?**  
**A**: (1) Establish objective criteria (recall≥70%, FPR≤5%, latency<100ms), (2) Evaluate all proposals against criteria, (3) Document trade-offs (interpretability vs performance), (4) Defer to data (A/B test if time permits), (5) Align on business priority (security vs trust).

**Q19: What questions would you ask your team at the start?**  
**A**: (1) Business constraints (acceptable FPR, latency budget), (2) Data assumptions (synthetic data handling), (3) Evaluation criteria (which metric to optimize), (4) Deployment target (browser extension vs API), (5) Time allocation (EDA vs modeling vs documentation).

**Q20: How would you debug if the pipeline crashes during the Group Exercise?**  
**A**: (1) Check error message (stack trace points to issue), (2) Validate inputs (schema, missing values, dtypes), (3) Reproduce in minimal example (isolate failing component), (4) Add print statements (intermediate outputs), (5) Ask teammate for second pair of eyes.

---

## 📋 Pre-Interview Checklist

### 24 Hours Before
- [ ] Run `bash run.sh` from clean slate → confirm no errors
- [ ] Review `results/baseline_metrics.json` → memorize your ROC AUC, recall, FPR
- [ ] Read your README top-to-bottom → can you explain every decision?
- [ ] Practice 10-min presentation with timer → stay under 10 minutes
- [ ] Prepare 3 questions to ask interviewers (e.g., "What's CyberProtect's current false positive rate?")

### Day Of Interview
- [ ] Open `eda.ipynb` and README in separate tabs → quick reference during Q&A
- [ ] Test laptop screen sharing → ensure charts are readable
- [ ] Charge laptop + bring charger
- [ ] Arrive 15 min early → calm nerves, review notes
- [ ] Smile and make eye contact → confidence matters

### Group Exercise Prep
- [ ] Install Git + configure name/email → `git config --global user.name "Your Name"`
- [ ] Practice cloning repo, creating branch, pushing commits
- [ ] Review pandas, sklearn, xgboost documentation → common methods
- [ ] Prepare code snippets: data loading, train/test split, model training, evaluation
- [ ] Mindset: collaboration > competition (you're being evaluated on teamwork)

---

## 🏆 Scoring Summary: How to Score 7-10/10

### Task 1: EDA Notebook
1. **Structure**: Problem → Profile → Analyze → Insights → Recommendations
2. **Visualizations**: 5-7 charts, each with title + interpretation paragraph
3. **Statistics**: Correlation matrix, skewness table, outlier percentages
4. **Business Translation**: Every finding linked to fraud risk, trust, or deployment

### Task 2: ML Pipeline
1. **run.sh**: Executes cleanly, validates environment, creates directories
2. **Preprocessing**: EDA-driven (fixes negatives, log-transforms, missing flags)
3. **Models**: 3 diverse (LogReg custom implementation, KNN, XGBoost)
4. **Evaluation**: Threshold tuning on validation set, ROC/PR curves, confusion matrix
5. **README**: Business problem → solution → results → deployment (quantified impact)

### Presentation
1. **Opening**: State business problem + your solution in 30 seconds
2. **EDA Highlights**: 1-2 charts + key findings (DomainAgeMonths, class imbalance)
3. **Pipeline**: Mermaid diagram + EDA→preprocessing decisions
4. **Results**: Model comparison table + threshold tuning trade-off
5. **Closing**: Deployment recommendation + next steps

---

**Final Advice**: The interviewers want to see **you understand why you made each decision**, not just that you can code. Memorize the business justifications for your top 5 choices (preprocessing, model selection, threshold tuning, evaluation metrics, deployment). Good luck! 🚀

---

## Prompt_202601161330

### Prompt-01

```
**forbid code blocks, interactive demo**
* CONTEXT: you're the interviewee who has virtually zero EDA, MLP experience, performed poorly in ASSESSMENT, and was given last-opportunity to **redo the ASSESSMENT from clean slate** prior to the Interview Session to remedy BENCHMARK-ACTUAL-GAP, win impression and get selected,
UPDATE `eda-mlp-detailed-implementation-lod-steps-interview.md` to outline step-by-step from clean slate to final deliverable and addresses FAQs, scoring rubric to improve performance from poor-to-qualified-to-excellent candidate

---

BENCHMARK: `eda-mlp-detailed-implementation-lod-steps.md`;
ASSESSMENT: `aisg-aiap22-technical-assessment.md`;
ACTUAL: `README.md`, `aisg-aiap22-task-1-eda-ipynb_20251201.md`;

---

Interview Session
```
Interview (1 hour): You have 10 minutes to present your Technical Assessment submission. The content of the presentation is decided by you. You can present directly from your submission (README, Jupyter Notebook) or prepare slides (PowerPoint, Google Slides). You will spend the remaining 50 minutes answering questions from the interviewers.
Group Exercise (2 hours): You are required to work on a case study together with 2 or 3 other candidates. The case study is disclosed on the spot. You are required to bring a personal laptop to code out the solution during the group exercise. The use of the internet and any other resources is allowed.
```
```
Building upon the foundation of the technical assessment, the Group Exercise will delve into the dynamic realm of classification analysis. 
You will be tasked with harnessing the power of this domain to address a real-world problem faced by CyberProtect, by strengthening their developed models to classify phishing attacks.
Sharpen your Python skills and be prepared to collaborate effectively within your team
on GitHub.
```
```

#### Response-01

